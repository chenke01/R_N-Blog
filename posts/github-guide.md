---
title: GitHub 完全使用指南
date: 2026-07-21
tags: [技术, 教程]
author: 渡鸦NULL
excerpt: 从注册账号到高级使用，全面掌握 GitHub 的每一个功能，包括仓库管理、协作开发、Pages 部署等。
---

# GitHub 完全使用指南

GitHub 是全球最大的代码托管平台，也是开发者必备的工具。本文将从零开始，带你全面掌握 GitHub 的使用。

---

## 一、GitHub 简介

### 1.1 什么是 GitHub

GitHub 是一个基于 Git 版本控制系统的代码托管平台，提供：

- **代码托管**：安全存储你的代码
- **版本控制**：追踪代码的每一次修改
- **协作开发**：多人同时开发同一个项目
- **开源社区**：发现和贡献开源项目
- **自动化**：CI/CD、项目管理等

### 1.2 GitHub 与 Git 的关系

- **Git**：版本控制工具，安装在本地电脑
- **GitHub**：在线平台，提供代码托管和协作功能
- Git 是工具，GitHub 是平台，两者配合使用

---

## 二、注册与设置

### 2.1 注册账号

1. 访问 https://github.com
2. 点击 **Sign up** 按钮
3. 输入邮箱、密码、用户名
4. 完成邮箱验证
5. 选择免费计划（Free）

### 2.2 个人资料设置

点击右上角头像 → **Settings**：

- **Profile**：设置头像、简介、位置、个人网站
- **Account**：修改用户名、删除账号
- **Emails**：管理邮箱地址
- **Notifications**：设置通知偏好

### 2.3 设置 SSH Key

SSH Key 可以让你无需每次输入密码：

```bash
# 生成 SSH Key
ssh-keygen -t ed25519 -C "your_email@example.com"

# 查看公钥
cat ~/.ssh/id_ed25519.pub
```

将公钥添加到 GitHub：
1. 点击右上角头像 → **Settings**
2. 左侧菜单选择 **SSH and GPG keys**
3. 点击 **New SSH key**
4. 粘贴公钥内容并保存

---

## 三、安装与配置 Git

### 3.1 安装 Git

**Windows：**
1. 访问 https://git-scm.com/download/win
2. 下载安装包并运行
3. 保持默认选项即可

**Mac：**
```bash
# 使用 Homebrew
brew install git
```

**Linux：**
```bash
# Ubuntu/Debian
sudo apt-get install git

# CentOS
sudo yum install git
```

### 3.2 配置 Git

```bash
# 设置用户名（必须与 GitHub 用户名一致）
git config --global user.name "你的用户名"

# 设置邮箱（必须与 GitHub 注册邮箱一致）
git config --global user.email "your_email@example.com"

# 查看配置
git config --list
```

---

## 四、仓库管理

### 4.1 创建仓库

**在 GitHub 上创建：**

1. 点击右上角 **+** → **New repository**
2. 填写仓库名称
3. 选择公开（Public）或私有（Private）
4. 勾选 **Initialize this repository with a README**
5. 点击 **Create repository**

**在本地创建并推送到 GitHub：**

```bash
# 创建项目文件夹
mkdir my-project
cd my-project

# 初始化 Git 仓库
git init

# 创建文件并提交
echo "# My Project" > README.md
git add README.md
git commit -m "Initial commit"

# 关联远程仓库
git remote add origin https://github.com/用户名/仓库名.git

# 推送到 GitHub
git push -u origin main
```

### 4.2 克隆仓库

```bash
# 使用 HTTPS
git clone https://github.com/用户名/仓库名.git

# 使用 SSH
git clone git@github.com:用户名/仓库名.git
```

### 4.3 Fork 仓库

Fork 是将别人的仓库复制到自己的账号下：

1. 打开要 Fork 的仓库页面
2. 点击右上角 **Fork** 按钮
3. 选择你的账号
4. 等待 Fork 完成

Fork 后可以：
- 自由修改代码
- 向原仓库提交 Pull Request
- 同步原仓库的更新

---

## 五、Git 基本操作

### 5.1 工作流程

```
工作区 → 暂存区 → 本地仓库 → 远程仓库
```

### 5.2 常用命令

```bash
# 查看状态
git status

# 添加文件到暂存区
git add 文件名        # 添加指定文件
git add .            # 添加所有文件

# 提交到本地仓库
git commit -m "提交说明"

# 推送到远程仓库
git push origin 分支名

# 拉取远程更新
git pull origin 分支名

# 查看提交历史
git log
git log --oneline    # 简洁模式
```

### 5.3 分支管理

```bash
# 查看分支
git branch

# 创建分支
git branch 分支名

# 切换分支
git checkout 分支名

# 创建并切换分支
git checkout -b 分支名

# 合并分支
git checkout main
git merge 分支名

# 删除分支
git branch -d 分支名
```

### 5.4 撤销操作

```bash
# 撤销工作区修改
git checkout -- 文件名

# 撤销暂存区文件
git reset HEAD 文件名

# 撤销最后一次提交（保留修改）
git reset --soft HEAD~1

# 撤销最后一次提交（丢弃修改）
git reset --hard HEAD~1
```

---

## 六、Pull Request

### 6.1 什么是 Pull Request

Pull Request（PR）是向原仓库贡献代码的方式：

1. Fork 仓库并克隆到本地
2. 创建新分支进行修改
3. 推送到你的 GitHub 仓库
4. 向原仓库提交 Pull Request
5. 等待审核和合并

### 6.2 提交 Pull Request

