# GitHub Pages 在线访问说明

这个仓库已经按 **GitHub Pages 静态网站** 的方式整理：根目录有 `index.html`，并且有 `.nojekyll`，所以可以直接由 GitHub Pages 发布。

> 说明：GitHub Pages 只能托管静态 HTML/CSS/JavaScript，不能直接运行完整 WordPress 的 PHP 后台和 MySQL/MariaDB 数据库。如果要在 GitHub 上直接打开网页访问，就只能发布静态页面；完整 WordPress 需要额外服务器或托管平台。

## 404 修复方式

如果打开下面地址是 404：

```text
https://hx-557.github.io/
```

请在 GitHub 仓库页面按下面方式设置一次：

1. 打开仓库的 **Settings**。
2. 左侧进入 **Pages**。
3. 在 **Build and deployment** 中，**Source** 选择 **Deploy from a branch**。
4. **Branch** 选择当前发布分支，例如 `work`；如果你已经把代码合并到默认分支，则选择 `main` 或 `master`。
5. 文件夹选择 `/ (root)`。
6. 点击 **Save**。
7. 回到仓库 **Actions**，等待 GitHub 自动生成的 `pages-build-deployment` 成功。
8. 再访问：

```text
https://hx-557.github.io/
```

通常需要等待几十秒到几分钟才会生效。

## 为什么之前会 404

常见原因是 GitHub Pages 还没有设置发布源，或者发布源选错了分支/目录。这个仓库的网站入口文件在根目录：

```text
index.html
```

所以 Pages 发布源必须指向包含 `index.html` 的分支，并且目录必须是 `/ (root)`。

## 当前仓库需要发布的文件

- `index.html`：网站首页入口。
- `css/`：页面样式。
- `js/`：页面脚本。
- `img/`：图片资源。
- `archives/`、`2022/`：已有文章页面。
- `.nojekyll`：告诉 GitHub Pages 不要用 Jekyll 处理文件，直接按静态文件发布。

## 如果还是 404，请检查

1. 仓库名应是 `<你的 GitHub 用户名>.github.io`。当前访问地址对应的仓库名应为 `Hx-557.github.io`。
2. Pages 的 **Branch** 必须选到真正包含 `index.html` 的分支。
3. Pages 的目录必须是 `/ (root)`，不要选 `/docs`。
4. 仓库需要是 public，或者你的 GitHub 计划支持私有仓库 Pages。
5. GitHub Actions 里的 `pages-build-deployment` 必须成功。
6. 修改设置后请等待几分钟，并强制刷新浏览器缓存。

## 如果你一定要 WordPress

GitHub Pages 无法直接运行完整 WordPress。可选方案：

- 用 WordPress 静态导出插件导出 HTML，再提交到这个仓库，由 GitHub Pages 托管。
- 把 WordPress 部署到支持 PHP + MySQL 的服务器或托管平台，再把域名解析过去。
- 使用 Headless WordPress：WordPress 后台部署在服务器，GitHub Pages 只部署前端静态页面。
