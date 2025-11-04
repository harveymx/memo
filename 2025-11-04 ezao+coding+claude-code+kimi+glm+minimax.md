

> 2025-11-04 继续ezao claude code vibe coding
## ezao claude code vie coding || 启用Kimi K2、GLM4.6、MiniMax M2三个模型同步开发
>借助 cc-model-switcher，配置了claude code使用Kimi K2、GLM4.6、MiniMax M2， 同时迭代多个版本的研发 😊

## 笔格设计：很好的切图工具，icon挺好用的

网址：https://bigesj.com/

## 在线去水印工具

网址：https://dewatermark.ai/zh-CN/upload

## Font Awesome：一套绝佳的图标字体库和CSS框架

* https://fontawesome.dashgame.com/

* 在AI编程时，如果想偷懒，可以在prompt中要求LLM使用Font Awesome风格的设计

## claude code使用经验和技巧
* claude --dangerously-skip-permissions：免授权模式
* /init 第一时间创建claude.md文件
* /memory 调取并查看claude.md文件
* /compact 压缩内容，要常使用，以节省token
* 提前写好项目需求文件.md格式，copy到项目目录
* 要求claude code生成技术文档：以下prompt
    @项目文档.md 是小程序的需求文档，现在需要你根据需求文档完成开发技术文档
     -如果使用图片或者是icon的化，请你使用如Font Awesome之类的开源资源，不要引用不存在的本地资源
    -需要注意需求文档中一些关于XX的专业信息和需求的专业内容
    -技术文档要严格遵守需求文档，不要扩展不需要的需求
    -完成技术文档之后，需要将需求文档和技术文档动态添加到CLAUDE.md文件中，让Claud Code获取到开发内容
* 也可以用kimi chat、claud chate界面，生成一个设计文档，提供给cc 
* 要求claude code启动开发的prompt:
 1.创建完整的项目结构，包括页面、组件、云函数
 2.实现三个核心模块：
    -XXX
    -XXX
    -XXX
 3.配置微信云开发环境（云数据库、云函数、安全规则）
 4.采用静默技术设计理念，确保用户体验简洁友好
 严格按照需求文档执行，需要添加额外功能
 ## 榨干 Claude Code 的 16 个实用小技巧

 https://www.cnblogs.com/javastack/p/18978280
 
1、把你的需求说具体点
2、把复杂的需求分步执行
3、先理解项目代码再开动
4、学会用快捷键，节省时间
斜线、上下键、Tab补全、Option + Enter 换行、Ctrl + C 退出终端
5、使用免授权模式
6、激活深度思考模式（“think” < “think hard” < “think harder” < “ultrathink”，但费钱）
7、输错指令，随时打断它工作
8、发送图片处理
9、恢复历史会话
Claude Code 提供两个选项来恢复之前的对话：
* claude --continue 或者 claude -c：自动继续最近的对话，无需任何提示
* claude --resume 或者 claude -r：显示历史对话选择器
这两个带参数的命令需要在「非交互模式」下进行，也就是还没有进入 Claude Code。
交互模式: 如果你已经进入了 Claude Code 会话，想恢复到之前的哪个历史会话，可以使用 /resume 命令恢复历史会话
10、记忆管理：/memory
* 修改用户级记忆文件：每次请用中文回答我。后续所有交互就都是中文回答的了。
* 如果 Claude Code 在某些情况下仍切换为英文，可以尝试清除会话缓存（如 /clear 命令）后重新加载配置。
* 也可以使用其他方法股东简体中文回答，自行搜索
11、和 Git 进行交互
我修改了哪些文件、用合理描述性信息提交我的更改、
推送本分支到远程、创建一个新分支:feature/test、
删除本分支并切换到master分支、显示最近3次提交中所有文件列表
12、和 Linux 交互
列出行数最多的前3个.java文件、claude -p "列出行数最多的前3个.java文件"
13、模型切换 :使用 /model 命令进行切换
14、查看消耗情况: /const
15、上下文压缩: /compact 清除对话历史记录，但保留上下文中的摘要, 减少对话上下文大小和token消耗
* 默认在上下文超过 95% 容量时自动压缩。
* 定时使用 clear 命令重置上下文
16、自定义快捷命令

## 网友的claude code使用经验和技巧

