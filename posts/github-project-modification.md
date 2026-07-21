---
title: GitHub项目修改与部署完整指南
date: 2026-07-21
tags: [技术, 教程, GitHub]
author: 渡鸦NULL
excerpt: 详细介绍如何修改GitHub上已有的项目，并确保修改后的内容在GitHub Pages中正确显示。
---

# GitHub项目修改与部署完整指南

本文档详细介绍如何修改GitHub上已有的项目，并确保修改后的内容在GitHub Pages中正确显示。

---

## 一、准备工作

### 1.1 安装Git工具

首先需要在本地安装Git工具：

**Windows系统：**
1. 访问 https://git-scm.com/download/win
2. 下载并安装Git for Windows
3. 安装过程中保持默认设置

**Mac系统：**
```bash
# 使用Homebrew安装
brew install git
```

**Linux系统：**
```bash
# Ubuntu/Debian
sudo apt-get install git

# CentOS/RHEL
sudo yum install git
```

### 1.2 配置Git身份信息

```bash
# 设置用户名
git config --global user.name "你的GitHub用户名"

# 设置邮箱
git config --global user.email "你的GitHub邮箱"
```

---

## 二、克隆项目到本地

### 2.1 获取仓库地址

1. 打开GitHub仓库页面：`https://github.com/chenke01/R_N-Blog`
2. 点击绿色的 **Code** 按钮
3. 复制HTTPS地址：`https://github.com/chenke01/R_N-Blog.git`

### 2.2 克隆仓库

打开终端或命令行，执行以下命令：

```bash
# 克隆仓库到本地
git clone https://github.com/chenke01/R_N-Blog.git

# 进入项目目录
cd R_N-Blog
```

### 2.3 查看项目结构

```bash
# 查看目录结构
ls -la

# 或使用Windows命令
dir
```

---

## 三、修改项目内容

### 3.1 修改现有文章

1. 进入 `posts` 文件夹
2. 使用文本编辑器（如VS Code）打开 `.md` 文件
3. 修改内容后保存

**示例：修改文章标题**
```markdown
---
title: 新的文章标题
date: 2026-07-21
tags: [技术, 教程]
author: 作者名
excerpt: 这是新的文章摘要
---

# 新的标题

这里是新的内容...
```

### 3.2 添加新文章

1. 在 `posts` 文件夹中创建新的 `.md` 文件
2. 编写文章内容
3. 更新 `manifest.json` 文件

**步骤一：创建新文章文件**

```bash
# 在posts文件夹中创建新文件
touch posts/my-new-article.md
```

**步骤二：编写文章内容**

```markdown
---
title: 我的新文章
date: 2026-07-21
tags: [技术, 生活]
author: 你的名字
excerpt: 这是文章的摘要，会显示在首页卡片上。
image: images/cover.jpg  # 可选，封面图片路径
---

# 文章标题

## 第一部分

这里是文章内容...

## 第二部分

更多内容...
```

**步骤三：更新manifest.json**

打开 `posts/manifest.json` 文件，添加新文章的文件名：

```json
[
    "blog-usage-guide.md",
    "github-guide.md",
    "javascript-async.md",
    "jimeng-ai-prompt-framework.md",
    "upload-to-github.md",
    "my-new-article.md"
]
```

### 3.3 修改样式文件

如果需要修改博客样式：

1. 打开 `css/style.css` 文件
2. 找到需要修改的CSS属性
3. 修改后保存

**示例：修改主题颜色**
```css
:root {
    --bg-primary: #0a0a0a;      /* 主背景色 */
    --text-primary: #f0f0f0;    /* 主文字颜色 */
    --accent: #ffffff;          /* 强调色 */
}
```

### 3.4 修改JavaScript功能

如果需要修改博客功能：

1. 打开 `js/app.js` 文件
2. 找到需要修改的函数
3. 修改后保存

**示例：修改每页显示文章数量**
```javascript
config: {
    postsDirectory: 'posts',
    postsPerPage: 12  // 修改为12篇
}
```

---

## 四、提交更改到GitHub

### 4.1 查看修改状态

```bash
# 查看哪些文件被修改
git status
```

### 4.2 添加文件到暂存区

```bash
# 添加所有修改的文件
git add .

# 或者添加特定文件
git add posts/my-new-article.md
git add posts/manifest.json
```

### 4.3 提交更改

```bash
# 提交更改
git commit -m "添加新文章：我的新文章"
```

### 4.4 推送到GitHub

```bash
# 推送到远程仓库
git push origin main
```

---

## 五、GitHub Pages部署配置

