
> 2025-11-19→22 在 mac mini 上配置环境，以继续ezao claude code vibe coding
## mac mini 配置
> 配置 mac 操作系统环境 && 开发环境

### mac 操作系统配置更新

#### 安装腾讯柠檬
#### 安装 home brew
#### 设置系统参数：
    * 键盘导航
    * 鼠标滚动方向
    * 访达设置:
        - 边栏显示项目-全选
        - 将以下位置的文件夹保持在顶部:全选
        - 执行搜索时，搜索当前文件夹        
        - 显示-路径栏、状态栏
    * 调整状态栏：
        - command+鼠标拖动
        - 鼠标拖动往状态栏放(蓝牙、声音等)

    * 触发角设置：右下-桌面，右上通知中心，左上角调度中心
    * 桌面-开启使用叠放
    * iCloud->关闭照片同步(访达的本地硬盘的photos libs 删除)
    * 悬停文本(可选)
    * 启动台：12*8
    * 应用程序->分栏式浏览
    * 程序坞设置
    
#### 安装微信输入法、chrome、evernote/印象笔记...
#### 安装上网工具
#### 安装 raycast
#### 安装@macwk:(dmg安装)
* cleanShotX：截屏
* BetterMouse：更靠近windows的鼠标平滑使用,尤其罗技鼠标   
#### 安装 罗技 options+
#### 安装 LocalSend : 跨系统局域网文件快传
#### 安装 X网友 tw93的清理软件:brew install tw93/tap/mole
#### 安装 unarchiver ： 解压缩软件
#### 安装 microsoft office
#### 安装坚果云 brew instal nutstore (同步 coding 工具)

### 安装开发者工具（with homebrew）：
    * (homebrew)+iTerm2+ oh-my-zsh: https://juejin.cn/post/7257740918432792632 暂时不用-可被下面取代
    * warp @ warp.dev
    * vs code : brew install --cask visual-studio-code
    * python3 : brew install python3 ；Mac有自带python，修改.zprofile,让brew版的python在最前面即可，与系统版互不干扰
    * OrbStack：极速docker替代品
    * Sublime Text 
    * cpolar
    * kimi
    * Cherry studio
    * Mac screen studio
    * setApp
    * nmap:网络端口扫描工具 ; brew install nmap ; nmap localhost

### claude code 环境
#### 安装 Node.js，这里使用 最先进的 volta 来管理 Node.js 的包
* 安装 volta
```
    brew install volta
```
* 配置 volta 环境变量
```
    //在～/.bash_profile 或者 ～/.zshrc 文件中进行配置
    export VOLTA_HOME="$HOME/.volta"
    export PATH="$VOLTA_HOME/bin:$PATH"
```
* 测试及安装
```
    //在终端中输入
    volta
    volta install node #安装最新版node
    //测试安装nodejs-v16版本
    volta install node@16
    //测试安装
    node -v

```
* volta 用法：
    * volta install：   安装设置工具的默认版本。如果该工具尚未在本地缓存，它也将获取该工具。示例：volta install node@16
    * volta uninstall： 删除已安装在 volta install 中的任何全局包。示例：volta uninstall node@16
    * volta pin：       更新一个项目的 package.json 文件以使用工具的选定版本。示例：volta pin node@16 volta pin yarn@1.19
    * volta list：      检查已安装的 Node 运行时、包管理器和带有二进制文件的包。示例：volta list

```
    brew install node #如果不用 volta
```

