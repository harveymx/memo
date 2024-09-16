## 2024-09-17 简单Agent基础实现
主要知识点：
* 综合利用好对函数调用和chain的利用，本次又增加了RunnableBranch的使用

const branch = RunnableBranch.from([
  [
    (input => input.type.includes("科普")),
    scienceChain,
  ],
  [
    (input => input.type.includes("编程")),
    programmingChain,
  ],
  generalChain
]);

* 开发者遇到了deno和jupyter的冲突,deno server经常crash，重新安装jupyter notebook,以及VS code的插件（更新到preview版本）解决了

* 练习IPad上的Drawthing AI，熟悉prompt和基础参数使用