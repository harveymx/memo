# 准备小程序开发

学习利用vible coding来做小程序，在windows11安装codeBase AI CLI，并创建一个示例项目：选择困难综合症点菜神器

> 本项目基于 [**CloudBase AI ToolKit**](https://github.com/TencentCloudBase/CloudBase-AI-ToolKit) 开发，通过AI提示词和 MCP 协议+云开发，让开发更智能、更高效，支持AI生成全栈代码、一键部署至腾讯云开发（免服务器）、智能日志修复。主要使用的链接有腾讯codebase的官方doc：https://docs.cloudbase.net/ai/cloudbase-ai-toolkit/getting-started ；以及，https://docs.cloudbase.net/cli-v1/ai/introduce 稀土掘金的博客文章：https://juejin.cn/post/7538713557677916203

## 以下是AI自动生成的md文件说明：

## 项目特点

- 📄 小程序完善的前端开发能力
- 🚀 集成云开发云函数等后端能力
- 🤖 集成 AI IDE 规则，提供智能化开发体验
- ☁️ 集成云开发 MCP，提供一站式云服务开发部署体验
- 🎁 深度集成腾讯云开发 CloudBase，提供一站式后端云服务

## 项目架构

### 云函数
- `getOpenId`：用于获取用户的 `openid`、`appid` 和 `unionid`。

### 小程序页面
- `index`：首页，展示项目信息、用户OpenID和CloudBase功能特点。

### 自定义组件
- `cloudbase-badge`：CloudBase品牌标识组件，可复用的badge显示组件。

## 开始使用

### 前提条件
- 安装小程序开发工具。
- 拥有腾讯云开发账号。

### 安装依赖
云函数依赖已在 `cloudfunctions/getOpenId/package.json` 中定义，可在云开发控制台中安装依赖。

### 配置云开发环境
在小程序开发工具中，打开 `miniprogram/app.js` 文件里修改环境 ID，找到如下代码部分：
```javascript
wx.cloud.init({
  env: 'your-env-id', // 替换为你的云开发环境 ID  
  traceUser: true,
});
```
将 `your-env-id` 替换为你实际的云开发环境 ID。

### 本地开发
1. 打开小程序开发工具，导入本项目。
2. 上传并部署 `getOpenId` 云函数。
3. 点击开发工具中的预览按钮，查看效果。

## 目录结构
```
├── cloudfunctions/
│   └── getOpenId/
│       ├── index.js
│       └── package.json
├── miniprogram/
│   ├── app.js
│   ├── app.json
│   ├── app.wxss
│   ├── components/
│   │   └── cloudbase-badge/      # CloudBase徽章组件
│   │       ├── index.js
│   │       ├── index.json
│   │       ├── index.wxml
│   │       └── index.wxss
│   ├── images/
│   │   └── powered-by-cloudbase-badge.svg  # CloudBase徽章图标
│   ├── pages/
│   │   └── index/
│   │       ├── index.js
│   │       ├── index.json
│   │       ├── index.wxml
│   │       └── index.wxss
│   └── sitemap.json
├── project.config.json
└── project.private.config.json
```

## 云开发使用示例

通过 `wx.cloud` 访问云开发服务：

```javascript
// 数据库操作
const db = wx.cloud.database();
const result = await db.collection('users').get(); // 查询数据
await db.collection('users').add({ data: { name: 'test' } }); // 添加数据

// 调用云函数
const funcResult = await wx.cloud.callFunction({ name: 'getOpenId' });

// 文件上传
const uploadResult = await wx.cloud.uploadFile({ cloudPath: 'test.jpg', filePath: tempFilePath });
// 调用数据模型
const models = wx.cloud.models;
```

## 扩展开发
您可以根据项目需求，添加新的云函数和页面，实现更多的云开发功能。# 美食选择工具 - 微信小程序

## 项目介绍
这是一个专为选择困难症用户设计的微信小程序，帮助用户快速决定吃什么。通过预设和用户自定义的食物列表，随机选择出最终结果。

## 功能特点

### 🎯 核心功能
- **预设美食推荐**：内置12种常见美食选择
- **自定义添加**：支持用户输入任意餐厅或食物名称
- **智能随机选择**：动画效果展示选择过程
- **本地存储**：自动保存用户的备选列表

### 🎨 界面设计
- 清新绿色主题，符合美食应用调性
- 卡片式布局，操作直观
- 流畅的动画反馈
- 响应式交互设计

### 📱 技术实现
- **框架**：微信小程序原生开发
- **样式**：WXSS + Flex布局
- **存储**：小程序本地存储(wx.setStorageSync)
- **动画**：微信小程序动画API

## 项目结构

```
miniprogram/
├── pages/
│   └── index/
│       ├── index.wxml    # 页面结构
│       ├── index.wxss    # 页面样式
│       ├── index.js      # 页面逻辑
│       └── index.json    # 页面配置
├── app.js               # 小程序逻辑
├── app.json             # 小程序公共配置
└── app.wxss             # 小程序公共样式
```

## 使用说明

### 开发环境
1. 使用微信开发者工具打开项目
2. 确保已配置云开发环境
3. 项目根目录为包含 `project.config.json` 的目录

### 功能操作
1. **添加预设食物**：点击推荐美食卡片直接添加
2. **自定义添加**：在输入框中输入食物名称后点击添加
3. **删除食物**：点击备选列表中的 × 按钮
4. **随机选择**：点击"帮我选择！"按钮开始随机选择

### 部署步骤
1. 在微信开发者工具中点击"上传"
2. 填写版本号和项目备注
3. 提交审核并发布

## 云开发配置

本项目使用微信小程序云开发能力，需要配置：
- 云开发环境ID：cloud1-4gn8s0yuda68deed
- 本地存储用于保存用户数据

## 更新日志

### v1.0.0 (2024-09-17)
- ✅ 基础功能实现
- ✅ 预设食物列表
- ✅ 自定义添加功能
- ✅ 随机选择动画
- ✅ 本地数据存储
- ✅ 响应式界面设计

## 开发团队
- 基于微信小程序云开发模板
- 专为选择困难症用户优化

## 联系方式
如有问题或建议，请通过小程序客服联系我们。
