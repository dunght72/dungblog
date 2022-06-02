+++
categories = ["Trick"]
date = ""
description = "Rclone là công cụ tuyệt vời để quản lý, di chuyển dữ liệu"
draft = true
featured = false
featuredImage = "/uploads/rclone-tools.jpg"
featuredImagePreview = ""
slug = "rclone-cong-cu-tuyet-voi-de-di-chuyen-du-lieu"
tags = ["Google Drive", "Rclone"]
title = "Rclone - Công cụ tuyệt vời để di chuyển dữ liệu"
toc = false

+++
Ngày hôm nay, có mấy phim ở Fshare cần di chuyển qua Google Drive để xem trên Kodi, vậy là nghĩ ngay đến 2 công cụ tuyệt vời: [fshare2gdrive](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwiWpazjqY74AhXEEIgKHQGuDqwQFnoECAQQAQ&url=https%3A%2F%2Fgithub.com%2Fduythongle%2Ffshare2gdrive&usg=AOvVaw2eyeEAzFjJO38qrhijBJgl) và [Rclone](https://rclone.org/).

1. **Cài đặt và cấu hình với Rclone**

   Cài đặt Rclone băng 1 câu lệnh duy nhất

       curl https://rclone.org/install.sh | sudo bash

   Sau khi cài đặt xong, bạn cấu hình bằng lệnh: 

       rclone config

   Phần này mình không hướng dẫn chi tiết, có thể tìm hiểu thêm ở trang web của rclone
2. **Các lệnh thường dùng với Rclone**

   Mount ổ đĩa

       	rclone mount gdrive:Media /mnt/Media --allow-other --read-only --buffer-size 1G --dir-cache-time 72h --drive-chunk-size 32M --fast-list --vfs-read-chunk-size 128M --vfs-read-chunk-size-limit off --stats 1m --log-level INFO --log-file /var/log/rclone/rclone-shared.log &

   Copy từ Share With Me sang ổ Team Drive

   Lưu ý bước này phải tạo lối tắt folder VIE từ Share With Me sang Google Drive của mình, nếu không khi copy dùng flag --drive-shared-with-me sẽ bị lỗi tạo mới folder khi copy

       rclone copy dung_swm:VIE/Bounty.Hunters.2016.ViE.1080p.BluRay.DD5.1.x264-WiKi.mkv TDrive:Media/Movies -P
   3. **Leech file trực tiếp từ Fshare sang Google Drive bằng fshare2gdrive**

      Lưu ý trong này mình dùng link từ github của mình, có sửa appid do bản của tác giả duythongle bị lỗi

      Đâu tiên, tạo Credential để login Fshare bằng lệnh:

          curl -sS https://raw.githubusercontent.com/dunght72/fixfshare/dev/fshare2gdrive.js | \
          tail -n+2 | node - login "emailfsharecuaban" "matkhaufshare"

      Để leech file từ Fshare sang Google Drive (Team Drive)

    curl -sS https://raw.githubusercontent.com/dunght72/fixfshare/dev/fshare2gdrive.js | \
    tail -n+2 | node - "https://www.fshare.vn/file/X4DB5HPVXU61CCH" "TDrive" "/Media/Movies/" | bash -s

Để leech cả folder từ Fshare sang Google Drive

    curl -sS https://raw.githubusercontent.com/dunght72/fixfshare/dev/fshare2gdrive.js | \
    tail -n+2 | node - \
    "https://www.fshare.vn/folder/TX4XWAPVFT" "TDrive" "/Media/TV" | bash -s

4. **Bonus (Đổi tên file hàng loạt trên Google Team Drive**

Khi leech bộ Gia Đình Là Số 1 qua Google Drive thì tên file đặt không chuẩn nên Kodi không nhận diện được, do đó mình cần đổi lại tên file, tuy nhiên gặp phải khó khăn là các app hiện tại liên kết với Google Drive để đổi tên lại không hỗ trợ Team Drive, vậy là phải dùng cách khác

Bước 1: Thực hiện mount Google Drive vào Server Ubuntu (Đã thực hiện từ trước)

Bước 2: Cài rename tool

    sudo apt install rename

Bước 3: Di chuyển đến thư mục chứa file cần đổi tên, thực hiện lệnh sau để xem tên sau khi đổi

    rename -n 's/HighKick/High.Kick.Through.The.Roof.2009.S01E/' *

Đây là kết quả, các file sẽ đổi từ **HighKick00x** thành **High.Kick.Through.The.Roof.2009.S01Ex**

![](/uploads/bulk-rename-google-team-drive.jpg)

Sau khi xác nhận đã đúng tên, thì chỉ cần bỏ **-n** trong câu lệnh trên là xong

    rename 's/HighKick/High.Kick.Through.The.Roof.2009.S01E/' *

Kết quả mỹ mãn.

Chúc các bạn thành công