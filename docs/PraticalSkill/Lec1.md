# Linux and shell

## 何为Linux

Linux内核最初只是由芬兰人林纳斯·托瓦兹（Linus Torvalds）在赫尔辛基大学上学时出于个人爱好而编写的。Linux是一套免费使用和自由传播的类Unix操作系统，是一个基于POSIX和UNIX的多用户、多任务、支持多线程和多CPU的操作系统。Linux能运行主要的UNIX工具软件、应用程序和网络协议。它支持32位和64位硬件。Linux继承了Unix以网络为核心的设计思想，是一个性能稳定的多用户网络操作系统。目前市面上较知名的发行版有：Ubuntu、RedHat、CentOS、Debain、Fedora、SuSE、OpenSUSE

## Shell 

[shell](https://blog.csdn.net/weixin_45506125/article/details/118058719)

Shell就是命令行工具的胶水，没有任何语言能像Shell一样方便地将一大堆命令行工具组合起来。原则上来说，Shell做什么都可以，但显然它最适合的是自动化，因为只需要将你原来手动敲的命令都复制到一个文件里面就行了。Shell跟标准的编程语言区别很大，它基本上是一个面向字符串的编程语言，组合用好awk/sed/grep，偶尔配合eval，有时候会发挥奇效，但也有可能原地爆炸。可以跟Python之类的其他语言配合起来，比如某个复杂的功能使用一个Python脚本来实现，然后在shell中调用这个脚本实现较复杂的功能；或者反过来，在Python脚本中调用外部的Shell脚本来提高自动化的效率，也是可以的。

## Shell指令

见CTF中的basic knowledge 以及 [zicx](https://github.com/cxzhou35)大佬的[文档](https://thorin-wang.oss-cn-hangzhou.aliyuncs.com/lec0.pdf)。