# 10点半 网站上线说明（Cloudflare + Vercel）

## 1. 前置准备

- 一个 GitHub 仓库（已包含本项目代码）
- 一个 Vercel 账号
- 一个 Cloudflare 账号
- 一个已购买域名（例如 `example.com`）

## 2. 项目侧已完成配置

- 已添加 `vercel.json`
  - 根路径 `/` 指向 `index.html`
  - `/demo` 指向 `demo.html`
  - 已添加基础安全响应头

## 3. 本地首次部署（命令行）

在项目根目录执行：

```bash
npx vercel
```

第一次会提示登录和绑定项目，按提示选择：

- Scope：你的个人账号或团队
- Link to existing project：No（首次）
- Project name：`half-ten`（可改）
- Directory：当前目录 `./`

预览环境发布成功后，再执行生产发布：

```bash
npx vercel --prod
```

## 4. 绑定自定义域名（Vercel）

在 Vercel 项目设置中添加域名：

- `example.com`
- `www.example.com`

Vercel 会给出需要配置的 DNS 记录。

## 5. Cloudflare DNS 配置

按 Vercel 给出的记录填写，常见为：

- `@` -> A 记录（Vercel IP）
- `www` -> CNAME 指向 Vercel 域名

建议：

- 先仅开 DNS（灰云）验证可用，再按需切换代理（橙云）
- SSL/TLS 选择 `Full`（若源站证书正常）
- 开启 `Always Use HTTPS`

## 6. 上线后验证清单

- 访问 `https://你的域名/` 正常打开
- 访问 `https://你的域名/demo` 正常打开
- 手机浏览器可正常操作发牌/亮牌/计分
- 强刷后本地积分持久化正常
- 控制台无明显报错

## 7. 回滚方式

- Vercel 控制台选择上一版本，执行 Promote/Rollback
- 或在本地回退代码后重新执行 `npx vercel --prod`
