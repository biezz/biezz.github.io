---
title: VIM配置Python开发环境
date: 2018-02-23 13:25:00
categories:
- VIM
tags:
- VIM
---

### 实现目的
　　VIM是一个强大而古老的编辑器，这里我们利用VIM来打造适合自己的Python开发环境，可能会涉及VIM其它的配置。

### 环境准备
1、CentOS Linux release 7.2.1511 (Core)  
2、VIM - Vi IMproved 8.0  
3、Python 2.7.5（自带）  

### 实施配置
1、升级VIM，由于CentOS系统自带的VIM版本是7.4，我们这里把它升级至8.0，避免版本太低出现其它问题。
  
  ```
  [root@biezz ~]# yum remove vim -y
  [root@biezz ~]# yum install ncurses-devel -y
  [root@biezz ~]# git clone https://github.com/vim/vim.git
  [root@biezz ~]# cd vim/src
  [root@biezz ~]# make && make install  # 这里有可能会出现缺少gcc而不能安装，如若出现，请yum安装gcc
  [root@biezz ~]# vi /etc/profile
  添加如下：
  export PATH=$PATH:/usr/local/bin/vim
  source /etc/profile
 ```
 此时可能会出现一个问题，vim不支持Python如下：
 ```
 [root@biezz ~]# vim --version |grep python
+comments          +libcall           -python            +vreplace
+conceal           +linebreak         -python3           +wildignore
 ```
 如果是已经编译安装过了，我们需要重新编译一次，我之前就是编译安装完了才发现不支持Python，解决方法如下：
 ```
 [root@biezz ~]# cd /usr/local/src/vim-master
[root@biezz vim-master]# make distclean
[root@biezz vim-master]# yum install -y python-devel python3-devel
[root@biezz vim-master]# yum install automake gcc gcc-c++ kernel-devel cmake  #后面安装YouCompleteMe时需要用到
[root@biezz vim-master]# ./configure --with-features=huge --enable-pythoninterp --enable-python3interp --enable-luainterp --enable-multibyte --enable-sniff --enable-fontset
[root@biezz vim-master]# make && make install
[root@biezz vim-master]# vim --version |grep python
+comments          +libcall           +python            +vreplace
+conceal           +linebreak         -python3           +wildignore
链接方式: gcc   -L/usr/local/lib -Wl,--as-needed -o vim        -lm -ltinfo -lnsl   -ldl    -L/usr/lib64/python2.7/config -lpython2.7 -lpthread -ldl -lutil -lm -Xlinker -export-dynamic       

 ```
2、安装Vundle扩展管理器
```
[root@biezz ~]# git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim
[root@biezz ~]# touch ~/.vimrc   # VIM 配置文件
我们在 VIM 的配置文件中添加如下内容：
set nocompatible              " required
filetype off                  " required

" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()

" alternatively, pass a path where Vundle should install plugins
"call vundle#begin('~/some/path/here')

" let Vundle manage Vundle, required
Plugin 'gmarik/Vundle.vim'

" Add all your plugins here (note older versions of Vundle used Bundle instead of Plugin)

" All of your Plugins must be added before the following line
call vundle#end()            " required
filetype plugin indent on    " required
```
VIM 编辑器执行`:PluginInstall `  
命令行执行：`vim +PluginInstall +qall`  
  
**这里我们穿插一下关于VIM中粘贴代码，格式混乱的问题   

VIM 中由于自动缩进，导致粘贴复制过来代码的时候，会有格式上的混乱，我们来执行 `:set paste` 来解决这个问题，当然你也可以加到vim的配置文件中
