# Linux Kernel Development [3rd]
## ch2 从内核出发
### 2.1 Get Source code
[PGP signature](https://www.kernel.org/category/signatures.html)</br>
[RC: Release](https://www.kernel.org/category/releases.html)</br>

    wget https://www.kernel.org/pub/linux/kernel/v3.0/linux-3.1.5.tar.xz
    wget https://www.kernel.org/pub/linux/kernel/v3.0/linux-3.1.5.tar.sign

    Git
        git clone后，直接checkout失败, 需要先git commit -a -m 'update' 才可

### 2.3 Compile
[make oldconfig](http://blog.csdn.net/david_xtd/article/details/7609529)

    ldk上关于make oldconfig作用一笔带过，网上查了下，大概如下:
    备份当前.config文件为.config.old，如若用make config/menuconfig设置不当可用于恢复先前的.config
    make oldconfig和make menuconfig都能将原来的.config文件保存为.config.old文件

[ncurses](http://www.oschina.net/p/ncurses)

    apt-get install libncurses5-dev
    make menuconfig




