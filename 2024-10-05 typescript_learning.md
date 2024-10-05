### typescript学习（阮一峰的教程）
学习装饰器知识
学习declare关键字、d.ts类型声明文件、类型运算符（keyof、in、[]、extends..?:、infer、is、
模板字符串、satisfies）、类型映射
```
    在语法上，装饰器有如下几个特征。
    （1）第一个字符（或者说前缀）是@，后面是一个表达式。
    （2）@后面的表达式，必须是一个函数（或者执行后可以得到一个函数）。
    （3）这个函数接受所修饰对象的一些相关值作为参数。
    （4）这个函数要么不返回值，要么返回一个新对象取代所修饰的目标对象。
    举例来说，有一个函数Injectable()当作装饰器使用，那么需要写成@Injectable，然后放在某个类的前面。
    ```
    @Injectable class A {
    // ...
    }
    ```

    @后面的表达式，最终执行后得到的应该是一个函数。
    装饰器一般只用来为类添加某种特定行为。

    //装饰器的类型定义结构如下：
    type Decorator = (
    value: DecoratedValue,
    context: {
        kind: string;
        name: string | symbol;
        addInitializer?(initializer: () => void): void;
        static?: boolean;
        private?: boolean;
        access: {
        get?(): unknown;
        set?(value: unknown): void;
        };
    }
    ) => void | ReplacementValue;
```
* 类装饰器：对类操作
    ```
    type ClassDecorator = (
    value: Function,
    context: {
        kind: 'class';
        name: string | undefined;
        addInitializer(initializer: () => void): void;
    }
    ) => Function | void;

    ```
    栗子：
    ```
    function Greeter(value, context) {
    if (context.kind === 'class') {
        value.prototype.greet = function () {
        console.log('你好');
        };
    }
    }

    @Greeter
    class User {}

    let u = new User();
    u.greet(); // "你好"
    ```
* 方法装饰器：用来装饰类的方法
    ```
    type ClassMethodDecorator = (
    value: Function,
    context: {
        kind: 'method';
        name: string | symbol;
        static: boolean;
        private: boolean;
        access: { get: () => unknown };
        addInitializer(initializer: () => void): void;
    }
    ) => Function | void;
    ```

* 属性装饰器用来装饰定义在类顶部的属性（field）
    ```
    type ClassFieldDecorator = (
    value: undefined,
    context: {
        kind: 'field';
        name: string | symbol;
        static: boolean;
        private: boolean;
        access: { get: () => unknown, set: (value: unknown) => void };
        addInitializer(initializer: () => void): void;
    }
    ) => (initialValue: unknown) => unknown | void;
    ``` 

* getter 装饰器和 setter 装饰器，是针对类的取值器（getter）和存值器（setter）的装饰器。
    ```
    type ClassGetterDecorator = (
    value: Function,
    context: {
        kind: 'getter';
        name: string | symbol;
        static: boolean;
        private: boolean;
        access: { get: () => unknown };
        addInitializer(initializer: () => void): void;
    }
    ) => Function | void;

    type ClassSetterDecorator = (
    value: Function,
    context: {
        kind: 'setter';
        name: string | symbol;
        static: boolean;
        private: boolean;
        access: { set: (value: unknown) => void };
        addInitializer(initializer: () => void): void;
    }
    ) => Function | void;
    ```

* accessor 装饰器,装饰器语法引入了一个新的属性修饰符accessor
    ```
    class C {
    accessor x = 1;
    }
    //或者
    class C {
    #x = 1;

    get x() {
        return this.#x;
    }

    set x(val) {
        this.#x = val;
    }
    }
    ```
    其类型如下:
    ```
    type ClassAutoAccessorDecorator = (
    value: {
        get: () => unknown;
        set: (value: unknown) => void;
    },
    context: {
        kind: "accessor";
        name: string | symbol;
        access: { get(): unknown, set(value: unknown): void };
        static: boolean;
        private: boolean;
        addInitializer(initializer: () => void): void;
    }
    ) => {
    get?: () => unknown;
    set?: (value: unknown) => void;
    init?: (initialValue: unknown) => unknown;
    } | void;
    ```

* 装饰器的执行顺序
    装饰器的执行分为两个阶段。
    （1）评估（evaluation）：计算@符号后面的表达式的值，得到的应该是函数。
    （2）应用（application）：将评估装饰器后得到的函数，应用于所装饰对象。
    也就是说，装饰器的执行顺序是，先评估所有装饰器表达式的值，再将其应用于当前类。
    应用装饰器时，顺序依次为方法装饰器和属性装饰器，然后是类装饰器。

    请看下面的例子。
    ```
    function d(str:string) {
    console.log(`评估 @d(): ${str}`);
    return (
        value:any, context:any
    ) => console.log(`应用 @d(): ${str}`);
    }

    function log(str:string) {
    console.log(str);
    return str;
    }

    @d('类装饰器')
    class T {
    @d('静态属性装饰器')
    static staticField = log('静态属性值');

    @d('原型方法')
    [log('计算方法名')]() {}

    @d('实例属性')
    instanceField = log('实例属性值');

    @d('静态方法装饰器')
    static fn(){}
    }
    ```
    上面示例中，类T有四种装饰器：类装饰器、静态属性装饰器、方法装饰器、属性装饰器。

    它的运行结果如下。

    评估 @d(): 类装饰器
    评估 @d(): 静态属性装饰器
    评估 @d(): 原型方法
    计算方法名
    评估 @d(): 实例属性
    评估 @d(): 静态方法装饰器
    应用 @d(): 静态方法装饰器
    应用 @d(): 原型方法
    应用 @d(): 静态属性装饰器
    应用 @d(): 实例属性
    应用 @d(): 类装饰器
    静态属性值
    可以看到，类载入的时候，代码按照以下顺序执行。

    （1）装饰器评估：这一步计算装饰器的值，首先是类装饰器，然后是类内部的装饰器，按照它们出现的顺序。
    注意，如果属性名或方法名是计算值（本例是“计算方法名”），则它们在对应的装饰器评估之后，也会进行自身的评估。
    （2）装饰器应用：实际执行装饰器函数，将它们与对应的方法和属性进行结合。
    静态方法装饰器首先应用，然后是原型方法的装饰器和静态属性装饰器，接下来是实例属性装饰器，最后是类装饰器。

    注意，“实例属性值”在类初始化的阶段并不执行，直到类实例化时才会执行。