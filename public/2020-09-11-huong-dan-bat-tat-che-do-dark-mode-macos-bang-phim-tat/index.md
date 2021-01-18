# Hướng dẫn bật/tắt chế độ Dark Mode macOS bằng phím tắt



Bắt đầu từ macOS Mojave, Apple đã trình làng chế độ Dark Mode (Chế độ tối) trên hệ điều hành của mình và giờ đây nó trở thành 1 phần không thể thiếu, đặc biệt đối với những người dùng hay sử dụng máy tính vào ban đêm.

Thông thường, để bật/tắt chế độ Dark Mode, người dùng cần vào _System Preferences / General_ và chọn _Dark_

<figure class="kg-card kg-image-card kg-card-hascaption"><img src="/assets/images/2020/09/image-2.png" class="kg-image" alt="Chế độ Dark Mode trên macOS Catalina" srcset="/assets/images/size/w600/2020/09/image-2.png 600w, /assets/images/2020/09/image-2.png 652w"><figcaption class="text-center">Hình 1: Chế độ Dark Mode trên macOS Catalina</figcaption></figure>

Tuy nhiên, có một cách nhanh hơn bằng cách sử dụng Automator để tạo phím tắt, giờ đây, chúng ta có thể bật/tắt chế độ Dark Mode mà không cần phải vào System Preferences. Hãy cùng bắt đầu nhé.

## Bước 1: Tạo script bật tắt Dark Mode bằng Automator

Các bạn truy cập vào ứng dụng **Automator** (có sẵn trong macOS, các bạn có thể bấm Command + Space và search Automator). Chọn _New Document -\> Quick Action_

<figure class="kg-card kg-image-card kg-card-hascaption"><img src="/assets/images/2020/09/image-3.png" class="kg-image" alt="Màn hình tạo Document Quick Action mới trong Automator" srcset="/assets/images/size/w600/2020/09/image-3.png 600w, /assets/images/2020/09/image-3.png 996w" sizes="(min-width: 720px) 720px"><figcaption class="text-center">Hình 1.1: Màn hình tạo Document Quick Action mới trong Automator</figcaption></figure>

Ở mục Workflow receives, các bạn chọn _no input_, các mục còn lại chọn như mặc định.

<figure class="kg-card kg-image-card kg-card-hascaption"><img src="/assets/images/2020/09/image-4.png" class="kg-image" alt='Chọn "no input" ở phần Workflow receives' srcset="/assets/images/size/w600/2020/09/image-4.png 600w, /assets/images/size/w1000/2020/09/image-4.png 1000w, /assets/images/2020/09/image-4.png 1009w" sizes="(min-width: 720px) 720px"><figcaption class="text-center">Hình 1.2: Chọn "no input" ở phần Workflow receives</figcaption></figure>

Ở màn hình tiếp theo, trong ô tìm kiếm của Automator, các bạn nhập vào _AppleScript_ và kéo _Run AppleScript_ vào ô cửa sổ bên cạnh. Sau đó, xoá hết những dòng code trong _Run AppleScript_ và nhập vào đoạn code sau:

    tell application "System Events"
    	
    	tell appearance preferences
    		
    		set dark mode to not dark mode
    		
    	end tell
    	
    end tell

Kết quả sẽ được như sau:

<figure class="kg-card kg-image-card kg-card-hascaption"><img src="/assets/images/2020/09/image-5.png" class="kg-image" alt="Dán code vào trong cửa sổ Run AppleScript" srcset="/assets/images/size/w600/2020/09/image-5.png 600w, /assets/images/2020/09/image-5.png 1000w" sizes="(min-width: 720px) 720px"><figcaption class="text-center">Hình 1.3: Dán code vào trong cửa sổ Run AppleScript</figcaption></figure>

Bạn có thể bấm nút _Play_ để kiểm tra thử, nếu macOS chuyển qua lại giữa Dark Mode và Light Mode có nghĩa là mọi thứ đã trơn tru. Bạn có thể bấm Command + S để lưu lại Automator này, đặt tên là _Dark Mode_ chẳng hạn.

## Bước 2: Tạo phím tắt (hoặc phím tắt Touchbar) cho Automator Dark Mode

Ở bước này, các bạn mở _System Prefecences/ Keyboard / Shortcuts_ để truy cập vào màn hình tạo phím tắt.

Ở màn hình Shortcuts, tiếp tục chọn vào Services, kéo xuống tìm Dark Mode đã tạo ở bước 1 và gán cho nó 1 phím tắt (Add Shortcuts), lưu ý hãy chọn những phím tắt khác với [những phím tắt thông dụng của macOS](/nhung-phim-tat-thong-dung-khi-dung-macos/) để tránh nhầm lẫn, ở đây mình chọn Command + B cho phím tắt này.

<figure class="kg-card kg-image-card kg-card-hascaption"><img src="/assets/images/2020/09/image-7.png" class="kg-image" alt="Gán phím tắt cho Dark Mode Automator" srcset="/assets/images/size/w600/2020/09/image-7.png 600w, /assets/images/2020/09/image-7.png 662w"><figcaption class="text-center">Hình 2.1: Gán phím tắt cho Dark Mode Automator</figcaption></figure>

Vậy là xong rồi đó, bạn có thể thử bấm Command + B để bật/tắt Dark Mode nhé. Đối với những máy hỗ trợ Touch Bar có thể làm thêm bước sau để hiển thị trên Touch Bar:

Các bạn mở _System Prefecences/ Extensions / Touchbar_ và enable _Dark Mode_ workflow. Sau đó quay lại _Keyboard/Customize Controlstrip_ kéo Dark Mode Workflow từ màn hình Customize vào Touch Bar. Vậy là xong, bạn có thể bật/tắt Dark Mode ngay trên Touch Bar của macbook rồi đó.

<figure class="kg-card kg-image-card kg-card-hascaption"><img src="/assets/images/2020/09/26412-37603-Touch-Bar-fix-xl.jpg" class="kg-image" alt="Kéo thả Dark Mode workflows vào Touch Bar" srcset="/assets/images/size/w600/2020/09/26412-37603-Touch-Bar-fix-xl.jpg 600w, /assets/images/size/w1000/2020/09/26412-37603-Touch-Bar-fix-xl.jpg 1000w, /assets/images/2020/09/26412-37603-Touch-Bar-fix-xl.jpg 1320w" sizes="(min-width: 720px) 720px"><figcaption class="text-center">Kéo thả Dark Mode workflows vào Touch Bar</figcaption></figure>

Bạn có sử dụng Dark Mode không? Và bạn đã tạo được phím tắt để bật tắt tính năng này chưa? Nếu có khó khăn gì hãy để lại comment bên dưới nhé. Chúc các bạn thành công.

[Tham Khảo: AppleInsider](https://appleinsider.com/articles/18/06/14/how-to-toggle-dark-mode-with-a-keyboard-shortcut-or-the-touch-bar)
