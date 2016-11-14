---
title: Sublime Text 3安装配置
date: 2016-11-10 20:00:11
tags:
	- sublime
	- 工具
	- 编辑器
---

# **简介**
sublime text 3是具有代码高亮、语法提示、自动完成且反应快速的编辑器软件，界面华丽，支持插件拓展(整个软件里我只觉得logo有点碍眼，引用我一个朋友的话：感觉是从一个十年前的软件上拿来的，文末提供kde主题里的logo可以替换)。
sublime text 3一直处于测试版状态，最新版本是build 3162，虽说还是测试版，稳定性没得说。
相对于vim的难上手，VS等大型IDE的臃肿，sublime text 3无疑是最佳选择。

<!-- more -->

# **下载**
[下载地址](https://www.sublimetext.com/3)
<img src="/assets/blogimg/sublime_web.png" title="sublime_web">
如图，sublime官方提供
	- windows(32/64位)的exe和免安装版(portable)
	- mac os(10.7以后可用)的dmg包
	- ubuntu(32/64位)版的deb包
	- tar.bz2压缩包给其他linux发行版
不同系统可以各取所需

# **安装**
以下安装方法主要针对非debian系的linux发行版(redhat系,arch系,etc)，当然debian系也是适用的。
以X64为例，打开终端

> wget https://download.sublimetext.com/sublime_text_3_build_3126_x64.tar.bz2
> tar -jxvf sublime_text_3_build_3126_x64.tar.bz2
> ls sublime_text_3

能看到下图
<img src="/assets/blogimg/ls_sublime.png" title="ls_sublime">
把快捷方式复制到`/usr/share/applications`下

> sudo cp sublime_text_3/sublime_text.desktop /usr/share/applications

把整个文件夹移动到`/opt`下

> sudo mv -r sublime_text_3 /opt/sublime_text

至此安装完毕
ps:以后软件有更新的话，下载最新版

> sudo rm -rf /opt/sublime_text_3

用上文的`tar -jxvf`命令解压，`sudo mv`移动

# **注册**
因为闭源收费，会要求注册，虽然可以无限期免费使用，但是会隔三差五弹出提示窗口，比较烦人，编辑窗口上还有一个降低逼格的` UNREGISTERED `标志。有钱的可以上官网买个注册码支持一下作者软件开发，当然注册码这种东西一搜一堆，复制后在`help->Enter license`粘贴就好。

# **安装插件**
Sublime Text 最大的特色就是支持大量插件，利用Package Control我们可以很方便地查找、安装和卸载 Sublime Text 中的插件。
## 安装Package Control
用`` ctrl+` ``打开sublime的控制台(`` ` ``是键盘上ESC下面的那个键)粘贴下面的代码：
	```
	import urllib.request,os,hashlib; h = 'df21e130d211cfc94d9b0905775a7c0f' + '1e3d39e33b79698005270310898eea76'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
	```
重启Sublime Text 3。如果看到`Perferences->package control`这一项，则安装成功。
打开`package control->install package`就可以搜索安装插件了
##插件推荐
**ConvertToUTF8** 支持 GBK, BIG5, EUC-KR, EUC-JP, Shift_JIS 等编码的插件
**Bracket Highlighter** 用于匹配括号，引号和html标签。对于很长的代码很有用。安装好之后，不需要设置插件会自动生效
**WakaTime** 可以精确地统计你花在某个项目上多长时间，用的什么语言，关键是适合发票圈装X。
**YouCompleteMe** 代码补全方面的神器
**ChineseLocalizations** 汉化补丁
**SideBarEnhancements** 功能强大的侧边栏
**terminal** 右键直接打开终端
**SublimeAStyleFormatter** 格式化c/c++代码，专治各种缩进不齐，强迫症必备
# 软件图标替换
还是这张图
<img src="/assets/blogimg/ls_sublime.png" title="ls_sublime">
软件的“low狗”就在Icon文件夹下，喜欢扁平化的人可以用[这里](https://raw.githubusercontent.com/T1h0can/blog_file/master/Icon.tar.gz)的替换掉。


原版   | kde                               
------|------
![sublime_def](/assets/blogimg/sublime-text_def.png) | ![sublime_new](/assets/blogimg/sublime-text_new.png)        

