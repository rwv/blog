---
title: 在 Hugo PaperMod 中添加 giscus 多语言支持
date: 2025-01-22T13:18:04+08:00
tags:
  - hugo
  - giscus
  - 多语言
  - 评论
  - 博客
  - PaperMod
---

其实 giscus 是支持多语言的，具体可以看 [giscus/giscus/locales](https://github.com/giscus/giscus/tree/main/locales)。但是他不支持自动识别语言，所以需要手动配置。而 Hugo PaperMod 没法简单地对不同语言设置不同的评论组件，所以需要手动配置。

## 配置 giscus

首先在 [giscus.app](https://giscus.app/) 创建一个评论组件，就像这样：

```html
<script
  src="https://giscus.app/client.js"
  data-repo="[ENTER REPO HERE]"
  data-repo-id="[ENTER REPO ID HERE]"
  data-category="[ENTER CATEGORY NAME HERE]"
  data-category-id="[ENTER CATEGORY ID HERE]"
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

我们注意到 `data-lang` 这个属性，这个属性就是用来设置语言的。

## 配置 Hugo PaperMod 模版 HTML

首先配置 PaperMod 的 `comments` 为 `true`，这样在每篇文章中都会显示评论组件。

[PaperMod 文档 - 评论](https://github.com/adityatelange/hugo-PaperMod/wiki/Features#comments)

```yaml
params:
  comments: true
```

然后创建 `layouts/partials/comments.html`，内容如下：

```html
{{ $giscusLang := "en" }} {{ if eq site.Language.Lang "zh" }} {{ $giscusLang =
"zh-CN" }} {{ else if eq site.Language.Lang "zh-tw" }} {{ $giscusLang = "zh-TW"
}} {{ else if eq site.Language.Lang "zh-hk" }} {{ $giscusLang = "zh-HK" }} {{
else if eq site.Language.Lang "ar" }} {{ $giscusLang = "ar" }} {{ else if eq
site.Language.Lang "be" }} {{ $giscusLang = "be" }} {{ else if eq
site.Language.Lang "bg" }} {{ $giscusLang = "bg" }} {{ else if eq
site.Language.Lang "ca" }} {{ $giscusLang = "ca" }} {{ else if eq
site.Language.Lang "cs" }} {{ $giscusLang = "cs" }} {{ else if eq
site.Language.Lang "da" }} {{ $giscusLang = "da" }} {{ else if eq
site.Language.Lang "de" }} {{ $giscusLang = "de" }} {{ else if eq
site.Language.Lang "el" }} {{ $giscusLang = "gr" }} {{ else if eq
site.Language.Lang "eo" }} {{ $giscusLang = "eo" }} {{ else if eq
site.Language.Lang "es" }} {{ $giscusLang = "es" }} {{ else if eq
site.Language.Lang "eu" }} {{ $giscusLang = "eu" }} {{ else if eq
site.Language.Lang "fa" }} {{ $giscusLang = "fa" }} {{ else if eq
site.Language.Lang "fr" }} {{ $giscusLang = "fr" }} {{ else if eq
site.Language.Lang "he" }} {{ $giscusLang = "he" }} {{ else if eq
site.Language.Lang "hu" }} {{ $giscusLang = "hu" }} {{ else if eq
site.Language.Lang "id" }} {{ $giscusLang = "id" }} {{ else if eq
site.Language.Lang "it" }} {{ $giscusLang = "it" }} {{ else if eq
site.Language.Lang "ja" }} {{ $giscusLang = "ja" }} {{ else if eq
site.Language.Lang "km" }} {{ $giscusLang = "kh" }} {{ else if eq
site.Language.Lang "ko" }} {{ $giscusLang = "ko" }} {{ else if eq
site.Language.Lang "nl" }} {{ $giscusLang = "nl" }} {{ else if eq
site.Language.Lang "pl" }} {{ $giscusLang = "pl" }} {{ else if eq
site.Language.Lang "pt" }} {{ $giscusLang = "pt" }} {{ else if eq
site.Language.Lang "ro" }} {{ $giscusLang = "ro" }} {{ else if eq
site.Language.Lang "ru" }} {{ $giscusLang = "ru" }} {{ else if eq
site.Language.Lang "th" }} {{ $giscusLang = "th" }} {{ else if eq
site.Language.Lang "tr" }} {{ $giscusLang = "tr" }} {{ else if eq
site.Language.Lang "uk" }} {{ $giscusLang = "uk" }} {{ else if eq
site.Language.Lang "uz" }} {{ $giscusLang = "uz" }} {{ else if eq
site.Language.Lang "vi" }} {{ $giscusLang = "vi" }} {{ end }}

<script
  src="https://giscus.app/client.js"
  data-repo="[ENTER REPO HERE]"
  data-repo-id="[ENTER REPO ID HERE]"
  data-category="[ENTER CATEGORY NAME HERE]"
  data-category-id="[ENTER CATEGORY ID HERE]"
  data-mapping="pathname"
  data-strict="0"
  data-reactions-enabled="1"
  data-emit-metadata="0"
  data-input-position="bottom"
  data-theme="preferred_color_scheme"
  data-lang="{{ $giscusLang }}"
  crossorigin="anonymous"
  async
></script>
```

这样子在每篇文章中都会显示评论组件，并且会根据文章的语言自动设置评论组件的语言。

注：Prettier 会自动格式化代码，所以看起来有点乱。

## 参考

- [giscus/giscus/locales](https://github.com/giscus/giscus/tree/main/locales)
- [PaperMod 文档 - 评论](https://github.com/adityatelange/hugo-PaperMod/wiki/Features#comments)
