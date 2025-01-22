+++
date = '2025-01-22T09:22:52+08:00'
draft = false
title = 'Migrating Blog System from Hexo to Hugo'
slug = 'migrate-blog-system-from-hexo-to-hugo'
+++

After four years, I'm ready to start blogging again. However, I felt the need to tinker with the system as [Hexo](https://hexo.io/) wasn't quite meeting my needs, so I decided to migrate to [Hugo](https://gohugo.io/). Another important reason was that [yilia](https://github.com/litten/hexo-theme-yilia) hasn't been updated for a very long time and doesn't even support dark mode.

## Migration Motivation

Here are the main advantages of migrating from Hexo to Hugo, along with avoiding some existing technical debt (such as messy git logs and lack of open source):

- **Faster Build Speed**: Hugo is written in Go, making it faster than Node.js-based solutions
- **Simpler Deployment**: Single binary file, no complex dependency management needed
- **Powerful Content Management**: Page Bundles feature makes article and resource management clearer
- **Active Community**: Rich ecosystem of themes and plugins
- **Internationalization Support**: Hugo's built-in multilingual support makes internationalization easy
- **Better Theme Options**: The [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme suits my aesthetic better than [yilia](https://github.com/litten/hexo-theme-yilia) and supports dark mode

## Migration Steps

### Creating a Hugo Site

```bash
# Install Hugo (macOS)
brew install hugo

# Create site
hugo new site my-blog
cd my-blog

# Install PaperMod theme
git init
git submodule add https://github.com/adityatelange/hugo-PaperMod themes/PaperMod
```

Modify the basic configuration file `hugo.toml`

```toml
baseURL = "https://blog.rwv.dev/"
title = "My Blog"
theme = "PaperMod"
languageCode = "en"
```

You can reference my configuration here: [config/\_default](https://github.com/rwv/blog/tree/ace7392bbad25d48d124b779dfe084c4d60ff8f8/config/_default)

### Content Migration

Converting article formats:

- Move articles from `source/_posts` to `content/posts`
- Convert front matter format:

```yaml
# Hexo format
---
title: Example Post
date: 2024-01-22 14:30:00
tags:
  - hugo
  - blog
---
```

```yaml
# Hugo format
---
title: Example Post
date: 2024-01-22T14:30:00+08:00
tags:
  - hugo
  - blog
aliases:
  - /2024/01/22/example-post/
---
```

The original URL path in Hexo was `permalink: :year/:month/:day/:title/`. In Hugo, we need to set aliases to prevent old links from breaking.

### Configuring Comments System

I also replaced the original Disqus commenting system with [giscus](https://giscus.app/). Here's the specific configuration:

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
  data-lang="en"
  crossorigin="anonymous"
  async
></script>
```

### Configuring GitHub Actions

I'm using GitHub Actions to automatically deploy the blog to both Cloudflare Pages and GitHub Pages for better disaster recovery (although such scenarios are unlikely). In the future, I might deploy to more platforms, possibly even IPFS, though I'm skeptical about IPFS's stability.

You can find the specific code in [.github/workflows/ci.yml](https://github.com/rwv/blog/blob/92193c6f296febeaa402d69097126b30d61cff7d/.github/workflows/ci.yml)

Why not use Cloudflare Pages' own build system? Because Cloudflare Pages has concurrent build limitations, and their Hugo version is too old to compile successfully. GitHub Actions' build system is more reliable.

## Open Source

Taking advantage of this migration, I've made the blog open source. The project is available at [rwv/blog](https://github.com/rwv/blog), and you can find the 'Edit' button at the top of each article to go directly to the source code. Here's the specific configuration:

```yaml
editPost:
  URL: "https://github.com/rwv/blog/blob/main/content"
  appendFilePath: true # to append file path to Edit link
```

Code: [config/\_default/params.yml#L21-L23](https://github.com/rwv/blog/blob/ace7392bbad25d48d124b779dfe084c4d60ff8f8/config/_default/params.yml#L21-L23)

## Conclusion

Hugo provides a more efficient blogging experience. While migration requires some effort, in the long run, it will enable me to write more blog posts. So the migration was worth it.
