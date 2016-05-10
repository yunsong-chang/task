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

    保证有1，2个可以启动的内核
    cp arch/i386/boot/bzImage /boot/vmlinuz-version
        或用 make install, 在/boot中多出
            System.map-2.6.32
            config-2.6.32
            vmlinuz-2.6.32: 2.4M
    make modules_insatll: 2.6.32出现在/lib/module中
    mkinitramfs -o initrd.img-2.6.32-my-test 2.6.32
        2.6.32是/lib/modules中的目录
        在当前目录下生产initrd.img
        ubuntu 找不到命令mkinitrd，取而代之的是mkinitramfs

## 2.4 内核开发的特点
[可重入函数](http://baike.baidu.com/link?url=ug_SlGc0LNPy5LmDUMVjG_4AAKBuqaWIyXlc-8DZmbaT8_O0N_RYuim7iv-JGcmixi1IvKzssEFaXprNQKI4uq)

    可重入函数 reentrant
        @h: 一个可以被多个任务调用的函数(过程)，任务在调用时不必担心数据是否会出错@
        不可重入函数在实时系统设计中被视为不安全函数。
        重入即表示重复进入，可被中断
        可以允许有该函数的多个副本在运行
        也可以说是可预测的: 即只要输入数据相同就应产生相同的输出
        允许被递归调用的函数。
            函数的递归调用是指当一个函数正被调用尚未返回时，又直接或间接调用函数本身。
            一般的函数不能做到这样，只有重入函数才允许递归调用。

        尽量使用局部变量（例如寄存器、堆栈中的变量）
            除了使用自己栈上的变量以外不依赖于任何环境（包括static），这样的函数就是purecode（纯代码）可重入
            可以允许有该函数的多个副本在运行，由于它们使用的是分离的栈，所以不会互相干扰。
        如果确实需要访问全局变量（包括static），一定要注意实施互斥手段。
            可重入函数在并行运行环境中非常重要，但是一般要为访问全局变量付出一些性能代价。
            若使用全局变量，则应通过关中断、信号量（即P、V操作）等手段对其加以保护。

        不可重入的函数：使用了一些系统资源，比如全局变量区，中断向量表等
            在实时系统的设计中，经常会出现多个任务调用同一个函数的情况

        所谓的函数是可重入的（也可以说是可预测的），即只要输入数据相同就应产生相同的输出。这个函数之所以是不可预测的，就是因为函数中使用了static变量，因为static变量的特征，这样的函数被称为：带“内部存储器”功能的的函数。

        满足下列条件的函数多数是不可重入的：
        1) 函数体内使用了静态的数据结构；
        2) 函数体内调用了malloc()或者free()函数；
        3) 函数体内调用了标准I/O函数。

        堆栈操作涉及内存分配，稍不留神就会造成益出导致覆盖其他任务的数据，所以，请谨慎使用堆栈！最好别用！很多黑客程序就利用了这一点以便系统执行非法代码从而轻松获得系统控制权。




