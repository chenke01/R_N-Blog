# 个人博客系统

一个基于纯前端技术的个人博客系统，专为GitHub Pages设计。

## ✨ 特性

- 🚀 **纯前端** - 无需后端，直接部署到GitHub Pages
- 📝 **Markdown支持** - 丢入.md文件即可显示
- 🏷️ **标签分类** - 自动提取标签，支持分类筛选
- 🎨 **五套主题** - 暗黑、白色、赛博朋克、复古纸张、霓虹风格
- 🌟 **科技感UI** - 全屏Hero区、粒子动画、滚动渐入效果
- 📱 **响应式** - 适配各种屏幕尺寸
- 💻 **代码高亮** - 支持多种编程语言
- 🔍 **下拉搜索** - 从导航栏搜索图标下拉打开，快速筛选文章
- 🖼️ **图片说明** - Markdown图片的alt文本自动显示为图片说明文字
- 📑 **固定目录** - 文章页左侧目录栏固定，独立滚动
- 🤖 **AI 助手** - 内置智能对话助手，支持大语言模型问答

## 🚀 快速开始

### 本地运行

```bash
# 使用Node.js
npm install -g http-server
http-server -p 8080

# 或使用Python
python -m http.server 8080
```

### 部署到GitHub Pages

1. Fork或克隆本仓库
2. 上传你的Markdown文件到 `posts` 文件夹
3. 更新 `posts/manifest.json`
4. 在仓库Settings中启用GitHub Pages
5. 等待几分钟即可访问

## 📝 添加文章

1. 在 `posts` 文件夹创建 `.md` 文件
2. 添加Frontmatter：

```yaml
---
title: 文章标题
date: 2024-01-20
tags: [标签1, 标签2]
author: 作者名
excerpt: 文章摘要
image: images/cover.jpg  # 可选，封面图片路径
---

正文内容...
```

3. 更新 `posts/manifest.json`
4. 刷新页面

### 使用图片

将图片放入 `images/` 文件夹，在Markdown中引用：

```markdown
![图片说明文字](images/your-image.jpg)
```

- 图片说明文字（alt文本）会自动显示在图片下方作为说明
- 支持相对路径和绝对URL
- 建议图片宽度不超过内容区宽度

## 🎨 主题切换

点击主题按钮循环切换，共十套风格：

| 主题 | 图标 | 说明 |
|------|------|------|
| Dark | ◐ | 暗黑模式（默认） |
| Light | ○ | 白色模式 |
| Cyberpunk | ◈ | 赛博朋克（紫色霓虹风格） |
| Sepia | ◎ | 复古纸张（暖色调，适合阅读） |
| Neon | ◆ | 霓虹风格（深紫底色 + 粉青点缀） |
| Nord | ❖ | Nord 配色（冷色调灰蓝，护眼舒适） |
| Dracula | ❂ | 吸血鬼主题（深紫灰 + 紫色强调） |
| Ocean | ≋ | 深海风格（深蓝底色 + 青绿强调） |
| Forest | ♧ | 森林风格（深绿底色 + 绿色强调） |
| Sunset | ☀ | 日落风格（深红底色 + 粉橙强调） |

所有 UI 元素（粒子、滚动条、导航栏、卡片等）均跟随主题变化。

## 🔍 搜索功能

点击导航栏右侧的搜索图标，会从图标下方弹出搜索框：

- 输入关键词即时筛选文章
- 按 `ESC` 或点击外部区域关闭
- 支持按标题、摘要、标签搜索

## 📑 文章目录

文章详情页左侧显示固定目录栏：

- 目录栏固定在屏幕左侧，不随文章滚动
- 返回首页按钮与目录之间有明确间隔
- 目录列表独立滚动，阅读文章时自动高亮当前章节
- 点击目录项平滑滚动到对应位置
- 屏幕宽度 ≤ 768px 时目录自动隐藏

## 🤖 AI 智能助手

内置 AI 对话助手，支持大语言模型问答。

### 配置

打开 `js/chat.js`，替换 API Key：

```javascript
config: {
    apiUrl: 'https://open.bigmodel.cn/api/paas/v4/chat/completions',
    apiKey: 'YOUR_API_KEY_HERE',  // 替换为你的智谱 API Key
    model: 'glm-4-flash',
    maxTokens: 1024
}
```

API Key 获取地址：https://open.bigmodel.cn/

### 使用

- 点击右下角聊天图标打开对话窗口
- 在底部输入框输入问题，回车或点击发送
- 对话历史自动保存，刷新页面不丢失
- 支持清空对话、关闭窗口

## 📁 项目结构

```
├── index.html              # 首页
├── article.html            # 文章详情页
├── css/
│   ├── style.css           # 主样式
│   └── highlight-github-dark.min.css  # 代码高亮样式
├── js/
│   ├── app.js              # 首页核心逻辑
│   ├── markdown.js         # Markdown解析
│   ├── theme.js            # 主题管理（5套主题）
│   ├── chat.js             # AI 对话助手
│   └── vendor/
│       ├── marked.min.js   # Markdown解析库
│       └── highlight.min.js # 代码高亮库
├── images/                 # 图片资源目录
├── posts/                  # Markdown文章
│   ├── manifest.json       # 文章列表
│   └── *.md                # 文章文件
└── docs/                   # 文档
```

## 🛠️ 自定义

### 修改配置

编辑 `js/app.js` 中的配置：

```javascript
config: {
    postsDirectory: 'posts',
    postsPerPage: 10
}
```

### 添加主题

在 `js/theme.js` 的 `themes` 对象中添加新主题，需包含以下 CSS 变量：

```javascript
新主题: {
    name: '主题名',
    icon: '图标',
    colors: {
        '--bg-primary': '#背景色',
        '--bg-secondary': '#次要背景',
        '--bg-tertiary': '#三级背景',
        '--bg-card': '#卡片背景',
        '--text-primary': '#主文字',
        '--text-secondary': '#次要文字',
        '--text-muted': '#弱化文字',
        '--accent': '#强调色',
        '--accent-dim': '#次要强调色',
        '--border': '#边框色',
        '--border-light': '#浅边框色',
        '--shadow': '阴影色',
        '--glow': '发光色'
    }
}
```

### 切换 AI 模型

在 `js/chat.js` 中修改 `model` 字段：

```javascript
config: {
    model: 'glm-4-flash',   // 快速模型
    // model: 'glm-4',      // 标准模型
    // model: 'glm-4v',     // 多模态模型（支持图片）
}
```

## 📖 文档

- [项目文档](docs/项目文档.md) - 详细了解项目架构
- [操作文档](docs/操作文档.md) - 使用指南和常见问题

## 🌐 浏览器支持

- Chrome 60+
- Firefox 60+
- Safari 12+
- Edge 79+

## 📄 许可证

MIT License

## 🤝 贡献

欢迎提交Issue和Pull Request！

## 📧 联系

如有问题，请提交Issue。