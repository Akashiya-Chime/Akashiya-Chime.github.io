---
title: Blog 搭建参考
tags: [Blog]
categories: [编程开发]
index_img: /img/Blog.png
date: 2023-01-03 20:39:00
---

主要是讲一下使用 Hexo 作为工具，并使用 Github pages 作为部署方案的个人静态 Blog 搭建的大致流程。

<!--more-->

## 前言

Blog 这个东西，怎么说呢，写到现在，感觉最大的用处就是拿来总结一些东西。就像笔记，为了让自己忘了的时候回来翻一翻（我装 Arch 那篇确实是翻了很多遍。。。）。但是呢理想中的用处还是想能够去帮助一部分人，虽然我现目前能写出的东西并不算高深，但确实是自己踩了不少坑总结下来的个人经验，想来或许能在别人遇到相同问题时能够有抛砖引玉的作用。

说到 Blog 搭建，其实工具还蛮多的。我最开始使用的是 [Gridea](https://gridea.dev/)：
<a href="https://smms.app/image/kear27imDXKyGHt" target="_blank"><img src="https://s2.loli.net/2023/01/03/kear27imDXKyGHt.png" /></a>
它好处是用起来比较的简单，集成度比较的高，配置好后点点点就能把 Blog 发布出去。但是后来由于国内访问 Github 速度上的诟病，同步半天同步不上让我选择了放弃。之后就转到了体系上更大社区更广的 [Hexo](https://hexo.io/zh-cn/)，然后就一种使用到现在。其实还有很多，诸如 [Jekyll ](https://www.jekyll.com.cn/)（拿 Ruby 写的）、[Hugo](https://gohugo.io/)（拿 Go 写的）、[VuePress](http://caibaojian.com/vuepress/)（Vue 生态中的一员）等等，前段时间还看到个建站工具叫 [halo](https://halo.run/)（拿 Java 写的），也是可以拿来搭 Blog 站点的。

这次还是主要讲 Hexo，我使用的主题是 [Fluid](https://hexo.fluid-dev.com/)，然后丢到白嫖来的 github pages 上就成了现在看到的样子，其实步骤还蛮简单的。

## 准备工作

实际上就只是装个 [Node.js](https://nodejs.org/zh-cn/)，下载个长期维护版安装一路下一步就完事。你说想自定义一下安装位置其实也行，但其实 node 使用得当也不是很占地方。

哦，默认你是有 [Git](https://git-scm.com/) 的，没有的话装一个。

## 搭建

### 装 Hexo

官网上其实有很明确是步骤，你可以直接装个全局的脚手架：
```shell
$ npm install hexo-cli -g
```
进阶一点的话你可以装局部的，甚至不使用npm，使用yarn、npx或者pnpm也是可以的，这里就不多说了。

### 初始化

使用刚装的 hexo 的脚手架新建一个 blog 项目
```shell
$ hexo init <name>
```
这里的 `<name>` 就是项目的名字，随便取一个。
然后进入到项目文件夹下，先装一下依赖
```shell
$ npm install
```
这个时候基本的项目就已经搭好了，你可以用一下命令开启一个本地的服务器查看效果：
```shell
$ hexo server
```

### 主题

你可以在 hexo 的主题页面中寻找自己喜欢的主题样式，或者直接上 github 搜索也是可行的，这里以 fluid 为例讲一下一般步骤。

一般来说装 hexo 主题有两种方式：
1. git clone 仓库到项目的 themes 文件夹下
2. 使用 npm 作为依赖下载

fluid 推荐 hexo 5.0.0 版本以上用户使用 npm 直接安装，所以：
```shell
$ npm install --save hexo-theme-fluid
```
然后到 `node_modules` 文件夹下找到 `hexo-theme-fluid`，把 `_config.yml` 复制到最外面的项目文件夹（项目根目录）下，重命名为 `_config.fluid.yml`。
再然后修改项目根目录下的 `_config.yml` 中的 `theme: fluid`，`language: zh-CN`。
由于该主题有个「关于」页，所以为了展示完全，需要新建一个 about 页：
```shell
$ hexo new page about
```
然后修改  `/source/about/index.md`：
```markdown
---
title: about
layout: about
---

这里写关于页的正文，支持 Markdown, HTML
```
关于主题细节方面的配置这里就不赘述了，[官网文档](https://hexo.fluid-dev.com/docs/guide/)写的非常丰富

## 部署

本篇主要讲如何使用 hexo 的一键部署功能将项目部署到 github pages

首先你得有个 github 账号，这里默认你有了，如果没有就注册一个。

新建一个仓库，仓库名为 `你的用户名.github.io` ，进入仓库， 到 `Settings -> Pages` 中将 github pages 启用。

然后到项目中修改 `_config.yml` 
```yaml
deploy:
  type: 'git'
  repo: <repository>
  branch: main
  message: "Site updated: {{ now('YYYY-MM-DD HH:mm:ss') }})"
```
这里的 `<repository>` 就是你仓库的地址

之后你就可以尝试部署：
```shell
hexo clean && hexo deploy
```

{% note warning %}
1. 如果遇到说找不到你 git 的问题：
<a href="https://smms.app/image/47WYEz2nim8CKXq" target="_blank"><img src="https://s2.loli.net/2023/01/03/47WYEz2nim8CKXq.png" /></a>
可以
```shell
npm install hexo-deployer-git --save
```
2. 如果遇到 git 使用密码登录失败的问题
<a href="https://smms.app/image/D3OVWgqn1adhNjE" target="_blank"><img src="https://s2.loli.net/2023/01/03/D3OVWgqn1adhNjE.png" /></a>
这是因为 github 在 2021 年改了政策，不让用用户名密码登录了，一种解决办法是使用 token，可以参考[**这篇文章**](https://zhuanlan.zhihu.com/p/465182461)
{% endnote %}

如果做完了以上步骤，那么一个基本的 Blog 站点搭建就算完成了，下面来说一说写 Blog 时的一些问题和技巧。

## 写作方面的问题

一般来说文章的开头会有一些注释性的问题，例如本篇：
```markdown
---
title: Blog 搭建参考
tags: [Blog]
categories: [编程开发]
index_img: /img/Blog.png
date: 2023-01-03 20:39:00
---
```
里面包含了文章的标题、标签、分类、封面图片以及发表日期，除了标题和日期以外的项目可能是与你的主题配置是相关联的，建议查看主题配置相关文档细致了解。

然后就是有的主题应该支持概要的功能，能将文章中的前面一些文字显示在 Blog 主页中，此时可以使用 `<!--more-->` 来截断，以免显示内容过多
<a href="https://smms.app/image/DC4rEcbXLOvAS1B" target="_blank"><img src="https://s2.loli.net/2023/01/03/DC4rEcbXLOvAS1B.png" /></a>
文章内容就是纯纯的 markdown 了，没什么好说的，如果你在写作中涉及了 Latex 数学公式或者 Mermaid 流程图，可以查看 Hexo 相关渲染插件以及主题配置中是否有相关内容的设置。

## 后话

其实写 Blog 不仅是对自我知识的归纳总结，也是知识交流的一种途径。在当下国内如百度搜索一堆没用的信息以及类似 CSDN 这类站点大家互相抄来抄去，抄到最后排版尽失、要点难寻甚至不明所以要我掏钱要我关注的一种局面下，找到一篇真正能够解决问题的文章着实是有点难，这还怎么让我在写代码的时候 `Ctrl C` and `Ctrl V`（bushi）。

所以我还是希望能有更多的人能够真正去写一些东西，分享出来，让我们不流失好的想法或者是可贵的经验。