### 5.1 启用GitHub Pages

1. 进入仓库设置：`https://github.com/chenke01/R_N-Blog/settings`
2. 左侧菜单找到 **Pages**
3. 在 **Source** 部分选择 **Deploy from a branch**
4. **Branch** 选择 `main`
5. **Folder** 选择 `/ (root)`
6. 点击 **Save**

### 5.2 添加.nojekyll文件

为确保GitHub Pages正确处理所有文件，在项目根目录创建 `.nojekyll` 文件：

```bash
# 创建.nojekyll文件
touch .nojekyll

# 提交并推送
git add .nojekyll
git commit -m "添加.nojekyll文件"
git push origin main
```

### 5.3 等待部署完成

1. 进入仓库的 **Actions** 选项卡
2. 查看部署工作流状态
3. 等待5-10分钟让部署完成

---

## 六、验证修改结果

### 6.1 检查GitHub仓库

1. 访问 `https://github.com/chenke01/R_N-Blog`
2. 确认文件已更新
3. 检查提交历史

### 6.2 检查GitHub Pages

1. 访问 `https://chenke01.github.io/R_N-Blog/`
2. 确认新文章已显示
3. 检查样式和功能是否正常

### 6.3 测试文章访问

测试以下URL是否正常：
- `https://chenke01.github.io/R_N-Blog/posts/manifest.json`
- `https://chenke01.github.io/R_N-Blog/posts/my-new-article.md`

---

## 七、常见问题解决

### Q1: 推送后GitHub Pages没有更新？

**解决方案：**
1. 检查 **Actions** 选项卡是否有部署错误
2. 等待10-15分钟让部署完成
3. 清除浏览器缓存后重试

### Q2: 文章显示404错误？

**解决方案：**
1. 检查 `manifest.json` 文件是否正确更新
2. 确认文件名大小写一致
3. 确认 `.nojekyll` 文件已添加

### Q3: 样式显示异常？

**解决方案：**
1. 检查CSS文件语法是否正确
2. 确认文件路径正确
3. 清除浏览器缓存

### Q4: 如何撤回错误的提交？

**解决方案：**
```bash
# 撤回最后一次提交（保留修改）
git reset --soft HEAD~1

# 撤回最后一次提交（丢弃修改）
git reset --hard HEAD~1
```

---

## 八、高级技巧

### 8.1 使用分支进行开发

```bash
# 创建新分支
git checkout -b feature/new-article

# 在新分支上开发
# ...

# 切换回主分支
git checkout main

# 合并新分支
git merge feature/new-article

# 推送更改
git push origin main
```

### 8.2 使用.gitignore文件

创建 `.gitignore` 文件排除不需要的文件：

```gitignore
# 忽略node_modules
node_modules/

# 忽略系统文件
.DS_Store
Thumbs.db

# 忽略编辑器配置
.vscode/
.idea/
```

### 8.3 使用GitHub Desktop

如果不喜欢命令行，可以使用GitHub Desktop：
1. 下载：https://desktop.github.com/
2. 登录GitHub账号
3. 克隆仓库
4. 修改文件后点击 **Commit to main**
5. 点击 **Push origin**

---

## 九、最佳实践

### 9.1 定期备份

```bash
# 定期拉取最新代码
git pull origin main

# 创建备份分支
git checkout -b backup/2026-07-21
```

### 9.2 提交信息规范

使用清晰的提交信息：
```bash
# 好的提交信息
git commit -m "添加新文章：GitHub项目修改指南"
git commit -m "修复首页样式问题"
git commit -m "更新manifest.json"

# 不好的提交信息
git commit -m "更新"
git commit -m "修复bug"
```

### 9.3 文件命名规范

- 使用小写字母
- 使用连字符分隔单词
- 避免空格和特殊字符

**示例：**
```
✅ github-project-modification.md
✅ my-new-article.md
❌ GitHub Project Modification.md
❌ 我的文章.md
```

---

## 十、总结

通过本文档，你已经学会了：

1. ✅ 如何克隆GitHub项目到本地
2. ✅ 如何修改项目内容
3. ✅ 如何添加新文章
4. ✅ 如何提交和推送更改
5. ✅ 如何配置GitHub Pages
6. ✅ 如何解决常见问题

现在你可以轻松地修改和维护你的GitHub项目了！

---

**相关链接：**
- [GitHub Pages官方文档](https://docs.github.com/en/pages)
- [Git官方文档](https://git-scm.com/doc)
- [Markdown语法指南](https://www.markdownguide.org/)

**最后更新：** 2026-07-21
**维护者：** 渡鸦NULL
