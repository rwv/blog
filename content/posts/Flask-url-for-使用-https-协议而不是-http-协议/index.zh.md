---
title: Flask url_for 使用 https 协议而不是 http 协议
date: 2019-10-24T17:02:32+08:00
tags:
  - 技术
  - Flask
  - Python
aliases:
  - /2019/10/24/Flask-url-for-使用-https-协议而不是-http-协议/
---

目前 `dos.zczc.cz` 的使用的是 Flask 后端，并且使用 Cloudflare 作为 CDN。但是有一个问题是 Flask 在使用 `url_for` 函数时并不会自动识别 https 协议。导致了 Mixed Content 的存在。

<!--more-->

## 初步尝试

在 nginx 中添加了 `proxy_set_header X-Forwarded-Proto $scheme;`，但是 Flask 并不遵守 `X-Forwarded-Proto` 的设定，而是会使用 `app.config['PREFERRED_URL_SCHEME']` 的设定

## 解决方案

```python
from werkzeug.middleware.proxy_fix import ProxyFix
from flask import Flask

app = Flask(__name__)
app.wsgi_app = ProxyFix(app.wsgi_app)
```

## 参考资料

- [X-Forwarded-For Proxy Fix - Werkzeug Documenation](https://werkzeug.palletsprojects.com/en/0.15.x/middleware/proxy_fix/)
- [Make Flask's url_for use the 'https' scheme in an AWS load balancer without messing with SSLify - stackoverflow](https://stackoverflow.com/questions/34802316/make-flasks-url-for-use-the-https-scheme-in-an-aws-load-balancer-without-mess)
