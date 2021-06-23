# Fix lỗi High CPU Usage gây ra bởi tiến trình accountsd trên macOS Catalina


## Lỗi "accountsd" là gì?

Sau khi Apple ra mắt bản cập nhập macOS Catalina 10.15.7, một số người dùng phản ánh Mac của họ bỗng nhiên trở nên chậm chạp hơn so với bình thường, mà nguyên nhân chính được phát hiện là do một process có tên "accountsd" gây ra lỗi chiếm dụng CPU.

Một người dùng trong Cộng đồng hỗ trợ của Apple đã chia sẻ ảnh chụp màn hình "accountsd" với mức sử dụng CPU trên 400%, khiến MacBook Pro 2018 của họ trở nên vô cùng chậm chạp.

<figure class="kg-card kg-image-card kg-card-hascaption"><img src="/assets/images/2020/10/ezgif-7-380d370680bd.jpg" class="kg-image" alt="Lỗi accountsd chiếm dụng CPU gây chậm máy"  sizes="(min-width: 720px) 720px"><figcaption class="text-center">Lỗi accountsd chiếm dụng CPU gây chậm máy</figcaption></figure>

Hiện tại, Apple chưa lên tiếng về sự cố này, và vẫn chưa có cách sửa chữa chính thức, người dùng vẫn đang phải tự tìm cách xoay xở, dưới đây là một số cách các bạn có thể "thử" để xem có cải thiện được tình hình trên Mac của bạn không nhé.

## Một số cách fix lỗi "accountsd"

### Cách 1: Thử đăng xuất Apple Id

Người dùng có thể thử đăng xuất khỏi tài khoản Apple ID của họ trong System Preferences \> Apple ID \> Overview \> Sign Out, sau đó khởi động lại máy Mac và đăng nhập lại vào tài khoản.

### Cách 2: Reset SMV và NVRAM

Nếu cách 1 không hoạt động, các bạn có thể thử reset lại SMC và NVRAM theo hướng dẫn của Apple.

- [Reset SMC](https://support.apple.com/en-us/HT201295)
- [Reset NVRAM](https://support.apple.com/en-us/HT204063)

**Lưu ý:** _2 cách tiếp theo dưới đây có can thiệp vào file hệ thống, vì vậy bạn hãy cân nhắc khi thực hiện, không chịu trách nhiệm đối với những hư hỏng do thực hiện theo những cách dưới đây._

### Cách 3: Đổi tên file Accounts4.sqlite (Không dành cho người mới)

Sao lưu lại file Accounts4.sqlite bằng cách

Đổi tên /Users/xxx/Library/Accounts/Accounts4.sqlite thành /Users/XXX/Library/Accounts/Accounts4.sqlite.bak

khi bạn khởi động lại Mac, 1 file Accounts4.sqlite sẽ được tạo mới, tiến hành đổi tên lại

Đổi tên /Users/xxx/Library/Accounts/Accounts4.sqlite.bak lại thành /Users/xxx/Library/Accounts/Accounts4.sqlite

### Cách 4: Dùng lệnh terminal (Không dành cho người mới)

Bạn mở Terminal và dán vào lệnh sau
```bash
sudo -v ; killall -9 accountsd http://com.apple.iCloudHelper ; defaults delete MobileMeAccounts ; mkdir ~/Library/Accounts/Backup ; mv ~/Library/Accounts/*.sqlite* ~/Library/Accounts/Backup/ ; killall -9 accountsd http://com.apple.iCloudHelper ; sudo reboot
```
Trên đây là một số cách mà người dùng macOS đã chia sẻ cho nhau để khắc phục lỗi "accountsd" trong khi đợi bản fix từ Apple.

Máy bạn có bị lỗi "accountsd" chiếm dụng CPU không? Bạn xử lý bằng cách nào? Hãy chia sẻ cùng mọi người thông qua phần bình luận nhé. Nice day, guys!


