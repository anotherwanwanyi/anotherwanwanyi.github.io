+++
title = "Customize Firefox Browser With CSS"
description = "使用 userChrome.css 定制 Firefox。"
date = 2024-04-27
tags = ["customize", "firefox"]
isCJKLanguage = true
+++

## 前言

作为一个喜欢网上冲浪探索新鲜事物的人，我的大多数时间都用在了电脑上，或者更准确地说，是用在了浏览器上。

浏览器作为人与互联网交互的窗口，在信息时代始终充当着一个相当重要的角色。

尽管现如今的互联网已没有过去那样开放，各大平台把信息封锁在各自的平台上，有意无意地限制网页端的使用体验、半强迫用户下载使用它们的 APP，使得浏览器的使用体验变差了很多。

但浏览器依旧是网上冲浪不可或缺的角色，是一种自由精神的代表。

这开头我水不下去了，越写越像小学生作文。

简而言之，浏览器是像我这样喜欢 *网上冲浪* 的人相当喜欢且常用的工具。

冲浪多了，自然就发现这个工具有很多可以根据个人习惯去定制和优化的地方。

正所谓“**工欲善其事，必先利其器**”，为了提高网上冲浪效率，俺自然是琢磨了很多改进浏览器的方法。

而 `Firefox` 的 `userChrome.css` 便是其中值得一提的一项。

## 认识`userChrome.css`

那么问题来了，什么是`userChrome.css`?

