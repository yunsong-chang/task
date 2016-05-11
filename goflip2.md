# QC Baseline Version
    H5_LF_1_1:              ES4 0.1.118.1   LF.BR.1.2.3.1
    MSM8909_H5_GFLIP2_DEV:  ES7 0.1.120.1   LF.BR.1.2.7

# [IEEE 1725](http://baike.baidu.com/link?url=WrEEcFkn3lzihHMWxwJflGJMMblbWzzXpzWkS1M7sDnjfQaSykPcfdsjB6AOjMnLLXf7HdYAk8uJFbzQlUXrOK)
    外 文 名 IEEE1725                      特    点 认证前提条件
    解    释 电芯涉及安全方面进行审核      目    的 以质量为主

[IEEE1725标准简介](http://www.elecfans.com/yuanqijian/dianchi/dianchishengchang/20091218137935.html)

# task
    掌握充电电流、电压，及温度

# low power mode 休眠
    power safe mode 三者是同一个东西
    cat /sys/kernel/debug/rpm_stats
        RPM Mode:vmin
            count: 0  (不是0就是休眠)
# 电池ID
    ID是如何实现的：是工程师在设计的时侯实现的，主要是防盗版（外国的品牌喜欢弄这些），
    里面的代码需要解码，码片烧好才可安在线路板上用，
    开机它会像主机发送代码信息，手机收到正确的就OK，不正确就显示无效，
    最简单的比喻，手机里面存有一句“床前明月光”，电池要向它发“疑是地上霜”才是正确的，才能正常使用。
    我说的太细你不可能明白，通俗点吧！如果要学最细的，破解美国人的秘密，就汲及到理科的东西，到博士后再说吧！

    行货且正品的电池带芯片的 芯片起到充电或放电时候保护电池
    另外也作为电池的相关信息的存储体 例如电池充放电次数 以及电池的信息等
    你说的ID就是存储在芯片里面的一串代码

# [Android电源管理的作用](http://book.51cto.com/art/201502/466463.htm)
