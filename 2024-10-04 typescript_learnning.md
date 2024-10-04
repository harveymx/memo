### typescript学习（阮一峰的教程）
* 10.03&今日：对象&interface&类&泛型Enum(枚举)类型&类型断言&模块module
* 模块module的基础知识：
  * 模块定位：编译参数moduleResolution，用来指定定位算法，常用的算法有两种：Classic和Node。
  * 如果没有指定moduleResolution，编译参数module设为commonjs时（项目脚本采用 CommonJS 模块格式），moduleResolution的默认值为Node，即采用 Node.js 的模块定位算法。其他情况下（module设为 es2015、 esnext、amd, system, umd 等等），就采用Classic定位算法。
  * 加载模块时，目标模块分为相对模块（relative import）和非相对模块两种（non-relative import）
  * 相对模块指的是路径以/、./、../开头的模块,相对模块的定位，是根据当前脚本的位置进行计算的，一般用于保存在当前项目目录结构中的模块脚本
  * 非相对模块指的是不带有路径信息的模块,非相对模块的定位，是由baseUrl属性或模块映射而确定的，通常用于加载外部模块。
  * Classic 方法:
    * 以当前脚本的路径作为“基准路径”，计算相对模块的位置。
    * 非相对模块，也是以当前脚本的路径作为起点，一层层查找上级目录

  * Node 方法就是模拟 Node.js 的模块加载方法，也就是require()的实现方法
    * 相对模块依然是以当前脚本的路径作为“基准路径”,优先依赖package.json文件
    * 非相对模块则是以当前脚本的路径作为起点，逐级向上层目录查找是否存在子目录node_modules

  * 路径映射
    * ypeScript 允许开发者在tsconfig.json文件里面，手动指定脚本模块的路径
    * 举例
    ```
        {
        "compilerOptions": {
            "baseUrl": ".",
            "paths": {
            "jquery": ["node_modules/jquery/dist/jquery"]
            }
            "rootDirs": ["src/zh", "src/de", "src/#{locale}"]
        }
        }
    ```
  * tsc 命令有一个--traceResolution参数，能够在编译时在命令行显示模块定位的每一步
  * tsc 命令的--noResolve参数，表示模块定位时，只考虑在命令行传入的模块