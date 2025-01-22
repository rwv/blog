+++
date = '2025-01-22T09:22:52+08:00'
draft = false
title = '将博客系统从 Hexo 迁移到 Hugo'
+++

时隔四年，又准备开始写博客了。但总归要再折腾折腾的，另外在使用过程中总感觉 [Hexo](https://hexo.io/) 不太得劲，所以决定迁移到 [Hugo](https://gohugo.io/)。另外还有一个重要的原因是 [yilia](https://github.com/litten/hexo-theme-yilia) 很久很久没有更新了，甚至不支持暗黑模式。

## 迁移动机

从 Hexo 迁移到 Hugo 的主要优势有以下这些，当然迁移了还可以避免一些原有的技术债务（像是 git log 混乱，未开源之类的）：

- **更快的构建速度**：Hugo 以 Go 语言编写，构建速度比 Node.js 更快
- **更简单的部署**：单一二进制文件，无需复杂的依赖管理
- **强大的内容管理**：Page Bundles 功能让文章和资源管理更清晰
- **活跃的社区**：丰富的主题和插件生态系统
- **国际化支持**：Hugo 支持多语言，可以方便地进行国际化
- **主题更好看**：[PaperMod](https://github.com/adityatelange/hugo-PaperMod) 主题比 [yilia](https://github.com/litten/hexo-theme-yilia) 主题更符合我的审美，且支持暗黑模式

## 迁移步骤

### 创建 Hugo 站点

```bash
# 安装 Hugo (macOS)
brew install hugo

# 创建站点
hugo new site my-blog
cd my-blog

# 安装 PaperMod 主题
git init
git submodule add https://github.com/adityatelange/hugo-PaperMod themes/PaperMod
```

修改基础配置文件 `hugo.toml`

```toml
baseURL = "https://blog.rwv.dev/"
title = "我的博客"
theme = "PaperMod"
languageCode = "zh-CN"
```

你可以参考一下我的配置：[config/\_default](https://github.com/rwv/blog/tree/ace7392bbad25d48d124b779dfe084c4d60ff8f8/config/_default)

### 内容迁移

转换文章格式：

- 将 `source/_posts` 中的文章移至 `content/posts`
- 转换 front matter 格式：

```yaml
# Hexo 格式
---
title: 示例文章
date: 2024-01-22 14:30:00
tags:
  - hugo
  - blog
---
```

```yaml
# Hugo 格式
---
title: 示例文章
date: 2024-01-22T14:30:00+08:00
tags:
  - hugo
  - blog
aliases:
  - /2024/01/22/示例文章/
---
```

原本在 Hexo 中用的 url 路径是 `permalink: :year/:month/:day/:title/`, 在 Hugo 中需要设置 aliases 防止原有链接失效。

### 配置评论系统

另外废弃了原有的 disqus 评论系统，改用 [giscus](https://giscus.app/zh-CN) 评论系统。具体配置如下：

```yaml
# config/_default/params.yml
comments: true
```

```html
<!-- layouts/partials/comments.html -->
<script
  src="https://giscus.app/client.js"
  data-repo="your-github-username/your-repo-name"
  data-repo-id="xxxx"
  data-category="Announcements"
  data-category-id="xxxx"
  data-mapping="pathname"
  data-strict="0"
  data-reactions-enabled="1"
  data-emit-metadata="0"
  data-input-position="bottom"
  data-theme="preferred_color_scheme"
  data-lang="zh-CN"
  crossorigin="anonymous"
  async
></script>
```

## 开源

借此迁移的机会，将博客开源了，项目地址在 [rwv/blog](https://github.com/rwv/blog)，你也可以找到在文章前面的 `编辑` 按钮直达文章源代码。具体配置代码如下：

```yaml
editPost:
  URL: "https://github.com/rwv/blog/blob/main/content"
  appendFilePath: true # to append file path to Edit link
```

代码：[config/\_default/params.yml#L21-L23](https://github.com/rwv/blog/blob/ace7392bbad25d48d124b779dfe084c4d60ff8f8/config/_default/params.yml#L21-L23)

## 总结

Hugo 提供了更高效的博客构建体验，虽然迁移需要一定工作量，但长期来看，迁移能让我写更多的博客。所以还是得迁移的。
