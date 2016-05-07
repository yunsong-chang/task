# Linux命令
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

ll `cat /etc/shells`
ll `tail -n +2 /etc/shells`  ;; line 2 and after

if :; then echo "always true"; fi
if /bin/true; then echo "always true"; fi
if /bin/false; then echo "always true"; fi
if ./a.out; then echo "always true"; fi

# regular express 不贪婪
    <html><head><title>Hello World</title>
    <body>Welcome to the world of regexp!</body></html>

    sed 's/<.*>//g' testfile
    ' '
    sed 's/<[^>]*>//g' testfile
    Hello World
    Welcome to the world of regexp!
