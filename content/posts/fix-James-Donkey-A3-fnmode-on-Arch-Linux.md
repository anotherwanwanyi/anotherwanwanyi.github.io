+++
title = 'Fix James Donkey A3 Fnmode on Arch Linux'
description = 'Arch Linux 下，修复 James Donkey A3 键盘 Fn 键不可用的问题。'
date = 2023-12-16
tags = ["keyboard"]
isCJKLanguage = true
+++

# 问题描述

最近我更换了新的键盘，淘宝上买的 [James Donkey A3](https://jamesdonkeylab.com/products/a3)。

发现其 F1 ~ F12 键在 Linux 下无法正常使用。
具体表现为不管是否按下 Fn ，这些按键始终输出媒体键（也就是音量控制之类的 Functional Key ）。

感觉这个 Bug 很影响我的日常使用体验，于是决定尝试解决。

# 解决过程

首先，我觉得这个问题应该是一种通病，所以尝试谷歌搜索 `James Donkey A3 Linux`。

很巧，搜到了这个讨论帖 [How to disable media keys (and enable Fn keys) on custom 75% keyboard / Kernel & Hardware / Arch Linux Forums](https://bbs.archlinux.org/viewtopic.php?id=283389)。

贴主和我使用了同样的键盘，有着同样的问题，而且是同样的Arch Linux。

一路看到最后，发现问题出在 `/sys/module/hid_apple/parameters/fnmode` 上。
看样子是我的键盘被识别成了 Apple 键盘，但又和默认的 `fnmode` 有所冲突。

通过 `cat /sys/module/hid_apple/parameters/fnmode`，我发现我的 `fnmode` 数值为3。
参考[Apple keyboard - ArchWiki](https://wiki.archlinux.org/title/Apple_Keyboard#hid_apple_module_options)，`fnmode` 的数值3代表为 `auto` ，也就是交给系统来判断。
看样子问题出在系统的判断有问题。
根据之前帖子的回复来看，想要解决这个问题，应该把 `fnmode` 的数值设置为2。

参考帖子里他人给出的链接 [ubuntu - How to swap the "fn" use of Function keys on an Apple Keyboard in Linux - Super User](https://superuser.com/questions/79822/how-to-swap-the-fn-use-of-function-keys-on-an-apple-keyboard-in-linux)，我的解决步骤是：

```
sudoedit /etc/modprobe.d/hid_apple.conf    # 在该文件写入 options hid_apple fnmode=2

sudo mkinitcpio -P                         # 重新生成所有 initramfs 映像
```

值得一提的是，`mkinitcpio` 是 Arch Linux 下的工具，如果你的系统是其他发行版，需要网上搜索一下如何重新生成 `initramfs` 映像。

重启系统，测试，发现已经可以正常使用。

# 总结

这个问题应该不止出现在我的 James Donkey A3 键盘上，其他的一些对 Linux 支持不积极的键盘应该也会有这样的问题。

希望我在这里的分享能帮到其他没有找到解决方案的人。

这篇文章的含金量不高，属于是自己用来备忘的随手记。
