---
title: 我的 Vim 配置
tags: [Linux, Vim]
categories: [应用系统]
index_img: /img/vim.png
date: 2021-11-12 10:00:00
---

Vim 作为一款高自由度的文本编辑器，广受众大佬的喜爱，然而高自由度另一方面带来的繁琐纷杂的配置劝退了 80% 的尝试者（像极了 DND 传教时玩家被 200 多页的玩家手册劝退）。但是呢，当你配置到位了，熟悉了 Vim 的快捷操作，它会回报你，它的开发效率可能会超过任何一个你使用过的 IDE。

<!--more-->

## 做一些说明
### 使用 Vim 的缘由
其实我一向是 VSCode 的拥护者，VSCode 的确给了我很好的编程体验，但是呢，某些时候会让我感到难受。在写 Go 的时候，会去装巨硬官方提供的扩展:

<a href="https://smms.app/image/o59OnK8ipG6NWPF" target="_blank"><img src="https://s2.loli.net/2022/12/30/o59OnK8ipG6NWPF.png" /></a>

但是，它会带来各种各样的问题，先是 gotools 安装失败，然后找个各种办法去解决，然后，最新的扩展跟新了改为 gopls（Go Language Server Protocol） 来处理 go，它要求你每个 module 需要在一个 VSCode 的 workplace 下，不然就会报以下的一个错：

```bash
gopls requires a module at the root of your workspace.
You can work with multiple modules by opening each one as a workspace folder.
Improvements to this workflow will be coming soon, and you can learn more here:
https://github.com/golang/tools/blob/master/gopls/doc/workspace.md.
```

很难受，网上最多的方法就是在 setting.json 中设置：

```json
"gopls": {
    "experimentalWorkspaceModule": true
}
```

但是我设置之后会导致鼠标放置提示消失，总之就是非常难受。

然后呢，想继续开发一下自己使用 Vim 的能力，于是就试试专门用 Vim 来做 Go 的 IDE 来试试。

### 关于配置
**本篇文章全部配置是我个人使用的配置，并没有涵盖所有的配置**

