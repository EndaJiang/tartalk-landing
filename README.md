# Tartalk Global Landing（Google OAuth 验证用静态站）

用途：Google Auth Platform 验证要求「主页可达 + 域名归属 + 隐私政策充分」。
tartalk.cn 与 api.tartalk.cn 都在腾讯云上海，Google 爬虫从海外抓取超时
（2026-10-30 两次验证均因此挂掉"homepage unresponsive / privacy insufficient
content"）。本目录是挂在海外可达位置的最小静态站，主域与 api 域均不动。

## 文件

- `index.html` — 英文 landing（Tartalk 品牌 + Privacy/Terms 链接 + 联系邮箱）
- `privacy.html` — 英文隐私政策静态副本（抓自 api 生产页 2026-10-30，语言切换已改指 api 中文页）
- `terms.html` — 英文条款静态副本（同上）
- `CNAME` — GitHub Pages 自定义域声明：`www.tartalk.cn`

## 联系邮箱

`index.html` 页脚为 `service@tartalk.cn`——与 privacy.html 正文中的联系邮箱
一致（2026-10-30 从隐私政策提取）；若客服邮箱变更需两处同步。建议 Branding
的 support email 也用它。

## 部署（GitHub Pages 路线，零 DNS 迁移风险）

1. GitHub 建公开仓库（如 `tartalk-landing`），把本目录 4 个文件传上去
2. 仓库 Settings → Pages → Source 选 `main` / `(root)` → Save
3. Pages 设置里的 Custom domain 填 `www.tartalk.cn`（仓库里有 CNAME 文件则自动带出）
4. DNSPod 加解析：主机记录 `www`、类型 `CNAME`、记录值 `<github用户名>.github.io`
5. 等 Pages 证书签发（几分钟到半小时），勾选 **Enforce HTTPS**
6. 验收：浏览器开 `https://www.tartalk.cn`、`/privacy.html`、`/terms.html` 全通

## 部署完成后回 Auth Platform

Branding 三处改 URL：
- App home page → `https://www.tartalk.cn`
- Privacy policy → `https://www.tartalk.cn/privacy.html`
- Terms of service → `https://www.tartalk.cn/terms.html`

域名归属（Search Console Domain 属性 tartalk.cn）已于 2026-10-30 验证通过，
覆盖 www 子域，**重提无需再等 24 小时**。

## 备注

- GitHub Pages 在中国大陆时常不可达——不影响本用途：这是 global 版面向海外
  用户的官网，cn 版继续用腾讯云上的 `tartalk.cn`（本次完全未动）。
- 若不想用 GitHub，任一海外可达静态托管（Cloudflare Pages / Vercel /
  Netlify）均可，CNAME 指向对应平台即可，文件不用改。
