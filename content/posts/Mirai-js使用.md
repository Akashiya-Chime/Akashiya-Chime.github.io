---
title: Mirai-js使用
tags: [Mirai]
categories: [编程开发]
index_img: /img/mirai-js.jpg
date: 2021-08-19 10:00:00
---

有关 QQ 机器人框架 Mirai 下的基于 Node.js 的框架 Mirai-js

> Mirai是一个免费开源的QQ机器人框架，由于其开源和易拓展的优势，现在已经有很多基于Mirai的官方和非官方衍生框架和应用，其关系错综复杂。
> 
> Mirai-js，一个运行在 Node.js、浏览器下的，简单的 QQ 机器人开发框架。

<!--more-->

## 前言

自从之前为人们广为熟知的 QQ 机器人框架「酷Q」停止运营，晨风机器人的作者被请喝茶后，一时间很多 QQ 机器人开发者开始陷入彷徨，不知何去何从。但总归 QQ 机器人的需求不会停止，新的框架会应运而生。

我在酷Q时代一直使用的插件「Dice!」的作者溯洄很快将框架转移到 Mirai 上，我也就了解到了这个框架。

> 溯洄大佬的 Dice! 论坛：[Dice! 论坛 (kokona.tech)](https://forum.kokona.tech/)

虽然开始用的时间比较早，但是实际上也只是前不久才开始着手开发自己的部分。

因为之前一直只拿 Dice! 当跑团骰子用，并没有想过开发点别的东西

另外就是因为酷Q时代开发使用易语言给我带来的阴影

不过等一段时间还是好的，毕竟需要框架本身进行一段时间自我完善，能够稳定或发展生态为开发者提供良好平台（别骂了别骂了，是我懒:cry:）

## 先从 Mirai 说起

Mirai 是使用 Kotlin 开发的，支持插件，一般用户可直接上论坛找大佬发布的插件装上就用

> [Mirai Github repository](https://github.com/mamoe/mirai)
> 
> [MiraiForum](https://mirai.mamoe.net/)

如果要参与开发，原生的当然是使用 kotlin，但是呢，也有一些原生的，如下：

|技术|维护者及项目地址|
|---|---|
|Kotlin Scripting|[iTXTech/mirai-kts](https://github.com/iTXTech/mirai-kts)|
|C++|[Nambers/MiraiCP](https://github.com/Nambers/MiraiCP)|
|JavaScript|[iTXTech/mirai-js](https://github.com/iTXTech/mirai-js)|
|酷 Q DLL 插件|[iTXTech/mirai-native](https://github.com/iTXTech/mirai-native)|

但是呢，这些原生的可能用着很难受

也许你注意到了 mirai-js，但和本文将要介绍和使用的 Mirai-js 并不是同一个东西，虽然我有尝试过使用 mirai-js 但是操作繁琐且 API 不全，就没有深入了解了

除此之外呢，还有基于 Mirai HTTP 生态下的第三方项目，如下

语言和技术	维护者及项目地址

<table><thead><tr><th style="text-align:left;">语言和技术</th><th style="text-align:left;">维护者及项目地址</th></tr></thead><tbody><tr><td style="text-align:left;"><code>C#</code></td><td style="text-align:left;"><a href="https://github.com/Executor-Cheng/mirai-CSharp" target="_blank" rel="noopener noreferrer">Executor-Cheng/mirai-CSharp<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>C#</code></td><td style="text-align:left;"><a href="https://github.com/theGravityLab/ProjHyperai" target="_blank" rel="noopener noreferrer">Hyperai<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>C#</code></td><td style="text-align:left;"><a href="https://github.com/Coloryr/ColorMirai" target="_blank" rel="noopener noreferrer">Coloryr/ColorMirai<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>C#</code></td><td style="text-align:left;"><a href="https://github.com/AHpxChina/Mirai.Net" target="_blank" rel="noopener noreferrer">AhpxChina/Mirai.Net<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>C#</code></td><td style="text-align:left;"><a href="https://github.com/Cyl18/Chaldene" target="_blank" rel="noopener noreferrer">Cyl18/Chaldene<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>C#</code></td><td style="text-align:left;"><a href="https://github.com/Miyakowww/CocoaFramework2" target="_blank" rel="noopener noreferrer">Miyakowww/CocoaFramework2<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>C++</code></td><td style="text-align:left;"><a href="https://github.com/cyanray/mirai-cpp" target="_blank" rel="noopener noreferrer">cyanray/mirai-cpp<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>C++</code></td><td style="text-align:left;"><a href="https://github.com/Chlorie/miraipp-template" target="_blank" rel="noopener noreferrer">Chlorie/miraipp<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>GDScript</code></td><td style="text-align:left;"><a href="https://github.com/Xwdit/RainyBot-Core" target="_blank" rel="noopener noreferrer">Xwdit/RainyBot-Core<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>Go</code></td><td style="text-align:left;"><a href="https://github.com/Logiase/gomirai" target="_blank" rel="noopener noreferrer">Logiase/gomirai<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>JavaScript</code> / Node.js</td><td style="text-align:left;"><a href="https://github.com/RedBeanN/node-mirai" target="_blank" rel="noopener noreferrer">RedBeanN/node-mirai<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>JavaScript</code> / Node.js</td><td style="text-align:left;"><a href="https://github.com/drinkal/Mirai-js" target="_blank" rel="noopener noreferrer">drinkal/Mirai-js<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>JavaScript</code> / TypeScript</td><td style="text-align:left;"><a href="https://github.com/YunYouJun/mirai-ts" target="_blank" rel="noopener noreferrer">YunYouJun/mirai-ts<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>JavaScript</code> / TypeScript</td><td style="text-align:left;"><a href="https://github.com/nepsyn/miraipie" target="_blank" rel="noopener noreferrer">nepsyn/miraipie<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>Julia</code></td><td style="text-align:left;"><a href="https://github.com/melonedo/MiraiBots.jl" target="_blank" rel="noopener noreferrer">MiraiBots.jl<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>PHP</code></td><td style="text-align:left;"><a href="https://github.com/nkxingxh/miraiez" target="_blank" rel="noopener noreferrer">nkxingxh/miraiez<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>Python</code></td><td style="text-align:left;"><a href="https://github.com/st1020/alicebot" target="_blank" rel="noopener noreferrer">AliceBot<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>Python</code></td><td style="text-align:left;"><a href="https://github.com/GraiaProject/Ariadne" target="_blank" rel="noopener noreferrer">Ariadne<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>Python</code></td><td style="text-align:left;"><a href="https://github.com/GraiaProject/Avilla" target="_blank" rel="noopener noreferrer">Avilla<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>Python</code></td><td style="text-align:left;"><a href="https://github.com/easyMirais/easyMirai" target="_blank" rel="noopener noreferrer">easyMirai<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>Python</code></td><td style="text-align:left;"><a href="https://github.com/ArcletProject/Edoves" target="_blank" rel="noopener noreferrer">Edoves<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>Python</code></td><td style="text-align:left;"><a href="https://github.com/wyapx/Elaina" target="_blank" rel="noopener noreferrer">Elaina<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>Python</code></td><td style="text-align:left;"><a href="https://github.com/nonebot/nonebot2" target="_blank" rel="noopener noreferrer">NoneBot<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>Python</code></td><td style="text-align:left;"><a href="https://github.com/jerrita/saaya" target="_blank" rel="noopener noreferrer">jerrita/saaya<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>Python</code></td><td style="text-align:left;"><a href="https://github.com/YiriMiraiProject/YiriMirai" target="_blank" rel="noopener noreferrer">YiriMirai<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>Python</code></td><td style="text-align:left;"><a href="https://github.com/Excaive/miraicle" target="_blank" rel="noopener noreferrer">Excaive/miraicle<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>Ruby</code></td><td style="text-align:left;"><a href="https://github.com/Shimogawa/rubirai" target="_blank" rel="noopener noreferrer">Shimogawa/rubirai<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>Rust</code></td><td style="text-align:left;"><a href="https://github.com/HoshinoTented/mirai-rs" target="_blank" rel="noopener noreferrer">HoshinoTented/mirai-rs<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>易语言</code></td><td style="text-align:left;"><a href="https://github.com/only52607/e-mirai" target="_blank" rel="noopener noreferrer">only52607/e-mirai<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr><tr><td style="text-align:left;"><code>易语言</code></td><td style="text-align:left;"><a href="https://github.com/Novices666/mirai-epl" target="_blank" rel="noopener noreferrer">Novices666/mirai-epl<span><svg class="external-link-icon" xmlns="http://www.w3.org/2000/svg" aria-hidden="true" focusable="false" x="0px" y="0px" viewBox="0 0 100 100" width="15" height="15"><path fill="currentColor" d="M18.8,85.1h56l0,0c2.2,0,4-1.8,4-4v-32h-8v28h-48v-48h28v-8h-32l0,0c-2.2,0-4,1.8-4,4v56C14.8,83.3,16.6,85.1,18.8,85.1z"></path><polygon fill="currentColor" points="45.7,48.7 51.3,54.3 77.2,28.5 77.2,37.2 85.2,37.2 85.2,14.9 62.8,14.9 62.8,22.9 71.5,22.9"></polygon></svg><span class="external-link-icon-sr-only"></span></span></a></td></tr></tbody></table>

### Mirai 生态

Mirai 的生态发展的有点复杂了，就如同官方文档所说的「错综复杂」，这花了我很多时间去理清他们之间的关系，一下提两句，有助于之后的开发

#### mirai-core

> 是 Mirai 对 QQ 的具体协议实现，它承担具体且核心的工作。

这里放一张官方文档的图：

<img src="https://mermaid.ink/img/eyJjb2RlIjoiZmxvd2NoYXJ0IExSXG4gICAgY2xhc3NEZWYgY29yZWhpZ2hsaWdodCBmaWxsOiNmOTYsc3Ryb2tlOiMzMzMsc3Ryb2tlLXdpZHRoOjNweDtcbiAgICBzdWJncmFwaCBtaXJhaSBbXCJNaXJhaSDmoYbmnrZcIl1cbiAgICAgICAgbWlyYWljb3JlYXBpKG1pcmFpLWNvcmUtYXBpKTo6OmNvcmVoaWdobGlnaHRcbiAgICAgICAgbWlyYWljb3JlcXFhbmRyb2lkKFwibWlyYWktY29yZTxici8-KFFRQW5kcm9pZCDljY_orq4pXCIpXG4gICAgICAgIG1pcmFpY29yZXFxYW5kcm9pZCAtLT4gfOaPkOS-m-WNj-iurnxtaXJhaWNvcmVhcGlcbiAgICBlbmRcbiAgICBtaXJhaWludGVyZmFjZShcIuS9oOe8luWGmeeahDxici8-5py65Zmo5Lq656iL5bqPXCIpXG4gICAgbWlyYWljb3JlYXBpIC0tPiB85o-Q5L6b5Z-656GA5Yqf6IO9fG1pcmFpaW50ZXJmYWNlIiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifSwidXBkYXRlRWRpdG9yIjpmYWxzZX0">

核心与底层的东西，前期了解太多不利于快速上手应用，所以了解个大概，知道底层是这个 core 在跑。

#### mirai-console

> mirai-console 就是 Mirai 官方开发组编写的 QQ 机器人程序，它**在 Mirai 框架提供的基础功能的基础上进行了封装并进一步提供了更方便的开放接口**。

就是一个终端，官方提供了命令行界面，你拿它来登陆你的 QQ 机器人，并对其进行部分操作。

官方还讲其分了前端后端的概念，感觉有些不便于理解，暂且不提。

#### mirai-api-http

mirai-api-http 插件就是一个将 mirai-core-api 的所有功能封装为 http 服务的插件，同时也提供了 WebSocket 服务。

比较核心的一个组件了，基本上所有第三方基于 Mirai 的框架都需要这个组件。http 和 websocket 为你提供类似服务器一样的地址和端口，你使用第三方框架的时候只需要监听这个端口即可与 Mirai 进行交互。

#### mirai-native

如果你是 酷Q 用户，想在 Mirai 中使用 酷Q 插件，你可以使用 mirai-native 插件，它可以加载 CQP.dll 并兼容大部分酷Q 插件，但不支持 CPK 和解包的 DLL。

给原酷Q用户的一个迁移端口（蛮良心的），实际上溯洄大佬的 Dice! 应该也是从这个为起点的。

但是官方文档也指出，酷Q既然也停止服务，那么就不推荐使用

#### mirai-console-loader

mirai-console-loader 应运而生，它的工作就是简化 console 启动流程，一键帮你下载 jar 文件，自动更新，文件损坏检查…… 你能在手动启动时担心的问题 mirai-console-loader 都帮你想到了！

官方缩写 MCL，mirai-console 的一键启动器，类似对 mirai-console 的封装，简化操作的，当然，坑也不少。

虽说他是怕你不懂 JVM，怕你被劝退，但是这个 MCL 的有些操作同样有点劝退人的味道。

#### 关于 Mirai 生态的后话

发展生态有好处也有弊端，好处是使其多元化，体现开源的特色，坏处是，花样一多，你不得不考虑他们之间的同步问题，他们之间版本跟新是否跟得上会很大程度影响开发体验，或者说给新手埋下多少坑（没错我就是受害者）。然后就是，不太好做文档，这牵一发而动全身的感觉着实不太好。

### 关于 Mirai 社区和插件

论坛活跃度还是蛮高的，一些常见的问题可以通过论坛的搜索功能查找。

你可以在论坛中看到官方发的公告（目前，最近一次在 2021 年 5 月 19 日），参与讨论，提交 Bug 反馈，分享插件。

对于插件，论坛上给的插件基本都是编译成 jar 文件的，只需要放入 MCL 的 plugins 文件夹下，然后重新启动就能使用，比较类似酷Q，还是蛮方便的。

大佬们给了很多有趣的插件，详询论坛插件板块。

## 然后说 Mirai-js

> 运行在 Node.js、浏览器下，基于 mirai-api-http 的 QQ 机器人开发框架。

特点就是基于 node，快速上手，全文异步，涵盖基本一个 QQ 账号能做的所有基本操作，包括但不限于：

- 发送消息
- 戳一戳
- 发送图片
- @
- 发送语音消息
- 发送 XML 和 JSON

在群组中也具有一定的功能，包括但不限于：

- 禁言
- 踢人
- 退群
- 设置群配置：
    + 群名称
    + 群公告
    + 是否开启坦白说
    + 是否允许群员邀请
    + 是否开启自动审批入群
    + 是否允许匿名聊天
- 设置群精华消息

> 项目地址：[Drincann/Mirai-js](https://github.com/Drincann/Mirai-js)
>
> [文档，API](https://mirai-js-drincann.vercel.app/#/?id=mirai-js)

## 正片：开发一个基于 Mirai-js 的 QQ 机器人

1. 创建一个 QQ 小号

一般来说都不会让你用大号来做机器人，到时候要是有什么闪失号玩没了就哦豁了。

另外就是 tx 神奇的检测机制，你的 Bot 有时会发不出消息（实际上已经发了，但是被 tx 给屏蔽了），这时往往需要自己手动挂一段时间的小号，并且不知道要挂多久。

如果你喜欢，请美化你的小号，然他/她成为大家的吉祥物:joy:

2. 安装 MCL

官方提供了一键安装工具 MCL-Instller，找到最新版本，下载对应系统的版本到一个本地空文件夹，这个文件夹就是你的项目文件夹。

运行后，根据官网，如果你是新手，那么一路回车。

注：

可能会有不一步到位的情况，可能装完 java 他就停了，那么再运行一遍 
有可能会有网络不佳的情况，视情况上tizi
当文件夹中出现 mcl.cmd 文件时即安装完成，双击或 cmd 运行 mcl.cmd，第一次执行会自动安装依赖，最后出现 successfully 即完成。


这个时候就可以试试登陆你的小号了

```bash
$ login [qq号] [密码]
```

OK，登上了的话，那么应该没啥问题

3. 安装 mirai-api-http

官网推荐你使用 MCL 自动更细插件的安装方式：

$ ./mcl --update-package net.mamoe:mirai-api-http --channel stable --type plugin
但是呢，我不推荐，这里不得不说 Mirai 生态下的坑。

执行以上命令后，他会讲 mirai-api-http 的依赖给 MCL，在你下次执行 mcl.cmd 的时候会检测出来并安装，但是呢，就我目前的时间点，自动安装的 mirai-api-http 版本过低，然后直接报错：


我看不懂，但是我大受震撼。百度甚至告诉我是 kotlin 版本问题，论坛上给出修改 config.json 文件，关闭自动更新等等方法，我只能说我不中嘞。不知道你在操作的时候，他修补这个 bug 没有。

所以，**我推荐的方法：手动安装**：

- 前往项目仓库：mirai-pai-htttp，找到最新的 release，下载那个 jar 文件，把它放到你的项目文件夹下的 plugins 目录下，然后运行 mcl.cmd，搞定。

4. 修改 mirai-api-http 配置

来到 Mirai-js 文档，打开准备工作，他会让你线修改 mirai-api-http 的配置，打开 config\net.mamoe.mirai-api-http\setting.yml，修改如下：

```yaml
## 配置文件中的值，全为默认值

## 启用的 adapter, 内置有 http, ws, reverse-ws, webhook
adapters:
  - http
  - ws

## 是否开启认证流程, 若为 true 则建立连接时需要验证 verifyKey
## 建议公网连接时开启
enableVerify: true
verifyKey: yourVerifyKey

## 开启一些调式信息
debug: false

## 是否开启单 session 模式, 若为 true，则自动创建 session 绑定 console 中登录的 bot
## 开启后，接口中任何 sessionKey 不需要传递参数
## 若 console 中有多个 bot 登录，则行为未定义
## 确保 console 中只有一个 bot 登陆时启用
singleMode: false

## 历史消息的缓存大小
## 同时，也是 http adapter 的消息队列容量
cacheSize: 4096

## adapter 的单独配置，键名与 adapters 项配置相同
adapterSettings:
  ## 详情看 http adapter 使用说明 配置
  http:
    host: localhost
    port: 8080
    cors: [*]

  ## 详情看 websocket adapter 使用说明 配置
  ws:
    host: localhost
    port: 8080
    reservedSyncId: -1
```

这与 Mirai-js 文档给出的稍有不同，以下是文档中的：

```yaml
adapters: 
- http
- ws
debug: false
enableVerify: true
verifyKey: INITKEYpff86IGV
singleMode: false
cacheSize: 4096
adapterSettings: 
    http:
        ## http server 监听的本地地址
        ## 一般为 localhost 即可, 如果多网卡等情况，自定设置
        host: localhost

        ## http server 监听的端口
        ## 与 websocket server 可以重复, 由于协议与路径不同, 不会产生冲突
        port: 8080

        ## 配置跨域, 默认允许来自所有域名
        cors: [*]
    ws:
        ## websocket server 监听的本地地址
        ## 一般为 localhost 即可, 如果多网卡等情况，自定设置
        host: localhost

        ## websocket server 监听的端口
        ## 与 http server 可以重复, 由于协议与路径不同, 不会产生冲突
        port: 8080

        ## websocket 用于消息同步的字段为 syncId, 一般值为请求时的原值，用于同步一次请求与响应
        ## 对于由 websocket server 主动发出的通知, 固定使用一个 syncId, 默认为 ”-1“
        reservedSyncId: -1
```

这里你需要自己定义并记住 verifykey，然后记住 port，下面要用

5. 开始使用 Mirai-js

以上的准备工作都做完了，现在正式开始。

先把小号在 MCL 里登上。

然后随便找个文件夹，推荐是空的，取个好听的名字，打开 cmd，cd 到这个文件夹然后：

该项目上架了 npm，所以可以直接 install

```bash
$ npm install mirai-js
```

或者使用 yarn

```bash
$ yarn add mirai-js
```

以下是官网的一个例子：

```javascript
const { Bot, Message, Middleware } = require('mirai-js');

(async () => {
    try {
        const baseUrl = 'http://example.com:8080';
        const verifyKey = 'verifyKey';
        const qq = 1234567890;
        const password = 'password';
        const bot = new Bot();

        // 在 mirai - console 登录一个账号
        await Bot.sendCommand({
            baseUrl,
            verifyKey,
            // 指令名
            command: '/login',
            // 指令参数列表，这条指令等价于 /login 1019933576 password
            args: [qq, password],
        });

        // 创建一个会话
        await bot.open({
            // mirai-api-http 的服务端地址，
            baseUrl,
            // 要绑定的 qq，须确保该用户已在 mirai-console 登录
            qq,
            // verifyKey 用于验证连接者的身份，在插件配置文件中设置
            verifyKey,
        });


        // 监听好友消息事件
        bot.on('FriendMessage', async ({
            messageChain,
            sender: {
                id: fromQQ,
                nickname: fromQQNickName,
                remark
            }
        }) => {
            console.log({ fromQQ, fromQQNickName, remark });
            const { id: messageId } = messageChain[0];

            bot.sendMessage({
                friend: fromQQ,
                quote: messageId,
                message: new Message().addText('hello world!'),
            });
        });

        // 监听群消息事件
        bot.on('GroupMessage', async ({
            messageChain,
            sender: {
                id: fromQQ,
                memberName: fromNickname,
                permission: fromQQPermission,
                group: {
                    id: fromGroup,
                    name: groupName,
                    permission: botPermission
                }
            }
        }) => {
            console.log({ fromQQ, fromNickname, fromQQPermission });
            console.log({ fromGroup, groupName, botPermission });

            // 复读机 ;)
            const { id: messageId } = messageChain[0];

            bot.sendMessage({
                group: fromGroup,
                quote: messageId,
                messageChain
            });

            // 你可以像这样来判断群成员的权限
            switch (fromQQPermission) {
            case Bot.groupPermission.OWNER:
                // 群主
                break;
            case Bot.groupPermission.ADMINISTRATOR:
                // 管理员
                break;
            case Bot.groupPermission.MEMBER:
                // 普通群成员
                break;
            }
        });


        // 使用中间件
        // 过滤分类 message
        bot.on('FriendMessage', new Middleware()
            .messageProcessor(['Plain', 'Image'])
            .textProcessor().done(({
                // 第一个中间件，分类过的 messageChain
                classified,
                // 第二个中间件，文本部分
                text,

                messageChain,
                sender: {
                    id: fromQQ,
                    nickname: fromQQNickName,
                    remark
                }
            }) => {
                console.log({ fromQQ, fromQQNickName, remark, messageChain, classified, text });

                bot.sendMessage({
                    friend: fromQQ,
                    message: new Message().addText(text),
                });
            }));

        // 自动重新登陆
        bot.on('BotOfflineEventForce',
            new Middleware()
                .autoReLogin({ bot, baseUrl, verifyKey, password })
                .done()
        );
    } catch (err) {
        console.log(err);
    }
})();
```

然后保存运行（例如以上例子文件名为 test.js）

```bash
$ node test.js
```

这样一个复读姬就产生了，你可以与你的小号对话，他会返回你的话。或者你可以把他拉进群聊，让群复读机+1。

## 后话

最后的开发工作就是查 API 了，也没啥好说的，就是一点 js async/await 的知识，开发还是蛮快的，如果你有服务器的话，把 MCL 和你的文件一起丢服务器上跑起来就可以24小时了。

## 参考：

> [Drincann/Mirai-js: 运行在 Node.js、浏览器下，基于 mirai-api-http 的 QQ 机器人开发框架。 (github.com)](https://github.com/Drincann/Mirai-js)
> 
> [Dice! 论坛 (kokona.tech)](https://forum.kokona.tech/)
> 
> [主页 | MiraiForum (mamoe.net)](https://mirai.mamoe.net/)
> 
> [Mirai | mirai (mamoe.net)](https://docs.mirai.mamoe.net/)
> 
> [Mirai-js 简单的开源 Mirai QQ 机器人框架](https://mirai-js-drincann.vercel.app/#/?id=mirai-js)

