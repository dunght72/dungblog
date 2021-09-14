---
title: "Reverse Proxy Cho Website Trong Cyber Panel"
date: 2021-09-14T08:04:09+07:00
featuredImage: /assets/images/2021/09/cyberpanel.jpeg
featuredImagePreview: /assets/images/2021/09/cyberpanel.jpeg
categories: ["Developer"]
description: "Ví dụ dưới đây thực hiện Reverse Proxy cho .Net Core Api chạy dưới Cyber Panel."
tags:
  - Developer
  - Cyberpanel
  - Reverse Proxy
---
Ví dụ dưới đây thực hiện Reverse Proxy cho .Net Core Api chạy dưới Cyber Panel

![Reverse Proxy Trong Cyberpanel](/assets/images/2021/09/cyberpanel.jpeg)

**Bước 1: Tạo Website mới trong Cyber Panel với domain tuỳ chọn**

**Bước 2: Issue SSL cho Website**

**Bước 3: Thực hiện SSH vào Server và edit file httpd_config**

Open command line and edit: /usr/local/lsws/conf/httpd_config.conf

```
extprocessor dockerbackend {
  type                    proxy
  address                 127.0.0.1:5000
  maxConns                100
  pcKeepAliveTimeout      60
  initTimeout             60
  retryTimeout            0
  respBuffer              0
}
```

**Bước 4: Tuỳ chỉnh Rewrite URL theo mẫu dưới đây** 

Use Rewrite Rules to Proxy traffic to your Container

```
REWRITERULE ^(.*)$ HTTP://dockerbackend/$1 [P]
```

**Bước 5: Restart Open Lite Speed và check lại.**
