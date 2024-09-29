## 2024-09-29 前端知识比较多，做成kindle小册：使用mdbook
* mdbook 介绍
  mdBook 是一个由 RUST 构建的命令行工具，可以将 Markdown 文档，变成 HTML 网站，可以用来制作电子书。这样的工具，用在产品信息或是 API 文档, 教程, 课件资料等等场景。
* 安装
  * 安装 Rust 环境
    sudo apt get update #升级系统最新包
    sudo apt get upgrade
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh #安装rust和cargo，得到如下：

        Welcome to Rust!

        This will download and install the official compiler for the Rust
        programming language, and its package manager, Cargo.

        Rustup metadata and toolchains will be installed into the Rustup
        home directory, located at:

        /home/xuhw/.rustup
                                                                                                    This can be modified with the RUSTUP_HOME environment variable.

        The Cargo home directory is located at:

        /home/xuhw/.cargo

        This can be modified with the CARGO_HOME environment variable.

        The cargo, rustc, rustup and other commands will be added to
        Cargo's bin directory, located at:

        /home/xuhw/.cargo/bin

        This path will then be added to your PATH environment variable by
        modifying the profile files located at:

        /home/xuhw/.profile
        /home/xuhw/.bashrc
        /home/xuhw/.zshenv
        /home/xuhw/.config/fish/conf.d/rustup.fish

        You can uninstall at any time with rustup self uninstall and
        these changes will be reverted.

        Current installation options:


        default host triple: x86_64-unknown-linux-gnu
            default toolchain: stable (default)
                    profile: default
        modify PATH variable: yes
    运行：source "$HOME/.cargo/env.fish"  #For fish
         cargo --version
  * 安装Chome(mdbook build需要内核)
        sudo apt-get install -y libappindicator1 fonts-liberation #安装依赖
        sudo apt-get install -f
        wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
        sudo dpkg -i google-chrome*.deb
        google-chrome-stable -version
  * 安装 mdbook
    cargo install mdbook
    cargo install mdbook-pdf
    cargo install mdbook-epub
  * 创建电子书目录
    mkdir  mdbook_ryf-typescript
    mdbook init  mdbook_ryf-typescript
  * 下载阮一峰的TypeScript教程（MD版）
    git clone https://github.com/wangdoc/typescript-tutorial.git
    将md文件复制到mdbook_ryf-typescript/src目录下
  * 编辑配置文件 mdbook_ryf-typescript/book.toml
        [book]
        authors = ["阮一峰"]
        language = "zh-CN"
        multilingual = false
        src = "src"
        title = "阮一峰《TypeScript 教程》"

        # 添加章节序号
        [preprocessor.chapter-number]

        # 导出 html、pdf、带目录的pdf
        [output.html]
        [output.pdf]
        [output.epub]

        # 添加页眉页脚
        display-header-footer= true
        header-template = "<h3 style='font-size:8px; margin-left: 85px;width:200px;' class='title'></h3><h3 style='margin-left:120px;font-size:8px;'>https://wangdoc.com/typescript/</h3>"
        footer-template = "<p style='font-size:10px; margin-left: 48%'><span class='pageNumber'></span> / <span class='totalPages'></span></p>"
        prefer-css-page-size = true

        [output.pdf-outline]
        optional = true
  * 编辑配置文件 mdbook_ryf-typescript/src/SUMMARY.md
        # Summary

        - [简介](./intro.md)
        - [基本用法](./basic.md)
        - [any 类型](./any.md)
        - [类型系统](./types.md)
        - [数组](./array.md)
        - [元组](./tuple.md)
        - [symbol 类型](./symbol.md)
        - [函数](./function.md)
        - [对象](./object.md)
        - [interface](./interface.md)
        - [类](./class.md)
        - [泛型](./generics.md)
        - [Enum 类型](./enum.md)
        - [类型断言](./assert.md)
        - [模块](./module.md)
        - [namespace](./namespace.md)
        - [装饰器](./decorator.md)
        - [装饰器（旧语法）](./decorator-legacy.md)
        - [declare 关键字](./declare.md)
        - [d.ts 类型声明文件](./d.ts.md)
        - [运算符](./operator.md)
        - [类型映射](./mapping.md)
        - [类型工具](./utility.md)
        - [注释指令](./comment.md)
        - [tsconfig.json 文件](./tsconfig.json.md)
        - [tsc 命令](./tsc.md)

  * 运行mdbook build,生成的pdf文件分别在： book/html,book/pdf,book/epub目录下
  * 将epub文件转换为mobi文件(在线转换工具):
        http://cn.epubee.com/?linkid=zhihu&utm_medium=zhihuArticle&utm_source=zhihu&utm_campaign=zhihu&utm_content=zhihu

  * 完成！

*参考链接：
    https://blog.csdn.net/quicmous/article/details/139075131
    https://www.cnblogs.com/LLW-NEU/p/17857553.html
    https://mp.weixin.qq.com/s?__biz=MzIyNDQ2MTQwOQ==&mid=2247493433&idx=1&sn=8a6f2c9975f34b9e2e7be62479f24478&chksm=e80c3037df7bb9212d320ca3fff025a81347fbc163add2a0456ea5a522ab6a836755af84ccb6&token=1949573976&lang=zh_CN#rd
    https://geekflare.com/install-chromium-ubuntu-centos/

