---
title: 2. Gvim Install
date: 2017-06-08 08:42:34
tags:
---

#. 从github上clone vim的最新代码到/opt/gvim/vim
```bash
#mkdir /opt/gvim
#cd /opt/gvim
#git clone git://github.com/vim/vim.git
#cd vim/src
```
#. 修改Make_ming.mak添加如下代码,主要添加python和lua的依赖，
依据你的系统修改MSYS2变量：
```makefile
UNDER_CYGWIN = no
MSYS2=N:/msys64

PYTHON=$(MSYS2)/mingw64
PYTHON_HOME=$(MSYS2)/mingw64
PYTHON_VER=27
PYTHONINC=-I$(MSYS2)/mingw64/include/python2.7
DYNAMIC_PYTHON_DLL=libpython2.7.dll

PYTHON3=$(MSYS2)/mingw64
PYTHON3_HOME=$(MSYS2)/mingw64
PYTHON3_VER=39
PYTHON3INC=-I$(MSYS2)/mingw64/include/python3.9
DYNAMIC_PYTHON3_DLL=libpython3.9.dll

STATIC_STDCPLUS=yes
LUA=$(MSYS2)/mingw64
LUA_VER=54
DYNAMIC_LUA=yes
include Make_cyg_ming.mak
```
#. 编译gvim,-j参数是多线程编译，你的CPU几多线程就用2倍的数,如果多次编译
那么可以把下面命令做成脚本。
```bash
#mingw32-make -f Make_ming.mak -j 8
#cd ..
#mkdir -p vim82-x86_64/vim82
#cp -a runtime/* vim82-x86_64/vim82
#cp -a src/*.exe vim82-x86_64/vim82
#cp -a src/GvimExt/gvimext.dll vim82-x86_64/vim82
#cp -a src/xxd/xxd.exe vim82-x86_64/vim82
#cp -a vimtutor.bat vim82-x86_64/vim82
#cp -a /mingw64/bin/lua54.dll vim82-x86_64/vim82
```
#. 然后复制二进制文件到相应目录里
```bash
#cp vim82-x86_64/vim82 /opt/gvim/
#mkdir /opt/gvim/vimfiles
#mkdir /opt/gvim/vimfiles/autoload
#mkdir /opt/gvim/vimfiles/plugged
```
#. 在/opt/gvim/下生成_vimrc配置文件
厅

