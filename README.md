# GitHub Pages 在线访问说明

这个仓库已经按 **GitHub Pages 静态网站** 的方式配置，可以直接部署到 GitHub 并通过网页访问。

> 重要说明：真正的 WordPress 需要 PHP 运行时和 MySQL/MariaDB 数据库，GitHub Pages 只能托管静态 HTML/CSS/JavaScript，不能在 GitHub 上直接运行 WordPress 后台、插件、主题 PHP 或数据库。
>
> 所以如果目标是“直接放 GitHub 上，然后打开网址就能访问”，可行方案是部署当前仓库里的静态网页；如果一定要完整 WordPress 后台，则必须使用 VPS、虚拟主机、Render、Railway、Cloudflare Tunnel + 服务器等支持 PHP 和数据库的平台。

## 访问地址

这个仓库名是 `Hx-557.github.io`，属于 GitHub Pages 用户站点仓库。启用 GitHub Pages 后，公网访问地址通常是：

```text
https://hx-557.github.io/
```

如果你绑定了自定义域名，则访问你绑定的域名。

## 已添加的自动部署

仓库已添加 GitHub Actions 工作流：

```text
.github/workflows/deploy-pages.yml
```

它会在推送到 `work`、`main` 或 `master` 分支时，把仓库根目录的静态文件发布到 GitHub Pages。

当前仓库根目录已有可访问的静态入口文件：

```text
index.html
```

因此部署完成后，浏览器打开 GitHub Pages 地址即可访问页面。

## 你需要在 GitHub 页面上开启一次 Pages

1. 打开 GitHub 仓库页面。
2. 进入 **Settings**。
3. 左侧进入 **Pages**。
4. 在 **Build and deployment** 里，把 **Source** 选择为 **GitHub Actions**。
5. 回到仓库 **Actions** 页面，等待 `Deploy static site to GitHub Pages` 工作流执行成功。
6. 成功后访问：

```text
https://hx-557.github.io/
```

## 如果访问不了，按这个顺序检查

1. **Actions 是否成功**：进入仓库的 **Actions** 标签页，确认 `Deploy static site to GitHub Pages` 是绿色成功状态。
2. **Pages Source 是否正确**：仓库 **Settings → Pages → Source** 必须选择 **GitHub Actions**。
3. **仓库名是否正确**：用户站点仓库应是 `<你的 GitHub 用户名>.github.io`。当前仓库名是 `Hx-557.github.io`，访问地址对应 `https://hx-557.github.io/`。
4. **等待 DNS/缓存刷新**：首次启用 GitHub Pages 后，通常需要等几十秒到几分钟。
5. **文件是否存在**：仓库根目录必须有 `index.html`。

## 如果你一定要 WordPress

GitHub Pages 无法直接运行完整 WordPress。可选方案：

- 用 WordPress 后台写文章，然后用静态导出插件导出 HTML，再提交到这个仓库，由 GitHub Pages 托管。
- 把 WordPress 部署到支持 PHP + MySQL 的服务器或托管平台，再把域名解析过去。
- 使用 Headless WordPress：WordPress 后台部署在服务器，GitHub Pages 只部署前端静态页面。
