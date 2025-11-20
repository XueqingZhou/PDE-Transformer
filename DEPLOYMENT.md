# GitHub Pages 部署详细配置指南

本指南将详细说明如何配置和部署 PDE-Transformer 项目到 GitHub Pages。

## 📋 目录

1. [准备工作](#准备工作)
2. [方法一：通过 GitHub 网页界面配置（推荐）](#方法一通过-github-网页界面配置推荐)
3. [方法二：通过 Git 命令行配置](#方法二通过-git-命令行配置)
4. [验证部署](#验证部署)
5. [常见问题解决](#常见问题解决)
6. [高级配置](#高级配置)

---

## 准备工作

### 1. 确保文件结构正确

项目应该有以下结构：
```
PDE-Transformer/
├── index.html          # 主页面文件
├── README.md           # 项目说明
├── assets/             # 静态资源
│   ├── css/
│   ├── js/
│   └── images/
└── .nojekyll           # 可选：禁用 Jekyll（如果使用纯 HTML）
```

### 2. 确保代码已推送到 GitHub

```bash
cd /Users/zxq/Desktop/project/PDE-Transformer
git status              # 检查是否有未提交的更改
git push origin main    # 确保代码已推送
```

---

## 方法一：通过 GitHub 网页界面配置（推荐）

### 步骤 1：打开仓库设置

1. 访问 GitHub 仓库：https://github.com/XueqingZhou/PDE-Transformer
2. 点击仓库顶部的 **Settings**（设置）标签

### 步骤 2：进入 Pages 设置

1. 在左侧菜单栏中，向下滚动找到 **Pages** 选项
2. 点击 **Pages** 进入 Pages 配置页面

### 步骤 3：配置部署源

在 **Source**（源）部分：

1. **Branch**（分支）：
   - 从下拉菜单选择 **main** 分支

2. **Folder**（文件夹）：
   - 选择 **/ (root)** （根目录）
   - 这意味着 GitHub Pages 将从仓库根目录的 `index.html` 开始

3. 点击 **Save**（保存）按钮

### 步骤 4：等待部署

- GitHub 会在几秒到几分钟内开始构建和部署
- 你会看到一条绿色提示：**"Your site is live at https://xueqingzhou.github.io/PDE-Transformer/"**
- 首次部署通常需要 1-2 分钟

---

## 方法二：通过 Git 命令行配置

### 创建 .nojekyll 文件（推荐）

GitHub Pages 默认使用 Jekyll 处理文件。对于纯 HTML 项目，建议添加 `.nojekyll` 文件来禁用 Jekyll：

```bash
cd /Users/zxq/Desktop/project/PDE-Transformer
touch .nojekyll
git add .nojekyll
git commit -m "Add .nojekyll to disable Jekyll processing"
git push origin main
```

### 使用 gh-pages 分支（可选）

如果不想在主分支上部署，可以创建一个专门的 `gh-pages` 分支：

```bash
# 创建 gh-pages 分支
git checkout -b gh-pages

# 或者从现有文件创建
git subtree push --prefix . origin gh-pages

# 然后在 GitHub Settings > Pages 中选择 gh-pages 分支
```

---

## 验证部署

### 1. 检查部署状态

在 GitHub 仓库中：
- 点击 **Actions** 标签
- 查看是否有 "pages build and deployment" 工作流
- 绿色 ✓ 表示部署成功，红色 ✗ 表示失败

### 2. 访问网站

部署成功后，你的网站地址将是：
- **URL**: `https://xueqingzhou.github.io/PDE-Transformer/`

注意：
- 首次部署可能需要几分钟时间
- URL 格式：`https://[用户名].github.io/[仓库名]/`

### 3. 检查网站内容

访问网站后，检查：
- ✅ 页面是否正常加载
- ✅ CSS 样式是否正确
- ✅ 图片和资源是否正常显示
- ✅ 链接是否正常工作

---

## 常见问题解决

### 问题 1：404 错误

**原因**：找不到 `index.html` 文件

**解决**：
- 确保 `index.html` 在仓库根目录
- 检查文件名大小写是否正确（GitHub 区分大小写）

### 问题 2：CSS/JS 文件无法加载

**原因**：Jekyll 可能忽略了以 `_` 开头的文件

**解决**：
- 创建 `.nojekyll` 文件（见方法二）
- 确保资源路径是相对路径（如 `assets/css/index.css`）

### 问题 3：部署后内容没有更新

**原因**：浏览器缓存或 GitHub 缓存

**解决**：
- 强制刷新浏览器（Ctrl+F5 或 Cmd+Shift+R）
- 等待几分钟让 GitHub 缓存更新
- 检查 Actions 标签确认最新部署成功

### 问题 4：CNAME 文件冲突

**原因**：如果使用自定义域名，需要 CNAME 文件

**解决**：
- 如果使用 `username.github.io`，不需要 CNAME
- 如果使用自定义域名，创建 CNAME 文件：
  ```
  echo "yourdomain.com" > CNAME
  git add CNAME
  git commit -m "Add CNAME for custom domain"
  git push origin main
  ```

---

## 高级配置

### 1. 自定义域名（可选）

如果你想使用自定义域名（如 `pde-transformer.com`）：

1. 在仓库根目录创建 `CNAME` 文件：
   ```bash
   echo "pde-transformer.com" > CNAME
   git add CNAME
   git commit -m "Add custom domain"
   git push origin main
   ```

2. 在 GitHub Pages 设置中，你会看到 "Custom domain" 选项

3. 在你的域名 DNS 设置中添加：
   - **Type**: CNAME
   - **Name**: @ 或 www
   - **Value**: `xueqingzhou.github.io`

### 2. 强制 HTTPS

1. 在 GitHub Pages 设置中
2. 勾选 **"Enforce HTTPS"**（强制 HTTPS）
3. 这需要几分钟来配置 SSL 证书

### 3. 自动部署脚本

创建部署脚本 `deploy.sh`：

```bash
#!/bin/bash
# 部署到 GitHub Pages

echo "Building site..."
# 可以在这里添加构建步骤

echo "Committing changes..."
git add .
git commit -m "Update site $(date +%Y-%m-%d)"

echo "Pushing to GitHub..."
git push origin main

echo "Deployment complete!"
echo "Site: https://xueqingzhou.github.io/PDE-Transformer/"
```

使用：
```bash
chmod +x deploy.sh
./deploy.sh
```

---

## 部署检查清单

部署前请确认：

- [ ] `index.html` 文件在仓库根目录
- [ ] 所有资源文件（CSS、JS、图片）路径正确
- [ ] `.nojekyll` 文件已创建（如果使用纯 HTML）
- [ ] 代码已推送到 GitHub `main` 分支
- [ ] GitHub Pages 已在设置中启用
- [ ] 部署源设置为 `main` 分支和 `/ (root)` 文件夹
- [ ] 检查 Actions 标签确认部署成功
- [ ] 访问网站验证所有功能正常

---

## 后续更新

每次更新网站内容：

1. 修改本地文件
2. 提交更改：
   ```bash
   git add .
   git commit -m "Update site content"
   git push origin main
   ```
3. GitHub 会自动重新部署（通常需要 1-2 分钟）
4. 在 Actions 标签中查看部署状态

---

## 参考链接

- [GitHub Pages 官方文档](https://docs.github.com/en/pages)
- [自定义域名配置](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)
- [GitHub Actions 部署](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)

---

**部署完成后，你的网站将在以下地址可用：**
🌐 **https://xueqingzhou.github.io/PDE-Transformer/**

