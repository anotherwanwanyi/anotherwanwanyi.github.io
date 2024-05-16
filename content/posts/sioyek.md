+++
title = "开始使用 Sioyek"
description = "简单地介绍了 PDF 阅读器 Sioyek 的上手使用及配置过程。"
date = 2024-05-16
tags = ["sioyek", "tool", "customize"]
isCJKLanguage = true
+++

## 前言

前几天我在翻看 Hacker News 的每日 Newsletter 时，发现一个 PDF 阅读器，名为`Sioyek`。

在看了其[官网](https://sioyek.info/)上的使用演示之后，我发现它与我现在在使用的`zathura`比较相似，有着同样的`vim-like`键位支持，不同的是`Sioyek`更倾向于一个开箱即用的软件，有着更加舒适的上手体验，而且[文档](https://sioyek-documentation.readthedocs.io/en/latest/)更加完备。

所以我决定从`zathura`切换到`Sioyek`。

## 安装

安装过程可以参考[Sioyek 代码仓库](https://github.com/ahrm/sioyek/)中的 README。

我的系统环境为`Arch Linux`，所以我只需使用`AUR Helper``paru`进行安装即可。

值得一提的是，在`AUR`中存在三个版本的`Sioyek`，分别为`sioyek`、`sioyek-git`和`sioyek-appimage`。

参考其各自在`AUR`上的`PKGBUILD`，这三个版本的二进制`Sioyek`来源如下表所示：

| 名称 | 来源 |
|--|--|
| sioyek | Github 仓库当中最新 Release 的源码编译版本（自行编译）|
| sioyek-git | Github 仓库当中 development 代码分支的源码编译版本（自行编译） |
| sioyek-appimage | Github 仓库当中最新 Release 中已编译好的 Linux 版本 |

考虑到Git版本的不稳定性，我首先排除了`sioyek-git`的选项。

随后在我的尝试当中，我发现`sioyek-appimage`版本的软件字体大小似乎有些问题，所以也排除了这一选项。

之后，我意外地发现我所使用的`archlinuxcn`源当中有预编译的`sioyek`包，这可以省去包更新带来的重新编译，所以我选择了`sioyek`包。在我的使用体验当中，`sioyek`没有出现类似`appimage`版本当中字体大小的问题。

## 上手使用

第一次启动时，`Sioyek`会打开一个`tutorial.pdf`，对软件的键位设置进行简易介绍。

该文件介绍较为全面，可以结合[文档](https://sioyek-documentation.readthedocs.io/en/latest/)学习此软件基础的使用。

由于以上官方文档的介绍较为全面，所以此处不过多介绍。

值得一提的是，使用`Shift + O`可以打开近期开启过的文件，如果觉得自己对键位还不太熟悉，可以使用该快捷键回到`tutorial.pdf`文件查看教学。

另外，尽管`Sioyek`自称为`PDF viewer`，但是由于其使用了`mupdf`作为渲染引擎，所以实际上`Sioyek`支持后者所支持的所有文件格式，例如`Epub`。

## Customize

就像在[配置文档](https://sioyek-documentation.readthedocs.io/en/latest/configuration.html)所说的那样：

> Sioyek uses four config files:

>  - `keys.config` which stores the default keybindings

>  - `keys_user.config` which stores the modified keybindings

>  - `prefs.config` which stores the default preferences

>  - `prefs_user.config` which stores the modified preferences

`Sioyek`的用户配置文件为`keys_user.config`与`prefs_user.config`，前者存储用户自定义的按键绑定，后者存储用户自定义的设置偏好。

在Linux下，这两个文件的位置应该在于`~/.config/sioyek`文件夹当中。

其中，具体的文件格式及可配置选项可以参考上述文档。

此处是我的`prefs_user.config`的文件内容：

```config
ruler_mode 1
ui_font serif
case_sensitive_search 0
should_launch_new_window 1

create_table_of_contents_if_not_exists 1
max_created_toc_size 5000

startup_commands toggle_custom_color;toggle_smooth_scroll

source ./catppuccin-mocha.config
```

值得一提的是，最后一行的`source ./catppuccin-mocha.config`为可选项，这行配置的效果为引入外部文件`catppuccin-mocha.config`中的配置项。

`catppuccin-mocha.config`的文件内容：

```config
background_color           #1e1e2e

text_highlight_color       #a6e3a1
visual_mark_color          0.27058825 0.2784314 0.3529412 0.2

status_bar_color           #1e1e2e
status_bar_text_color      #cdd6f4

search_highlight_color     #f9e2af
link_highlight_color       #89b4fa
synctex_highlight_color    #a6e3a1

highlight_color_a          #f9e2af
highlight_color_b          #a6e3a1
highlight_color_c          #89dceb
highlight_color_d          #eba0ac
highlight_color_e          #cba6f7
highlight_color_f          #f38ba8
highlight_color_g          #f9e2af

custom_background_color    #1e1e2e
custom_text_color          #cdd6f4

ui_text_color              #cdd6f4
ui_background_color        #313244
ui_selected_text_color     #cdd6f4
ui_selected_background_color #585b70

page_separator_color       #1e1e2e
```

该文件的作用为自定义`Sioyek`的一些颜色。

该配色方案参考了网络文件[`base16-catppuccin-mocha.config`](https://github.com/loiccoyle/base16-sioyek/blob/main/colors/base16-catppuccin-mocha.config)与[`catppuccin-mocha.conf`](https://github.com/catppuccin/sioyek/blob/main/themes/catppuccin-mocha.config)。

如果你不需要该配色方案，那么可将`prefs_user.config`中的行`source ./catppuccin-mocha.config`删掉，并将启动指令`startup_commands`中的`toggle_custom_color;`删去。

## 结语

希望本文能对你有所帮助。