#### 安装 cluade code
```
    npm install -g @anthropic-ai/claude-code
```
#### 配置 kimi api 环境变量
```
    # 添加到 zsh 配置文件（macOS 默认）
    echo 'export ANTHROPIC_AUTH_TOKEN="你的API密钥"' >> ~/.zshrc
    echo 'export ANTHROPIC_BASE_URL="https://api.kimi.com/coding/"' >> ~/.zshrc
    echo 'export ANTHROPIC_MODEL="kimi-for-coding/"' >> ~/.zshrc
    echo 'export ANTHROPIC_SMALL_FAST_MODEL="kimi-for-coding"' >> ~/.zshrc

    # 如果使用 Bash
    echo 'export ANTHROPIC_AUTH_TOKEN="你的API密钥"' >> ~/.bash_profile
    echo 'export ANTHROPIC_BASE_URL="https://api.kimi.com/coding/"' >> ~/.bash_profile
    echo 'export ANTHROPIC_MODEL="kimi-for-coding/"' >> ~/.bash_profile
    echo 'export ANTHROPIC_SMALL_FAST_MODEL="kimi-for-coding"' >> ~/.bash_profile

    # 重新加载配置
    source ~/.zshrc  # 或 ~/.bash_profile

```
    或者编辑 ~/.zshrc文件，将环境变量加入

#### 配置 claude Code 的外网访问环境（可直接利用 claude 的模型）
    * 进入.claude 目录（～目录下），创建一个 settings.json文件
```
    {
    "env":{

        "HTTP_PROXY": "http://127.0.0.1:7897",

        "HTTPS_PROXY": "http://127.0.0.1:7897"

    }
}
```
    * 如果直接使用 claude 的模型 （1）代理股东米国 IP （2）代理模式要切换全局 （！重要！）

#### 让claude 用中文回答（并触发记忆）：
```
        # Always reply in Chinese.  
```
### git 环境配置
#### 配置用户（全局生效）：

bash
```
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

git config --global user.name "harveymx"
git config --global user.email "meetxu@gmail.com"


#### 登录方式1：HTTPS 方式（最简单，VS Code 开箱即用）
 
在 vscode 中第一次 Push 时弹窗 → 用户名填 GitHub/Gitee 账号，密码填「个人访问令牌」（不是登录密码！）
令牌生成入口：GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic) → 勾选  repo  → Generate
macOS 钥匙串会记住，以后 VS Code / 终端都不再问。

#### 登录方式 2：SSH 方式（本机生成公钥，提供给 github，一劳永逸，无需反复输令牌） 
---没有采用

#### 设置git代理

永久性设置：
```
    git config --global http.proxy http://127.0.0.1:7897
    git config --global https.proxy http://127.0.0.1:7897
```
用完随时可关：
```
    git config --global --unset http.proxy
    git config --global --unset https.proxy
```

所以，为了方便，在~/.zshrc 创建一个快速函数 git_proxy_on 和 git_proxy_off，可执行：
```
    git_proxy_on() {
    git config --global http.proxy http://127.0.0.1:7890
    git config --global https.proxy http://127.0.0.1:7890
    echo "Git proxy on"
    }
    git_proxy_off() {
    git config --global --unset http.proxy
    git config --global --unset https.proxy
    echo "Git proxy off"
    }
```

#### 同理，可以设置terminal 终端的代理
如 curl 的应用
```
    export https_proxy=http://127.0.0.1:7897   # 端口换成你的
    export http_proxy=$https_proxy

    // 测试一下
    curl -I https://github.com

```
#### 查看 http proxy变量信息
```
    echo $https_proxy
```
或
```
    env | grep -i proxy
```
看 git 的代理：
```
    git config --global --get https.proxy
```

#### 一不小心提交了有点本地文件信息的文件，练习用 git-filter-repo 抹掉路径历史

```
# 安装工具（一次性）
brew install git-filter-repo

# 进入本地仓库
cd your-repo

# 彻底删除 “private/秘密文件夹” 及其历史
git filter-repo  --invert-paths --force --path private/秘密文件夹

# 查看你原来的远程地址（复制备用）
git remote -v
# 通常为空，因为被清掉了

# 重新添加 origin
git remote add origin https://github.com/你的用户名/仓库.git