第一层：基础篇（人人必会）
1. 主动压缩：Claude 会在上下文剩余20%时自动压缩，但那时基本为时已晚。要养成手动提前使用 /compact 命令 的好习惯。
2. 一事一议，用完即焚：**为每个独立任务多开几个终端窗口 。任务一旦完成，立刻关闭窗口 (/clear 也行)**。保持任务的原子性，防止不相关的上下文污染后续对话。
3. 杀鸡焉用牛刀，明智选择模型：日常开发坚决使用 Sonnet。只有在啃硬骨头时，才请出 Opus 这尊“大佛”。可以通过 /model sonnet的命令切换当前使用的模型。
4. 定期查账，心里有数：多用 /cost 命令检查 Token 消费情况。还可以通过这个命令看看自己烧了多少Token、花了多少钱？npx ccusage@latest
5.** 编辑代替追问：别一错就再加一句“你刚才错了，试试这个”，直接编辑原始提示，避免记住所有历史错误**。

第二层：工作流优化（善用工具组合）
1. **划定禁区，善用 .gitignore**：Claude Code 会尊重你项目中的 .gitignore 文件。把 node_modules、日志、构建产物等无关文件夹都加进去，能从源头上阻止它进行无效扫描。
2. **文档驱动，让AI先做计划**：不要随意对话。**先让 Claude Code 生成一个任务清单（TODO List）** 。然后你再引导它逐一完成。这种“先规划，后执行”的模式，能让每一次交互都更精准。这也是我之前推荐的AI编程工作流：发现个用 Claude Code 的高效…
3. **管理记忆：**运行 /memory 命令可以查看和编辑 Claude “记住”了哪些核心信息。对于版本号、关键工具链等固定内容，在这里一次性修正，就不用在对话中反复纠错了。
4. 借力打力，混合工具流：让其他工具干脏活累活！比如，像饼干哥哥一样，搭配Trae，3美金/月，用来做文档、梳理等，例如为项目自动生成初步的文档说明，再让 Claude Code 基于这些精准的说明进行具体的代码实现。但不建议用Trae来跑复杂任务，我最近在搭建自己的品牌官方，用Trae折腾了几天，审美不行、多语言报错等等，后来用Claude Code给它擦屁股，20分钟就解决了。
5. 随时存档，git commit 是你的后悔药：每次 Claude 完成一个独立的小任务，立刻 git commit 保存当前状态 。万一后续出现 Bug，可以轻松回溯，避免大量的返工和 Token 浪费。

第三层：高阶篇（极限省钱大师）
1. 强制约束，给 Claude 上“紧箍咒”：这是最高级的技巧。在项目配置或初始提示中，用规则强制约束 Claude 的行为 。例如：禁止读取：明确禁止读取日志文件、锁文件、二进制文件等。禁用工具：除非明确要求，否则禁用某些工具的使用权限。设置预算：设定 Token 预算、延迟目标、每次获取最大行数等硬性限制。
2. 精简输入，只喂“干货”：不要给 Claude 整个文件，只给它预期会更改的代码，外加周边 20-40 行的相关上下文 。**用5点总结替代长篇大论的文档。传递文件路径而非原始内容，让模型按需请求**。这样做，同样任务的 Token 消耗能减少80%以上！
在做跨对话、甚至跨AI的时候，可以用我之前分享的这个提示词，提前把内容做压缩总结：https://mp.weixin.qq.com/s/cPgAVS07EvCjxpPwYdmUww

###附压缩prompt（https://mp.weixin.qq.com/s/cPgAVS07EvCjxpPwYdmUww）
分享一个 AI 对话总结提示词，可用于跨模型交接、切换新对话等场景不同 AI 都有自己的特性，所以我日常都是多个 AI搭配用，例如 o3 做规划方案、claude 做执行、gemini 写总结文章。但这样，不同工具共享一个上下文就成为了痛点。
此时这个提示词就能派上用场，快速总结当前对话的重点内容，用于跨模型或者切换新对话等场景，包括：
1. 对话“打包”与交接
它要求模型生成一份“全景式”报告，把当前对话中的每个要点、背景信息、决策脉络都梳理出来，方便把这份摘要交给另一实例（或另一模型）继续工作，而不会丢失上下文。
2. 绕过上下文长度限制
大模型一次能记住的 token 有上限。把长对话压缩成详尽摘要后，再喂给模型，既节省 token，又保留关键信息。
3. 减少“忘记/走偏”风险
总结完毕再继续对话，相当于给模型定期“校准”。这样新一轮回答会更聚焦、连贯，降低跑题或幻觉概率。
4. 便于归档 & 复用
报告可直接存档，用作项目文档、会议纪要、下次 prompt 的素材，也方便后续检索和复盘。
提示词：
Please provide a comprehensive report on everything we've spoken about in this conversation. It should outline all elements to such a degree that by giving this report to a new AI instance it will have all the necessary context to pick up and continue from where we are right now. Do not worry about token output length.

