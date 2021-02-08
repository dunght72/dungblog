---

toc: true
categories: ["macOS"]
date: "2020-09-28T08:22:02Z"
featuredImage: /assets/images/2020/09/homebrew-social-card.png
featuredImagePreview: /assets/images/2020/09/homebrew-social-card.png
tags:
- huong-dan-chung
- thu-thuat
- homebrew
title: Homebrew là gì? Cách sử dụng Homebrew trên macOS
---

Nếu bạn là người dùng macOS, chắc hẳn bạn đã từng nghe đến Homebrew, brew... Vậy đó là cái gì? Nó có gì hay ho? Và sử dụng Homebrew như thế nào? Bài viết này sẽ chia sẻ đến bạn kiến thức về Homebrew nhé.

## Homebrew là gì?
<figure class="kg-card kg-image-card kg-card-hascaption"><img src="/assets/images/2020/09/homebrew-social-card.png" class="kg-image" alt="Homebrew - Trình quản lý gói phần mềm mã nguồn mở cho macOS" sizes="(min-width: 720px) 720px"><figcaption class="text-center">Homebrew - Trình quản lý gói phần mềm mã nguồn mở cho macOS</figcaption></figure>

Về cơ bản, Homebrew là trình quản lý gói phần mềm mã nguồn mở giúp việc cài đặt phần mềm trên macOS &nbsp;và Linux nói chung dễ dàng hơn.

Nói dễ hiểu, khi người sử dụng muốn cài đặt ứng dụng A trên macOS, mà ứng dụng A đó yêu cầu phải có phần phụ thuộc A.1, A.2 phải được cài đặt trước, thay vì việc phải tìm kiếm, cài đặt thủ công từng phần phụ thuộc và ứng dụng A thì Homebrew sẽ làm điều đó cho bạn, nó sẽ cài đặt tất cả những thứ liên quan đến A để ứng dụng có thể chạy được trên macOS của bạn.

Homebrew được viết bằng ngôn ngữ lập trình Ruby. Các gói ứng dụng của Homebrew thường được cài vào thư mục riêng của chúng &nbsp;và sau đó tạo sym link đến thư mục /usr/ local.

## Cài đặt Homebrew như thế nào?

Để cài đặt Homebrew, các bạn mở ứng dụng Terminal và dán vào dòng lệnh sau:

    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

Sau khi lệnh chạy xong, thực hiện chạy lệnh dưới để thực hiện update brew. Quá trình cài đặt có thể mất một lúc tuỳ thuộc vào cấu hình máy và tốc độ đường truyền internet của bạn.

    brew update

## Cài đặt gói phần mềm dùng Homebrew

Homebrew đã được cài đặt. Vậy làm cách nào để cài đặt ứng dụng và các phần phụ thuộc đi kèm bằng Homebrew. Rất đơn giản, chỉ cần thực hiện lệnh sau trong Terminal

    brew cask install ten-ung-dung

**Ví dụ:** Nếu bạn muốn cài đặt trình duyệt Google Chrome, hãy gõ lệnh sau:

    brew cask install google-chrome

Giờ đây, Homebrew sẽ nhanh chóng tìm ra Google Chrome cần những gói phụ thuộc nào, gói nào &nbsp;đã được cài đặt trên máy của bạn và gói nào còn thiếu hoặc nếu có bất kỳ điều gì cần được cập nhật để làm cho trình duyệt Chrome hoạt động tối ưu trên hệ thống cụ thể của bạn. Sau đó, Homebrew sẽ cài đặt tất cả các gói &nbsp;phụ thuộc phần mềm cần thiết cho bạn. Tuỳ thuộc vào dung lượng ứng dụng, gói phụ thuộc và cấu hình máy cũng như đường truyền mà quá trình này sẽ mất 1 khoảng thời gian, thường rất nhanh.

## Danh sách các lệnh của Homebrew

Bạn có thể tham khảo Cheatsheet sau để biết thêm về các command của Homebrew:

<figure class="kg-card kg-image-card kg-card-hascaption"><img src="/assets/images/2020/09/cheatsheet-homebrew.png" class="kg-image" alt="Homebrew Cheatsheet (Nguồn: Code2bits)" sizes="(min-width: 720px) 720px"><figcaption class="text-center">Homebrew Cheatsheet (Nguồn: Code2bits)</figcaption></figure>

## Tóm lại

Homebrew là một phương pháp khá tốt để bạn cài đặt và quản lý ứng dụng trên macOS. Bạn có đang sử dụng Homebrew không? Hãy chia sẻ thêm cùng với mọi người nhé. Nice day guys!

