# WordPress deployment for this repository

这个仓库现在包含一套可部署的 WordPress 生产环境配置：

- **WordPress + Apache/PHP**：运行站点应用。
- **MariaDB**：保存 WordPress 数据。
- **Caddy**：自动申请 HTTPS 证书，并把公网流量反代到 WordPress。
- **Cloudflare Tunnel（可选）**：没有公网 IP 或不想开放 80/443 端口时使用。

> 注意：GitHub Pages 只能托管静态 HTML/CSS/JS，不能直接运行 WordPress 所需的 PHP 和数据库。因此，“部署到这个仓库”的方式是把 WordPress 部署配置保存在仓库里，然后在一台 VPS/云服务器/NAS 上克隆仓库并运行 Docker Compose，公网通过域名访问。

## 1. 准备服务器

服务器需要：

- Docker Engine 和 Docker Compose Plugin。
- 一个已经解析到服务器公网 IP 的域名，例如 `blog.example.com`。
- 防火墙/安全组放行 TCP `80` 和 `443`。

如果没有公网 IP，可以跳到下面的「Cloudflare Tunnel 方式」。

## 2. 配置环境变量

```bash
cp .env.example .env
nano .env
```

至少修改这些值：

```dotenv
SITE_DOMAIN=你的域名
ACME_EMAIL=你的邮箱
WORDPRESS_DB_PASSWORD=一个强密码
MARIADB_ROOT_PASSWORD=另一个强密码
```

不要把 `.env` 提交到 Git；仓库已经通过 `.gitignore` 忽略它。

## 3. 启动 WordPress

```bash
docker compose up -d
```

查看状态：

```bash
docker compose ps
```

查看日志：

```bash
docker compose logs -f caddy wordpress db
```

当 Caddy 成功申请证书后，打开：

```text
https://你的域名
```

按 WordPress 页面提示完成初始化。

## 4. Cloudflare Tunnel 方式（可选）

适用于没有公网 IP、家庭宽带、NAT 后面的机器，或不想在服务器上开放 80/443 端口的情况。

1. 在 Cloudflare Zero Trust 创建 Tunnel。
2. 把 Public Hostname 指向服务：`http://wordpress:80`。
3. 把 Tunnel Token 写入 `.env`：

```dotenv
CLOUDFLARE_TUNNEL_TOKEN=你的-token
```

4. 启动带 tunnel 的服务：

```bash
docker compose --profile cloudflare-tunnel up -d db wordpress cloudflared
```

这种方式下可以不启动 `caddy`，公网入口由 Cloudflare 提供。

## 5. 常用维护命令

备份数据库：

```bash
docker compose exec db mariadb-dump -u root -p wordpress > wordpress-backup.sql
```

备份站点文件：

```bash
docker run --rm -v hx-557githubio_wordpress_data:/data -v "$PWD":/backup alpine tar czf /backup/wordpress-files.tar.gz -C /data .
```

升级镜像：

```bash
docker compose pull
docker compose up -d
```

停止服务：

```bash
docker compose down
```

彻底删除数据卷（危险，会清空站点和数据库）：

```bash
docker compose down -v
```

## 6. 文件说明

- `docker-compose.yml`：WordPress、MariaDB、Caddy 和可选 Cloudflare Tunnel 服务定义。
- `Caddyfile`：HTTPS 和反向代理配置。
- `.env.example`：环境变量模板。
- `uploads.ini`：WordPress 上传大小和 PHP 运行参数。
