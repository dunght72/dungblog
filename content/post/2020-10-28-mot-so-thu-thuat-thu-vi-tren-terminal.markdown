---

toc: true
categories: ["macOS"]
date: "2020-10-28T06:05:05Z"
featured: false
featuredImage: /assets/images/2020/10/image-11.png
featuredImagePreview: /assets/images/2020/10/image-11.png
tags:
- thu-thuat
title: Một số lệnh tuỳ biến, vui vẻ trên Terminal của macOS
description: "Với Terminal, bạn có thể thực hiện một số lệnh can thiệp sâu vào hệ thống để tuỳ biến theo ý thích. Dưới đây là một số thủ thuật trên Terminal mà bạn có thể áp dụng."
---

Với Terminal, bạn có thể thực hiện một số lệnh can thiệp sâu vào hệ thống để tuỳ biến theo ý thích. Dưới đây là một số thủ thuật trên Terminal mà bạn có thể áp dụng.

Terminal có thể mở từ màn hình Launchpad hoặc truy cập nhanh bằng (⌘ + Space, sau đó gõ Terminal)

<figure class="kg-card kg-image-card"><img src="/assets/images/2020/10/image-11.png" class="kg-image"  sizes="(min-width: 720px) 720px"></figure>

### Hiện tập tin và thư mục ẩn

Để hiện tập tin, thư mục ẩn trên Mac, bạn có thể thực hiện copy, paste dòng lệnh sau vào Terminal để thực thi.

    defaults write com.apple.finder AppleShowAllFiles -bool TRUE
    
    killall Finder
    

Thay "TRUE" thành "FALSE" nếu bạn muốn ẩn tập tin, thư mục ẩn.

### Sao chép tập tin giữa các thư mục

Sao chép tập tin có thể thực hiện từ ngay Finder bằng menu Copy hoặc bằng cách kéo thả, tuy nhiên nếu muốn trải nghiệm một cách mới, bạn có thể sử dụng lệnh Ditty với cú pháp:

```bash
Ditto [original folder] [new folder]
```

Trong đó: _Original Folder_ là thư mục nguồn, _New Folder_ là thư mục gốc muốn sao chép đến.

### Download tập tin từ Internet

Dùng lệnh Curl bạn có thể download tập tin trực tiếp từ ngay trong Terminal. Cú pháp của lệnh này là:
```bash
    curl -O [the URL of the file]
```
URL of the file là direct link cần download

### Tắt đổ bóng khi chụp màn hình

Khi bạn chụp màn hình bằng công cụ có sẵn của macOS (⌘ + ⇧ + 4), thường sẽ có hiệu ứng đổ bóng được thêm vào, bạn có thể tắt hiệu ứng đổ bóng này bằng lệnh sau:
```bash
    defaults write com.apple.screencapture disable-shadow -bool TRUE
    
    killall SystemUIServer
```
### Giữ máy Mac luôn mở

Bằng cách sử dụng lệnh caffeinate bạn có thể ghi đè cấu hình về thời gian sleep máy được quy định trong Energy preferences.
```bash
    caffeinate
```
hoặc giới hạn theo thời gian
```bash
    caffeinate -u -t [number of seconds]
```
### Tự khởi động lại Mac nếu gặp lỗi hoặc bị treo

Khi máy Mac của bạn bị treo, thường thì cách giải quyết duy nhất là nhấn giữ nút nguồn và đợi nó khởi động lại. Sử dụng lệnh này để làm cho nó tự động khởi động lại khi có sự cố.
```bash
    sudo systemsetup -setrestartfreeze on
```
### Chơi xếp hình (Tetris), Rắn săn mồi, Pong trực tiếp từ Terminal

Emacs là trình soạn thảo văn bản được cài sẵn macOS và có thể chạy từ Terminal, có một số Easter Egg dưới dạng trò chơi ở trong Emacs này. Để hiển thị chúng, gõ **Emacs** rồi nhấn enter, sau đó tiếp tục bấm **Fn + F10** rồi **t** rồi đến **g** Bạn sẽ thấy các trò chơi có sẵn được liệt kê và bây giờ có thể sử dụng các phím con trỏ để chọn chúng.

### Tạo biểu ngữ bằng các ký tự ASCII

Sử dụng lệnh sau để tạo một biểu ngữ dưới dạng mã ASCII, khá là thú vị.
```bash
    banner -w [the width of the banner in pixels] [your message]
```
Ví dụ: Tạo biểu ngữ với dòng chữ Pickamac, kết quả:

