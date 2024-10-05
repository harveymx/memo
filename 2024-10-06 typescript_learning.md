### typescript学习（阮一峰的教程）
学习 类型工具、注释指令、tsconfig.json、TSC命令：

* 类型工具主要有以下内置组件：
    Awaited<Type>
    ConstructorParameters<Type>
    Exclude<UnionType, ExcludedMembers>
    Extract<Type, Union>
    InstanceType<Type>
    NonNullable<Type>
    Omit<Type, Keys>
    OmitThisParameter<Type>
    Parameters<Type>
    Partial<Type>
    Pick<Type, Keys>
    Readonly<Type>
    Record<Keys, Type>
    Required<Type>
    ReadonlyArray<Type>
    ReturnType<Type>
    ThisParameterType<Type>
    ThisType<Type>
    字符串类型工具
        Uppercase<StringType>
        Lowercase<StringType>
        Capitalize<StringType>
        Uncapitalize<StringType>

* 注释指令主要有：
    // @ts-nocheck
    // @ts-check
    // @ts-ignore
    // @ts-expect-error
    JSDoc
    @typedef
    @type
    @param
    @return，@returns
    @extends 和类型修饰符

* tsconfig.json是 TypeScript 项目的配置文件，放在项目的根目录。反过来说，如果一个目录里面有tsconfig.json，TypeScript 就认为这是项目的根目录。
    * tsc --init 可以生成初始文件
    * 一个基础栗子：
    ```
    {
    "compilerOptions": {
        "outDir": "./built",
        "allowJs": true,
        "target": "es5"
    },
    "include": ["./src/**/*"]
    }
    ```
    include：指定哪些文件需要编译。
    allowJs：指定源目录的 JavaScript 文件是否原样拷贝到编译后的目录。
    outDir：指定编译产物存放的目录。
    target：指定编译产物的 JS 版本。
    * 可以使用别人预先写好的 tsconfig.json 文件，npm 的@tsconfig名称空间下面有很多模块，都是写好的tsconfig.json样本，比如 @tsconfig/recommended和@tsconfig/node16，需要安装：
    ```
    $ npm install --save-dev @tsconfig/deno
    # 或者
    $ yarn add --dev @tsconfig/deno
    ```
    之后在tsconfig.json中配置：
    ```
    {
     "extends": "@tsconfig/deno/tsconfig.json"
    }
    * 具体参数看文档
* TSC基本用法
    ```
    # 使用 tsconfig.json 的配置
    $ tsc

    # 只编译 index.ts
    $ tsc index.ts

    # 编译 src 目录的所有 .ts 文件
    $ tsc src/*.ts

    # 指定编译配置文件
    $ tsc --project tsconfig.production.json

    # 只生成类型声明文件，不编译出 JS 文件
    $ tsc index.js --declaration --emitDeclarationOnly

    # 多个 TS 文件编译成单个 JS 文件
    $ tsc app.ts util.ts --target esnext --outfile index.js
    ```

### 礼毕，TypeScript全部学完（了解大概）

