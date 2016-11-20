---
title: markdown语法总结备忘
date: 2016-11-15 22:27:29
tags:
	- markdown
	- 备忘
---

markdown基本语法防健忘备忘录。。。

# 标题
## 类Atx 的标题形式
`#`个数决定标题等级，最多六级
```
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```

## 类 Setext 的标题形式
`=` 代表最高阶标题,`-` 代表第二阶标题,举个栗子:

```
一级标题
==========
二级标题
-----------------
```

注：`=`和`-`的数量没有明确规定，随便按

<!-- more -->

# 引用
在markdown中， `>`标记区块引用,可以在引用的每一行都加上`>`，也可以偷懒只在引用的段落的第一行加上`>`,举个栗子(通过adb发送脏奶牛):

```
 > adb push libs/armeabi/run-as /data/local/tmp/run-as
[100%] /data/local/tmp/run-as
adb shell 'chmod 777 /data/local/tmp/run-as'
adb shell '/data/local/tmp/dirtycow /system/bin/run-as /data/local/tmp/run-as'
warning: new file size (9464) and file old size (17944) differ
```

或者：

```
> adb push libs/armeabi/run-as /data/local/tmp/run-as
> [100%] /data/local/tmp/run-as
> adb shell 'chmod 777 /data/local/tmp/run-as'
> adb shell '/data/local/tmp/dirtycow /system/bin/run-as /data/local/tmp/run-as'
> warning: new file size (9464) and file old size (17944) differ
```

注： 在引用中同样可以使用markdown的语法。

# 列表
markdown支持有序列表和无需列表
## 无序列表
无序列表使用`*`，`+`和`-`作为标记
```
* hello
* world
```
等效于
```
+ hello
+ world
```
或
```
- hello
- world
```

## 有序列表
有序列表的标记是阿拉伯数字+英语句点
```
1. hello
2. world
```

# 代码
在markdown中插入代码用`` ` ``标记
```
`sudo apt-get update`
```
当代码中有`` ` ``时,代码的开始和结尾用多个`` ` ``标记
```
`` 这是一个(`) ``
```

# 插入链接
插入链接的形式通常是`[链接标题]( 链接)`
```
[google](https://www.google.com)
```

# 插入图片
插入图片的形式通常是`![图片标题](图片地址)`,图片的地址可以是本地地址，也可以是网上的链接
```
![Avatar](/assets/blogimg/wifli.png)
```

# 强调
想要强调某个关键词或者某句话时可以用`*`，`**`或`_`，`__`表示,其中`*`和`_`表示斜体，`**`和`__`表示加粗。
```
*斜体*
_斜体_
**加粗**
__加粗__
```

# 表格

```
| left | center | right |
| :------- | :----------: |  ---------: |
|左对齐 | 居中   | 右对齐 |
| aaaa  | bbbb | cccc  |
| a         | b         | c          |
```

# 分割线
用三个以上的星号、减号、下划线来建立一个分隔线，行内不能有其他东西，也可以在星号或是减号中间插入空格。

```
-----------------
___________
**********
```