```bash
# 1. Fork 并克隆仓库
git clone https://github.com/你的用户名/仓库名.git

# 2. 创建新分支
git checkout -b feature/my-feature

# 3. 修改代码并提交
git add .
git commit -m "Add my feature"

# 4. 推送到你的仓库
git push origin feature/my-feature

# 5. 在 GitHub 上点击 "New pull request"
```

### 6.3 Pull Request 最佳实践

- **标题清晰**：简要说明修改内容
- **详细描述**：解释为什么要做这个修改
- **关联 Issue**：如果修复了某个 Issue，在描述中引用
- **保持小 PR**：每个 PR 只做一件事
- **及时响应**：回复审核者的评论

---

## 七、Issue 管理

### 7.1 创建 Issue

Issue 用于报告 bug、提出建议或讨论问题：

1. 进入仓库页面
2. 点击 **Issues** 标签
3. 点击 **New issue**
4. 填写标题和描述
5. 添加标签（Labels）
6. 点击 **Submit new issue**

### 7.2 Issue 最佳实践

- **使用模板**：如果仓库有 Issue 模板，按模板填写
- **提供复现步骤**：报告 bug 时要详细说明如何复现
- **截图说明**：必要时提供截图或录屏
- **搜索现有 Issue**：避免重复提交

### 7.3 关联 Issue

在提交信息中引用 Issue：

```bash
# 自动关闭 Issue
git commit -m "Fix #123: 修复登录问题"

# 只引用不关闭
git commit -m "Ref #123: 部分修复登录问题"
```

---

## 八、GitHub Pages

### 8.1 什么是 GitHub Pages

GitHub Pages 是免费的静态网站托管服务，可以用来部署：

- 个人博客
- 项目文档
- 作品集

### 8.2 部署步骤

**方式一：从分支部署**

1. 进入仓库 **Settings** → **Pages**
2. **Source** 选择 `Deploy from a branch`
3. **Branch** 选择 `main` 或 `master`
4. 文件夹选择 `/ (root)` 或 `/docs`
5. 点击 **Save**

**方式二：使用 GitHub Actions**

创建 `.github/workflows/pages.yml`：

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/configure-pages@v3
      - uses: actions/jekyll-build-pages@v1
      - uses: actions/upload-pages-artifact@v1
  
  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - uses: actions/deploy-pages@v1
        id: deployment
```

### 8.3 访问网站

部署完成后，访问地址为：

```
https://用户名.github.io/仓库名/
```

如果仓库名是 `用户名.github.io`，则直接访问：

```
https://用户名.github.io/
```

### 8.4 自定义域名

1. 在仓库根目录创建 `CNAME` 文件，内容为你的域名
2. 在域名服务商设置 DNS：
   - A 记录：`185.199.108.153`、`185.199.109.153`、`185.199.110.153`、`185.199.111.153`
   - 或 CNAME 记录：`用户名.github.io`
3. 在 GitHub Pages 设置中勾选 **Enforce HTTPS**

---

## 九、GitHub Actions

### 9.1 什么是 GitHub Actions

GitHub Actions 是自动化工具，可以：

- 自动运行测试
- 自动部署项目
- 自动发布版本

### 9.2 工作流文件

工作流文件放在 `.github/workflows/` 目录：

```yaml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Install dependencies
        run: npm install
      - name: Run tests
        run: npm test
```

### 9.3 常用 Actions

- **actions/checkout**：检出代码
- **actions/setup-node**：设置 Node.js 环境
- **actions/upload-artifact**：上传构建产物
- **peaceiris/actions-gh-pages**：部署到 GitHub Pages

---

## 十、协作技巧

### 10.1 代码审查

- 使用 Pull Request 进行代码审查
- 提供建设性的反馈
- 及时回应审查意见

### 10.2 项目管理

- 使用 **Projects** 管理任务
- 使用 **Milestones** 规划版本
- 使用 **Labels** 分类 Issue

### 10.3 团队协作

- 制定分支策略（如 Git Flow）
- 编写贡献指南（CONTRIBUTING.md）
- 使用代码规范和自动化检查

---

## 十一、常见问题

### Q: 如何撤销已推送的提交？

A: 使用 `git revert` 创建新的提交来撤销：

```bash
git revert HEAD
git push origin main
```

### Q: 如何同步 Fork 的仓库？

A: 添加原仓库为 upstream 并拉取更新：

```bash
git remote add upstream https://github.com/原作者/仓库名.git
git fetch upstream
git merge upstream/main
```

### Q: 如何解决合并冲突？

A: 手动编辑冲突文件，选择要保留的代码，然后：

```bash
git add 冲突文件
git commit -m "Resolve merge conflict"
```

### Q: GitHub 免费账号有什么限制？

A: 免费账号提供：
- 无限公开仓库
- 无限私有仓库（最多 3 个协作者）
- 2000 分钟 GitHub Actions 时间/月
- 1GB GitHub Packages 存储

### Q: 如何删除仓库？

A: 进入仓库 **Settings** → **Danger Zone** → **Delete this repository**

---

## 十二、快捷键

| 按键 | 功能 |
|------|------|
| `T` | 文件搜索 |
| `S` / `/` | 全局搜索 |
| `G` + `N` | 跳转到通知 |
| `G` + `C` | 跳转到代码 |
| `G` + `I` | 跳转到 Issue |
| `G` + `P` | 跳转到 Pull Request |
| `.` | 在线编辑器 |
| `Ctrl + Enter` | 提交评论 |

---

感谢阅读这份 GitHub 使用指南！如有其他问题，欢迎反馈。
