# GinaWai Blog

基于 Hugo + GitHub Pages + Cloudflare 搭建的个人博客。

- 域名：[ginawai.com](https://ginawai.com)
- 主题：[cactus-plus](https://github.com/orechou/hugo-theme-cactus-plus)

## 本地开发

```bash
# 首次克隆需拉取主题子模块
git submodule update --init --recursive

# 本地预览
hugo server

# 浏览器访问 http://localhost:1313
```

## 写文章

```bash
hugo new posts/my-new-post.md
```

编辑文件，将 `draft: true` 改为 `draft: false` 后推送即可发布。

## 发布

```bash
git add .
git commit -m "新文章：文章标题"
git push
```

GitHub Actions 会自动构建并部署到 GitHub Pages。

## 目录结构

```
ginawai-blog/
├── .github/
│   └── workflows/
│       └── deploy.yml      # 自动部署配置
├── content/
│   ├── posts/              # 博客文章
│   └── about.md            # 关于页面
├── themes/
│   └── cactus-plus/        # Hugo 主题（子模块）
├── static/                 # 静态资源（图片等）
├── .gitmodules
├── .gitignore
└── hugo.toml               # Hugo 配置文件
```

## 初次部署步骤

详见 [DEPLOY.md](./DEPLOY.md)
