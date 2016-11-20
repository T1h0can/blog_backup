---
title: AOSP Marshmallow编译教程
date: 2016-11-13 11:01:02
tags:
    - android
    - 系统
---

AOSP，就是"Android Open-Source Project"的缩写，中文意为"Android 开放源代码项目"。AOSP是android系统中最纯净的版本，既不包含GAPPS也没有各手机厂商的个性化代码，但是它是所有分支的基础。

编译AOSP主要有四个步骤：1.构建编译环境，2.下载AOSP源码，3.编译源码，4.运行

推荐在实体机使用Ubuntu14.04 LTS作为工作系统(虚拟机性能低下，编译时间会过长)，如果使用Ubuntu 16.04 LTS需要对编译脚本做一处修改，下文会提到。

<!-- more -->

# 构建编译环境
系统可能自带jdk，但是为了防止版本不对导致编译出错，需要卸载掉现有版本然后再安装正确版本的jdk。
首先用`ctrl + alt + t`快捷键打开终端，输入以下命令
> sudo apt-get purge openjdk-\* icedtea-\* icedtea6-\*

然后安装正确版本的jdk，Marshmallow需要使用jdk7，运行以下命令。
> sudo apt-get update
> sudo apt-get install openjdk-7-jdk

安装完成后输入下面命令查看java版本是否正确。
> java -version

如果显示
```
    java version "1.7.0_65"
    OpenJDK Runtime Environment (IcedTea 2.5.3)
    OpenJDK 64-Bit Server VM (build 24.65-b04, mixed mode)
```
说明版本正确。

接下来安装一些编译是依赖的工具
Ubuntu 14.04下运行：
> sudo apt-get install bison g++-multilib git gperf libxml2-utils make zlib1g-dev:i386 zip

Ubuntu 16.04下务必运行：
> sudo apt-get install libx11-dev:i386 libreadline6-dev:i386 libgl1-mesa-dev g++-multilib 
> sudo apt-get install tofrodos python-markdown libxml2-utils xsltproc zlib1g-dev:i386 
> sudo apt-get install dpkg-dev libsdl1.2-dev libesd0-dev
> sudo apt-get install git-core gnupg flex bison gperf build-essential  
> sudo apt-get install zip curl zlib1g-dev gcc-multilib g++-multilib 
> sudo apt-get install libc6-dev-i386 
> sudo apt-get install lib32ncurses5-dev x11proto-core-dev libx11-dev 
> sudo apt-get install lib32z-dev ccache
> sudo apt-get install libgl1-mesa-dev libxml2-utils xsltproc unzip m4

下载android源码需要工具repo
> mkdir ~/bin
> curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
> chmod a+x ~/bin/repo

接下来需要把repo所在的文件夹添加到环境变量
> nano ~/.bashrc

在文件末尾追加一行
> export PATH=~/bin:$PATH

为了让添加的立即生效
> source ~/.bashrc

现在所有需要用到的工具就安装完成了

# 下载AOSP源码
在终端下运行：
> mkdir ~/android-6.0.1
> cd ~/android-6.0.1

**注意** 如果是第一次使用git，先运行：
>  git config --global user.name "Your Name"
> git config --global user.email "you@example.com"

然后运行：
> repo init -u https://android.googlesource.com/platform/manifest -b android-6.0.1_r70

**注意** 请确保硬盘有至少60G的空间，因为AOSP源码体积相当庞大，而且编译过程中还会生成很多文件。

现在运行` repo sync `就会开始下载源代码，下载时长取决于网络速度，慢慢等着就好。

# 编译源码
**Ubuntu 16.04注意**
找到` art/build/Android.common_build.mk `，定位到第75行，把代码改成下面的样子：
> ifeq ($(WITHOUT_HOST_CLANG),false)

在源码下载完毕后运行下面命令：
> source build/envsetup.sh && lunch

现在会列出所有可以编译的设备的列表，
```
    You're building on Linux

Lunch menu... pick a combo:
     1. aosp_arm-eng
     2. aosp_arm64-eng
     3. aosp_mips-eng
     4. aosp_mips64-eng
     5. aosp_x86-eng
     6. aosp_x86_64-eng
     7. aosp_deb-userdebug
     8. aosp_flo-userdebug
     9. full_fugu-userdebug
     10. aosp_fugu-userdebug
     11. mini_emulator_arm64-userdebug
     12. m_e_arm-userdebug
     13. mini_emulator_mips-userdebug
     14. mini_emulator_x86_64-userdebug
     15. mini_emulator_x86-userdebug
     16. aosp_flounder-userdebug
     17. aosp_angler-userdebug
     18. aosp_bullhead-userdebug
     19. aosp_hammerhead-userdebug
     20. aosp_hammerhead_fp-userdebug
     21. aosp_shamu-userdebug

Which would you like? [aosp_arm-eng]

```
输入目标硬件的编号回车，运行下面命令开始编译：
> make -jn

**注意** 此处n是机器的cpu的线程数，举个例子：如果你的机器的cpu是i7-6700k，6700k是四核八线程，所以这里n是8的时候理论上是编译速度最快的

接下来就是等待。。。当显示

```
#### make completed successfully (49:58 (mm:ss)) ####
```

说明编译成功

# 运行
不要关闭终端，启动模拟器：
> emulator

等一会就会出现模拟器的画面

# 附录
AOSP编译额外命令：
- `croot` 回到aosp源码树根目录
- `godir [filename]` 跳转到包含某个文件的目录
- `m` 在源码树的根目录执行编译
- `mm` 编译当前路径下所有模块，但不包含依赖
- `mma` 编译当前路径下所有模块，且包含依赖
- `mmm [module_path]` 编译指定路径下所有模块，但不包含依赖
- `mmma [module_path]` 编译指定路径下所有模块，且包含依赖
- `make snod` 重新打包生成system.img

