---
title: git提交代码到github远程仓库
date: 2018-09-14 10:06:00
categories:
- git
tags:
- git
---

### 写在前面
  原来提交代码到远程仓库的时候，经常会出现无缘无故的报错，有可能是少了某些操作步骤，或者其他原因。故现在总结一下，清晰整个过程，避免没必要的时间浪费。  
  1、github 上面新建一个仓库：biezz  
    ![add repository](/images/2018091401.png)
    
  2、在桌面上创建文件夹，命名为biezz,假设这个文件夹是我们的工作目录,打开git工具
    ```
    Administrator@SC-201805251712 MINGW64 ~/Desktop/python (master)
    $ cd /c/Users/Administrator/Desktop/biezz

    Administrator@SC-201805251712 MINGW64 ~/Desktop/biezz (master)
    $ pwd
    /c/Users/Administrator/Desktop/biezz
    
    $ git init
    Initialized empty Git repository in C:/Users/Administrator/Desktop/biezz/.git/
    
    # 这时我们把需要上传的代码放到biezz文件夹下
    $ echo "这个文件是用来删除redis数据库中的key" >> README.md

    Administrator@SC-201805251712 MINGW64 ~/Desktop/biezz (master)
    $ git status
    On branch master

    No commits yet

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

            README.md
            clear_key.py

    nothing added to commit but untracked files present (use "git add" to track)
    
    $ git add .
    warning: LF will be replaced by CRLF in README.md.
    The file will have its original line endings in your working directory.

    Administrator@SC-201805251712 MINGW64 ~/Desktop/biezz (master)
    $ git commit -m "first commit"
    [master (root-commit) 4b838ef] first commit
     2 files changed, 153 insertions(+)
     create mode 100644 README.md
     create mode 100644 clear_key.py
     
    Administrator@SC-201805251712 MINGW64 ~/Desktop/biezz (master)
    $ git remote add origin https://github.com/biezz/biezz.git
    
    Administrator@SC-201805251712 MINGW64 ~/Desktop/biezz (master)
    $ git push -u origin master
    Enumerating objects: 4, done.
    Counting objects: 100% (4/4), done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (4/4), done.
    Writing objects: 100% (4/4), 1.83 KiB | 938.00 KiB/s, done.
    Total 4 (delta 0), reused 0 (delta 0)
    remote:
    remote: Create a pull request for 'master' on GitHub by visiting:
    remote:      https://github.com/biezz/biezz/pull/new/master
    remote:
    To https://github.com/biezz/biezz.git
     * [new branch]      master -> master
    Branch 'master' set up to track remote branch 'master' from 'origin'.
    
    ```