~~根据 Mozilla 发布的[这篇指南](https://support.mozilla.org/en-US/kb/contributors-guide-firefox-advanced-customization)：~~

Edit: 我仔细看了一下，发现这篇是 Contributors 写的，应该不算是 *Mozilla 发布*，不过在此处影响不大：

> Firefox’s user interface is built of web-like elements (HTML and XUL elements) and styled using CSS. Users can set Firefox to look for a userChrome.css file at startup, so the rules in the file can restyle various elements of the user interface. For example, custom rules can change colors and sizes of many elements, hide them, or reposition them. 

我试着翻译一下：

> 火狐浏览器的 UI 是由像网页一样的元素（HTML 和 XUL 元素）构成的，并且由 CSS 风格化。用户可以设置 Firefox 以让它在启动时寻找一个`userChrome.css`文件，以此来使用文件中的规则重新风格化UI的多种元素。例如，自定义规则可以改变很多元素的颜色、大小，或是隐藏他们、将它们放到其他的位置。

我的解读是：`userChrome.css`代表着用户对浏览器的高阶掌控，用户可以使用CSS规则去定制浏览器的界面。

比如，对于我这样使用小屏笔记本而又偏爱 HiDPI 的人，平日为了看到更多网页内容，可以将书签栏设置成自动隐藏，仅在鼠标放置到导航栏上的时候暂时显示；在熟练使用很多键盘快捷键操作之后，还可以把很多导航栏上的元素隐藏掉。

或者，对于我这样经常同时打开很多网页的人，为了能更好浏览各个标签页，我可以结合插件定制一个垂直标签页栏（插件在这里的作用是初始模板 —— web-like elements provider），然后，既然实现了一个垂直标签页栏，那么水平的垂直标签页便也可以隐藏掉了。

还有，作为一名[猫布奇诺(Catppuccin)](https://github.com/catppuccin)爱好者，我想要在浏览器级别获得配色的一致性，那么用`userChrome.css`去配色也是一个绝佳的选择。

还有很多其他可以使用`userChrome.css`的情况，任君想象，限于篇幅，不再展开。

我相信大多数喜欢定制自己的工具的人应该都会喜欢这种感觉。

## 使用`userChrome.css`

> 写到这里的时候，我本来是想要参考 Reddit 上 [r/FirefoxCSS](https://old.reddit.com/r/FirefoxCSS/) 社区的 wiki 并给出参考链接的，结果打开之后我发现这个社区不知何时变成了私有状态，真是令人摸不着头脑。最初我刚开始使用`userChrome.css`的时候是它的 wiki 帮了我很多。

> 不过还好，我在互联网档案馆上找到了 wiki 上 tutorial 的[备份](https://web.archive.org/web/20240208182245/https://www.reddit.com/r/FirefoxCSS/wiki/index/tutorials)。不得不感叹，一个开放的互联网是多么令人向往。

### 开启设置

想要让 Firefox 在启动时加载 `userChrome.css`，首先要去`about:config`页面将`toolkit.legacyUserProfileCustomizations.stylesheets`的值改为`true`。

> 提示：你可以把`about:config`当作一个网址输入到浏览器的网址栏中访问。

> 彩蛋：Firefox 浏览器在`about:*`系列网页当中留下了一个彩蛋`about:robots`，前几天我刚发现这个彩蛋的时候笑了半天。

### 定位`userChrome.css`

`userChrome.css`文件在你的 Profile 文件夹当中。

关于 Firefox 的 Profile，此处不过多介绍，只介绍其也是 Firefox 的一种进阶玩法。

想要知道当前所使用的 Profile 配置文件位置，可以访问`about:profiles`或者`about:support`查看。

`userChrome.css`就在其中的`chrome`文件夹当中。

> 如果你的 Profile 文件夹十分干净没有`chrome`文件夹的话，可以自己手动创建一个，具体操作可以查看我先前给出的 wiki tutorial 的备份。

### 上手`userChrome.css`

使用`vscode`之类的文本编辑器打开文件，加入

```CSS
#navigator-toolbox {
    height: 200px !important;
}
```

然后再重启浏览器，你会发现 Firefox 的导航栏一下高了不少，这就是这段 CSS 代码的作用。

这是一种相当原始的自定义方法，需要不停地重启浏览器才能逐渐摸索到你想要的配置选项。

而且只是用这种方法的话，你是无法知道浏览器各个元素的名称和属性的，大小都只能靠猜。

那么有没有一种更加现代的方法呢？

有，而且相当方便、相当现代。

现在，你可以把刚才加进去的代码删掉了。

### REPL `userChrome.css`

不知道你曾经是否把玩过浏览器的开发者工具箱，那是一个相当好用的网页 Debug 工具。

只要打开它，网页的任何元素、布局、代码还有网络请求全部展露无遗。

更重要的是，你可以直接更改网页的代码并且收到实时的反馈。

这可以说是一种 REPL(Read-Eval-Print Loop)。

据我所知，两个快捷方式可以打开它，一个是`<F12>`一个是`<Ctrl> + <Shift> + I`。

我猜第二个快捷方式当中的`I`代表着“Inspect”。

既然有那么一个让网页展露无遗的工具箱，那么会不会有一个让浏览器展露无遗的工具箱呢？

毕竟，Mozilla 前面也说了，Firefox 的 UI 的组成逻辑就像一个网页，`built of web-like elements and styled using CSS`，照理来说要实现应该也没那么难。

不卖关子了。

针对浏览器的开发人员工具，确实存在，但是需要一点小操作才能启用。

[这里](https://firefox-source-docs.mozilla.org/devtools-user/browser_toolbox/index.html)是 Mozilla 的文档。

> The Browser Toolbox is not enabled by default. To enable it you need to check the settings “Enable chrome and addon debugging” and “Enable remote debugging”.

> 浏览器工具箱不是默认启用的。要启用它，你需要勾选设置选项“启用浏览器界面及附加组件的调试工具箱”和“启用远程调试”。

想要启用浏览器工具箱，你只需要先`<F12>`或者`<Ctrl + Shift + I>`打开网页工具箱，然后点击其右上角的三个点，打开设置，拉到最下方的`高级设置`，勾选这两个选项即可。

随后，你便可以通过快捷键`<Ctrl + Shift + Alt + I>`打开浏览器工具箱，享受现代化热加载的 REPL 浏览器定制体验了。

### 一些提醒

#### 热修改

你可以到工具箱的`样式编辑器`页面查看浏览器已加载的 CSS 文件，其中便有文章所介绍的`userChrome.css`。

在这里，你可以修改文件并实时查看浏览器对应的变化，如果对修改结果满意，可以用快捷键`<Ctrl + S>`保存修改后的文件。

可以说这就是`userChrome.css`的 IDE :smiling_face_with_three_hearts: 。

#### 值得借鉴的仓库

[firefox-csshacks](https://github.com/MrOtherGuy/firefox-csshacks)

## 结尾

这篇文章我很早就想要整理分享出来，只不过后来忙于折腾些别的东西就把这事给忘了...

前段时间，我平时在使用的 [Floorp](https://github.com/Floorp-Projects/Floorp) 浏览器（基于 Firefox ESR）更新了，结果引入了一些 CSS 相关的 [bug](https://github.com/Floorp-Projects/Floorp/issues/1097)，我花了点时间用前文介绍的方法找到了 bug 的来源，提出了人生第一个被 merge 的 [PR](https://github.com/Floorp-Projects/Floorp-core/pull/70)（现在回想起来内心还是有点小激动）。

解决 bug 的时候我才突然想起，“好像我原本打算写一篇关于这个的介绍文章来着”，于是就有了这篇文章。