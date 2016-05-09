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

    log
        make        ;; 24分钟
        make > ../my_log.txt
        make > ../my_log.txt 2>&1
        make > /dev/null  @h: 错误会显示在屏幕上 @
        make -j32 > /dev/null  (16核 CPU)

### 2.4 install
[ubuntu编译内核及刷内核](http://www.cnblogs.com/hongzg1982/articles/2163620.html)</br>
[grub的引导顺序](http://blog.sina.com.cn/s/blog_4438cd290101a5zb.html)</br>
[initrd 百度百科](http://baike.baidu.com)</br>
[mkinitrd](http://blog.csdn.net/hilaochen/article/details/8222759)</br>

    grub
        在早期的一些Ubuntu版本下，修改grub的引导顺序的方法如下：
        配置文件不在/boot/grub/grub.cfg [u12.04]，而是在menu.lst中
        修改的方法基本同理，主要是修改default和timeout这两项，其他的可以自己的喜好做一些定制

    * 保证有1，2个可以启动的内核
    * cp arch/i386/boot/bzImage /boot/vmlinuz-version
        * 或用 make install, 在/boot中多出
            System.map-2.6.32
            config-2.6.32
            vmlinuz-2.6.32
    * make modules_insatll: 2.6.32出现在/lib/module中
        * vmlinuz-2.6.32-my-test: 2.4M
    * mkinitramfs -o initrd.img-2.6.32-my-test 2.6.32
        * 2.6.32是/lib/modules中的目录
        * 在当前目录下生产initrd.img
        * ubuntu 找不到命令mkinitrd，取而代之的是mkinitramfs
    *



