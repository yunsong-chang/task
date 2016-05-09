[TOC]
# Linux命令

## 命令组合
    ll `cat /etc/shells`
    ll `tail -n +2 /etc/shells`  ;; line 2 and after

## [ls](http://linux.vbird.org/linux_basic/0220filemanager.php#ls)
    -d -S -F -r -R
    ls -d           ; 显示本目录 ./
    ls -d *         ; 显示本目录下的所有
    ls */           ; 显示sbu1目录内容
    ls -d */        ; 显示以/结尾的文件名(就是目录)
    ls /etc         ;
    ls /etc/*       ; 显示sub1目录内容
    ls -d /etc/*

## 只显示目录
    ls -F | grep /$    # -F使得ls将文件分类，通过在文件后面加一些标记来实现
    ls -F | grep /
    ls -l | grep ^d
    ls -d */
    ls -ld */


## 只显示文件
    ls -F | grep [^\/]$  # 注意行尾匹配符号$不可少
    ls -F | grep [^/]$
    ls -l | grep ^-
    ls -l | grep ^- | wc -l  # wc命令统计行数
    find . -type f -maxdepth 1 | xargs ls -al
    ls -p | grep [^/]$  # -p使得ls命令在目录后面加斜杠
    find . ! -name . -prune -type f   # 这个命令不会很好排序文件

## time 命令
## 目录大小
    du -sm /etc
    28     /etc  # 實際目錄約佔有 28MB 的意思！
## 压缩
    time [gzip|bzip2|xz] -c services > services.[gz|bz2|xz]
    打包
    time tar -zpcv -f /root/etc.tar.gz  /etc
    time tar -jpcv -f /root/etc.tar.bz2 /etc
    time tar -Jpcv -f /root/etc.tar.xz  /etc   ; 有p无p, 时间都保持原样

    壓　縮：tar -jcv -f filename.tar.bz2 要被壓縮的檔案或目錄名稱
    查　詢：tar -jtv -f filename.tar.bz2
    解壓縮：tar -jxv -f filename.tar.bz2 -C 欲解壓縮的目錄

# Shell Script
    if :; then echo "always true"; fi
    if /bin/true; then echo "always true"; fi
    if /bin/false; then echo "always true"; fi
    if ./a.out; then echo "always true"; fi

# regular express 不贪婪
    <html><head><title>Hello World</title>
    <body>Welcome to the world of regexp!</body></html>

    sed 's/<.*>//g' testfile
    结果空
    sed 's/<[^>]*>//g' testfile
    Hello World
    Welcome to the world of regexp!
