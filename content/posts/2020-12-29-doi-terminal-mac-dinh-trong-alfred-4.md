---

toc: true
categories: ["macOS"]
date: "2020-12-28 07:05:05"
featured: false
featuredImage: /assets/images/2020/12/alfred_terminal_2.png
featuredImagePreview: /assets/images/2020/12/alfred_terminal_2.png
tags:
- macos
- tricks
- alfred
title: Hướng dẫn thay đổi Terminal mặc định sang Hyper trong Alfred
---
Alfred là ứng dụng cực hay ho thay thế Spotlight trên macOS với rất nhiều tính năng hữu ích, trong đó có tính năng chạy các command trực tiếp. Thông thường sẽ chạy command bằng cách gõ "> command", terminal mặc định trên macOS sẽ được mở lên và thực thi command đó. Tuy nhiên, với những ai sử dụng Hyper thay cho Terminal mặc định, sẽ cần phải tuỳ chỉnh 1 chút để command có thể được mở từ Hyper.

[Tham khảo thêm về các tính năng khác của Alfred](https://Dũng Hoàng.net/post/2020-10-13-alfred-su-thay-the-hoan-hao-cho-spotlight-cua-macos/)


Cách thực hiện như sau:

### Mở Alfred Preferences
Mở Alfred Preferences, sau đó vào phần Features, chọn Terminal. 
Tại màn hình Terminal, bạn chọn:
* Prefix: >
* Application: Custom

![Thay đổi Terminal mặc định sang Hyper trong Alfred](/assets/images/2020/12/alfred_terminal.png)

### Nhập Apple Scripts để thực thi mở Hyper thay cho Terminal
Ở màn hình bên dưới, bạn nhập vào đoạn code sau:

```
on hyper_win()
	set _running to (application "Hyper" is running)
	tell application "Hyper" to activate
	tell application "System Events"
		log (name of first application process whose frontmost is true)
		repeat while (name of first application process whose frontmost is true) is not "Hyper"
			delay 0.05
		end repeat
		
		set _hyper to first application process whose frontmost is true
		-- If Hyper was running, create a new window to run command
		if _running then
			tell _hyper to set _target to (count windows) + 1
			keystroke "n" using {command down}
		else
			set _target to 1
		end if
		
		-- Wait for wanted window count
		tell _hyper
			repeat while (count windows) < _target
				delay 0.05
			end repeat
		end tell
	end tell
end hyper_win

on alfred_script(q)
	my hyper_win()
	tell application "System Events"
		keystroke q
		key code 36
	end tell
end alfred_script
```

Kể từ giờ, mỗi khi bạn gọi command bằng cách sử dụng "> command", Hyper sẽ được mở lên và command sẽ được thực thi. ^^

![Thay đổi Terminal mặc định sang Hyper trong Alfred](/assets/images/2020/12/alfred_terminal_2.png)