我的配置已经上传到 [Github](https://github.com/Akashiya-Chime/MyArchConf)，不过没什么注释，下面我会进行比较详细的注解，尽量保证没一行配置都能知道干了什么

每个代码段的第一行注释注明了所修改的文件以及文件在我的（ArchLinux）系统中的绝对位置，可以作为参考（其实可能也就只有 `.vimrc` （vim run commands，也有说 run control 的）文件需要修改）

Windows 的用户，可以在 Vim 中使用 `:version` 查看系统或者用户 `.vimrc` 文件位置

### 基础操作
在写配置之前，需要一些基础的 Vim 操作知识

- 模式：Vim 具有 NORMAL、INSERT、VISUAL 三个模式

    + NORMAL：命令模式，在这个模式下使用命令

    + INSERT：输入模式，这个模式下打字

    + VISUAL：可视模式，这个模式下进行文本操作，比如复制、剪切等

- 基础命令
    + `:w` 写入，`:q` 退出，组合起来就是喜闻乐见的常用的保存并退出 `:wq`
    + `h` 左，`l` 右，`j` 上，`k` 下
    + `w` word，移动到下一个单词开头
    + `b` before，移动到上一个单词开头
    + `e` end，移动到下一个单词结尾
    + `a` append，在光标后进入 `INSERT` 模式，`A` 在光标所在行的末尾进入 `INSERT` 模式
    + `i` insert，在光标处进入 `INSERT` 模式，`I` 在光标所在行的开头进入 `INSERT` 模式
    + `o` 在光标下插入一行进入 `INSERT` 模式
    + `yy` 复制光标所在行
    + `dd` 剪切光标所在行
    + `p` 粘贴
    + `gg` 跳到第一行
    + `G` 跳到最后一行
    + `u` undo，撤销
    + `Ctrl+r` redo，把撤销的步骤撤销回来
    + `v` 进入 `VISUAL` 模式
    + `<ESC>` 退出当前的 `INSERT` 或 `VISUAL` 模式，进入 `NORMAL` 模式
    + `>>` 增加一级缩进，`<<` 取消一级缩进，`==` 取消全部缩进

- 查询
    + / 查询
    + 回车后，使用 n next 和 l last 来上下跳转筛选项目

## 基础配置

```vim
" ~/.vimrc
" 打开高亮
syntax on
" 打开行号
set number
" 光标所在行高亮
set cursorline
" 在底部显示键入的指令
set showcmd
" 命令模式用 Tab 自动补全
set wildmenu
" 高亮搜索匹配结果
set hlsearch
" 去掉高亮（感觉有点玄学）
exec "nohlsearch"
" 边输入边高亮
set incsearch
" 忽略大小写
set ignorecase
" 只能大小写（其实就是只对第一个字母大写的搜索词大小写敏感）
set smartcase
" 自动缩进，回车后下一行的缩进与上一行的缩进保持一致
set autoindent
" 智能缩进
set smartindent
" 一个 Tab 缩进 4 个字符
set tabstop=4
" 增加或取消一级缩进时的字符数，建议与缩进保持一致
set shiftwidth=4
" 由于 Tab 键在不同的编辑器缩进不一致，该设置自动将 Tab 转为空格
set expandtab
" 智能缩进，根据文件其他地方的缩进来确定一个 Tab 多少缩进
set smarttab
" Tab 转换为 2 个空格
set softtabstop=2
" 支持鼠标（虽然但是，“我们是为了解放鼠标才来用 Vim 的！”）
set mouse=a
" 状态栏现实光标当前位置（哪行哪列）
set ruler
" 设置 utf-8 编码
set encoding=UTF-8
" 是否显示状态栏。0 表示不显示，1 表示只在多窗口时显示，2 表示显示
set laststatus=2
```

## 进阶配置
这个地方的配置是更加个性化的配置，我会讲解部分个性化配置的方法，并且给出我的部分个性化配置以做参考

首先得搞清楚一些缩写或者字符串所代表的含义

|标识符号|	代表含义|
|---|---|
|`<Esc>`代表| Escape 键|
|`<CR>`|	代表 Enter 键|
|`<C-Esc>`|	代表 Ctrl-Esc|
|`<S-F1>`|	表示 Shift-F1|
|`<D>`|	代表 Command 键，对于 Mac 用户，可以使用|
|`<M-key>` 或 `<A-key>`|	代表 Alt 键|

- `<leader>` leader 键，默认是反斜杠 \，很多人喜欢改成空格

- `<C-r>` ：Ctrl + r

- `<CR>` 回车，或者叫 Enter

`map` 是 Vim 配置中的处理映射的关键字，在它的前面可以加一些不同的前缀来体现一些特殊含义，如下表：

|前缀|	含义|
|---|---|
|nore|	非递归|
|n|	NORMAL 模式生效|
|v|	VISUAL 模式生效|
|i|	INSERT 模式生效|
|c|	命令行模式生效|
|un|	后面跟组合键，表示删除这个映射|
|clear|	清除相关模式下所有映射|

```vim
" ~/.vimrc
" 设置 leader 键，默认反斜杠 \
let mapleader=" " " 或者转义一下，\<space>
```

通常我们在对 `.vimrc` 文件进行修改后，需要 `:wq` 保存退出再重新进到 Vim 中才能看到我们的修改生效，但其实可以通过同 Linux 的 source 一样的方式来重新读取配置文件来快速“刷新”，例如以下配置：

```vim
" ~/.vimrc
" 使用 R 来输入命令 :source $MYVIMRC，并在最后回车执行
map R :source $MYVIMRC<CR>
```

我们可以看到 `map` 的用法很简单，就是用后面接的第一个字符来表示后面的字符或命令。

这里再推荐一些我的配置：

```vim
" ~/.vimrc
" 使用 <leader>w 来完成保存
nmap <leader>w :w<CR>
" 使用 <leader>q 来完成退出
nmap <leader>q :q<CR>

" 使用 J 来实现光标向下跳转 5 行
noremap J 5j
" 使用 K 来实现光标向上跳转 5 行
noremap K 5k
" 使用 H 来实现光标到行首
noremap H ^
" 使用 L 来实现光标到行末
noremap L $
" 使用 <leader> 回车来关闭搜索时留下的高亮（这个要靠谱点）
noremap <leader><CR> :nohlsearch<CR>
```

以上，我关于原生的配置就了解的差不多了，这些都比较的简单，你可以查询 Vim 官方的相关文档找到更多更详尽的配置条目和更高级的配置方法。

## 插件
Vim 的插件生态也是 Vim 兴盛的必不可少也是情理之中的特点，插件的存在让我们不用重复地造轮子，又因其高自由度和开源，你甚至可以在别人的轮子上修改出自己舒适的形状，他就像 VSCode 的扩展一样让人感到亲切。

### 插件管理器
安装 Vim 插件的方式很多，最原生的方式就是将插件的仓库 clone 下来，然后将插件文件丢到 .vim 文件夹下。但是呢，这样不够优雅。为了方便日后的插件管理，我们应当想到并使用插件管理工具

Vim 的插件管理器数不胜数，你甚至可以自己写一个，比较流行的，比如 Vundle，很多插件推荐或者教程都会使用 Vundle 的插件安装方式

这里介绍另一个，也是我使用的，叫 [vim-plug](https://github.com/junegunn/vim-plug)，简洁，易用

> vim-plug: [GitHub - junegunn/vim-plug: Minimalist Vim Plugin Manager](https://github.com/junegunn/vim-plug)

- **安装 vim-plug**：

    GitHub 上给出了很多自动化，不同操作系统的命令行代码，比如：
    ```shell
    $ curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
        https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
    ```
    实际上操作就是将该仓库下的 plug.vim 文件下载下来放到 `~/.vim/autoload/` 目录下，如果你用 curl 用地不爽，你完全可以手动操作（[plug.vim 文件](https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim)）

- **使用 vim-plug**：

    我们回到 ~/.vimrc 文件，使用 vim-plug 很简单，我们需要将插件仓库包裹在 plug 代码块间，如下：（以下的就是我已经安装的插件，后文我会介绍）
    ```vim
    " ~/.vimrc
    " ===
    " === vim-plug
    " ===
    call plug#begin('~/.vim/plugged')

    Plug 'vim-airline/vim-airline'
    Plug 'vim-airline/vim-airline-themes'
    Plug 'connorholyday/vim-snazzy'
    Plug 'preservim/nerdtree'
    Plug 'neoclide/coc.nvim', {'branch': 'release'}
    Plug 'fatih/vim-go', { 'do': ':GoUpdateBinaries' }
    Plug 'dracula/vim', { 'as': 'dracula' }
    Plug 'Yggdroot/indentLine'
    Plug 'mhinz/vim-startify'
    Plug 'jiangmiao/auto-pairs'
    Plug 'preservim/nerdcommenter'
    Plug 'ryanoasis/vim-devicons'
    Plug 'tiagofumo/vim-nerdtree-syntax-highlight'
    Plug 'Xuyuanp/nerdtree-git-plugin'

    call plug#end()
    ```
    
    然后我们用用前面配置的方法，`<leader>w` 保存，然后 `R` “刷新”一下

    之后我们使用命令 `:PlugInstall` 来安装插件（速度慢问题见下一点）

- **解决速度慢问题**：

    首先得清楚为什么会慢，那当然是因为它是从 Github 下载的，会遇到墙之巨人，怎么解决呢，可以考虑使用镜像源，比如 fastgit

    可以参考一下文章：

    > [VIM-Plug安装插件时，频繁更新失败，或报端口443被拒绝等_htx1020的博客-CSDN博客](https://blog.csdn.net/htx1020/article/details/114364510)

    简单来说就是更改刚下下载下来的 `~/.vim/autoload/plug.vim` 中的
    ```vim
    let fmt = get(g:, 'plug_url_format', 'https://git::@github.com/%s.git')
    ```
    改为：
    ```vim
    let fmt = get(g:, 'plug_url_format', 'https://git::@hub.fastgit.org/%s.git')
    ```
    将：
    ```vim
    \ '^https://git::@github\.com', 'https://github.com', '')
    ```
    改为：
    ```vim
    \ '^https://git::@hub.fastgit\.org', 'https://hub.fastgit.org', '')
    ```
- **vim-plug 的其他操作**：

    + `:PlugInstall`：安装插件

    + `:PlugUpdate`：更新插件

    + `:PlugClean`：删除不在配置列表的插件

    + `:PlugUpgrade`：更新 vim-plug 自身

    + `:PlugStatus`：检查插件状态

    + `:PlugDiff`：用来插件回滚（版本回退）

- vim-plug 还有一些全局的配置，可以参考 [Github](https://github.com/junegunn/vim-plug) 的仓库，这里不赘述

那我们就来介绍一些好用的插件

### vim-airline
> [vim-airline]([GitHub - vim-airline/vim-airline: lean & mean status/tabline for vim that's light as air](https://github.com/vim-airline/vim-airline))

Vim 最下方的一个横条，分了 A、B、C、X、Y、Z 几个区，可以显示当前模式，配合 git 显示当前分支等等。总之就是非常好看，如图：

<a href="https://smms.app/image/EAbPlIvaoZWep8h" target="_blank"><img src="https://s2.loli.net/2022/12/30/EAbPlIvaoZWep8h.png" /></a>

可以配合使用 airline-themes 来使用不同主题

> [vim-airline-themes](https://github.com/vim-airline/vim-airline-themes#vim-airline-themes--)

我有如下配置：
```vim
" ~/.vimrc
" ===
" === vim-airline
" ===
set laststatus=2  " 永远显示状态栏
let g:airline_powerline_fonts = 1  " 支持 powerline 字体
let g:airline#extensions#tabline#enabled = 1 " 显示窗口tab和buffer
let g:airline_theme='dracula'
if !exists('g:airline_symbols')
let g:airline_symbols = {}
endif
let g:airline_left_sep = '▶'
let g:airline_left_alt_sep = '❯'
let g:airline_right_sep = '◀'
let g:airline_right_alt_sep = '❮'
let g:airline_symbols.linenr = '¶'
```

### Dracula
> [dracula/vim](https://github.com/dracula/vim)

Dracula 主题的 Vim 版，配色还行偏粉紫，如图：

<a href="https://smms.app/image/14geBjAnzNLusZW" target="_blank"><img src="https://s2.loli.net/2022/12/30/14geBjAnzNLusZW.png" /></a>

在配置文件 `~/.vimrc` 中添加
```vim
" ~/.vimrc
color dracula
```
来设置为 dracula

### NERDTree
> [preservim/nerdtree](https://github.com/preservim/nerdtree)

文件树，配置和指令可参考 Github 的仓库，也可以在 nerdtree 下输入 ? 来取得帮助

配合一些别的插件可以让 nerdtree 更好看一点，如：

> [ryanoasis/vim-devicons](https://github.com/ryanoasis/vim-devicons)
>
> [tiagofumo/vim-derdtree-syntax-highlight](https://github.com/tiagofumo/vim-derdtree-syntax-highlight)
>
> [Xuyuanp/nerdtree-git-plugin](https://github.com/Xuyuanp/nerdtree-git-plugin)

第一个是文件和文件夹的 icon，第二个是高亮，第三个是 git 插件

我有以下配置：
```vim
" ~/.vimrc
" ===
" === nerdtree
" ===
nnoremap <C-n> :NERDTree<CR>
"Show hide file.
let g:NERDTreeHidden=0
"Delete help information at the top
let NERDTreeMinimalUI=1

" ===
" === vim-devicons
" ===
"Can be enabled or disabled
let g:webdevicons_enable_nerdtree = 1
"whther or not to show the nerdtree brackets around flags
let g:webdevicons_conceal_nerdtree_brackets = 1
"adding to vim-airline's tabline
let g:webdevicons_enable_airline_tabline = 1
"adding to vim-airline's statusline
let g:webdevicons_enable_airline_statusline = 1

" ===
" === vim-nerdtree-syntax-highlight
" ===
"Highlight full name (not only icons). You need to add this if you don't have vim-devicons and want highlight.
let g:NERDTreeFileExtensionHighlightFullName = 1
let g:NERDTreeExactMatchHighlightFullName = 1
let g:NERDTreePatternMatchHighlightFullName = 1
"Highlight full name (not only icons). You need to add this if you don't have vim-devicons and want highlight.
let g:NERDTreeHighlightFolders = 1
"highlights the folder name
let g:NERDTreeHighlightFoldersFullName = 1
"you can add these colors to your .vimrc to help customizing
let s:brown = "905532"
let s:aqua =  "3AFFDB"
let s:blue = "689FB6"
let s:darkBlue = "44788E"
let s:purple = "834F79"
let s:lightPurple = "834F79"
let s:red = "AE403F"
let s:beige = "F5C06F"
let s:yellow = "F09F17"
let s:orange = "D4843E"
let s:darkOrange = "F16529"
let s:pink = "CB6F6F"
let s:salmon = "EE6E73"
let s:green = "8FAA54"
let s:Turquoise = "40E0D0"
let s:lightGreen = "31B53E"
let s:white = "FFFFFF"
let s:rspec_red = "FE405F"
let s:git_orange = "F54D27"
let s:gray = "808A87"

" ===
" === nerdtree-git-plugin
" ===
let g:NERDTreeGitStatusUseNerdFonts = 1
let g:NERDTreeGitStatusShowIgnored = 1
let g:NERDTreeGitStatusIndicatorMapCustom = {
    \ "Modified"  : "✹",
    \ "Staged"    : "✚",
    \ "Untracked" : "✭",
    \ "Renamed"   : "➜",
    \ "Unmerged"  : "═",
    \ "Deleted"   : "✖",
    \ "Dirty"     : "✗",
    \ "Clean"     : "✔︎",
    \ 'Ignored'   : '☒',
    \ "Unknown"   : "?"
    \ }
```

配置玩后会有以下效果：

<a href="https://smms.app/image/dhcUkF6HJpSuzqW" target="_blank"><img src="https://s2.loli.net/2022/12/30/dhcUkF6HJpSuzqW.png" /></a>

- 注：你也许以后想装一个叫 vim-rainbow 的插件，这是一个彩色标注括号的插件，但它与 vim-devicon 不兼容，会导致文件夹被一对放括号包住，很难受。

### indentLine
> [Yggdroot/indentLine](https://github.com/Yggdroot/indentLine)

缩进线插件，但似乎对 Go 的支持不是很好，效果如图：

<a href="https://smms.app/image/5Zap9Kz6ILbseWu" target="_blank"><img src="https://s2.loli.net/2022/12/30/5Zap9Kz6ILbseWu.png" /></a>

### vim-startify
> [mhinz/vim-startify](https://github.com/mhinz/vim-startify)

start screen，开始界面，如图：

<a href="https://smms.app/image/16BE2Y4imA7baOo" target="_blank"><img src="https://s2.loli.net/2022/12/30/16BE2Y4imA7baOo.png" /></a>

### auto-pairs
> [jiangmiao/auto-pairs](https://github.com/jiangmiao/auto-pairs)

括号自动补全，简单，但是好用，而且智能

### NERDCommenter
> [preservim/nerdcommenter](https://github.com/preservim/nerdcommenter)

注释插件，有常用操作：
- `<leader>cc` 注释当前行和选中行
- `<leader>cn` 没有发现和\cc有区别
- `<leader>c<space>` 如果被选区域有部分被注释，则对被选区域执行取消注释操作，其它情况执行反转注释操作
- `<leader>cm` 对被选区域用一对注释符进行注释，前面的注释对每一行都会添加注释
- `<leader>ci` 执行反转注释操作，选中区域注释部分取消注释，非注释部分添加注释
- `<leader>cs` 添加性感的注释，代码开头介绍部分通常使用该注释
- `<leader>cy` 添加注释，并复制被添加注释的部分
- `<leader>c$` 注释当前光标到改行结尾的内容
- `<leader>cA` 跳转到该行结尾添加注释，并进入编辑模式
- `<leader>ca` 转换注释的方式，比如：/**/和//
- `<leader>cl` \cb 左对齐和左右对其，左右对其主要针对/**/
- `<leader>cu` 取消注释

我有如下配置：
```vim
" ~/.vimrc
" ===
" === nerdcommenter
" ===
" Create default mappings
let g:NERDCreateDefaultMappings = 1
" Add spaces after comment delimiters by default
let g:NERDSpaceDelims = 1
" Use compact syntax for prettified multi-line comments
let g:NERDCompactSexyComs = 1
" Align line-wise comment delimiters flush left instead of following code indentation
let g:NERDDefaultAlign = 'left'
" Set a language to use its alternate delimiters by default
let g:NERDAltDelims_java = 1
" Add your own custom formats or override the defaults
let g:NERDCustomDelimiters = { 'c': { 'left': '/**','right': '*/' } }
" Allow commenting and inverting empty lines (useful when commenting a region)
let g:NERDCommentEmptyLines = 1
" Enable trimming of trailing whitespace when uncommenting
let g:NERDTrimTrailingWhitespace = 1
" Enable NERDCommenterToggle to check all selected lines is commented or not 
let g:NERDToggleCheckAllLines = 1
```

### coc.nvim

> [neoclide/coc.nvim](https://github.com/neoclide/coc.nvim)
>
> Make your Vim/Neovim as smart as VSCode. (Conquer of Completion)

最后放这里压轴，毕竟 coc 太强了（当然，这里不是 Call of Cthulhu）

coc 可以为我们带来什么呢，插件下的插件，你可以安装很多 coc 的插件来达到 VSCode 那样的体验，它提供了各种语言的 LSP（Language Server Protocol），让你在写不同语言时能够有良好的代码补全体验。

也许，你得去看看它的 GitHub 仓库，进行更个性化的配置

我的配置有：
```vim
" ~/.vimrc
" ===
" === coc.nvim
" ===
nnoremap tt :CocCommand explorer<CR>

let g:coc_global_extensions = ['coc-json', 'coc-vimlsp', 'coc-go']

set encoding=utf-8
set updatetime=100
set shortmess+=c

nmap <silent> [g <Plug>(coc-diagnostic-prev)
nmap <silent> ]g <Plug>(coc-diagnostic-next)

nmap <silent> <F12> <Plug>(coc-definition)
nmap <silent> gy <Plug>(coc-type-definition)
nmap <silent> gi <Plug>(coc-implementation)
nmap <silent> gr <Plug>(coc-references)

xmap <leader>f  <Plug>(coc-format-selected)
nmap <leader>f  <Plug>(coc-format-selected)

autocmd CursorHold * silent call CocActionAsync('highlight')

if has("nvim-0.5.0") || has("patch-8.1.1564")
  set signcolumn=number
else
  set signcolumn=yes
endif

inoremap <silent><expr> <TAB>
      \ pumvisible() ? "\<C-n>" :
      \ <SID>check_back_space() ? "\<TAB>" :
      \ coc#refresh()
inoremap <expr><S-TAB> pumvisible() ? "\<C-p>" : "\<C-h>"

function! s:check_back_space() abort
  let col = col('.') - 1
  return !col || getline('.')[col - 1]  =~# '\s'
endfunction
```

## 参考
追随大佬的步伐，这里推荐一 up 主，可以说我的 vim 启蒙是从他那里来的：

[@TheCW](https://space.bilibili.com/13081489)

- 你可以从这俩视频里看到他的 Vim 玩得多溜：

    + [【硬货】新时代最流行的编程语言？10分钟学会Golang基础](https://www.bilibili.com/video/BV1AJ411D7j3)

    + [用多线程给代码提速800% —— Golang高并发教程+实战](https://www.bilibili.com/video/BV1qT4y1c77u)

- 他的 Vim 入门教学：[上古神器Vim：从恶言相向到爱不释手 - 终极Vim教程01 - 带你配置属于你自己的最强IDE](https://www.bilibili.com/video/BV164411P7tw/)

- 他的 coc 讲解：[【硬货】让你的vim像vscode一样强大 —— coc.nvim终极指南](https://www.bilibili.com/video/BV1Ka4y1E7AM)