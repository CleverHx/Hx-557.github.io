# Hx-557 的个人博客

这是一个干净的静态个人博客仓库，适合直接部署到 GitHub Pages，然后通过网页访问。

## 在线访问

仓库名是 `Hx-557.github.io`，启用 GitHub Pages 后，访问地址是：

```text
https://hx-557.github.io/
```

## GitHub Pages 设置

在 GitHub 仓库页面设置一次即可：

1. 进入 **Settings → Pages**。
2. **Source** 选择 **Deploy from a branch**。
3. **Branch** 选择包含这些文件的分支，例如 `work`、`main` 或 `master`。
4. 目录选择 `/ (root)`。
5. 点击 **Save**，等待 `pages-build-deployment` 完成。
6. 打开 `https://hx-557.github.io/`。

## 当前结构

```text
.
├── index.html              # 博客首页
├── 404.html                # GitHub Pages 404 页面
├── posts/
│   └── hello-world.html    # 第一篇文章
├── assets/
│   └── styles.css          # 全站样式
├── .nojekyll               # 关闭 Jekyll 处理，直接发布静态文件
└── README.md
```

## 写新文章

1. 在 `posts/` 目录新增一个 HTML 文件，例如 `posts/my-note.html`。
2. 复制 `posts/hello-world.html` 的结构并修改标题、日期和正文。
3. 在 `index.html` 的“最新文章”区域新增一张文章卡片。
4. 提交并推送到 GitHub，GitHub Pages 会发布最新内容。

## 关于 WordPress

GitHub Pages 只能托管静态 HTML/CSS/JavaScript，不能直接运行 WordPress 的 PHP 后台和数据库。

如果以后一定要用 WordPress，可以：

- 用 WordPress 静态导出插件导出 HTML 后提交到这个仓库；
- 或者把 WordPress 部署到支持 PHP + MySQL 的服务器，再把域名解析到服务器。
