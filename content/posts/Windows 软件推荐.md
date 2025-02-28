---
title: Windows 软件推荐
tags: [App]
categories: [应用系统]
index_img: /img/software.png
date: 2023-01-09 13:00:00
---

 上次的软件推荐快有两年了，如今接触的东西更多了，体验上手的软件也多了，又有了可推荐的。本文主要介绍一些正常使用免费的，较为小众的应用、Linux 到 Windows 可选的代替软件以及用于某些特定领域的软件。

<!--more-->

## 系统相关
## Etcher
> 官网链接：[balenaEtcher - Flash OS images to SD cards & USB drives](https://www.balena.io/etcher/)

一款开源的系统盘制作工具。

如果你安装过 Windows 系统，你也许使用过[微PE工具箱](https://www.wepe.com.cn/)来制作系统盘，而 Etcher 就更适合拿来装 Linux 系统，它更加的简洁和轻量化，没有微PE工具箱里携带的很多可能会用上也可能用不上的工具，它就是个纯粹的系统盘制作工具。
<a href="https://smms.app/image/hDc3t5MoBWdCmNf" target="_blank"><img src="https://s2.loli.net/2023/01/09/hDc3t5MoBWdCmNf.png" /></a>
### Dism++
> 软件获取：[Chuyu-Team/Dism-Multi-language: Dism++ Multi-language Support & BUG Report (github.com)](https://github.com/Chuyu-Team/Dism-Multi-language)

如图所示，是一个工具箱，功能还是非常多的
- 能够帮我删除一下我一般没有注意到的，但又没什么用占用我磁盘空间的垃圾
	- 比如一些临时文件、没用的日志、回收站或者是 Windows 更新文件
- 帮我删除系统预装的软件
	- 虽然但是我一般用 geek
- 调整一些系统设置
	- 比如关闭搜索栏、小娜、人脉、OneDrive 还有各种广告等等杂七杂八的东西
	- 也包括去掉快捷方式小箭头、去掉管理员运行的小盾牌之类的很「妙」的小功能，很多东西可能会戳中你以前找了很久如何设置但又百度不到的痛点
	- 也包括了一些如系统备份还原、引导修复、hosts编辑等常见的工具

<a href="https://smms.app/image/HDeGQ8pnPWOyC7V" target="_blank"><img src="https://s2.loli.net/2023/01/09/HDeGQ8pnPWOyC7V.png" /></a>
### SpaceSniffer
> 软件获取：[SpaceSniffer download (uderzo.it)](http://www.uderzo.it/main_products/space_sniffer/download.html)

磁盘扫描，然后用图形方块来显示文件和文件夹占用的空间大小，虽然他稍微有些慢，有时候甚至会卡住，但是相较我之前找过的替代品来说，他是视觉效果最好的一个。

由于我的电脑只有一个256G的固态，导致我时常产生剩余空间不足的焦虑，就经常会打开软件看看什么大软件占用了我的空间。

同时也方便我去删除电脑QQ产生的没用的图片缓存。
<a href="https://smms.app/image/KzoYHaZhNJMcg1m" target="_blank"><img src="https://s2.loli.net/2023/01/09/KzoYHaZhNJMcg1m.webp" /></a>
### Geek
> 官网：[Geek Uninstaller - the best FREE uninstaller](https://geekuninstaller.com/)

最喜欢，个人感觉最好用的卸载工具。简洁、快速，删除软件同时删除残留的文件夹以及注册表，还能删除系统预装的软件。

神
<a href="https://smms.app/image/A1tibDXZ3werBG8" target="_blank"><img src="https://s2.loli.net/2023/01/09/A1tibDXZ3werBG8.png" /></a>
### 系统服务控制管理器批量辅助增强工具
> 软件获取：https://wwn.lanzouw.com/iyoAt067zw6h
> 提取码：e913

{% note danger %}
注意：这个软件如果操作不当将可能对你的系统造成严重损害，由此产生的问题本人概不负责，勿谓言之不预。
{% endnote %}

软件的作者是b站up [有限的未知](https://space.bilibili.com/1199158766)，软件的详细使用请先完整观看他的视频：[自编_系统服务辅助增强工具，无限制批量修改、禁用、卸载系统服务，涉及系统服务管理、优化、备份及相关技巧，可以相当自由的操作服务，拒绝强制你接受的服务](https://www.bilibili.com/video/BV1hr4y1V7Yk/)

视频中有对该软件使用非常详细的说明，这里简单来说就是对 Windows「服务」的几乎完全掌控，你可以用它来删掉各种流氓软件在你系统中安装的各种流氓服务，也可以做到停用甚至是删除 Windows 的更新服务以及 Windows Defender。

在你动手系统的服务时，你需要自行了解那些服务会影响到哪些东西。比如有的软件在安装或者使用时会检测 Windows 的防火墙状态，如果他发现你的防火墙没有正常开启，他就不会让你用（尤其是跟网络连接有关的应用），如果你关闭了 Windows Defender 服务，那么很有可能导致软件无法正常运作。

但这个软件的确非常的强大，就是需要谨慎使用。
<a href="https://smms.app/image/M26CEZBmkqdhSR5" target="_blank"><img src="https://s2.loli.net/2023/01/09/M26CEZBmkqdhSR5.png" /></a>
## 便捷工具
### File Converter
> 官网：[File Converter - Convert & compress everything in 2 clicks! (file-converter.org)](https://file-converter.org/)

一个方便的文件转换工具。相比较广为人知的格式工厂，这个软件更加的简洁，有时候相同的输出条件甚至会快一些。软件也是支持自定义输入详细配置的。如果你有视频、音频或者图片格式装换的需求，可以尝试一下。
<a href="https://smms.app/image/1JGr7MA2NVfmipR" target="_blank"><img src="https://s2.loli.net/2023/01/09/1JGr7MA2NVfmipR.gif" /></a>
### Motrix
> 官网：[Motrix](https://motrix.app/)

一个开源的下载工具，一般是用来下载磁力链接。相比同类型知名软件 BitTorrent 来说，Motrix 界面更加养眼，看上去更加简洁，更为关键的一点在于，Motrix 设置和更新 Tracker 更加简便。如果你有下载磁力链接的需求，不妨放下吸血鬼迅雷，来试一试 Motrix。

<a href="https://smms.app/image/zxyceYvrKA4jiku" target="_blank"><img src="https://s2.loli.net/2023/01/09/zxyceYvrKA4jiku.png" /></a>
### antdownload
> 一代：[antdownload v3.0.6  | 克隆窝 (kelongwo.com)](https://www.kelongwo.com/antdownload/)
> 二代：[antdownload2 v1.0.6 | 克隆窝 (kelongwo.com)](https://www.kelongwo.com/antdownload2/)

上面下磁力链接应对迅雷，那么现在来讲讲如何应对百度网盘。尽管百度网盘可以通过开启所谓的「优化速率」模式来稍微提升一下他允许的下载速度，但不影响他不开心的时候让你在5G网络下拥有 1KB/s 的高速下载。

antdownload 支持批量打包下载以及多线程，而且无需登录百度网盘（但是软件得关注公众号登录），速度虽然不是拉满的，但总好过百度网盘虚伪的诚意。

**据作者说，一代停用了，建议使用二代**

<a href="https://smms.app/image/wbfvacYZN6WK9QI" target="_blank"><img src="https://s2.loli.net/2023/01/09/wbfvacYZN6WK9QI.png" /></a>
## 命令行工具
Linux 用多了导致对终端命令行爱不释手，即便是在 Windows 下，ssh 链接服务器以及 git 来管理项目也会经常用到命令行，这促使我不停地去寻找好用的 Windows 下能用的命令行工具。

在此之前，我们先理清一些东西，来简单地看看什么是终端、什么是终端模拟器、什么是Shell，并举些例子来帮助理解。

- **终端**：也就是 terminal，终端在以前是一个单独的物理设备，用以多个使用者对同一个计算机进行交互。现在的电脑上呢，终端就以软件的形式存在。比如 Windows 上的 conhost，就是我们熟悉的黑底白字：
	<a href="https://smms.app/image/zBdLwOMSV7e81pU" target="_blank"><img src="https://s2.loli.net/2023/01/09/zBdLwOMSV7e81pU.png" /></a>
- **Shell**：其实分了图形化的Shell和命令行的Shell，命令行Shell也被直接叫做**命令行**。我们通过终端与计算机的交互不是直接进行的，我们在终端中输入指令回车后，指令被送往 Shell，可以理解为是命令解释器（有点像是解释型编程语言的解释器），经过 Shell 的处理后计算机再操作，如果有返回的内容又返给 Shell，最终显示在终端上。比如 Linux 下的 bash、zsh以及 Windows 下的 cmd 和 powershell。如图，我们可以使用 conhost 打开 cmd 和 powershell（因为 conhost 默认打开的是 cmd，所以看到输入 cmd 回车后感觉没什么变化）：
	<a href="https://smms.app/image/WmzGvOR1BrlhDeM" target="_blank"><img src="https://s2.loli.net/2023/01/09/WmzGvOR1BrlhDeM.png" /></a>
- **终端模拟器**：终端模拟器呢，说他是模拟器其实是相较物理的终端设备而言的，所以你可以叫他模拟终端设备的模拟器，是电脑软件。那么他和终端有什么区别呢，实际现在电脑软件的终端都是终端模拟器，都是现在图形化操作系统下用以模拟以前物理终端设备的**软件**，所以，也可以直接叫终端模拟器为终端。那么现代一点的终端有比如 Alacritty、simple terminal（st）、Wezterm 以及 Windows Terminal。

可能我说的繁琐了一些，简单说就是我们下了个终端的软件，连上了 shell，然后疯狂输出。

下面呢就介绍一些在 Windows 下能用终端（模拟器）和命令行（也就是 Shell）工具。

### 终端模拟器
#### Windows Terminal
前两年巨硬搓出来的，现在 win11 已经作为默认的终端了。
*可怜的 conhost，人们几乎都不知道它的名字，一直管他叫 cmd*

看上去更加 Fluent 了，而且也在不断地更新，这里就不多赘述了。
#### Alacritty
> 官网：[Alacritty - A cross-platform, OpenGL terminal emulator](https://alacritty.org/)
> Github 仓库：https://github.com/alacritty/alacritty

挺好看的一个终端，配置文件使用的 yaml，配置挺方便也听全面的，主要是在 Linux 下使用，Windows 倒也能用，但有些渲染问题，最让我难受的一点是不支持 ligatures（就是连字符，比如 `->`  渲染成一个箭头）

<a href="https://smms.app/image/zELVFwe4AkjaRUQ" target="_blank"><img src="https://s2.loli.net/2023/01/09/zELVFwe4AkjaRUQ.png" /></a>
#### Wezterm
> Github 仓库：https://github.com/wez/wezterm

我目前在用的一个终端，跨平台，配置文件使用 lua，配置也挺方便的，能在 Windows 下将标题栏也去掉，然后通过按住 Ctrl 加鼠标左键拖动移动，虽然跟 Alacritty 一样在 Windows 下存在一些渲染上的问题，但总体而言我的体验还是不错的。

<a href="https://smms.app/image/cauRMevIE9OzKCr" target="_blank"><img src="https://s2.loli.net/2023/01/09/cauRMevIE9OzKCr.png" /></a>
### Shell
#### nushell
> 官网：[| Nushell](http://www.nushell.sh/)
> Github 仓库：https://github.com/nushell/nushell

Windows 下是真的没什么好用的 Shell，一个 cmd，虽然挺快，但是完全不支持配色方案，看着扎眼睛；另一个 powershell，首先慢得要死，每次打开等几秒到十几秒我可忍不了，另外虽然能够有一些配置的余地，但是配置起来要多难受有多恼火（我甚至看不懂报错）。

得亏这两年 Rust 逐渐进入视野，然后碰巧看到了 nushell。它安装方便，而且本身就很好看，配置起来非常方便，而且设置了很多 Linux 常用指令。

我目前就是 nushell 配合 Wezterm 使用，很香啊，很香。

<a href="https://smms.app/image/mJPTgpVObcEHh8D" target="_blank"><img src="https://s2.loli.net/2023/01/09/mJPTgpVObcEHh8D.png" /></a>
{% note warning %}
nushell 在 wezterm 下会出现不停换行的问题，找到的有效解决办法是修改 `config.nu` 中 `shell_integration: false`
{% endnote %}
### 命令行工具
#### scoop
> 官网：[Scoop](https://scoop.sh/)
> Github仓库：https://github.com/ScoopInstaller/scoop

Linux 安装软件我们一般会用到包管理工具，比如 Ubuntu 下有 apt，Arch 下有 pacman，那么Windows 是不是也可以搞个包管理工具呢，然后就有人做了 scoop，或者你也听说过 [Chocolatey](https://chocolatey.org/)。好处就是更好的帮助我们找到需要下载的软件以及控制软件版本（我百度一下甚至找不到 scoop 官网），然而最大的坏处是，他的软件库放在了 Github，如果你与 Github 的网络连接不佳，那么体验可能非常难受。下面介绍到的命令行工具就可以通过 scoop 来安装。

#### bottom
> Github 仓库：https://github.com/ClementTsang/bottom

一个跨平台的命令行图形系统监视器，类似 top、btop 或者 Windows 下的任务管理器，使用 Rust 编写，功能丰富，好看，如果你哪天不想看任务管理器了，不如来试试。

<a href="https://smms.app/image/6EfKW9bZYS4gAON" target="_blank"><img src="https://s2.loli.net/2023/01/09/6EfKW9bZYS4gAON.png" /></a>
#### lazygit
> Github 仓库：https://github.com/jesseduffield/lazygit

一个我爱不释手的 git 工具，使用 Go 编写，我现在已经成了一个记不住 git 命令的 lazy 废物了，他几乎能让你用快捷键做所有 git 命令能做的事，比起那些图形化的 git 工具，我会更喜欢这个，相信我，如果你上手了 lazygit，你也会爱上他。

<a href="https://smms.app/image/acLUyZMDPImN653" target="_blank"><img src="https://s2.loli.net/2023/01/09/acLUyZMDPImN653.png" /></a>
## 后话
以上差不多就是这次的软件推荐了，至今还是很喜欢 [Topbook](https://space.bilibili.com/29959830) 的那句话：
> 让工具回归工具，让你成为你

有了工具，最终还是得用工具干实事。