---
title: 各类项目上传 GitHub 完整指南
date: 2026-07-21
tags: [技术, 教程]
author: 渡鸦NULL
excerpt: 详细介绍如何将各种类型的项目上传到 GitHub，包括前端项目、Node.js 项目、Python 项目、静态网站等。
---

# 各类项目上传 GitHub 完整指南

本文详细介绍如何将各种类型的项目上传到 GitHub，涵盖前端、后端、Python、静态网站等常见项目类型。

---

## 一、上传前的准备工作

### 1.1 注册 GitHub 账号

访问 https://github.com 注册账号，建议用户名与你的身份相关。

### 1.2 安装 Git

**Windows：**
1. 访问 https://git-scm.com/download/win
2. 下载安装包，一路下一步即可

**Mac：**
```bash
brew install git
```

**Linux：**
```bash
sudo apt-get install git    # Ubuntu/Debian
sudo yum install git        # CentOS
```

### 1.3 配置 Git

```bash
git config --global user.name "你的用户名"
git config --global user.email "你的邮箱@example.com"
```

### 1.4 配置 SSH Key（推荐）

```bash
# 生成 SSH Key
ssh-keygen -t ed25519 -C "你的邮箱@example.com"

# 查看公钥
cat ~/.ssh/id_ed25519.pub
```

将公钥添加到 GitHub：
1. 点击右上角头像 → **Settings**
2. 左侧 **SSH and GPG keys** → **New SSH key**
3. 粘贴公钥并保存

---

## 二、通用上传流程

无论什么类型的项目，基本流程都是：

```bash
# 1. 进入项目目录
cd 项目目录

# 2. 初始化 Git 仓库
git init

# 3. 添加所有文件
git add .

# 4. 提交
git commit -m "Initial commit"

# 5. 关联远程仓库（在 GitHub 创建仓库后获得地址）
git remote add origin git@github.com:用户名/仓库名.git

# 6. 推送
git push -u origin main
```

---

## 三、前端项目（HTML/CSS/JS）

### 3.1 项目结构示例

```
my-website/
├── index.html
├── css/
│   └── style.css
├── js/
│   └── main.js
├── images/
│   └── logo.png
└── README.md
```

### 3.2 创建 .gitignore

```gitignore
# 编辑器配置
.vscode/
.idea/

# 系统文件
.DS_Store
Thumbs.db

# 日志
*.log
```

### 3.3 上传步骤

```bash
cd my-website
git init
git add .
git commit -m "Initial commit"
git remote add origin git@github.com:用户名/my-website.git
git push -u origin main
```

### 3.4 部署到 GitHub Pages

1. 进入仓库 **Settings** → **Pages**
2. **Source** 选择 `Deploy from a branch`
3. **Branch** 选择 `main`，文件夹选择 `/ (root)`
4. 保存后访问 `https://用户名.github.io/my-website/`

---

## 四、Vue / React 项目

### 4.1 项目结构示例

```
my-app/
├── public/
├── src/
├── package.json
├── vite.config.js
├── .gitignore
└── README.md
```

### 4.2 创建 .gitignore

```gitignore
node_modules/
dist/
.env
.env.local
*.log
.DS_Store
```

### 4.3 上传步骤

```bash
cd my-app
git init
git add .
git commit -m "Initial commit"
git remote add origin git@github.com:用户名/my-app.git
git push -u origin main
```

### 4.4 部署到 GitHub Pages

**方式一：使用 Vite 配置**

在 `vite.config.js` 中添加：

```javascript
export default defineConfig({
  base: '/仓库名/',
  // ...
})
```

构建并部署：

```bash
npm run build
git add dist -f
git commit -m "Add dist"
git subtree split --prefix dist -b gh-pages
git push -f origin gh-pages
```

**方式二：使用 GitHub Actions**

创建 `.github/workflows/deploy.yml`：

```yaml
name: Deploy

on:
  push:
    branches: [ main ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: 18
      - run: npm install
      - run: npm run build
      - uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
```

---

## 五、Node.js 项目

### 5.1 项目结构示例

```
my-api/
├── src/
│   ├── index.js
│   └── routes/
├── package.json
├── .env.example
├── .gitignore
└── README.md
```

### 5.2 创建 .gitignore

```gitignore
node_modules/
.env
dist/
*.log
coverage/
.DS_Store
```

### 5.3 创建 .env.example

```env
# 将 .env.example 提交到仓库，.env 不提交
PORT=3000
DATABASE_URL=your_database_url
SECRET_KEY=your_secret_key
```

### 5.4 上传步骤

```bash
cd my-api
git init
git add .
git commit -m "Initial commit"
git remote add origin git@github.com:用户名/my-api.git
git push -u origin main
```

### 5.5 README.md 模板

```markdown
# 项目名称

简短的项目描述

## 安装

```bash
npm install
```

## 配置

复制 `.env.example` 为 `.env` 并填写配置

## 运行

```bash
npm start
```

## API 文档

| 接口 | 方法 | 说明 |
|------|------|------|
| /api/users | GET | 获取用户列表 |
```

---

## 六、Python 项目

### 6.1 项目结构示例

```
my-python-app/
├── src/
│   ├── __init__.py
│   └── main.py
├── tests/
│   └── test_main.py
├── requirements.txt
├── .gitignore
├── README.md
└── setup.py
```

