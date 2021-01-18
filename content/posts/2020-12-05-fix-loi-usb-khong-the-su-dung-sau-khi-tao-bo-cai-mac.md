---

toc: true
categories: ["macOS"]
date: "2020-12-05 06:05:05"
featured: false
featuredImage: /assets/images/2020/12/format-usb-dunghoang.png
featuredImagePreview: /assets/images/2020/12/format-usb-dunghoang.png
tags:
- macos
- tricks
title: Hướng dẫn fix lỗi USB không thể sử dụng sau khi tạo bộ cài macOS
---
Thông thường sau khi sử dụng USB để tạo bộ cài macOS thì sau đó USB không thể hoạt động ổn định được, không thể copy file trên các máy Windows và bị chia thành 2 phân vùng, trong đó có 1 phân vùng 200MB là sử dụng được gây ra sự khó chịu cho người dùng nếu không biết cách xử lý.

Để có thể khắc phục vấn đề này các bạn có thể làm như sau:

* Gắn ổ USB vào máy Mac của bạn
* Mở ứng dụng Disk Utility (có thể search bằng cách sử dụng phím ⌘ + Space, sau đó gõ Disk Utility)
* Chọn USB cần format dữ liệu và ấn nút Erase
* Trong ô Format, chọn exFAT (hoặc FAT32 đều được)
* Trong ô Scheme, chọn Master Boot Record
  
![Format usb trên macOS](/assets/images/2020/12/format-usb-dunghoang.png)

* Nhấn nút Erase, ngồi chờ cho ổ format xong là usb sẽ hoạt động bình thường trở lại.

Bạn hãy thử cách trên xem có xử lý được tình trạng usb không hoạt động sau khi sử dụng làm bộ cài macOS không nhé.