# Một số lệnh Terminal hay sử dụng

Một số Code Snippet hay sử dụng trong terminal, dùng để ghi nhớ cá nhân

![Code Snippet hay dùng](/assets/images/hyper-feature.png)

### Lệnh copy file từ remote xuống Local

```bash
scp -r user@server.com:/path/to/remote /path/to/local
```

### Lệnh copy file từ Local lên Remote

```bash
scp /path/to/local user@server.com:/path/to/remote
```

### Lệnh copy giữa Cloud Drive và Local dùng rclone hoặc giữa các Cloud

- Bước 1: Cài đặt rclone từ trang chủ
- Bước 2: Cấu hình Cloud Drive trên rclone
- Bước 3: Dùng lệnh sau để copy giữa các Drive hoặc giữa Drive và Local
```bash
rclone copy tendrive:path/to/folder destination:path/to/folder --disable copy
```
Lưu ý: Nếu là Google Drive thì có giới hạn copy là 750GB/ngày

### Dùng Screen trong linux

Tạo screen mới
```bash
screen
```
Truy cập vào một screen
```bash
screen -r (id)
```
Thoát tạm thời khỏi screen
```bash
Ctrl + A + D
```
### Lệnh mount drive dùng rclone

```bash
rclone mount gdrive:Media /mnt/Media --allow-other --read-only --buffer-size 1G --dir-cache-time 72h --drive-chunk-size 32M --fast-list --vfs-read-chunk-size 128M --vfs-read-chunk-size-limit off --stats 1m --log-level INFO --log-file /var/log/rclone/rclone-shared.log &
```


