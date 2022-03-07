---
title: 3. YouCompleteMe on Msys2
date: 2017-06-04 09:44:08
tags:
---

### 安装MSYS2

先安装MSYS2，然后更换软件源地址：
[MSYS2国内源](https://gist.github.com/elvisw/cc00088e9c8fd1c83aca)
不过文件里的地址过时了，下面有个回复说了新的地址，不过要手动输入。
替换完成，更新一下Msys2的软件

``` bash
pacman -Syu
```

### 安装依赖软件

``` bash
$pacman -S mingw-w64-i686-gcc
$pacman -S mingw-w64-i686-cmake
$pacman -S mingw-w64-i686-llvm
$pacman -S mingw-w64-i686-python2
$pacman -S mingw-w64-i686-make
$pacman -S git
```

### 下载YouCompleteMe

可以用vim的插件工具安装，也可以用git手动下载到相应文件夹。github在国内下载可能会
很慢，只有50kB/s，可以参考git代理的方法设置一个代理，可以提速。同时还要更新子模块。

``` bash
$ git clone https://github.com/Valloric/YouCompleteMe
$ cd YouCompleteMe
$ git submodule update --init --recursive
```

### 编译YouCompleteMe

在home下新建一个ycmd_build目录用于编译的中间文件存放，编译完可以删掉。
找到/mingw32/bin/clang.dll复制一份为clang.dll.4.0不然好像报一个找不到clang.dll.4.0的错

``` bash
$ mkdir ycmd_build
$ cd ycmd_build
$ cmake -G "MSYS Makefiles" -DPATH_TO_LLVM_ROOT=/mingw32 -DCMAKE_C_COMPILER=/mingw32/bin/gcc.exe -DCMAKE_CXX_COMPILER=/mingw32/bin/g++.exe -DCMAKE_MAKE_PROGRAM=/mingw32/bin/mingw32-make . /usr/share/vim/vimfiles/plugged/YouCompleteMe/third_party/ycmd/cpp/
```

如果不报错就生成了Makefile，这时可以用mingw32-make编译了,多核可以加 -j 参数

``` bash
$ mingw32-make ycm_core [-j 2*核数]
```

### 编辑vimrc

要在vimrc中指定python解释器，不然报windows Error2.

``` bash
let g:ycm_python_binary_path = 'python2.exe'
let g:ycm_server_python_interpreter = 'python2.exe'
```