# 强制推送到 GitHub（会重写远程历史）
git remote add origin https://github.com/你的用户名/仓库.git
git push origin --force --all
git push origin --force --tags
```
删除完之后，所有人都要 重新 clone（历史已变）。本地 所有旧副本也要删掉再重新拉取，否则会被“污染”重新推上去。

### 编程字体(免费)

#### 安装
```
# 连字 + 超高辨识度
brew install --cask font-jetbrains-mono
brew install --cask font-fira-code
brew install --cask font-cascadia-code
brew install --cask font-source-code-pro

# 超窄 / 可定制狂魔
brew install --cask font-iosevka

# 经典 Mac 风味
brew install --cask font-meslo-lg-nerd-font   # Monaco 血统 + Powerline 符号
```
#### 使用:
* vs code： ⌘,  → 搜索  font  →
```
"editor.fontFamily": "FiraCode-Retina, JetBrains Mono, MesloLGS NF, monospace",
"editor.fontSize": 14,
"editor.lineHeight": 22,
"editor.fontLigatures": true
```
* iTerm2 : ⌘,  → Profiles → Text → Change Font → 选 MesloLGS NF 13 pt → 勾选「Use ligatures」

#### 推荐组合
* 日常开发：JetBrains Mono 14 pt + 1.5 行距（VS Code 默认）
* 终端 + oh-my-zsh：MesloLGS NF 13 pt（iTerm2 自带 Powerline 符号不缺失）
* 想省屏幕宽度：Iosevka 12 pt（比同类窄 10 %，一屏多看 20 列）


### 相关参考
* 购买Macbook之后，一定要改变的设置 & 必装软件！（2024最新）feat. 隐藏功能 ｜大耳朵TV
https://www.bilibili.com/video/BV1bC4y1q7t8?spm_id_from=333.788.player.player_end_recommend&vd_source=5342240dd1e8515fba0e9b9e99f77a5e

* 在终端设置代理：
export http_proxy="http://127.0.0.1:7897"  
export https_proxy="http://127.0.0.1:7897"
export socks_proxy="socks://127.0.0.1/7897"
curl -v https://www.google.com
mac 终端设置代理，具体看 ： https://ichochy.com/posts/mac/20231125.html

* iTerm2最常用的主题是Solarized Dark theme
下载地址：http://ethanschoonover.com/solarized，打开iTerm2 -> Preferences，然后Profiles ---> Colors -> Color Presets -> Import ，选择Solarized Dark.itermcolors文件，导入，最后选择Solarized Dark。

* x 网友tw93 的 Mole 系统优化工具：
网址： https://github.com/tw93/Mole 
近似等于 Clean My Mac + AppCleaner + DaisyDisk + Sensei + iStat 的能力，
小鼹鼠的 5 大功能：
mo clean，用于像鼹鼠一样强力挖掘你的 Mac 里面的各种垃圾，各种缓存以及孤岛文件，第一次使用可以清理掉非常多无用空间。 
mo uninstall，很彻底的卸载你的软件，除去软件 app 本身，还有各种注册项、启动项、配置文件等都可以非常彻底的清理掉。 
mo optimize，帮我一键优化系统，比如说各种刷新、错误重置、重置缓存，重置服务、检查开机项等内容。 
mo analyze，可视化的方式下钻你的磁盘空间，可以看到有些可以清理的无用文件，这里是对 clean 的一个很好的补充。 
mo status，可以很清楚看到你的电脑的运行健康情况，包括磁盘使用读写、电池使用、网络情况、进程占用、甚至是代理运行情况是否正常。

* claude code 的配置@mac
https://blog.veeblue.com/2025/07/19/%F0%9F%A7%AD-macOS-Claude-Code-%E5%9F%BA%E4%BA%8EKIMI-%E5%85%A8%E6%B5%81%E7%A8%8B%E5%AE%89%E8%A3%85%E6%8C%87%E5%8D%97/

* volta 及 node 安装
https://www.jianshu.com/p/438c811f564a

