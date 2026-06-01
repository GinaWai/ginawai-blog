# 部署指南

## 第一步：安装 Hugo（本地开发用）

```bash
brew install hugo
hugo version
```

---

## 第二步：克隆并初始化项目

```bash
cd ginawai-blog
git init
git submodule add https://github.com/orechou/hugo-theme-cactus-plus.git themes/cactus-plus
```

本地预览：
```bash
hugo server
# 访问 http://localhost:1313
```

---

## 第三步：创建 GitHub 仓库

1. 登录 GitHub，创建**两个**仓库：
   - 仓库一（存放源码）：`ginawai-blog`（私有或公开均可）
   - 仓库二（GitHub Pages）：`YOUR_USERNAME.github.io`（必须公开）

2. 推送源码到仓库一：
```bash
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/YOUR_USERNAME/ginawai-blog.git
git push -u origin main
```

---

## 第四步：配置 GitHub Personal Access Token

1. 打开 GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. 点击 **Generate new token**，权限勾选 `repo`（全部）
3. 复制生成的 token

4. 回到 `ginawai-blog` 仓库 → Settings → Secrets and variables → Actions
5. 点击 **New repository secret**：
   - Name: `PERSONAL_TOKEN`
   - Value: 粘贴刚才的 token

---

## 第五步：修改 deploy.yml

打开 `.github/workflows/deploy.yml`，修改这一行：

```yaml
EXTERNAL_REPOSITORY: YOUR_GITHUB_USERNAME/YOUR_GITHUB_USERNAME.github.io
```

替换为你的实际 GitHub 用户名，例如：

```yaml
EXTERNAL_REPOSITORY: ginawai/ginawai.github.io
```

提交并推送后，GitHub Actions 会自动构建并部署。

---

## 第六步：开启 GitHub Pages

在 `YOUR_USERNAME.github.io` 仓库 → Settings → Pages：
- Source: `Deploy from a branch`
- Branch: `master`
- 保存

访问 `https://YOUR_USERNAME.github.io` 验证是否部署成功。

---

## 第七步：配置自定义域名 ginawai.com

### 7.1 注册 Cloudflare 账号

1. 打开 [cloudflare.com](https://cloudflare.com) 注册账号
2. 点击 **Add a Site**，输入 `ginawai.com`
3. 选择免费计划
4. Cloudflare 会给你两个 Nameserver 地址，形如：
   - `xxx.ns.cloudflare.com`
   - `yyy.ns.cloudflare.com`

### 7.2 修改域名 Nameserver

登录你购买域名的注册商（如 GoDaddy、Namecheap 等），将域名的 Nameserver 改为 Cloudflare 提供的地址（等待几分钟到几小时生效）。

### 7.3 在 Cloudflare 添加 DNS 记录

| 类型  | 名称 | 内容                    | 代理状态 |
|-------|------|-------------------------|----------|
| A     | @    | 185.199.108.153         | 已代理   |
| A     | @    | 185.199.109.153         | 已代理   |
| A     | @    | 185.199.110.153         | 已代理   |
| A     | @    | 185.199.111.153         | 已代理   |
| CNAME | www  | YOUR_USERNAME.github.io | 已代理   |

### 7.4 在 GitHub Pages 设置自定义域名

在 `YOUR_USERNAME.github.io` 仓库 → Settings → Pages → Custom domain，填入 `ginawai.com`，保存。

### 7.5 开启 HTTPS

在 Cloudflare → SSL/TLS → 概述：
- 加密模式选 **Flexible**
- 开启 **始终使用 HTTPS**

---

## 完成！

访问 [https://ginawai.com](https://ginawai.com) 即可看到你的博客。

---

## 日常写博客

```bash
# 新建文章
hugo new posts/my-new-post.md

# 编辑文章，将 draft: true 改为 draft: false

# 发布
git add .
git commit -m "新文章：标题"
git push
```

GitHub Actions 自动构建，约 1 分钟后博客更新。
