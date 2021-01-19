---
author: "Dũng Hoàng"
toc: true
categories: ["Trick"]
date: "2020-06-18T19:03:36Z"
featuredImage: /assets/images/map-network-drive.jpg
featuredImagePreview: /assets/images/map-network-drive.jpg
title: Hướng dẫn chat Telegram bằng Terminal
---
Telegram đang ngày càng trở nên phô biến do tính bảo mật tốt, tốc độ nhanh và thân thiện. Sử dụng telegram trên app thì bình thường rồi, bạn còn có thể nhắn tin Telegram trên chính Terminal bằng cách sử dụng Telegram-cli. Nếu bạn muốn thể hiện thì hãy dùng thử nhé ^^
![Telegram Cli](/assets/images/telegram-cli-2.png)

### Cài đặt Telegram CLI trên Macos

#### Cài đặt trên Ubuntu

``` bash
 sudo apt-get install libreadline-dev libconfig-dev libssl-dev lua5.2 liblua5.2-dev libevent-dev libjansson-dev libpython-dev make 
```

#### Cài đặt trên Macos dùng Homebrew

```bash
brew install telegram-cli
```

### Một số lệnh cơ bản:
- _dialog_list_: Xem lại list chat
- _msg @user "nội dung"_: Gửi tin nhắn đến user
- _contact_list_: Xem danh sách contact của Telegram
- _help_: Danh sách command

Ngoài ra có thể tham khảo full cheatsheet tại [đây](https://github.com/vysheng/tg)

Chúc các bạn trải nghiệm vui vẻ.

---
