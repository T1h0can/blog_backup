---
title: 构建Kali-NetHunter教程
date: 2016-11-11 08:08:39
tags:
    - android
    - Kali
    - 安全
---

kali linux是大名鼎鼎的渗透测试系统，基于debian发行，但是采用滚动更新，系统集成了众多渗透测试工具，他的前身是同样有名的backtrack。
2014年官方发布了适用于android平台的NetHunter工具包，因为nethunter需要修改内核，最初只支持nexus系列，经过各路大神的努力，现在已经适配六十种机型或系统
<!-- more -->
    ```
    htc_pmewl manta flounder flocm
    flo grouper angler shamu shamucm bullhead
    hammerheadmon hammerheadcm hammerhead makocm mako
    shieldtablet oneplusxcm oneplus2cm oneplus2oos
    oneplus3 oneplus1 h830 h850 hlteeur hltecan hltespr
    hltekor hlteeur-touchwiz hltecan-touchwiz hltespr-
    touchwiz hltekor-touchwiz hltedcm-touchwiz hltekdi-
    touchwiz jfltexx klte kltekdi kltespr kltevzw kltechn
    klte-touchwiz klteduos-touchwiz kltespr-touchwiz
    klteusc-touchwiz kltevzw-touchwiz klteskt-touchwiz
    kltekdi-touchwiz herolte heroltekor hero2lte
    hero2ltekor gracelte graceltekor kipper cancrocm
    a5ulte a5ulte-touchwiz dogo yuga kiwi
    ```
因为我手上有米3,正好还用着cm13系统，以下教程全部以米3(cancro)为例

# 下载源码

> git clone https://github.com/offensive-security/kali-nethunter

# 构建准备

> ls kali-nethunter

![ls_nethunter](/assets/blogimg/ls_nethunter.png)

> cd kali-nethunter/nethunter-installer
> ./bootstrap.sh

接下来会出现两个问题，都输入`y`
    ```
    Would you like to use the experimental devices branch? (y/N): y
    Would you like to grab the full history of devices? (y/N): y
    ```
等下载完成后准备工作就完成了

# 构建
运行`python build.py`构建刷机包前有些需要注意的地方:
1.此处`python`需要用python2,默认使用python3的系统在运行时把改成`python2 build.py`
2.`build.py`中有以下参数
    ```
    --help 或 -h : 显示帮助信息并退出
    --device 或 -d : 构建时后跟目标设备
    --kitkat 或 -kk : android4.4.4
    --lollipop 或 -l : Android 5
    --marshmallow 或 -m : Android 6
    --nougat 或 -n : Android 7
    --forcedown 或 -f : 强制重新下载
    --uninstaller或 -u : 构建一个卸载工具
    --kernel 或 -k : 只构建内核
    --nokernel 或 -nk : 构建的刷机包里不包含内核
    --nosu 或 -ns : 构建的刷机包不包含SuperSU
    --nobrand 或 -nb : 构建的刷机包不包含nethunter的壁纸和启动动画
    --nofreespace 或 --nb : 构建的刷机包不检测可用空间
    --generic ARCH 或 -g ARCH : 构建更新包（只修改ramdisk）
    --rootfs SIZE 或 -fs SIZE : 构建时选择完整程度（full 或者 minimal）
    --release VERSION, -r VERSION : 指定刷机包发行版本
    ```
对于基于cm13的米3,命令如下
> python build.py -d cancrocm -m -fs full 

运行完成后文件夹下会出现`nethunter-cancrocm-marshmallow-kalifs-full-20161111_141351.zip`

# 安装
把`nethunter-cancrocm-marshmallow-kalifs-full-20161111_141351.zip`放到手机sdcard下，用TWRP刷入

# 安装后可能出现的问题
第一次开机会很慢
通知栏下拉会不显示快捷开关
各种工具可能需要从刷机包里解压手动安装
手机会明显卡顿

**此教程仅供参考，如果您的设备在刷入安装包后出现包括但不仅限于以上的问题，本人概不负责，Kali官方团队也不会为此负责**
