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

### 最后，晚上对TypeScript的总结情况进行回顾和复习！
 * 开始使用
 ```

    yarn global add typescript  // 全局安装
    mkdir demo && cd demo
    touch index.ts 
    yarn init   // 初始化项目环境
    tsc --init  // 初始化 ts，文件目录下多了一个tsconfig.json
 ``` 

 * tsconfig.json & package.json的配置
    ```

    //  tsconfig.json
    {
    "compilerOptions": {
        "target": "es5",                            // 指定 ECMAScript 目标版本: 'ES5'
        "module": "commonjs",                       // 指定使用模块: 'commonjs', 'amd', 'system', 'umd' or 'es2015'
        "moduleResolution": "node",                 // 选择模块解析策略
        "experimentalDecorators": true,             // 启用实验性的ES装饰器
        "allowSyntheticDefaultImports": true,       // 允许从没有设置默认导出的模块中默认导入。
        "sourceMap": true,                          // 把 ts 文件编译成 js 文件的时候，同时生成对应的 map 文件
        "strict": true,                             // 启用所有严格类型检查选项
        "noImplicitAny": true,                      // 在表达式和声明上有隐含的 any类型时报错
        "alwaysStrict": true,                       // 以严格模式检查模块，并在每个文件里加入 'use strict'
        "declaration": true,                        // 生成相应的.d.ts文件
        "removeComments": true,                     // 删除编译后的所有的注释
        "noImplicitReturns": true,                  // 不是函数的所有返回路径都有返回值时报错
        "importHelpers": true,                      // 从 tslib 导入辅助工具函数
        "lib": ["es6", "dom"],                      // 指定要包含在编译中的库文件
        "typeRoots": ["node_modules/@types"],
        "outDir": "./dist",
        "rootDir": "./src"
    },
    "include": [                                  // 需要编译的ts文件一个*表示文件匹配**表示忽略文件的深度问题
        "./src/**/*.ts"
    ],
    "exclude": [
        "node_modules",
        "dist",
        "**/*.test.ts",
    ]
    }

    // package.json
    "scripts": {
        "build": "tsc", // 编译
        "build:w": "tsc -w" // 监听文件，有变动即编译
    },

    ``` 
* 看到一段不错的工程实践用法，用于加深理解
    使用接口定义复杂的数据结构，增强代码的可读性和维护性。
    使用类型别名（type）来简化复杂类型，提高代码清晰度。
    使用枚举来表示一组常量，避免硬编码。
    使用泛型提高代码的灵活性，避免重复代码。
    使用类来组织代码和数据，促进面向对象编程。
    使用模块化编程，将代码拆分成模块，提高代码复用性。
    遵循一致的命名规范，提高代码的可读性。

### 礼毕，TypeScript全部学完（了解大概）！

链接：
https://wangdoc.com/typescript/
https://juejin.cn/post/7271862751957155859

