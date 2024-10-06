### node.js、typescript学习 from TypeScript Deep Dive （中文版）
链接：https://rexdainiel.gitbooks.io/typescript/content/
**新认识了TypeScript的编辑器 ALM** 
    * A complete dev and analysis environment.
    * Easy to install: npm install alm -g
    * Easy to use: alm
    * 注：不好用，删除之
**快速开始一个node项目**
    1. 开始一个 nodejs 项目 package.json。快速的方法：npm init -y
    2. 添加 TypeScript（npm install typescript --save-dev）
    3. 添加 node.d.ts (npm install @types/node --save-dev)
    4. 为 TypeScript 选项初始化一个 tsconfig.json（node ./node_modules/.bin/tsc --init）
就是这样！启动你的 IDE（例如 alm -o）然后玩耍起来。现在你可以使用所有以 node 模块构建的东西（例 import fs = require('fs')），并且享受 TypeScript 的安全性和开发者人体工程学。
**即时编译和运行**
    1. 添加 ts-node，我们将会使用它来在 node 中进行即时编译 + 运行（npm install ts-node --save-dev）
    2. 添加 nodemon，它会在一个文件改变的时候调用 ts-node（npm install nodemon --save-dev）
    3. 编辑package.json,添加入口应用index.ts
    
    
    "scripts": {
        "start": "npm run build:live",
        "build:live": "nodemon --exec ./node_modules/.bin/ts-node -- ./index.ts"
      }
    
  现在你可以运行npm start 并且当你编辑 index.ts 时：
    * nodemon 重新运行它的命令（ts-node）
    * ts-node 自动获取 tsconfig.json 和当前安装的 typescript 版本转换编译
    * ts-node 通过 node 运行输出的 javascript。
    
    