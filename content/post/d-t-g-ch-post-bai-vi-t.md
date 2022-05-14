+++
categories = ["Trick"]
date = 2022-05-12T17:00:00Z
description = "Dùng UFW để kiểm soát truy cập, chỉ cho phép máy tính ở nhà truy cập Server"
featured = false
featuredImage = ""
featuredImagePreview = "/uploads/ufw-firewall-1200x675.png"
tags = ["Trick"]
title = "Dùng UFW cho phép kết nối máy ở nhà vào Server"
toc = true

+++
Khi iptables mở hết các kết nối thì đương nhiên là ai trên Internet cũng truy cập được vào máy ảo. Ubuntu có sẵn ứng dụng tường lửa ufw, mình sẽ dùng ufw để kiểm soát truy cập. UFW thực chất cũng gọi iptables lên để thi hành thôi, nhưng có cú pháp đơn giản hơn nhiều so với đám câu lệnh loằng ngoằng của iptables cũng như firewall-cmd.  
Code:

    ufw allow 22/tcp
    ufw enable

Lưu ý thứ tự 2 câu trên, đầu tiên mở SSH, sau đó bật ufw lên. Do mặc định ufw sẽ chặn mọi kết nối từ ngoài vào nên nếu không mở SSH trước mà bật ufw lên thì tự mình đã khóa mình ở bên ngoài cửa luôn.  
  
Tạo 1 script lấy IP từ tên miền dynamic dns của nhà và chỉ cho phép IP đó truy cập vào máy ảo, mình không dùng cách cho phép list IP VN truy cập vào nữa do nếu nạp list IP của VN vào thì đống câu lệnh của tường lửa sẽ phình ra quá nhiều, máy ảo xử lý cũng mệt.  
Code:

    nano ufw-ddns.sh
    
    #!/bin/bash
    HOSTNAME=THAY_TÊN_DDNS_VÀO_ĐÂY
    
    if [[ $EUID -ne 0 ]]; then
       echo "This script must be run as root"
       exit 1
    fi
    
    new_ip=$(host $HOSTNAME | head -n1 | cut -f4 -d ' ')
    old_ip=$(/usr/sbin/ufw status | grep $HOSTNAME | head -n1 | tr -s ' ' | cut -f3 -d ' ')
    
    if [ "$new_ip" = "$old_ip" ] ; then
        echo IP address has not changed
    else
        if [ -n "$old_ip" ] ; then
            /usr/sbin/ufw delete allow from $old_ip to any
        fi
        /usr/sbin/ufw allow from $new_ip to any comment $HOSTNAME
    fi

Chỉnh cho script này chạy liên tục mỗi 2 phút để cập nhật IP:  
Code:

    chmod +x ufw-ddns.sh
    crontab -e
    */2 * * * * /home/ubuntu/ufw-ddns.sh

Chỉnh ufw giữ trạng thái đang hoạt động khi restart máy, nếu không khi restart máy, ufw sẽ bị tắt:  
Code:

    nano /lib/systemd/system/ufw.service
    
    Before=network.target
    After=netfilter-persistent.service

  
**Nguồn: VOZ**