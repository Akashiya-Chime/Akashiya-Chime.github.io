---
title: Webpack打包基础
tags: [Webpack]
categories: [编程开发]
index_img: /img/webpack.jpg
date: 2021-02-18 10:00:00
---

之前为了学习 Vue2 而去学了点 webpack 的基础，然而现在尤大发布 vue3 之后自己整了一个 vite，那这不得不去再学 vite

文章放 CSDN 上了：

> https://blog.csdn.net/Akashiyachime/article/details/106841056

<!--more-->

- 前端资源构建工具，静态模块打包器

- 坑：
    如果你webpack和webpack-cli是局部安装的，想要使用webpack命令必须进入node_modules/.bin/webpack才能执行webpack命令，.bin目录包含的是一系列可以执行的命令，但是如果你是全局安装的webpack-cli，就不需要进入bin目录，webpack就能够寻找到它的命令路径了，以上是我的个人总结
    （所以说啥本地安装啊，还是安全局的吧。。。）

## 核心概念

|Entry|	入口(Entry)指示Webpack以哪个文件为入口起点开始打包，分析构建内部依赖图|
|-----|-----|
|Output|输出(Output)指示Webpack打包后的资源bundle输出到哪里去，以及如何命名|
|Loader|Loader让Webpack能够去处理哪些非JavaScript文件(Webpack自身只理解JavaScript)|
|Plugins|插件(Plugins)可以用于执行范围更广的任务。插件范围包括，从打包优化和压缩，一直到重新定义环境中的变量等|
|Mode|模式(Mode)指示Webpack使用相应的模式的配置|

## 流程

- index.js： Webpack 入口起点文件

1. 运行指令：
    开发环境：webpack ./src/index.js -o ./build/built.js --mode=development
    webpack 会以 ./src/index.js 为入口文件开始打包，打包后输出到 .build/built.js
    整体打包环境是 开发环境
    生产环境：webpack ./src/index.js -o ./build/built.js --mode=production

2. 结论：
（1）webpack 能处理 js/json 资源，不能处理 css/img 等资源
（2）生产环境和开发环境将 ES6 模块化编译成浏览器能识别的模块化
（3）生产环境比开发环境多一个压缩 js 代码

## 打包样式资源

- src 同级目录下创建 webpack.config.js 文件，该文件是 webpack 的配置文件
    作用：指示 webpack 工作（运行 webpack 指令时，会加载里面的配置）

    + 所有构建工具都是基于 node.js 平台运行，模块化默认采用 commonjs

```javascript
// resolve 用来拼接绝对路径的方法
const { resolve } = require('path')

module.exports = {
    // webpake 配置
    // 入口起点
    entry: './src/index.js',
    // 输出
    output: {
        // 输出文件名
        filename: 'built.js',
        // 输出路径
        // __dirname 是 node.js 的变量，代表当前文件的目录绝对路径
        path: resolve(__dirname, 'build')
    },
    // loader 的配置
    module: {
        rules: [
            // 详细的 loader 配置
            // 不同文件必须配置不同的 loader 处理
            {
                // 匹配哪些文件
                test: /\.css$/,
                // 使用哪些 loader 进行处理
                // 当要使用多个 loader 时，需用 use: []
                use: [
                    // use 数组中 loader 执行顺序：从后到前，依次执行
                    // 创建 style 标签，将 js 中的样式资源插入进去，添加到<header>中生效
                    'style-loader',  //后执行
                    // 将 css 文件变成 commonjs 模块加载 js 中，里面内容是样式字符串
                    'css-loader'  //先执行
                ]
            }
        ]
    },
    // plugins 的配置
    plugins: [
        // 详细的 plugins 配置
    ],
    // 模式
    mode: 'development'  // 开发模式
    // mode: 'production'  //生产模式
}
```

## 打包html

- 需要一个 plugin：html-webpack-plugin

```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
    plugins: [
        // 默认创建空的 HTML，自动引入打包输出的所有资源（JS/CSS）
        // 需要有结构的 HTML
        new HtmlWebpackPlugin({
            // 复制 './src/index.html' 文件，并自动引入打包输出的所有资源（JS/CSS）
            template: './src/index.html'
        })
    ]
}
```

## 打包图片资源
- 需要一个 loader：

```javascript
module.exports = {
    module: {
        rules: [
            {
                // 问题：默认处理不了 html 中引入图片（可处理样式中的图片）
            	test: /\.(jpg|png|gif)$/,
            	// 当只有一个 loader 时，可直接loader:
            	loader: 'url-loader'
            	option: {
            		// 图片大小小于 8kb ，就会被 base64 处理（一般 8~12kb）
            		// 优点：减少请求数量（减轻服务器压力）
            		// 缺点：图片体积会更大（文件请求速度更慢）
            		limit: 8 * 1024,  // 8kb
                	// 问题：因为 url-loader 默认使用 ES6 模块化解析
                	// 而 html-loader 引入图片是 commonjs
                	// 解析时会出问题：[object Module]
                	// 解决：关闭 url-loader 的 ES6 模块化，使用 commonjs解析
                	esModule: false,
                	// 给图片进行重命名
                	// [hash:10] 取图片的 hash 前10位
                	// [ext] 取文件原来的扩展名
                	name: '[hash:10].[ext]'
            	}
            },
            {
            	test: /\.html$/,
            	// 处理 html 文件的图片（引入 img，从而能被 url-loader 处理）
            	loader: 'html-loader'
            }
        ]
    }
}

// 最终图片的名称是一个 hash 值
```

## 打包其他资源

- 一些不需要进行压缩等处理的文件

```javascript
module.exports = {
    module: {
        rules: [
            // 打包其他资源（除了 html/js/css 资源以外的资源）
            {
                // 排除
                exclude: /\.html|js|css$/,
                loader: 'file-loader'
            }
        ]
    }
}
// 也是 hash 值（也可以用 options 处理一下）
```