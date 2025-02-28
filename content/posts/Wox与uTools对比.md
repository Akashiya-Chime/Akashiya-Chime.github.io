---
title: Wox与uTools对比
tags: [software]
categories: [应用系统]
index_img: /img/wox-utools.png
date: 2021-04-02 10:00:00
---

最近又开始吹 uTools 了，老多推送推荐 uTools，说是「国产软件之光」、「全平台装机必备」、「黑科技神器」，诸如此类，吹得不要飞起。甚至有人评论：「用了 wox 之后，“listary 是什么垃圾？”，用了 utools 之后：“wox 是什么垃圾？”」

个人最开始使用的是 Wox，其实在去年或是更早一些的时候（记不得了，感觉在疫情之前）就已经接触到 uTools 了，但是不久之后又乖乖滚回来用 wox，解释其原因，也就是此文的主要目的了。

<!--more-->

<img src="https://i.loli.net/2021/04/02/Fh3EeV5HrzgjLKc.png">

## 获取途径

> 官网：
> wox：http://www.wox.one/
> utools：https://u.tools/

## 软件的一些信息

### 拿来对比的版本

- Wox：1.4.1196（本体开源）
- uTools：1.3.5（本体非开源）

### 更新情况
- Wox：最近一次更新在 2020.5.26，目前可能已无更新，Github 里躺了接近 600 条 issue（598 Open，2369 Closed）
- uTools：最近一次更新在 2020.9.9（日期来自社区），更新速度还行，官方建了社区，用户在社区与开发者交流，提供版本bug、功能需求以及插件发布，官方回复速度可观

## 比较

### 软件大小

- Wox：安装包 8.87 MB，安装后占用空间约 28 MB

- uTools：安装包 50.4 MB，安装后占用空间约 169 MB

### 使用时内存占用情况

- Wox：40-70 MB 左右（跳动较大，有时甚至上百）
- uTools：30 MB 左右（跳动不大）

### 插件

- Wox：目前官方有289个插件，大部分来自外国开发者，实用的也就那几个，因为软件本身开源，所以插件开发上传是允许的。通过 wpm install 来安装：

<img src="https://i.loli.net/2021/04/02/j9aCJqRHVsD8Ab6.png">

- uTools：同样上百个，且几乎所有（我看到的都是）国内开发者开发的，极强的可读性，但实用的也确实只有那几个，好的是，官方开放了插件开发和上传途径，且文档中有比较详细的说明。通过自带的 UI 来安装：

<img src="https://i.loli.net/2021/04/02/aigpz5moSvX2Zn8.png">

在插件这一块，是两个软件核心的东西，但对于个人来说千差万别，每个人对插件的需要和理解是不同的。

这里着重说最常用的 everything 的插件。

两者都需要 everything client，everything 确实是一款非常不错的软件，对于文件搜索的速度快得飞起，但是会有一个问题，那就是 everything 的内存占用，动辄上百居高不下的内存占用，成为我开机内存占用最高的应用，但是如果不启动，wox 和 utools 都无法使用 everything 的插件功能

<img src="https://i.loli.net/2021/04/02/AP7LvOslJUjFMeT.png">

这里提供一个 everything 的下载途径：https://www.voidtools.com/zh-cn/downloads/

**两者的区别体现在下面这几点：**

- uTools 要使用 everything 插件（其实是所有插件都要）必须先键入关键词，而且不提供关键词的修改。相比较起来 Wox 就好了很多，wox 有关键词 *，可以不用输入关键词就可以进行搜索，而且，插件的关键词可以修改。

<img src="https://i.loli.net/2021/04/02/JrZnzIikagPwjft.png">

<img src="https://i.loli.net/2021/04/02/t2g6LiNWzPUE8AO.png">

<img src="https://i.loli.net/2021/04/02/vNTQqEudChoGI1m.png">

- uTools 的搜索自带了文件类型分类以及预览模式，分类思想是好的，预览也对图片以及一些文字展示有好处，但是做为我个人使用的习惯，会用这种方式去打开某些常用的快捷方式，但是 uTools 并不配备搜索出的选项置顶的功能，让我很烦恼，甚至没有配置过滤选项还找不到快捷方式，而且过滤规则是值得研究的，有一定的学习成本。其他的一些常用功能（比如打开所在文件夹，拷贝，拷贝路径）两者都有，另外，Wox 还能以管理员身份运行

<img src="https://i.loli.net/2021/04/02/BcnkQFugmZjRiEG.png">

个人比较追求简约，Wox 提供自由的配色，对半透明的表现也非常令人满意，但是 uTools 就相对贫瘠了，本身只支持明亮与暗色两种主题，也只有修改透明度一个「效果不好」的滑条（透明会看不清文字）

<img src="https://i.loli.net/2021/04/02/aM3AgIm24BlYDpX.png">

<img src="https://i.loli.net/2021/04/02/VK82B9Zyuvi4cOf.png">

### 一些其他问题

- 收费：Wox 开源完全免费，uTools 开通会员会有云端数据备份（虽然感觉用不到，但是重装系统多了有点心虚）

- 平台问题：Wox 似乎只能 Windows，uTools 支持 Windows，Mac，Linux

- 文档问题：Wox 无，uTools 有比较完备（长）的介绍使用以及插件开发的文档（关于这点，文档是开发软件的一个优秀素质，但是从另一个方面来说，也体现了学习成本的区别，我 Wox 大多数功能用用就知道了，但 uTools 功能比较繁多，而且就连基础的一些功能也需要学习一下才能掌握，而且不保证记得住）

- uTools 有个鼠标中键的扩展功能，似乎可以语音输入，没怎么用（还是那句话，需要学），官方图：

<img src="https://i.loli.net/2021/04/02/ply7gnoaf5sLV3k.png">

- Wox 因为具有全局插件的概念，所以一些常用的插件可以直接用，识别性也很好（比如计算器，复杂加减乘除用起来很爽，又比如打开 URL 等等）

## 结论

结论就是适合自己的就是好用的，uTools 确实好用，但对我的一些依赖性功能，他比较「慢」，要么是需要花时间配置或学习，要么是使用的步骤繁琐，但是他氛围好的社区以及插件发布更新是非常香的，很多插件确实吸引我的眼球，也许几个版本后，我也会放下 Wox 用上 uTools（因为实在是太香了）。

最后，支持国产软件发展。

{% note primary %}
2022年12月30日注：现在已经从wox切到utools了，utools优于其良好的更新以及广大的社区，现在已经发展地很强大很好用了，修了很多以前的恶性bug，综合体验上来讲，我认为utools已经胜过wox了。
{% endnote %}