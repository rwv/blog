---
title: Add Giscus Multilingual Support in Hugo PaperMod
date: 2025-01-22T13:18:04+08:00
tags:
  - hugo
  - giscus
  - multilingual
  - comments
  - blog
  - PaperMod
---

Giscus actually supports multiple languages, as you can see in [giscus/giscus/locales](https://github.com/giscus/giscus/tree/main/locales). However, it doesn't automatically detect the language, so manual configuration is needed. Hugo PaperMod doesn't have a simple way to set different comment components for different languages, so we need to configure it manually.

## Configure Giscus

First, create a comment component at [giscus.app](https://giscus.app/), which looks like this:

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

Notice the `data-lang` attribute - this is what we use to set the language.

## Configure Hugo PaperMod Template HTML

First, set PaperMod's `comments` to `true` so that the comment component will be displayed in every article.

[PaperMod Documentation - Comments](https://github.com/adityatelange/hugo-PaperMod/wiki/Features#comments)

```yaml
params:
  comments: true
```

Then create `layouts/partials/comments.html` with the following content:

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

This way, the comment component will be displayed in every article and will automatically set its language based on the article's language.

Note: Prettier will automatically format the code, which is why it might look a bit messy.

## References

- [giscus/giscus/locales](https://github.com/giscus/giscus/tree/main/locales)
- [PaperMod Documentation - Comments](https://github.com/adityatelange/hugo-PaperMod/wiki/Features#comments)
