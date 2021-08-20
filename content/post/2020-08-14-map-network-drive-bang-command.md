---

toc: true
categories:
- Trick
date: "2020-08-14T07:50:00Z"
featuredImage: /assets/images/map-network-drive.jpg
featuredImagePreview: /assets/images/map-network-drive.jpg
title: Hướng dẫn map Network Drive bằng Command Line
description: "Các lệnh dưới đây dùng để map Network Drive, sử dụng cho mục đích ghi nhớ cá nhân."
---
Các lệnh dưới đây dùng để map Network Drive, sử dụng cho mục đích ghi nhớ cá nhân.

![Map Network Drive](/assets/images/map-network-drive.jpg)

Mapping a network drive to a shared folder from Windows’ graphic interface isn’t hard. But if you already know the network path for the shared folder, you can map drives a lot quicker using the Command Prompt.

Mapping a drive to a network share assigns that share a drive letter so that it’s easier to work with. We’ll be using the net use command in Command Prompt to map a network drive for this tutorial. You can also use the same command in PowerShell if you prefer.

To map a network drive, type the following command and then hit Enter:

```bash
net use DRIVE: PATH
```

DRIVE is the drive letter you want to use and PATH is the full UNC path to the share. So, for example, if we wanted to map drive letter S to the share \\tower\movies, we’d use the following command:

```bash
net use s: \\tower\movies
```

If the share to which you’re connecting is protected with some sort of authentication, and you’d rather not type in the credentials every time you open the network drive, you can add the user name and password to the command with the /user: switch. For example, if we wanted to connect the same share from above, but with the username HTG and the password CrazyFourHorseMen, we’d use the command:

```bash
net use s: \\tower\movies /user:HTG CrazyFourHorseMen
```

By default, mapped drives are not persistent. If we map drives using the commands we’ve talked about so far, the mapped drives would disappear when you restarted your computer. If you’d rather those mapped drives stick around, you can make them persistent by using the /persistent switch. The switch works as a toggle:

* /persistent:Yes: Makes the connection you’re currently creating persistent. Future connections you make using the command during the same session are also persistent (you don’t need to keep using the switch) until you use the /persistent:No switch to turn it off.
* /persistent:No: Turns off the persistency toggle. Future connections you make are not persistent until you turn the toggle back on.

So, essentially, you could type something like the following command:

```bash
net use s: \\tower\movies /user:HTG CrazyFourHorseMen /persistent:Yes
```
And the drive map would be persistent. All future mapping you create (even if you don’t use the /persistent:Yes switch) will also be persistent until you turn it off using the /persistent:No switch.

If you ever need to delete a mapped network drive, all you have to do is specify the drive letter and add the /delete switch. For example, the following command would delete the drive mapping we assigned to drive S:

You can also use the asterisk as a wildcard should you ever want to delete all your mapped drives in one go:

```bash
net use * /delete
```

Nguồn: Howtogeek
