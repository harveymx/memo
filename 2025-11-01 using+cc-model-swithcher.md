
> 2025-11-01 安装cc-model-switcher，便捷更换claude code的模型环境
## 安装cc-model-switcher，便捷更换claude code的模型环境
>https://github.com/XiaYeAI/cc-model-switcher
>还有一个更强大的cc-switch，它使用GUI界面，但没有这个简洁：https://zhuanlan.zhihu.com/p/1957906461037421251 ；https://news.qq.com/rain/a/20250901A08V7J00 ；https://github.com/farion1231/cc-switch

# 🚀 cc-switch - Claude Code模型切换器

一个简洁的Node.js CLI工具，用于快速切换Claude Code的大模型。

## 📦 安装

```bash
npm install -g cc-model-switcher
```

## 🎯 使用方法

安装完成后，你可以在任何路径下使用以下命令：

### 基本使用
```bash
cc_switch              # 使用默认Kimi模型
cc_switch deepseek     # 使用DeepSeek模型
cc_switch --list       # 查看所有可用模型
cc_switch --interactive  # 交互式选择模型
```

### 简写命令
```bash
cc_switch -l           # 查看所有模型
cc_switch -i           # 交互式选择
```

## 🔧 配置

安装后会在用户主目录下创建 `.models.json` 配置文件：

**Windows:** `C:\Users\用户名\.models.json`
**macOS/Linux:** `~/.models.json`

### 添加新模型

编辑 `~/.models.json` 文件，添加更多模型：

```json
{
  "models": {
    "your_model": {
      "description": "Your custom model",
      "env": {
        "ANTHROPIC_BASE_URL": "https://api.your-model.com/anthropic",
        "ANTHROPIC_AUTH_TOKEN": "your-api-key",
        "API_TIMEOUT_MS": "600000",
        "ANTHROPIC_MODEL": "your-model-name",
        "ANTHROPIC_SMALL_FAST_MODEL": "your-model-name"
      }
    }
  }
}
```

## 📋 默认模型

| 模型名称 | 描述 |
|----------|------|
| `kimi` | Kimi AI (Moonshot) |
| `deepseek` | DeepSeek V3.1 |

## 🏗️ 开发

```bash
# 克隆项目
git clone [项目地址]
cd cc-model-switcher

# 安装依赖
npm install

# 本地测试
npm link

# 取消本地链接
npm unlink -g cc-model-switcher
```

## 🚀 发布到npm

```bash
# 登录npm
npm login

# 发布
npm publish
```

## 📄 许可证

MIT