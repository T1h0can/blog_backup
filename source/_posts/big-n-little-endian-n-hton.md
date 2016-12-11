---
title: 大尾端，小尾端及互相转换
date: 2016-12-01 03:15:23
tags:
	- unix环境高级编程
	- 笔记
	- 备忘
---

# 大小尾端
尾端也叫端序或字节顺序，是计算机数据存储的一种模式，分为大尾端和小尾端两大阵营。
采用大尾端的处理器有` Motorola 6800,  PowerPC 970`等，采用小尾端的最常见的就是目前PC的主流架构` X86`，还有一些处理器是大小尾端可配置的，如手机端的` ARM`。

## 起源
尾端的英文单词是`endian`，源自于格列夫游记中吃鸡蛋时打破大端的(big-end)和打破小端的(little-end)两派，形象的区分了两者。

<!-- more -->

## 存储方式
大尾端机器数据的存储方向和一般的阅读方向相同，从左往右，数据的高位在低地址。
小尾端与之相反，数据低位在低地址。

其实上面都是废话，引用微信公众号“Linux爱好者”发的一篇有关端序的文章里的配图就能解释清一切
![endian](/assets/blogimg/endian.jpg)

运行以下C程序可以知道当前机器的默认端序：

```
#include <stdio.h>
int main()
{
	int c = 16;
	char * point = (char *) (&c);
	if (* point == 16)
		printf("little endian\n");
	else {
		printf("big endian\n");
		printf("%s\n", * point);
	}
	return 0;
}
```

# 转换
在涉及到网络编程的时候，数据从我们的机器发出后，接收数据的机器的默认端序我们并不知道，为了防止16变4096的情况发生，IP协议中定义大端序为网络端序。

在转换端序时会用到下面四个函数(包含在头文件netinet/in.h中):

- unsigned short int htons(unsigned short int hostshort)  //小端序无符号短整形转换为大端序
- unsigned long int htons(unsigned long int hostlong)        //小端序无符号长整形转换为大端序
- unsigned short int ntohs(unsigned short int netshort) //大端序无符号短整形转换为小端序
- unsigned long int ntohl(unsigned long int netlong)        //大端序无符号长整形转换为小端序

以上四个函数返回值为对应端序的数据

-----------------------------
解释一下16是如何变成4096的

16用十六进制表示是0x0010,小端序方式存储时数据在内存中的顺序是,假设存储这个数字的地址是从100开始的

| 100 | 101 |
| ----- | ------ |
|0x10 | 0x00 |

如果不经转换直接发送到大端序机器上,顺序还是

| 100 | 101 |
| ----- | ------ |
|0x10 | 0x00 |

但是表示的数据却是0x1000,转换成十进制数是4096