### 6.2 创建 .gitignore

```gitignore
__pycache__/
*.py[cod]
*$py.class
*.so
.Python
env/
venv/
.env
*.egg-info/
dist/
build/
.DS_Store
```

### 6.3 创建 requirements.txt

```bash
# 生成依赖文件
pip freeze > requirements.txt
```

示例内容：

```
flask==2.3.2
requests==2.31.0
pandas==2.0.3
```

### 6.4 上传步骤

```bash
cd my-python-app
git init
git add .
git commit -m "Initial commit"
git remote add origin git@github.com:用户名/my-python-app.git
git push -u origin main
```

### 6.5 README.md 模板

```markdown
# 项目名称

简短的项目描述

## 安装

```bash
pip install -r requirements.txt
```

## 使用

```bash
python src/main.py
```

## 测试

```bash
pytest tests/
```
```

---

## 七、静态网站 / 博客

### 7.1 项目结构示例

```
my-blog/
├── index.html
├── article.html
├── css/
├── js/
├── images/
├── posts/
└── README.md
```

### 7.2 上传步骤

```bash
cd my-blog
git init
git add .
git commit -m "Initial commit"
git remote add origin git@github.com:用户名/my-blog.git
git push -u origin main
```

### 7.3 部署到 GitHub Pages

1. 进入仓库 **Settings** → **Pages**
2. **Source** 选择 `Deploy from a branch`
3. **Branch** 选择 `main`，文件夹选择 `/ (root)`
4. 保存后访问 `https://用户名.github.io/my-blog/`

---

## 八、已有本地 Git 仓库

### 8.1 如果项目已经有 Git 仓库

```bash
# 直接关联远程仓库
git remote add origin git@github.com:用户名/仓库名.git

# 推送
git push -u origin main
```

### 8.2 如果远程仓库有内容（如 README）

```bash
# 先拉取远程内容
git pull origin main --allow-unrelated-histories

# 解决冲突后推送
git push -u origin main
```

---

## 九、大型项目注意事项

### 9.1 使用 Git LFS 管理大文件

```bash
# 安装 Git LFS
git lfs install

# 追踪大文件类型
git lfs track "*.psd"
git lfs track "*.zip"
git lfs track "*.mp4"

# 提交 .gitattributes
git add .gitattributes
git commit -m "Track large files with LFS"
```

### 9.2 .gitignore 常用规则

```gitignore
# 依赖目录
node_modules/
vendor/
venv/

# 构建产物
dist/
build/

# 环境变量
.env
.env.local

# 编辑器配置
.vscode/
.idea/

# 系统文件
.DS_Store
Thumbs.db

# 日志
*.log

# 缓存
.cache/
__pycache__/
```

### 9.3 提交信息规范

```bash
# 格式：<类型>: <描述>

# 常用类型
feat:     新功能
fix:      修复 bug
docs:     文档更新
style:    代码格式（不影响功能）
refactor: 重构
test:     测试相关
chore:    构建/工具相关

# 示例
git commit -m "feat: 添加用户登录功能"
git commit -m "fix: 修复首页加载缓慢问题"
git commit -m "docs: 更新 README 文档"
```

---

## 十、常见问题

### Q: 提示 "Permission denied" 怎么办？

A: 检查 SSH Key 是否配置正确：

```bash
ssh -T git@github.com
```

如果失败，重新配置 SSH Key。

### Q: 提示 "remote: Repository not found" 怎么办？

A: 检查：
1. 仓库名是否正确
2. 仓库是否已创建
3. 是否有访问权限

### Q: 推送时提示 "rejected" 怎么办？

A: 远程仓库有本地没有的提交，先拉取再推送：

```bash
git pull origin main --rebase
git push origin main
```

### Q: 如何修改已提交的文件？

A: 修改后重新添加并提交：

```bash
git add 修改的文件
git commit -m "Update: 修改说明"
git push origin main
```

### Q: 如何删除远程仓库的文件？

A: 使用 git rm 命令：

```bash
git rm 文件名
git commit -m "Remove: 文件名"
git push origin main
```

### Q: 如何撤销已推送的提交？

A: 使用 revert 创建新提交：

```bash
git revert HEAD
git push origin main
```

### Q: 文件太大无法推送怎么办？

A: 使用 Git LFS 或检查是否误提交了大文件：

```bash
# 查看大文件
git rev-list --objects --all | git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' | sort -k3 -n -r | head -10
```

---

## 十一、完整的项目上传示例

以一个前端博客项目为例，完整演示上传过程：

```bash
# 1. 进入项目目录
cd E:\项目开发\个人博客

# 2. 初始化 Git
git init

# 3. 创建 .gitignore
echo "node_modules/
.DS_Store
*.log
.vscode/" > .gitignore

# 4. 添加所有文件
git add .

# 5. 提交
git commit -m "Initial commit: 博客项目初始化"

# 6. 在 GitHub 创建仓库后，关联远程仓库
git remote add origin git@github.com:用户名/my-blog.git

# 7. 推送
git push -u origin main

# 8. 设置 GitHub Pages
# 进入 Settings → Pages → Branch 选择 main → Save

# 9. 访问网站
# https://用户名.github.io/my-blog/
```

---

感谢阅读这份上传指南！如有其他问题，欢迎反馈。
