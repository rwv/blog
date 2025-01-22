# rwv's Blog / rwv 的博客

[![Build and Deploy](https://github.com/rwv/blog/actions/workflows/ci.yml/badge.svg)](https://github.com/rwv/blog/actions/workflows/ci.yml)

A bilingual personal blog built with Hugo and PaperMod theme, sharing tech articles and life moments.

一个基于 Hugo 和 PaperMod 主题的双语个人博客，分享技术文章和生活点滴。

## Blog / 博客

- English: [https://blog.rwv.dev/en](https://blog.rwv.dev/en)
- 中文: [https://blog.rwv.dev/](https://blog.rwv.dev/)

## Local Development / 本地开发

To run this blog locally, you need to have [Hugo installed](https://gohugo.io/installation/). Then:

要在本地运行此博客，您需要[安装 Hugo](https://gohugo.io/installation/)。然后：

```bash
# Clone the repository
git clone https://github.com/rwv/blog.git
cd blog

# Update the theme
git submodule update --init --recursive

# Start the Hugo server
hugo server
```

The site will be available at `http://localhost:1313/`.

网站将在 `http://localhost:1313/` 上可访问。
