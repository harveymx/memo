
# 准备小程序开发，创建vibe coding环境
学习利用vible coding来做小程序，在windows11安装claude code cli，使用kim大模型，agent功能增强，实际上实现了agentic能力，调用MCP。Kimi K2的Agentic能力的确不错，能够成功调度和操纵。
> 主要链接：
    > 月之暗面的官方文档: https://platform.moonshot.cn/docs/guide/agent-support#%E4%BD%BF%E7%94%A8%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9 ;
    > 刘小排的博客： https://mp.weixin.qq.com/s/3IdclzkMo_bMVw2CyZ5t3Q
## 安装Claude Code

 打开 windows 终端中的 powershell 终端，安装 nodejs：右键按 Windows 按钮，点击「终端」， 然后依次执行下面的
```
winget install OpenJS.NodeJS
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```
 
然后关闭终端窗口，新开一个终端窗口， 安装 claude-code
```
npm install -g @anthropic-ai/claude-code --registry=https://registry.npmmirror.com
```

#### 初始化配置
```
node --eval "
    const homeDir = os.homedir();
    const filePath = path.join(homeDir, '.claude.json');
    if (fs.existsSync(filePath)) {
        const content = JSON.parse(fs.readFileSync(filePath, 'utf-8'));
        fs.writeFileSync(filePath,JSON.stringify({ ...content, hasCompletedOnboarding: true }, 2), 'utf-8');
    } else {
        fs.writeFileSync(filePath,JSON.stringify({ hasCompletedOnboarding: true }), 'utf-8');
    }"
```

### 配置环境变量(可以直接设置到系统或者用户的环境便利中)
Windows Powershell 启动高速版 kimi-k2-turbo-preview 模型
```
$env:ANTHROPIC_BASE_URL="https://api.moonshot.cn/anthropic";
$env:ANTHROPIC_AUTH_TOKEN="YOUR_MOONSHOT_API_KEY"
$env:ANTHROPIC_MODEL="kimi-k2-turbo-preview"
$env:ANTHROPIC_SMALL_FAST_MODEL="kimi-k2-turbo-preview"
claude
```
### 确认环境变量是否生效
在Claude Code中输入/status确认模型状态.
## 安装Claude Code statusline状态栏（1-3步骤与上述重复）
1. 先卸载老的版本（如果有）： npm uninstall -g @anthropic-ai/claude-code
2. 然后安装： npm install -g @anthropic-ai/claude-code
3. 配置windows系统的环境变量：
```
ANTHROPIC_AUTH_TOKEN=sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxxx
ANTHROPIC_BASE_URL=https://api.moonshot.cn/anthropic
ANTHROPIC_MODEL=kimi-k2-turbo-preview
ANTHROPIC_SMALL_FAST_MODEL=kimi-k2-turbo-preview
//此处配置kimi模型，也可以选择其他模型
```
4. 安装Claude Code statusline状态栏：
```
在用户主目录下的.claude/settings.json文件中，添加：{
"statusLine": {
"type": "command",
"command": "~/.claude/statusline.sh",
"padding": 0
}}
//如果这个文件还不存在，手动创建。
```
## 做一个小练手（用 Claude Code + CloudBase + Figma 完成商业小程序全栈开发）
https://juejin.cn/post/7528712837885837353
该项目完成度比较高，但需要figma商业版，来支持MCP调用，自动生成前端