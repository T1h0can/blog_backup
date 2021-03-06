---
title: PDP-11
date: 2016-11-16 06:29:15
tags:
	- C语言
---

PDP-11是1970年由DEC公司推出的第一款16位小型机（美国工业协会评为“70年代最具影响力的技术产品”）。PDP系列小型机对于UNIX系统的诞生有不可忽视的功劳。1969年，AT&T贝尔实验室中止Multics项目后，原项目成员转到PDP-7小型机上开发系统，最初项目名叫“UNICS”，因为PDP-7性等低下这个项目被肯·汤普逊与丹尼斯·里奇移植到PDP-11/20上，并改名为UNIX。第一版UNICS由PDP-7汇编写成，第二版UNIX由B语言和汇编混合写成，肯·汤普逊与丹尼斯·里奇1971年发明C语言后在1973年用C重写了UNIX。PDP小型机对于计算机的发展做出的贡献有通用寄存器和unibus总线,PDP汇编对于C语言也有很大影响，比如让很多人困惑的`i++`和`++ i`自加的灵感就源自于PDP。
<!-- more -->
--------------------------------------------------------------
说句题外话，理论上前自加性能是高于后自加的，因为后自加多出了一个步骤是复制。
--------------------------------------------------------------
下面那个大块头就是pdp-11,还是用纸帶的
![pdp-11](https://upload.wikimedia.org/wikipedia/commons/e/ee/Pdp-11-40.jpg)

今年上半年信息课的作业是写一个简单的PDP-11仿真器，一开始学了些简单的micro-11汇编，明显感觉汇编的晦涩，高级编程语言更接近人的思维习惯。虽然PDP-11已经很老了，但是它的系统设计合理，又没有现代操作系统那么复杂，一个学期写出来一个实现了24条汇编命令的Emulator收获还是挺大的。在写的过程中总是有一些不确定的想法想去实验，当时没有用git的习惯，所以大量备份了不同阶段的代码，前些时候再翻看已经分不清谁是谁的谁了，所以重新整理了一遍，找出了最终版本，加入了从文件输入(以前都是用`<`把文件重定向到标准输入),已经存到了github上。

如果有人感兴趣可以点[这里](https://github.com/T1h0can/pdp-11_emulator)查看，代码质量不高，见谅。

要是将来在莫物理的学弟学妹们搜到了这篇文章，代码随便拿去参考，如果评分标准没有改的话这应该是10分的程度了，虽然塔基亚娜只列出了3到9分的标准，233。