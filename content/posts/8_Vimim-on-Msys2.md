---
title: 8. Vimim on Msys2
date: 2017-06-01 08:42:34
tags:
---

### 安装VIMIM(gvim己带输入法自动切换，vim有插件切换）

先用插件字装工具，安装vimim

``` bash
Plug 'vim-scripts/VimIm'
```

``` bash
:PlugInstall
```

再自己整理一个五笔98的码表，先码后字地一个个排好，我是从ibus里的五笔98码表里
提取出来的，用vim整理一下格式就可以用了。不过文件名一定要vimim.xxxx.txt这种格式

``` bash
gi	#进入中文输入模式

Ctrl+_	#切换中英

Ctrl+^	#切换输入法
```
最后还是没法切换中英文标点，但是我发现按Alt是可以输入英文标点，至少写这编Markdown
时没有什么大问题。

我了解了一下小狼毫的后端，其实是有可能在vimim的基础上加入支持librime的输入法神器
不过得两方面都得研究清楚，得花时间啊。。。。。。