<figure class="kg-card kg-image-card"><img src="/assets/images/2020/10/image-9.png" class="kg-image"  sizes="(min-width: 720px) 720px"></figure>

### Thay đổi âm thanh khi kết nối Mac với nguồn điện giống iPhone (Power Chime)

Khi bạn cắm sạc iPhone, bạn thường nghe 1 âm thanh thông báo đã kết nối đến nguồn điện, nếu bạn muốn làm điều tương tự với Mac, có thể sử dụng lệnh sau
```bash
    defaults write com.apple.PowerChime ChimeOnAllHardware -bool true; open /System/Library/CoreServices/PowerChime.app
```
### Thay đổi thư mục lưu trữ mặc định khi chụp màn hình

Để thay đổi thư mục mặc định khi chụp màn hình trên macOS (thường là lưu trực tiếp trên Desktop), bạn có thể dùng lệnh sau:
```bash
    defaults write com.apple.screencapture location [place where you want screen grabs saved]
```
Sau đó chạy tiếp lệnh sau và Enter
```bash
    killall SystemUIServer
```
Ví dụ: Thay đổi thư mục lưu mặc định về foler Screenshot trên Desktop

<figure class="kg-card kg-image-card"><img src="/assets/images/2020/10/image-10.png" class="kg-image"  sizes="(min-width: 720px) 720px"></figure>

### Tắt tính năng tự lưu về iCloud của một số ứng dụng

Mặc định, một số ứng dụng macOS như TextEdit và iWork lưu tài liệu vào iCloud. Bạn có thể thay đổi điều đó bằng cách sử dụng:
```bash
    defaults write NSGlobalDomain NSDocumentSaveNewDocumentsToCloud -bool false
```    

Để khôi phục lại, chỉ cần chạy lệnh trên nhưng thay **false** bằng **true** ở cuối dòng lệnh.

### Xem phiên bản hoạt hình ASCII của Star War

Nếu bạn là fan của Star War thì bạn không thể bỏ lỡ điều này. Sử dụng lênh sau để xem phiên bản ASCII của bộ phim nổi tiếng này.
```bash
    telnet towel.blinkenlights.nl
```
Để thoát, dùng tổ hợp phím **Ctrl + ]**, sau đó gõ lệnh **quit**

<figure class="kg-card kg-image-card kg-card-hascaption"><img src="/assets/images/2020/10/starwar-ascii.gif" class="kg-image" alt><figcaption class="text-center">Phiên bản ASCII củ bộ phim Star War</figcaption></figure>

### Tăng tốc độ hiển thị thanh Dock

Nếu bạn sử dụng chế độ "Show and Hide Dock", bạn sẽ nhận thấy rằng khi bạn di con trỏ chuột vào cuối màn hình hoặc bất kỳ cạnh nào bạn giữ Dock, sẽ có độ trễ trước khi Dock trượt vào chế độ xem. Bạn có thể loại bỏ độ trễ đó bằng các lệnh sau:
```bash
    defaults write com.apple.dock autohide-delay -float 0
    
    killall Dock
```
Số **0** đại diện cho độ trễ trước khi Dock hiển thị, vì vậy nếu bạn muốn giảm đột trễ này hãy thay thế **0** bằng một giá trị khác, tính bằng giây.

Để quay &nbsp;về mặc định, sử dụng lệnh:
```bash
    defaults delete com.apple.dock autohide-delay
    
    killall Dock
```
### Hiển thị dòng chữ tuỳ chỉnh trên màn hình đăng nhập

Để hiển thị một dòng chữ tuỳ chỉnh trên màn hình đăng nhập (VD: Họ tên của bạn, một câu danh ngôn yêu thích...), hãy sử dụng lệnh sau:
```bash
    sudo defaults write /Library/Preferences/com.apple.loginwindow LoginwindowText "Your message here"
```
Để xoá dòng chữ này:
```bash
    sudo defaults delete /Library/Preferences/com.apple.loginwindow
```
### Tóm Lại

Trên đây là một số câu lệnh tuỳ chỉnh, vui vẻ dành cho Terminal, nếu bạn có biết thêm những câu lệnh hữu ích khác, hãy chia sẻ nhé. Nice day guys! See ya!

Tham Khảo: [MacWorld](https://www.macworld.co.uk/how-to/mac-terminal-projects-tutorial-3613813/)

