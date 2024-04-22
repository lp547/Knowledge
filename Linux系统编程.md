# Linux系统编程-第01天（基本命令）

##  学习目标

- 说出Linux下的目录结构和常见目录的作用
- 熟练使用Linux下的相对路径和绝对路径
- 熟练使用Linux下常用文件和目录操作相关的命令
- 熟练使用修改用户权限、用户和用户组相关的命令
- 熟练使用find命令相关参数进行文件查找
- 熟练使用grep命令根据文件内容进行文件的查找

## Linux/Unix操作系统简介

![image-20240416141716689](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\image-20240416141716689.png)

### Linux操作系统的目标(了解)

- 方便性：使计算机系统易于使用

- 有效性：以更有效的方式使用计算机系统资源

- 扩展性：方便用户有效开发、测试和引进新功能

- 开放性：所谓开放性，是指系统能遵循世界标准规范，特别是遵循开放系统互连OSI 国际标准。

  

### Linux操作系统的作用(了解)

操作系统在计算机系统中承上启下的地位：向下封装硬件，向上提供操作接口。

![image-20240416141813597](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\image-20240416141813597.png)

### 2.3 Unix家族 (了解)

- 1965：贝尔实验室（Bell Labs）加入一项由通用电气和麻省理工学院合作的计划，该计划要建立一套多使用者、多任务、多层次的MULTICS操作系统。后来因为项目太为复杂失败。
- 1969：其主要开发者Thompson（后被称为UNIX之父）和Ritchie领导一组开发者，开发了一个新的多任务操作系统—UNICS，后来被改名为Unix，最初的Unix是用B语言和汇编语言混合编写而成。
- 1971：两人在贝尔实验室共同发明了C语言，并于1973用C语言重写了Unix。
- 1974：UNIX第一次出现在贝尔实验室以外。此后UNIX被政府机关，研究机构，企业和大学注意到，并逐渐流行开来。
- 1980：有两个最主要的Unix的版本线，一个是Berkeley的BSD UNIX，另一个是AT&T的Unix，两者的竞争最终引发了Unix的战争，最终导致Unix出现各种各样的变种。
- 1982：AT&T基于版本7开发了UNIX System Ⅲ的第一个商业版本，并不再开源。
- 1992~2001：由于版权问题，AT&T公司与BSD开发组开始了一场将近10年的版权官司。UNIX由于其昂贵的费用，仅局限于大型机的应用；BSD因为版权问题，失去了宝贵的发展时期。

### Linux家族(了解)

- Minix（mini-UNIX）最初是由Andrew Tanenbaum教授，仿照4.3BSD的源代码，白手起家完成了12000行C语言的编写工作这个系统只是一个教学工具，没有什么实际应用价值。
- 1990年，Linus Torvalds决定编写一个自己的Minix内核，初名为Linus' Minix，意为Linus的Minix内核，后来改名为Linux，此内核于1991年正式发布，并逐渐引起人们的注意。
- Linux操作系统的诞生、发展、和成长过程依赖于五个重要支柱：unix操作系统、minix操作系统、GNU计划、POSIX标准和互联网。
- GNU计划：GNU是“GNU is Not Unix”的递归缩写，由Richard M.Stallman于1984年创办,旨在开发一个免费、类unix的操作系统-GNU系统及其开发工具；Emacs编辑系统、BASH shell程序、GCC、GDB等开发工具都是GNU组织的产品。
- 1992年Linux与其他GNU软件结合，完全自由的操作系统正式诞生。该操作系统往往被称为“GNU/Linux”或简称Linux。
- POSIX标准：POSIX标准定义了操作系统应该为应用程序提供的接口标准，POSIX标准用来统一Unix、Linux各分支编程接口，以提高其通用性和可移植性。

### Linux和Unix的联系(了解)

- UNIX系统是工作站上最常用的操作系统，它是一个多用户、多任务的实时操作系统，允许多人同时访问计算机， 并同时运行多个任务。UNIX系统具有稳定、高效、安全、方便、功能强大等诸多优点，自20世纪70年代开始便运行在许多大型和小型计算机上。
- UNIX虽然是一个安全、稳定且功能强大的操作系统，但它也一直是一种大型的而且对运行平台要求很高的操作系统，只能在工作站或小型机上才能发挥全部功能，并且价格昂贵，对普通用户来说是可望而不可及的，这为后来Linux的崛起提供了机会，Linux是一个类UNIX操作系统。
- Linux是免费的、不受版权制约、与UNIX兼容的操作系统。
- Linux在x86架构上实现了UNIX系统的全部特性，具有多用户多任务的能力，同时保持了高效性和稳定性。
- Linux具有如下的优秀的特点：
  1) 开放性；
  2) 完全免费；
  3) 多用户；
  4) 多任务；
  5) 良好的用户界面；
  6) 设备独立性；
  7) 提供了丰富的网络功能；
  8) 可靠的系统安全性；
  9) 良好的可移植性。

### Linux内核介绍(了解)

内核(kernel)是系统的心脏，是运行程序和管理像磁盘和打印机等硬件设备的核心程序，它提供了一个在裸设备与应用程序间的抽象层。

Linux内核版本又分为**稳定版**和**开发版**，两种版本是相互关联，相互循环：

- 稳定版：具有工业级强度，可以广泛地应用和部署。新的稳定版相对于较旧的只是修正一些bug或加入一些新的驱动程序。
- 开发版：由于要试验各种解决方案，所以变化很快。

内核源码网址：http://www.kernel.org，所有来自全世界的对Linux源码的修改最终都会汇总到这个网站，由Linus领导的开源社区对其进行甄别和修改最终决定是否进入到Linux主线内核源码中。

OpenWRT(Linux内核 + 文件系统)

**Linux内核源码获取方式：**

| Protocol                                     | Location                                                     |
| :------------------------------------------- | :----------------------------------------------------------- |
| [HTTP](https://www.ietf.org/rfc/rfc2616.txt) | https://www.kernel.org/pub/                                  |
| [GIT](https://git-scm.com/)                  | https://git.kernel.org/                                      |
| [RSYNC](https://rsync.samba.org/)            | [rsync://rsync.kernel.org/pub/](rsync://rsync.kernel.org/pub/) |

 

### Linux发行版本(了解)

Linux发行版 (也被叫做 GNU/Linux 发行版) 通常包含了包括桌面环境、办公套件、媒体播放器、数据库等应用软件。

这些操作系统通常由Linux内核、以及来自GNU计划的大量的函式库，和基于X Window的图形界面，在X Window中用户同样可以通过使用鼠标对窗口、菜单等进行操作来完成相应的工作。

X Window系统是一个非常出色的图形窗口系统，是类UNIX系统的图形用户界面的工业标准。X Window系统最重要的特征之一就是它的结构与设备无关。

X Window系统的**主要特点**有如下几点：

- X Window系统是客户机/服务器结构的。X Window的实现是与操作系统内核分开的，其主要由X Server和X Client两部分组成。
- X Window系统不是Unix/Linux操作系统的必须的构成部分，而只是一个可选的应用程序组件。

**Best Linux distro for developers in 2018**

| **POSITION** | **2015**   | **2014**   | 2018                                     |
| :----------- | :--------- | :--------- | :--------------------------------------- |
| 1            | Linux Mint | Linux Mint | [Arch Linux](https://www.archlinux.org/) |
| 2            | Debian     | Ubuntu     | [Debian](https://www.debian.org/)        |
| 3            | Ubuntu     | Debian     | [Raspbian](http://raspbian.org/)         |
| 4            | openSUSE   | openSUSE   | [Gentoo](https://www.gentoo.org/)        |
| 5            | Fedora     | Fedora     | [Ubuntu](https://www.ubuntu.com/)        |
| 6            | Mageia     | Mageia     | [Fedora](https://getfedora.org/)         |
| 7            | Manjaro    | Arch       | [OpenSUSE](https://www.opensuse.org/)    |
| 8            | CentOS     | Elementary | [CentOS](https://www.centos.org/)        |
| 9            | Arch       | CentOS     | [Solus](https://solus-project.com/)      |
| 10           | Elementary | Zorin      | [Puppy Linux](http://puppylinux.org/)    |

参考网址：[Best Linux distro for developers in 2018](https://www.techradar.com/news/best-linux-distro-for-developers)

推荐使用Ubuntu Centos

### Unix/Linux开发应用领域介绍(了解)

- Unix/Linux服务器

  是目前Unix/Linux应用最多的一个领域，可以提供Web、FTP、Gopher、SMTP/POP3、Proxy/Cache、DNS等服务器，支持服务器集群，支持虚拟主机、虚拟服务、VPN等。

- 嵌入式Linux系统

  嵌入式Linux是将流行的Linux操作系统进行剪裁修改，能够在嵌入式计算机系统上运行的一种操作系统。Linux嵌入式系统能够支持多种CPU和硬件平台，性能稳定，剪裁性好，开发和使用容易。其中包括Embedix、uCLinux、muLinux等。

- 桌面应用

  近年来，Linux系统特别强调在桌面应用方面的改进，并且已达到相当的水平，完全可以作为一种集办公应用、多媒体应用、网络应用等多方面功能于一体的图形界面操作系统，在办公应用方面，Unix/Linux集成了openOffice、SUN公司的StarOffice以及KOffice等工具。

- 电子政务

  随着Linux的快速发展，Linux已逐渐成为Windows系统重要的竞争力量。尤其是Linux在安全性方面的独特优势，又使得Linux在政府应用领域得到很大的发展。目前一些国家正将其电子政务系统向Linux平台迁移。中国政府也对Linux给予极大的支持。

OpenWrt

## Linux目录结构

###  Win和Linux文件系统区别 (了解)

在 Linux 下，我们是看不到这些驱动器盘符，我们看到的是文件夹

在早期的 UNIX 系统中，各个厂家各自定义了自己的 UNIX 系统文件目录，比较混乱。Linux 面世不久后，对文件目录进行了标准化，于1994年对根文件目录做了统一的规范，推出 FHS ( Filesystem Hierarchy Standard ) 的 Linux 文件系统层次结构标准。FHS 标准规定了 Linux 根目录各文件夹的名称及作用，统一了Linux界命名混乱的局面。

和Windows操作系统类似，所有Unix/Linux的数据都是由文件系统按照树型目录结构管理的。而且Unix/Linux操作系统同样要区分文件的类型，判断文件的存取属性和可执行属性。

Unix/Linux也采用了树状结构的文件系统，它由目录和目录下的文件一起构成。但Unix/Linux文件系统不使用驱动器这个概念，而是使用单一的根目录结构，所有的分区都挂载到单一的“/”目录上，其结构示意图如图所示：

![image-20240416142112257](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\image-20240416142112257.png)

无论何种版本的 Linux 发行版，桌面、应用是 Linux 的外衣，文件组织、目录结构才是Linux的内心。

### Linux常见目录介绍(熟悉)

- **/：**根目录，一般根目录下只存放目录，在Linux下有且只有一个根目录。所有的东西都是从这里开始。当你在终端里输入“/home”，你其实是在告诉电脑，先从/（根目录）开始，再进入到home目录。
- **/bin:** **/usr/bin:** 可执行二进制文件的目录，如常用的命令ls、tar、mv、cat等。
- **/boot：**放置linux系统启动时用到的一些文件，如Linux的内核文件：/boot/vmlinuz，系统引导管理器：/boot/grub。
- **/dev：**存放linux系统下的设备文件，访问该目录下某个文件，相当于访问某个设备，常用的是挂载光驱 mount /dev/cdrom /mnt。
- **/etc**：系统配置文件存放的目录，不建议在此目录下存放可执行文件，重要的配置文件有 /etc/inittab、/etc/fstab、/etc/init.d、/etc/X11、/etc/sysconfig、/etc/xinetd.d。
- **/home：**系统默认的用户家目录，新增用户账号时，用户的家目录都存放在此目录下，~表示当前用户的家目录，~edu 表示用户 edu 的家目录。
- **/lib: /usr/lib: /usr/local/lib**系统使用的函数库的目录，程序在执行过程中，需要调用一些额外的参数时需要函数库的协助。
- **/lost+fount：**系统异常产生错误时，会将一些遗失的片段放置于此目录下。
- **/mnt:/media：**光盘默认挂载点，通常光盘挂载于 /mnt/cdrom 下，也不一定，可以选择任意位置进行挂载。
- **/opt：**给主机额外安装软件所摆放的目录。
- **/proc**：此目录的数据都在内存中，如系统核心，外部设备，网络状态，由于数据都存放于内存中，所以不占用磁盘空间，比较重要的目录有 /proc/cpuinfo、/proc/interrupts、/proc/dma、/proc/ioports、/proc/net/* 等。
- **/root：**系统管理员root的家目录。
- **/sbin:/usr/sbin:/usr/local/sbin：**放置系统管理员使用的可执行命令，如fdisk、shutdown、mount 等。与 /bin 不同的是，这几个目录是给系统管理员 root使用的命令，一般用户只能"查看"而不能设置和使用。
- /**tmp**：一般用户或正在执行的程序临时存放文件的目录，任何人都可以访问，重要数据不可放置在此目录下。
- **/srv：**服务启动之后需要访问的数据目录，如 www 服务需要访问的网页数据存放在 /srv/www 内。
- **/usr**：应用程序存放目录，/usr/bin 存放应用程序，/usr/share 存放共享数据，/usr/lib 存放不能直接运行的，却是许多程序运行所必需的一些函数库文件。/usr/local: 存放软件升级包。/usr/share/doc: 系统说明文件存放目录。/usr/share/man: 程序说明文件存放目录。
- **/var：**放置系统执行过程中经常变化的文件，如随时更改的日志文件 /var/log，/var/log/message：所有的登录文件存放目录，/var/spool/mail：邮件存放的目录，/var/run:程序或服务启动后，其PID存放在该目录下。

##  Linux命令解析器

###  概述

- 很多人可能在电视或电影中看到过类似的场景，黑客面对一个黑色的屏幕，上面飘着密密麻麻的字符，梆梆一顿敲，就完成了窃取资料的任务。
- Linux 刚出世时没有什么图形界面，所有的操作全靠命令完成，就如同电视里的黑客那样，充满了神秘与晦涩。
- 近几年来，尽管 Linux 发展得非常迅速，图形界面越来越友好，但是在真正的开发过程中，Linux 命令行的应用还是占有非常重要的席位，而且许多Linux功能在命令行界面要比图形化界面下运行的快。可以说不会命令行，就不算会 Linux。
- Linux 提供了大量的命令，利用它可以有效地完成大量的工作，如磁盘操作、文件存取、目录操作、进程管理、文件权限设定等。Linux 发行版本最少的命令也有 200 多个，这里只介绍比较重要和使用频率最多的命令。

### 4.2 shell命令解释器

命令解析器的作用：交互式地解释、执行用户输入的命令，将用户的操作翻译成机器可以识别的语言，完成相应功能。

![image-20240416142308365](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\image-20240416142308365.png)

Linux系统中提供了好几种不同的命令解释器，如shell(/bin/sh)、bash(/bin/bash)等，一般默认使用bash作为默认的解释器。

## 05. Bash解析器常用快捷键(熟练)

**5.1 Tab键**

- 补齐命令
- 补齐路径
- 显示当前目录下的所有目录

**5.2 清屏**

clear作用为清除终端上的显示(类似于DOS的cls清屏功能)，也可使用快捷键：Ctrl + L ( “L” 为字母 )。

> deng@itcast:~$ clear

**5.3 中断进程**

ctlr+c的作用是中断终端的操作。

> deng@itcast:/$ sleep 3000

**5.4 遍历输入的历史命令**

- 从当前位置向上遍历：ctrl + p （**↑**）
- 从当前位置向下遍历： ctrl + n（**↓**）

**5.5 光标相关操作**

- 光标左移： ctrl + b （**←**）
- 坐标右移： ctrl + f （**→**）
- 移动到头部： ctrl + a（**Home**）
- 移动到尾部： ctlr + e（**End**）

**5.6 字符删除**

- 删除光标前边的字符：ctrl + h（Backspace）

- 删除光标后边的字符：ctrl + d

  光标后边的字符即光标覆盖的字符

- 删除光标前所有内容：ctrl + u

- 删除光标后所有内容：ctrl + k

## Linux系统相关快捷键(了解)

###  图形打开终端方式：(三种方式)

1）Alt + F2 打开运行输入 gnome-terminal

2） 搜索您的计算机 --> 输入终端 --> 打开

3）右击桌面打开终端

### 终端相关快捷键

(终端必须选中)

Ctrl + Shift + N 新建一个终端 

Ctrl + Shift + T 在终端里新建一个标签 

Ctrl + Shift + W 关闭标签页 

Ctrl + Shift + Q 关闭窗口

Ctrl + Shift + C 复制

 Ctrl + Shift + V 粘贴

Alt + [1 - 9] 标签之间切换 

Ctrl + Shift + = 放大终端字体 

Ctrl + - 缩小终端字体 

Ctrl + 0 普通大小 

F11 全屏 再次按F11退出全屏 

Ctrl + D 关闭当前一个终端 Alt + F4 关闭整个终端 

Ctrl + Shift + F 查找

终端字体推荐使用：DejaVu Sans Mono Book

Alt + Tab 应用程序间切换 Ctrl + Alt + Backspace 注销 Ctrl + Alt + F7 回到图形界面

Ctrl + Alt + F1到 Ctrl + Alt + F6 可以访问6个虚拟控制台

## 内建命令和外部命令(掌握)

### 什么是内建命令

shell内建命令是指bash（或其它版本）工具中集成的命令。一般都会有一个与之同名的系统命令，比如bash中的echo命令与/bin/echo是两个不同的命令，尽管他们行为大体相仿。当在bash中键入一个命令时系统会先看他是否是一个内建命令，如果不是才会查看是否是系统命令或第三方工具。所以在bash中键入echo命令实际上执行bash工具集中的bash命令也就是内建命令，而不是/bin/echo这个系统命令。

### 外部命令

外部命令是安装外部软件所带的命令

### 内建命令和外部命令对比

内建命令要比系统论命令有比较高的执行效率。外部命令执行时往往需要fork出（产生出）一个子进程，而内建命令一般不用。外部命令是在bash之外额外安装的，通常放在/bin，/usr/bin，/sbin，/usr/sbin......等等。可通过“echo $PATH”命令查看外部命令的存储路径，比如：ls、vi等。

### 命令类型查看方法

使用type命令查看：

**格式：**

type [-afptP] 名称 [名称 ...] 显示命令类型的信息。

使用方法示例：

> deng@itcast:~$ type -a cd
>
> cd 是 shell 内建
>
> deng@itcast:~$ type -a echo
>
> echo 是 shell 内建
>
> echo 是 /bin/echo
>
> deng@itcast:~$ type -a ls
>
> ls 是 `ls --color=auto' 的别名
>
> ls 是 /bin/ls

## 08. Linux命令格式(掌握)

**command [ -options] [parameter1] …**

**说明:**

- command：命令名，相应功能的英文单词或单词的缩写
- [-options]：选项，可用来对命令进行控制，也可以省略，[]代表可选
- parameter1 …：传给命令的参数，可以是零个一个或多个

![image-20240416151422709](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\image-20240416151422709.png)

##  帮助文档查看方法

### man(有问题找男人)

man 是 Linux 提供的一个手册，包含了绝大部分的命令、函数使用说明。

该手册分成很多章节（section），使用 man 时可以指定不同的章节来浏览不同的内容。

**man** **中各个** **section** **意义如下：**

> deng@itcast:~$ man man

1)．Standard commands（标准命令）

2)．System calls（系统调用，如open,write）

3)．Library functions（库函数，如printf,fopen）

4)．Special devices（设备文件的说明，/dev下各种设备）

5)．File formats（文件格式，如passwd）

6)．Games and toys（游戏和娱乐）

7)．Miscellaneous（杂项、惯例与协定等，例如Linux档案系统、网络协定、ASCII 码；environ全局变量）

8)．Administrative Commands（管理员命令，如ifconfig）

**man使用格式如下：**

man [选项] 命令名

**man设置了如下的功能键:**

| **功能键** | **功能**             |
| :--------- | :------------------- |
| 空格键     | 显示手册页的下一屏   |
| Enter键    | 一次滚动手册页的一行 |
| b          | 回滚一屏             |
| f          | 前滚一屏             |
| q          | 退出man命令          |
| h          | 列出所有功能键       |
| /word      | 搜索word字符串       |

**用法示例：**

> man -k passwd 搜索关键词
>
> passwd man -a passwd 浏览passwd所有相关的页 
>
> man -f passwd 等价于whatis 
>
> man 1 printf 浏览printf第1页介绍 
>
> man 2 read 浏览read第2页介绍 
>
> man 3 printf 浏览printf第3页介绍 
>
> man 5 passwd 浏览passwd第5页介绍 
>
> man 8 chpasswd 浏览chpasswd第8页介绍

如，我们想查看 ls 的用法：**man 1 ls** ( 1：为数字“1”，代表第 1 个 section，标准命令 ) :

![image-20240416152421470](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\image-20240416152421470.png)

实际上，我们不用指定第几个章节也用查看，如，**man ls**。但是，有这个一种情况，假如，命令的名字和函数的名字刚好重名（如：printf），它既是命令，也可以是库函数，如果，我们不指定章节号，man printf，它只查看命令的用法，不会查询函数的用法，因为 man 是按照手册的章节号的顺序进行搜索的。

![image-20240416152619526](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\image-20240416152619526.png)

所以，使用 man 手册时，最好指定章节号：

 ![image-20240416152635775](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\image-20240416152635775.png)

### 内建命令(help)

**格式： help + 内建命令**

应用示例：

![image-20240416152918290](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\image-20240416152918290.png)

###  外部命令(--help)

一般是 Linux 命令自带的帮助信息，并不是所有命令都自带这个选项。

如我们想查看命令 ls 的用法：**ls --help**

##  绝对路径和相对路径

Unix/Linux路径由到达定位文件的目录组成。在Unix/Linux系统中组成路径的目录分割符为斜杠“/”，而DOS则用反斜杠“\”来分割各个目录。

路径分为**绝对路径**和**相对路径**：

**1）绝对路径**

- 绝对路径是从目录树的树根“/”目录开始往下直至到达文件所经过的所有节点目录。
- 下级目录接在上级目录后面用“/”隔开。
- 注意：绝对路径都是从“/”开始的，所以第一个字符一定是“/”。

/home/test

test

/var/ftp/pub

**2）相对路径**

- 相对路径是指目标目录相对于当前目录的位置。
- 如果不在当前目录下，则需要使用两个特殊目录“.”和“..”了。目录“.”指向当前目录，而目录“..”。

举例说明：

 

## 目录相关的命令

###  pwd

格式：

pwd [-LP] 打印当前工作目录的名字。

使用pwd命令可以显示当前的工作目录，该命令很简单，直接输入pwd即可，后面不带参数。

> deng@itcast:~$ pwd
>
> /home/deng

###  cd

在使用Unix/Linux的时候，经常需要更换工作目录。cd命令可以帮助用户切换工作目录。Linux所有的目录和文件名大小写敏感。

cd后面可跟绝对路径，也可以跟相对路径。如果省略目录，则默认切换到当前用户的主目录。

| **命令** |                           **含义**                           |
| :------: | :----------------------------------------------------------: |
|    cd    | 切换到当前用户的主目录(/home/用户目录)，用户登陆的时候，默认的目录就是用户的主目录。 |
|   cd ~   |            切换到当前用户的主目录(/home/用户目录)            |
|   cd .   |                        切换到当前目录                        |
|  cd ..   |                        切换到上级目录                        |
|   cd -   |                    可进入上一个进入的目录                    |

**注意：**如果路径是从根路径开始的，则路径的前面需要加上 “ / ”，如 “ /mnt ”，通常进入某个目录里的文件夹，前面不用加 “ / ”。

### 11.3 mkdir

用法：mkdir [选项]... 目录...

通过mkdir命令可以创建一个新的目录(不能新建普通文件)。参数-p可递归创建目录。

需要注意的是新建目录的名称不能与当前目录中已有的目录或文件同名，并且目录创建者必须对当前目录具有写权限。

使用示例：

> mkdir test 在当前目录下创建test目录 
>
> mkdir /tmp/test 在根目录下tmp目录里创建test目录 
>
> mkdir file{1..100} 在当前目录下创建file1到file100的目录,这里会创建100个目录 
>
> mkdir "file{1..100}" 在当前目录下创建file{1..100}目录,这里只创建一个目录 
>
> mkdir -p a/b/c 在当前目录下创建a/b/c目录树 
>
> mkdir "a b" 创建以"a b"命名的一个目录 mkdir a\ b 创建以"a b"命名的一个目录 mkdir a b 创建目录a和目录b

### 11.4 rmdir

用法：rmdir [选项]... 目录... 删除指定的空目录。

可使用rmdir命令删除一个目录。必须离开目录，并且目录必须为空，不然提示删除失败。

使用示例：

> rmdir test 删除当前目录的test目录，test必须是空目录 
>
> rmdir /tmp/test 删除/tmp下的test目录 
>
> rmdir file{1..100} 删除file1到file100的目录 
>
> rmdir "file{1..100}" 删除file{1..100}目录 
>
> rmdir "a b" 删除a b这个目录 
>
> rmdir a\ b 删除"a b"目录 
>
> rmdir a b c 删除目录a 目录b 目录c

## 文件类型

 **Linux下一切皆文件。**

在Unix/Linux操作系统中必须区分文件类型，通过文件类型可以判断文件属于可执行文件、文本文件还是数据文件，无扩展名

**文件类型分类**

通常，Unix/Linux系统中常用的文件类型有7种：普通文件、目录文件、设备文件、管道文件、链接文件和套接字。

![image-20240416161433766](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\image-20240416161433766.png)

**1）普通文件**

普通文件是OS用于存放数据、程序等信息的文件，一般都长期存放于外存储器（磁盘、磁带等）中。普通文件一般包括**文本文件、数据文件、可执行的二进制程序文件**等。

在Unix/Linux中可以通过file命令来查看文件的类型。如果file文件后面携带文件名，则查看指定文件的类型，如果携带通配符“*”，则可以查看当前目录下的所有文件的类型。

**2）目录文件**

Unix/Linux系统把目录看成是一种特殊的文件，利用它构成文件系统的树型结构。

目录文件只允许系统管理员对其进行修改，用户进程可以读取目录文件，但不能对它们进行修改。

每个目录文件至少包括两个条目，“..”表示上一级目录，“.”表示该目录本身。

**3）设备文件**

Unix/Linux系统把**每个设备都映射成一个文件**，这就是设备文件。它是用于向I/O设备提供连接的一种文件，分为字符设备和块设备文件。

字符设备的存取以一个字符为单位，块设备的存取以字符块为单位。每一种I/O设备对应一个设备文件，存放在/dev目录中，如行式打印机对应/dev/lp，第一个软盘驱动器对应/dev/fd0。

> deng@itcast:~/share$ echo "hello world" > /dev/pts/22 hello world

**4）管道文件**

管道文件也是Unix/Linux中较特殊的文件类型，这类文件多用于进程间的通信。

**5）链接文件**

似于 windows 下的快捷方式，链接又可以分为软链接（符号链接）和硬链接。

**示例：**

普通文件

> deng@itcast:~/test$ ls -l /etc/passwd
>
> -rw-r--r-- 1 root root 2372 3月 21 22:48 /etc/passwd

目录文件

> deng@itcast:~/test$ ls -ld /etc
>
> drwxr-xr-x 134 root root 12288 5月 28 11:28 /etc

字符设备

> deng@itcast:~/test$ ls -l /dev/input/mouse0
>
> crw-rw---- 1 root input 13, 32 5月 26 17:01 /dev/input/mouse0

块设备

> deng@itcast:~/test$ ls -l /dev/sda1
>
> brw-rw---- 1 root disk 8, 1 5月 26 17:01 /dev/sda1

创建一个管道文件

> deng@itcast:~/test$ mkfifo fifo
>
> deng@itcast:~/test$ ls -l fifo
>
> prw-rw-r-- 1 deng deng 0 5月 28 11:59 fifo

符号链接

> deng@itcast:~/test$ ls -l /bin/sh
>
> lrwxrwxrwx 1 root root 4 11月 17 2017 /bin/sh -> dash
>
> deng@itcast:~/test$

 

套接字文件

> deng@itcast:~/tmp/test$ ls -l /run/systemd/notify
>
> srwxrwxrwx 1 root root 0 8月 8 11:00 /run/systemd/notify

 

## 文件相关命令

###  ls

ls是list简写，其功能为列出目录的内容

Linux文件或者目录名称最长可以有256个字符，“.”代表当前目录，“..”代表上一级目录，以“.”开头的文件为隐藏文件，需要用 -a 参数才能显示。

**用法：ls [选项]... [文件]...**

ls常用参数：

| **参数** | **含义**                                     |
| :------- | :------------------------------------------- |
| -a       | 显示指定目录下所有子目录与文件，包括隐藏文件 |
| -l       | 以列表方式显示文件的详细信息                 |
| -h       | 配合 -l 以人性化的方式显示文件大小           |

使用示例：

> ls -al 显示所有文件包括隐藏文件列表 
>
> ls -lt 显示按日期时间排序后的文件列表 等价于ls -l -t 
>
> ls -lh 显示计算大小为KB为单位的文件列表
>
> ls -dl 显示文件夹详细列表

图中列出的信息含义如下图所示：

![ls -l](assets/ls -l.png)

 

与DOS下的文件操作类似，在Unix/Linux系统中，也同样允许使用特殊字符来同时引用多个文件名，这些特殊字符被称为通配符。 "

| **通配符（了解)** | **含义**                                                     |
| :---------------- | :----------------------------------------------------------- |
| *                 | 文件代表文件名中所有字符                                     |
| ls te*            | 查找以te开头的文件                                           |
| ls *html          | 查找结尾为html的文件                                         |
| ？                | 代表文件名中任意一个字符                                     |
| ls ?.c            | 只找第一个字符任意，后缀为.c的文件                           |
| ls a.?            | 只找只有3个字符，前2字符为a.，最后一个字符任意的文件         |
| []                | “[”和“]”将字符组括起来，表示可以匹配字符组中的任意一个。“-”用于表示字符范围。 |
| [abc]             | 匹配a、b、c中的任意一个                                      |
| [a-f]             | 匹配从a到f范围内的的任意一个字符                             |
| ls [a-f]*         | 找到从a到f范围内的的任意一个字符开头的文件                   |
| ls a-f            | 查找文件名为a-f的文件,当“-”处于方括号之外失去通配符的作用    |
| \                 | 如果要使通配符作为普通字符使用，可以在其前面加上转义字符。“?”和“*”处于方括号内时不用使用转义字符就失去通配符的作用。 |
| ls *a             | 查找文件名为*a的文件                                         |

使用示例：

deng@itcast:~/test$ ls [123].html 1.html 2.html 3.html

deng@itcast:~/test$ ls [1-9].html 1.html 2.html 3.html 4.html 5.html 6.html 7.html 8.html 9.html

###  touch

**用法：touch [选项]... 文件...**

1）如果文件不存在, 创建新文件(只能是普通文件，不能是文件夹)

2）如果文件存在, 更新文件时间

示例：

> touch file 创建file空文件，如果file存在则更新file的存取和修改时间 
>
> touch file{2,3,4} 同时创建file2,file3,file4三个空文件 
>
> touch "file{2,3,4}" 创建file{2,3,4}一个空文件

### cp

cp命令的功能是将给出的文件或目录复制到另一个文件或目录中，相当于DOS下的copy命令 。

| 选项 | 含义                                                         |
| :--- | :----------------------------------------------------------- |
| -a   | 该选项通常在复制目录时使用，它保留链接、文件属性，并递归地复制目录，简单而言，**保持文件原有属性**。 |
| -f   | 删除已经存在的目标文件而不提示                               |
| -i   | 交互式复制，在覆盖目标文件之前将给出提示要求用户确认         |
| -r   | 若给出的源文件是目录文件，则cp将递归复制该目录下的所有子目录和文件，目标文件必须为一个目录名。 |
| -v   | 显示拷贝进度                                                 |

示例：

> cp file dirs/ 把file文件复制到dirs目录下 
>
> cp file1 file2 dirs/ 把file1 file2文件拷贝到dirs目录下 
>
> cp -i file1 file2 把文件file1拷贝到file2中，并且提示 
>
> cp -t dirs file1 把文件file1拷贝到dirs目录下 
>
> cp -r dir1/ dir2/ 把dir1目录复制到dir2目录下 
>
> cp -R dir1 dir2 把dir1目录拷贝到dir2目录下 
>
> cp -a file dirs/ 把file文件复制到dirs目录下，保留文件的原来属性 cp -rf dir1/ dir2/ 强制复制文件夹，不提示 
>
> cp -rvf dir1/ dir2/ 把dir1目录复制到dir2目录下，并且显示复制过程

### 13.4 rm

可通过rm删除文件或目录。

常用参数及含义如下表所示：

| **参数** | **含义**                                         |
| :------- | :----------------------------------------------- |
| -i       | 以进行交互式方式执行                             |
| -f       | 强制删除，忽略不存在的文件，无需提示             |
| -r       | 递归地删除目录下的内容，删除文件夹时必须加此参数 |

示例：

> rm a 删除文件a,在删除之前用户需确认删除该文件 
>
> rm a b c 删除文件a b c,在删除之前用户需确认是否删除该文件 
>
> rm -i a 删除文件a,在删除之前用户需确认是否删除该文件 
>
> rm -f a 删除文件a,强制删除该文件,不需要用户确认是否删除 
>
> rm -v a 删除文件a,删除之后会显式结果 
>
> rm -r dirs 递归删除目录dirs,并且每一次删除都需要用户确认是否删除 
>
> rm -rf dirs 强制递归删除目录dirs,每一次删除都不需要用户确认是否删除
>
> rm file* 删除所有file打头的文件 
>
> rm -i file* 提示是否确定删除 
>
> rm -f file* 不提示，强行删除 
>
> rm -r dir2 删除目录 
>
> rm -f [ab].txt 等价于
>
> rm -f a.txt b.txt rm -f [^ab].txt 删除除a.txt b.txt以外的所有?.txt 
>
> rm -f ?.txt ?代表一个字符 rm -f ???.txt

### 13.5 mv

用户可以使用mv命令来移动文件或目录，也可以给文件或目录重命名。

常用选项说明：

| **选项** | **含义**                                                     |
| :------- | :----------------------------------------------------------- |
| -f       | 禁止交互式操作，如有覆盖也不会给出提示                       |
| -i       | 确认交互方式操作，如果mv操作将导致对已存在的目标文件的覆盖，系统会询问是否重写，要求用户回答以避免误覆盖文件 |
| -v       | 显示移动进度                                                 |

 

示例：

> mv file file2 把file文件重命名为file2 
>
> mv file dirs/ 把file文件移动到dirs目录下 
>
> mv file1 file2 dirs/ 把file1 file2文件剪切到dirs目录下 
>
> mv dir1 dir2 dir3/ 把dir1 dir2目录剪切到dir3目录下 
>
> mv -i file1 dir1/ 把file1文件剪切到dir1目录下,如果存在覆盖就提示用户 
>
> mv -f file1 dir1/ 把file1文件剪切到dir1目录下,如果存在覆盖也不提示用户 
>
> mv -u dir1/* dir2/ 把dir1目录下所有文件移动到dir2目录下，并且根据文件时间来决定要不要移动

## 文件内容查看命令

### cat

cat 将文件内容一次性输出到终端。

缺点：终端显示的内容有限，如果文件太长无法全部显示。

gedit 文件名

示例：

> cat /etc/passwd 查看/etc/passwd内容
>
> cat -n /etc/passwd 查看/etc/passwd内容,对输出的所有行编号
>
> cat -b /etc/passwd 查看/etc/passwd内容并且给非空行编号
>
> cat -A /etc/passwd 等价于 -vET

### more(了解)

more命令将文件内容分页显示到终端，但是只能一直向下浏览，不能回退：

> deng@itcast:~$ more /etc/passwd

相关说明：

| **命令**      | **作用**   |
| :------------ | :--------- |
| 回车          | 显示下一行 |
| 空格          | 显示下一页 |
| q（ctrl + c） | 退出       |
| h             | 获取帮助   |

###  less

less命令将文件内容分页显示到终端，可以自由上下浏览

| **命令**       | **作用**   |
| :------------- | :--------- |
| 回车(ctrl + n) | 显示下一行 |
| ctrl + p       | 显示上一行 |
| 空格(PageDown) | 显示下一页 |
| PageUp         | 显示上一页 |
| q              | 退出       |
| h              | 获取帮助   |

> deng@itcast:~/share/test$ less /etc/passwd

### head

- head命令从文件头部开始查看前 n 行的内容。
- 如果没有指定行数，默认显示前10行内容。

命令格式：

head –n[行数] 文件名

示例：

> head /etc/passwd 查看/etc/passwd前10行内容 
>
> head -c 30 /etc/passwd 查看/etc/passwd前30个字符 
>
> head -30 /etc/passwd 查看/etc/passwd前30行 
>
> head -n 30 /etc/passwd 查看/etc/passwd前30行内容 
>
> head -q /etc/passwd 查看/etc/passwd的内容,但是不打印头信息 head -v /etc/passwd 查看/etc/passwd的内容,但是打印头信息

### tail

- 从文件尾部向上查看最后 n 行的内容
- 使用方式：tail –n[行数] 文件名
- 如果没有指定行数，默认显示最后10行内容

示例：

> tail /etc/passwd 查看/etc/passwd后10行内容 
>
> tail -n 30 /etc/passwd 查看/etc/passwd后30行内容 
>
> tail -c 30 /etc/passwd 查看/etc/passwd后30个字符 
>
> tail -f /etc/passwd 实时查看/etc/passwd文件内容 
>
> tail -q /etc/passwd 查看/etc/passwd的内容,但是不打印头信息 
>
> tail -v /etc/passwd 查看/etc/passwd的内容,但是打印头信息

## du和df命令 (了解)

### du

du命令用于查看某个目录大小。

du命令的使用格式如下：

du [选项] 目录或文件名

| **选项** | **含义**                                           |
| :------- | :------------------------------------------------- |
| -a       | 递归显示指定目录中各文件和子目录中文件占用的数据块 |
| -s       | 显示指定文件或目录占用的数据块                     |
| -b       | 以字节为单位显示磁盘占用情况                       |
| -h       | 以K，M，G为单位，提高信息的可读性                  |

### df

df命令用于检测文件系统的磁盘空间占用和空余情况，可以显示所有文件系统对节点和磁盘块的使用情况。

| **选项** | **含义**                          |
| :------- | :-------------------------------- |
| -a       | 显示所有文件系统的磁盘使用情况    |
| -m       | 以1024字节为单位显示              |
| -h       | 以K，M，G为单位，提高信息的可读性 |

## 查找相关命令(重点)

### find

find命令功能非常强大，通常用来在特定的目录下搜索符合条件的文件，也可以用来搜索特定用户属主的文件。

**按文件名查询：使用参数 -name**

**命令：find + 路径 + -name +“文件名”**

示例：find /home -name “a.txt”

**按文件大小查询：使用参数 -size**

命令：find + 路径 + -size + 范围

范围

Ø 大于：+表示 -- +100k

Ø 小于：-表示 -- -100k

Ø 等于: 不需要添加符号 -- 100k

大小

Ø M 必须大写（10M）

Ø k 必须小写（20k）

例子: 查询目录为家目录

等于100k的文件: find ~/ -size 100k

大于100k的文件: find ~/ -size +100k

大于50k, 小于100k的文件: find ~/ -size +50k -size -100k

**按文件类型查询：使用参数 -type**

命令：find + 路径 + -type + 类型

类型

Ø 普通文件类型用 **f** 表示而不是-

Ø d -> 目录

Ø l -> 符号链接

Ø b -> 块设备文件

Ø c -> 字符设备文件

Ø s -> socket文件，网络套接字

Ø p -> 管道

查找指定目录下的普通文件： find /home -type f

> 查找根目录下所有的普通文件
>
> deng@itcast:~$ find / -type f
>
> 查找根目录中所有的目录稳步
>
> deng@itcast:~$ find / -type d
>
> 查找根目录所有的字符设备
>
> deng@itcast:~$ find / -type c
>
> 查找根目录下所有的块设备
>
> deng@itcast:~$ find / -type b
>
> 查找根目录下所有的符号链接
>
> deng@itcast:~$ find / -type l
>
> 查找根目录下所有的套接字
>
> deng@itcast:~$ find / -type s
>
> 查找根目录下所有的管道
>
> deng@itcast:~$ find / -type p

 

示例：

```
find /etc -name grub.conf   查找/etc目录下的grub.conf文件
find / -name "*.conf"       查找/下所有.conf文件
find  / -iname grub.conf    查找/目录下的grub.conf文件，忽略大小写
find / -maxdepth 2 -name grub.conf     可以使用-maxdepath参数来控制查找的层次，就是说只查当前目录和子目录,最多查2级目录
find / -mindepth 2 -name grub.conf     最少查二级目录
find /etc -type d           查找/etc/下所有的目录
find /etc -type f           查找/etc/下的所有普通文件
find /etc -type l -name *.conf      查找/etc/下软链接文件是.conf结尾的文件
find /etc -type s           查找/etc/下所有socket文件
find /etc -type c           查找/etc/下的所有字符设备文件
find /etc -type p           查找/etc/下所有管道文件
find /etc -user root        查找/etc/所属用户是root的文件
find /etc -group root       查找/etc/所属用户组是root的文件
find /etc -uid 500          查找/etc/下uid是500的文件,和-user类似
find /etc -gid 500          查找/etc/下gid是500的文件,和-group类似
find /etc -nouser           查找没有所属用户的文件
find /etc -nogroup          查找没有所属用户组的文件
find /etc -perm 777 -type d    查找/etc/下权限为777的目录
find . -perm  111           查找权限是111的文件
find . -size +10M           查找当前目录下大于10M的文件，单位可以有K,M,G,b等
find / -size -2M            查找根目录下少于2M的文件
find / -mtime 1             查找根目录下1天以前修改的所有文件
find / -mtime +2            查找根目录下2天以前修改的所有文件
find / -mtime -3            查找根目录下最近3天内修改的所有文件
find / -atime 1             查找根目录下1天以前访问或读过的所有文件
find / -atime -1            查找根目录下最近1天内读过或访问的文件
find / -ctime -3            查找根目录下最近3天内状态发生改变的文件
find / -cmin -3             查找根目录下最近3分钟内状态发生改变的文件
find / -empty               查找根目录下所有空白文件或者空目录
find / -false               查找根目录下总是错误的文件
```



```
高级用法：
find / -false -exec ls -l {} \;   查找根目录下总是错误的文件并且用ls -l查看
find . -name "*.conf" -exec rm -rf {} \;
find . -name "*.conf" | xargs rm -rf 删除当前目录下所有以 .conf 结尾的文件

deng@itcast:~$ find cmd/ -name "txt" -ok  rm -rf {} \;  删除之前做确认
< rm ... cmd/txt > ? y
```

### 16.2 grep

Linux系统中grep命令是一种强大的文本搜索工具，grep允许对文本文件进行模式查找。如果找到匹配模式， grep打印包含模式的所有行。

grep一般格式为：

**grep [-选项] ‘搜索内容串’ 文件名**

在grep命令中输入字符串参数时，最好引号或双引号括起来。例如：grep ‘a ’1.txt。

 

常用选项说明：

| **选项** | **含义**                                 |
| :------- | :--------------------------------------- |
| -v       | 显示不包含匹配文本的所有行（相当于求反） |
| -n       | 显示匹配行及行号                         |
| -i       | 忽略大小写                               |

 

命令：grep -r + “查找的关键字” + 路径

搜索目录需要添加参数： -r

查找 /home/itcast 下包含“hello，world“字符串的文件

grep -r "hello，world" /home/itcast

示例：

> grep -a hello /bin/ls 将二进制文件以文本文件的方式搜索hello grep -i hello /etc/passwd 在/etc/passwd文件里找hello并且忽略大小写查找 grep -n hello /etc/passwd 搜索hello结果并显示在文件里出现的行号 grep -w hello /etc/passwd 搜索完全匹配hello单词的行 grep -v hello /etc/passwd 显示出在/etc/passwd文件里没有hello的行 grep -r hello /etc/ 在/etc/目录里所有文件里找hello并显示结果 grep -i hello /etc/passwd --color=auto 在/etc/passwd文件中找hello并且忽略大小写，然后高亮显示匹配的关键字

## 17. 管道

管道(**|**)：一个命令的输出可以通过管道做为另一个命令的输入。

管道我们可以理解现实生活中的管子，管子的一头塞东西进去，另一头取出来，这里“ | ”的左右分为两端，左端塞东西(写)，右端取东西(读)。

> cat /etc/passwd | less

 

## 18. 压缩包管理(重点)

 

### 18.1 tar

计算机中的数据经常需要备份，tar是Unix/Linux中最常用的备份工具，此命令可以把一系列文件归档到一个大文件中，也可以把档案文件解开以恢复数据。

tar使用格式

> tar [选项] 打包文件名 文件

tar命令很特殊，其选项前面可以使用“-”，也可以不使用。

常用参数：

| **参数** | **含义**                                                  |
| :------- | :-------------------------------------------------------- |
| -c       | 生成档案文件，创建打包文件                                |
| -v       | 列出归档解档的详细过程，显示进度                          |
| -f       | 指定档案文件名称，f后面一定是.tar文件，所以必须放选项最后 |
| -t       | 列出档案中包含的文件                                      |
| -x       | 解开档案文件                                              |

注意：除了f需要放在参数的最后，其它参数的顺序任意。

![2016-05-30_000235_副本](assets/clip_image002-1527435606703.jpg)

 

tar -cvf 创建归档文件

tar -xvf 解除归档文件(还原)

tar -tvf 查看归档文件内容

### 18.2 gzip

l tar与gzip命令结合使用实现文件打包、压缩。

l tar只负责打包文件，但不压缩，用gzip压缩tar打包后的文件，其扩展名一般用xxxx.tar.gz。



gzip使用格式如下：

> gzip [选项] 被压缩文件



常用选项：

| **选项** | **含义**       |
| :------- | :------------- |
| -d       | 解压           |
| -r       | 压缩所有子目录 |

一次性压缩多个文件: gzip后面不能跟目录

![1533779697262](assets/1533779697262.png)

![1533779918198](assets/1533779918198.png)

![2016-05-30_002353](assets/clip_image002-1527435669757.jpg)

tar这个命令并没有压缩的功能，它只是一个打包的命令，但是在tar命令中增加一个选项(-z)可以调用gzip实现了一个压缩的功能，实行一个先打包后压缩的过程。



**压缩用法：**tar cvzf 压缩包包名 文件1 文件2 ...

| -z   | 指定压缩包的格式为：file.tar.gz |
| :--- | :------------------------------ |
|      |                                 |



例如：**tar zcvf test.tar.gz 1.c 2.c 3.c 4.c**把 1.c 2.c 3.c 4.c 压缩成 test.tar.gz![20150317165114719](assets/clip_image002-1527435687329.jpg)

**解压用法：** tar zxvf 压缩包包名

| **参数** | **含义**                        |
| :------- | :------------------------------ |
| -z       | 指定压缩包的格式为：file.tar.gz |



![20150317171031803](assets/clip_image002-1527435714808.jpg)



**解压到指定目录：**-C （大写字母“C”）



例子：tar -xvf new.tar.gz -C ./test/ 将 new.tar.gz 解压到当前目录下的 test 目录下：![20150317171859409](assets/clip_image004.jpg)

 

### 18.3 bzip2

- tar与bzip2命令结合使用实现文件打包、压缩(用法和gzip一样)。
- tar只负责打包文件，但不压缩，用bzip2压缩tar打包后的文件，其扩展名一般用xxxx.tar.bz2。
- 在tar命令中增加一个选项(-j)可以调用bzip2实现了一个压缩的功能，实行一个先打包后压缩的过程。
- 压缩用法：tar jcvf 压缩包包名 文件...(tar jcvf bk.tar.bz2 *.c)
- 解压用法：tar jxvf 压缩包包名 (tar jxvf bk.tar.bz2)

 

tar -czvf

tar -cjvf

tar -xzvf

tar -xjvf

tar -xvf 万能解压 (gzip bzip2)

生成一个bz2压缩包

> deng@itcast:~/share$ tar -cjvf test.tar.bz2 test

解压bz2压缩包

> deng@itcast:~/share$ tar -xjvf share.tar.bz2

 

### 18.4 zip和unzip

l 通过zip压缩文件的目标文件不需要指定扩展名，默认扩展名为zip。

l 压缩文件：zip -r 目标文件(没有扩展名) 源文件

l 解压文件：unzip -d 解压后目录文件 压缩文件![2016-05-30_004727](assets/clip_image002-1527435799084.jpg)

 

## 19. 文件权限管理

 

### 19.1 文件权限

文件权限就是文件的访问控制权限，即哪些用户和组群可以访问文件以及可以执行什么样的操作。

Unix/Linux系统是一个典型的多用户系统，不同的用户处于不同的地位，对文件和目录有不同的访问权限。为了保护系统的安全性，Unix/Linux系统除了对用户权限作了严格的界定外，还在用户身份认证、访问控制、传输安全、文件读写权限等方面作了周密的控制。

在 Unix/Linux中的每一个文件或目录都包含有访问权限，这些访问权限决定了谁能访问和如何访问这些文件和目录。

### 19.2 访问用户分类

通过设定权限可以从以下三种访问方式限制访问权限：

**1）只允许用户自己访问（所有者）**

所有者就是创建文件的用户，用户是所有用户所创建文件的所有者，用户可以允许所在的用户组能访问用户的文件。



**2）允许一个预先指定的用户组中的用户访问（用户组）**

用户都组合成用户组，例如，某一类或某一项目中的所有用户都能够被系统管理员归为一个用户组，一个用户能够授予所在用户组的其他成员的文件访问权限。



**3）允许系统中的任何用户访问（其他用户）**

用户也将自己的文件向系统内的所有用户开放，在这种情况下，系统内的所有用户都能够访问用户的目录或文件。在这种意义上，系统内的其他所有用户就是 other 用户类



这有点类似于 QQ 空间的访问权限：

l 这个 QQ 空间是属于我的，我相当于管理者（也就是“所有者”），我想怎么访问就怎么访问。

l 同时，我可以设置允许 QQ 好友访问，而这些 QQ 好友则类似于“用户组”。

l 当然，我可以允许所有人访问，这里的所有人则类似于(不完全等价)“其他用户”。

### 19.3 访问权限说明

用户能够控制一个给定的文件或目录的访问程度，一个文件或目录可能有读、写及执行权限：

- 读权限（r）

对文件而言，具有读取文件内容的权限；对目录来说，具有浏览目录的权限。

- 写权限（w）

对文件而言，具有新增、修改文件内容的权限；对目录来说，具有删除、移动目录内文件的权限。

- 可执行权限（x）

对文件而言，具有执行文件的权限；对目录了来说该用户具有进入目录的权限。

注意：通常，Unix/Linux系统只允许文件的属主(所有者)或超级用户改变文件的读写权限。

 

### 19.4 chmod(掌握)

chmod 修改文件权限有两种使用格式：字母法与数字法。

**字母法：**chmod u/g/o/a +/-/= rwx 文件

| **[ u/g/o/a ]** | **含义**                                                  |
| :-------------- | :-------------------------------------------------------- |
| u               | user 表示该文件的所有者                                   |
| g               | group 表示与该文件的所有者属于同一组( group )者，即用户组 |
| o               | other 表示其他以外的人                                    |
| a               | all 表示这三者皆是                                        |



| **[ +-= ]** | **含义** |
| :---------- | :------- |
| +           | 增加权限 |
| -           | 撤销权限 |
| =           | 设定权限 |



| **rwx** | **含义**                                                     |
| :------ | :----------------------------------------------------------- |
| r       | read 表示可读取，对于一个目录，如果没有r权限，那么就意味着不能通过ls查看这个目录内部的内容。 |
| w       | write 表示可写入，对于一个目录，如果没有w权限，那么就意味着不能在目录下创建新的文件。 |
| x       | excute 表示可执行，对于一个目录，如果没有x权限，那么就意味着不能通过cd进入这个目录。 |

 

**chmod o+w file** 给文件file的其它用户增加写权限：

![20150318101929779](assets/clip_image002-1527436344760.jpg)



**chmod u-r file** 给文件file的拥有者减去读的权限：

![20150318102451521](assets/clip_image004-1527436344760.jpg)



**chmod g=x file**设置文件file的所属组权限为可执行，同时去除读、写权限：

![20150318102845115](assets/clip_image006.jpg)

**数字法：**“rwx” 这些权限也可以用数字来代替

| r    | 读取权限，数字代号为 "4"      |
| :--- | :---------------------------- |
| w    | 写入权限，数字代号为 "2"      |
| x    | 执行权限，数字代号为 "1"      |
| -    | 不具任何权限，数字t代号为 "0" |



如执行：chmod u=rwx,g=rx,o=r filename

就等同于：chmod u=7,g=5,o=4 filename(不可以执行)

**chmod 751 file\****：**

l 文件所有者：读、写、执行权限

l 同组用户：读、执行的权限

l 其它用户：执行的权限

![20150318104319700](assets/clip_image002-1527436373799.jpg)



chmod 777 file：所有用户拥有读、写、执行权限

![20150318105238743](assets/clip_image004-1527436373799.jpg)



注意：如果想递归所有目录加上相同权限，需要加上参数“ -R ”。

如：chmod 777 test/ -R 递归 test 目录下所有文件加 777 权限。

 

 

### 19.5 chown(了解)

l chown用于修改文件所有者

l 使用方法：chown 用户名 文件或目录名

 

![2016-05-30_212216](assets/clip_image002-1527436391297.jpg)



将文件所属者修改为root用户

> deng@itcast:~/share/test的密码： ls -l txt -rw-rw-r-- 1 root deng 0 10月 10 11:12 txt

将文件所属者改为deng 所属组改为root

> deng@itcast:~/share/test ls -l txt -rw-rw-r-- 1 deng root 0 10月 10 11:12 txt

单独只修改文件所属组

> deng@itcast:~/share/test ls -l txt -rw-rw-r-- 1 deng root 0 10月 10 11:12 txt

### 19.6 chgrp (了解)

l chgrp用于修改文件所属组

l 使用方法：chgrp 用户组名 文件或目录名

 

![2016-05-30_212432](assets/clip_image002-1527436456220.jpg)

 

单独修改文件所属组

> deng@itcast:~/share/test ls -l txt -rw-rw-r-- 1 deng deng 0 10月 10 11:12 txt

 

## 20. 进程管理(后面再讲)

### 20.1 ps

进程是一个具有一定独立功能的程序，它是操作系统动态执行的基本单元。

ps命令可以查看进程的详细状况，常用选项(选项可以不加“-”)如下：

| **选项** | **含义**                                 |
| :------- | :--------------------------------------- |
| -a       | 显示终端上的所有进程，包括其他用户的进程 |
| -u       | 显示进程的详细状态                       |
| -x       | 显示没有控制终端的进程                   |
| -w       | 显示加宽，以便显示更多的信息             |
| -r       | 只显示正在运行的进程                     |

ps aux

ps ef

ps -a

![2016-05-29_230200](assets/clip_image002-1527436564167.jpg)

### 20.2 top

top命令用来动态显示运行中的进程。top命令能够在运行后，在指定的时间间隔更新显示信息。可以在使用top命令时加上-d 来指定显示信息更新的时间间隔。



在top命令执行后，可以按下按键得到对显示的结果进行排序：

| **按键** | **含义**                           |
| :------- | :--------------------------------- |
| M        | 根据内存使用量来排序               |
| P        | 根据CPU占有率来排序                |
| T        | 根据进程运行时间的长短来排序       |
| U        | 可以根据后面输入的用户名来筛选进程 |
| K        | 可以根据后面输入的PID来杀死进程。  |
| q        | 退出                               |
| h        | 获得帮助                           |



![2016-05-29_231626](assets/clip_image002-1527436598410.jpg)

 

### 20.3 kill

kill命令指定进程号的进程，需要配合 ps 使用。

使用格式：

kill [-signal] pid

信号值从0到15，其中9为绝对终止，可以处理一般信号无法终止的进程。



**kill 9133** ：9133 为应用程序所对应的进程号

![20150318112100659](assets/clip_image002-1527436647473.jpg)



有些进程不能直接杀死，这时候我们需要加一个参数“ -9 ”，“ -9 ” 代表强制结束：

![20150318112401325](assets/clip_image002-1527436664857.jpg)

 

### 20.4 killall

 

通过进程名字杀死进程

![1527498996963](assets/1527498996963.png)

## 21. 软件安装和卸载

### 21.1 在线安装

如果是在ubuntu平台，软件的安装可以通过互联网在线安装，更加方便快捷：

| **命令**                 | **含义**               |
| :----------------------- | :--------------------- |
| sudo apt-get update      | 获得最新的软件包的列表 |
| sudo apt-get install xxx | 从源中安装xxx软件      |
| sudo apt-get remove xxx  | 删除xxx软件            |
| sudo apt-get clean       | 清理安装包             |



![2016-05-29_200452_副本](assets/clip_image002-1527436722457.jpg)

 

### 21.2 软件包安装

在Ubuntu下安装文件为deb格式

软件安装

sudo dpkg -i xxx.deb

软件卸载

sudo dpkg -r 软件名

 

示例:

tree软件安装

> deng@itcast:~$ sudo dpkg -i tree_1.6.0-1_amd64.deb

tree软件卸载

> deng@itcast:~$ sudo dpkg -r tree

## 22. 重定向

重定向

标准输入 代码 0 默认设备为键盘
​ 标准输出 代码 1 默认设备为屏幕
​ 错误输出 代码 2 默认设备为屏幕

ls /etc/passwd > output.txt 标准正确输出重定向到output.txt ls /etc/shadow >> output.txt 标准正确输出追加重定向到output.txt ls dddddd 2> error.txt 标准错误输出重定向到error.txt ls ddddd 2>> error.txt 标准错误输出重定向到error.txt,追加的方式 ls dddddd 2> /dev/null 标准错误输出重定向到黑洞 ls ddddd /etc/passwd &> /dev/null 标准正确输出标准错误输出全都重定向到黑洞 ls ddddd /etc/passwd &>> txt 标准正确输出标准错误输出以追加的方式全都重定向到txt

cat < file 标准输入重定向,file作为cat输入的内容

## 23. 其它命令

### 23.1 tree

tree 以树状形式查看指定目录内容，使用该命令需要安装软件 tree：

> sudo apt install tree



常用选项：

| -L n | 查看n层目录 |
| :--- | :---------- |
|      |             |



![img](assets/clip_image002-1527436987887.jpg)

 

### 23.2 ln(掌握)

ln命令主要用于创建链接文件。Linux链接文件类似于Windows下的快捷方式。



链接文件分为软链接和硬链接：

- 软链接：软链接不占用磁盘空间，源文件删除则软链接失效。
- 硬链接：硬链接只能链接普通文件，不能链接目录。



使用格式：

ln 源文件 链接文件

ln -s 源文件 链接文件



如果没有-s选项代表建立一个硬链接文件，两个文件占用相同大小的硬盘空间，即使删除了源文件，链接文件还是存在，所以-s选项是更常见的形式。

注意：如果软链接文件和源文件不在同一个目录，源文件最好要使用绝对路径，不要使用相对路径。

 

![img](assets/clip_image002-1527437184702.jpg)

 

readlink命令读取符号链接文件的内容(存储目标文件的路径)

> deng@itcast:~/share$ readlink a_link2 /home/deng/share/a

## 00. 目录

[00. 目录](#header-n0)[01. 学习目标](#header-n3)[02. 编辑器gedit介绍](#header-n18)[03. 什么是vi(vim)](#header-n26)[04. vim工作模式](#header-n34)[4.1 命令模式](#header-n37)[4.2 编辑模式](#header-n42)[4.3 末行模式](#header-n47)[05. vim教程](#header-n51)[06. vim基本操作](#header-n56)[07. vim实用操作](#header-n70)[7.1 命令模式下的操作](#header-n71)[7.2 末行模式下的操作](#header-n252)[08. GCC编译器简介](#header-n372)[09. GCC工作流程和常用选项](#header-n391)[10. 静态连接和动态连接](#header-n462)[11. 静态库和动态库简介](#header-n505)[12. 静态库制作和使用](#header-n510)[13. 动态库制作和使用](#header-n553)[14. GDB调试器](#header-n627)[14.1 GDB简介](#header-n628)[14.2 生成调试信息](#header-n643)[14.3 启动GDB](#header-n650)[14.3 显示源代码](#header-n667)[14.4 断点操作](#header-n677)[14.5 条件断点](#header-n700)[14.6 维护断点](#header-n706)[14.7 调试代码](#header-n718)[14.8 数据查看](#header-n735)[14.9 自动显示](#header-n740)[14.10 查看修改变量的值](#header-n758)

## 01. 学习目标

- 熟练使用压缩工具完成文件或目录的压缩解压缩
- 熟练掌握Ubuntu下的软件安装和卸载
- 掌握vim命令模式下相关命令的使用
- 掌握从命令模式切换到编辑模式的相关命令
- 掌握vim末行模式下相关命令的使用
- 能够说出gcc的工作流程和掌握常见参数的使用

## 02. 编辑器gedit介绍

gedit是一个[GNOME](https://baike.baidu.com/item/GNOME)[桌面环境](https://baike.baidu.com/item/桌面环境)下兼容UTF-8的[文本编辑器](https://baike.baidu.com/item/文本编辑器)。它使用[GTK+](https://baike.baidu.com/item/GTK%2B)编写而成，因此它十分的简单易用，有良好的语法高亮，对中文支持很好，支持包括[gb2312](https://baike.baidu.com/item/gb2312)、[gbk](https://baike.baidu.com/item/gbk)在内的多种[字符编码](https://baike.baidu.com/item/字符编码)。gedit是一个[自由软件](https://baike.baidu.com/item/自由软件)。

这是 Linux 下的一个纯文本编辑器,但你也可以把它用来当成是一个集成开发环境 (IDE), 它会根据不同的语言高亮显现关键字和标识符。

gedit是一个Linux环境下的文本编辑器，类似windows下的写字板程序，在不需要特别复杂的编程环境下，作为基本的文本编辑器比较合适。

> deng@itcast:~$ gedit txt &

打开gedit图形界面如下：

![1527505979128](assets/1527505979128.png)

## 03. 什么是vi(vim)

vi (Visual interface)编辑器是 Linux 系统中最常用的文本编辑器，vi 在Linux界有编辑器之神的美誉，几乎所有的 Linux 发行版中都包含 vi 程序。

vi 工作在字符模式下，不需要图形界面，非常适合远程及嵌入式工作，是效率很高的文本编辑器，尽管在 Linux 上也有很多图形界面的编辑器可用，但vi的功能是那些图形编辑器所无法比拟的。

vim 是 vi 的升级版，它不仅兼容 vi 的所有指令，而且还有一些新的特性，例如 vim 可以撤消无限次、支持关键词自动完成、可以用不同的颜色来高亮你的代码。vim 普遍被推崇为类 vi 编辑器中最好的一个。

 

> vim键盘

![vim键盘](assets/vim键盘.jpg)

## 04. vim工作模式

vi有三种基本工作模式: **命令模式、文本输入模式(编辑模式)、末行模式**。

![clip_image002](assets/clip_image002.jpg)

### 4.1 命令模式

任何时候,不管用户处于何种模式,只要按一下ESC键,即可使vi进入命令模式。我们在shell环境(提示符为$)下输入启动vim命令，进入编辑器时，也是处于该模式下。



在命令模式下，用户可以输入各种合法的vi命令，用于管理自己的文档。此时从键盘上输入的任何字符都被当做编辑命令来解释，若输入的字符是合法的vi命令，则vi在接受用户命令之后完成相应的动作。但需注意的是，所输入的命令并不在屏幕上显示出来。若输入的字符不是vi的合法命令，vi会响铃报警。

 

### 4.2 编辑模式

在命令模式下输入插入命令i（I）、附加命令a（A） 、打开命令o（O）、替换命s（S）都可以进入文本输入模式，此时vi窗口的最后一行会显示“插入”。

![1527506715865](assets/1527506715865.png)

在该模式下,用户输入的任何字符都被vi当做文件内容保存起来，并将其显示在屏幕上。在文本输入过程中，若想回到命令模式下，按键**ESC**即可。

 

### 4.3 末行模式

末行模式下，用户可以对文件进行一些附加处理。尽管命令模式下的命令可以完成很多功能，但要执行一些如字符串查找、替换、显示行号等操作还是必须要进入末行模式的。

在命令模式下，输入冒号即可进入末行模式。此时vi窗口的状态行会显示出冒号，等待用户输入命令。用户输入完成后，按回车执行，之后vi编辑器又自动返回到命令模式下。

 

## 05. vim教程

> deng@itcast:~/test$ vimtutor

![1527507035917](assets/1527507035917.png)

 

## 06. vim基本操作

**6.1 打开文件**

**vim filename**：打开或新建文件，并将光标置于第一行行首，如果文件不存在，则会新建文件。

打开不存在文件：

![1527561037701](assets/1527561037701.png)

**6.2 编辑文件**

如果通过vi打开一个已经存在的文件，首先进入命令模式，此时输入的任何字符都被视为命令，不能输入内容。

在命令模式输入i

 

**6.3 保存文件**

一定要先退出插入模式(按Esc进入命令模式)，然后(小写状态下)，shift + zz （按住 “shift” + 按两下“z”键），或者（大写状态下：ZZ） 即可保存退出当前文件。

第一步：进入命令模式（ESC）

第二步：shifit + z z

 

## 07. vim实用操作

### 7.1 命令模式下的操作

**1）切换到编辑模式**

| 按键    | 功能                                   |
| :------ | :------------------------------------- |
| i       | 光标位置当前处插入文字                 |
| I       | 光标所在行首插入文字                   |
| o(字母) | 光标下一行插入文字（新行）             |
| O(字母) | 光标上一行插入文字（新行）             |
| a       | 光标位置右边插入文字                   |
| A       | 光标所在行尾插入文字                   |
| s       | 删除光标后边的字符，从光标当前位置插入 |
| S       | 删除光标所在当前行，从行首插入         |

 

**2) 光标移动**

| **按键** | **功能**                             |
| :------- | :----------------------------------- |
| Ctrl + f | 向前滚动一个屏幕                     |
| Ctrl + b | 向后滚动一个屏幕                     |
| gg       | 到文件第一行行首                     |
| G(大写)  | 到文件最后一行行首，G必须为大写      |
| mG或mgg  | 到指定行，m为目标行数                |
| 0(数字)  | 光标移到到行首（第一个字符位置）     |
| $        | 光标移到到行尾                       |
| l(小写L) | 向右移动光标                         |
| h        | 向左移动光标                         |
| k        | 向上移动光标                         |
| j        | 向下移动光标                         |
| ^        | 光标移到到行首（第一个有效字符位置） |

 

**3）复制粘贴**

| **按键** | **功能**                     |
| :------- | :--------------------------- |
| [n]yy    | 复制从当前行开始的 n 行      |
| p        | 把粘贴板上的内容插入到当前行 |

 

**4）删除**

| **按键**    | **功能**                                                     |
| :---------- | :----------------------------------------------------------- |
| [n]x        | 删除光标后 n 个字符                                          |
| [n]X        | 删除光标前 n 个字符                                          |
| D           | 删除光标所在开始到此行尾的字符                               |
| [n]dd       | 删除从当前行开始的 n 行（准确来讲，是剪切，剪切不粘贴即为删除） |
| dG          | 删除光标所在开始到文件尾的所有字符                           |
| dw          | 删除光标开始位置的字,包含光标所在字符                        |
| d0(0为数字) | 删除光标前本行所有内容,不包含光标所在字符                    |
| dgg         | 删除光标所在开始到文件首行第一个字符开始的所有字符           |

 

**5）撤销恢复**

| **按键**  | **功能**            |
| :-------- | :------------------ |
| **.**(点) | 执行上一次操作      |
| u         | 撤销前一个命令      |
| ctrl+r    | 反撤销              |
| 100 + .   | 执行上一次操作100次 |

 

**6）保存退出**

| **按键**      | **功能** |
| :------------ | :------- |
| ZZ(shift+z+z) | 保存退出 |

 

**7）查找**

| **按键** | **功能**                                   |
| :------- | :----------------------------------------- |
| /字符串  | 从当前光标位置向下查找（n，N查找内容切换） |
| ?字符串  | 从当前光标位置向上查找（n，N查找内容切换） |

 

**8）替换**

| **按键** | **功能**                                |
| :------- | :-------------------------------------- |
| r        | 替换当前字符                            |
| R        | 替换当前行光标后的字符(ESC退出替换模式) |

 

**9）可视模式**

| **按键**  | **功能**                                                     |
| :-------- | :----------------------------------------------------------- |
| v         | 按字符移动，选中文本，可配合h、j、k、l选择内容，使用d删除，使用y复制 |
| Shift + v | 行选（以行为单位）选中文本，可配合h、j、k、l选择内容，使用d删除，使用y复制 |
| Ctrl + v  | 列选 选中文本，可配合h、j、k、l选择内容，使用d删除，使用y复制 |

 

### 7.2 末行模式下的操作

**1）保存退出**

| **按键**    | **功能**                                     |
| :---------- | :------------------------------------------- |
| :wq         | 保存退出                                     |
| :x(小写)    | 保存退出                                     |
| :w filename | 保存到指定文件                               |
| :q          | 退出，如果文件修改但没有保存，会提示无法退出 |
| :q!         | 退出，不保存                                 |
|             |                                              |

all 表示所有

**2）替换**

| **按键**         | **功能**                               |
| :--------------- | :------------------------------------- |
| :s/abc/123/      | 光标所在行的第一个abc替换为123         |
| :s/abc/123/g     | 光标所在行的所有abc替换为123           |
| :1,10s/abc/123/g | 将第一行至第10行之间的abc全部替换成123 |
| :%s/abc/123/g    | 当前文件的所有abc替换为123             |
| :%s/abc/123/gc   | 同上，但是每次替换需要用户确认         |
| :1,$s/abc/123/g  | 当前文件的所有abc替换为123             |

 

**3）分屏**

| **按键**           | **功能**                       |
| :----------------- | :----------------------------- |
| :sp                | 当前文件水平分屏               |
| :vsp               | 当前文件垂直分屏               |
| : sp 文件名        | 当前文件和另一个文件水平分屏   |
| : vsp 文件名       | 当前文件和另一个文件垂直分屏   |
| ctrl-w-w           | 在多个窗口切换光标             |
| :wall/:wqall/:qall | 保存/保存退出/退出所有分屏窗口 |
| vim -O a.c b.c     | 垂直分屏                       |
| vim -o a.c b.c     | 水平分屏                       |

 

**4) 其它用法(扩展)**

| 按键                         | 功能                                             |
| :--------------------------- | :----------------------------------------------- |
| :!man 3 printf               | 在vim中执行命令 （q退出）                        |
| :r !ls -l                    | 将ls -l执行的结果写入当前文件中                  |
| :r /etc/passwd               | 将/etc/passwd文件中的内容写入到当前文件中        |
| :w /tmp/txt                  | 将当前文件内容写入到/tmp/txt文件中               |
| :w! /tmp/txt                 | 强制将当前文件内容写入到/tmp/txt文件中           |
| :1,10s/^/\/\//g              | 将第1行到10行行首添加// (^表示行首) /\/\转移字符 |
| :1,10s#^#//#g                | 将第1行到10行行首添加// (#可以临时代替/ 分隔)    |
| :%s/;/\r{\r\treturn0;\r}\r/g | 将;替换成{ return 0; }                           |
| :1,10s#//##g                 | 将第1行到10行行首去掉// (#可以临时代替/ 分隔)    |

 

**5) 配置文件**

局部配置文件（推荐）

> deng@itcast:~/share/2nd$ vim ~/.vimrc

全局配置文件:

> deng@itcast:~/share/2nd$ sudo vim /etc/vim/vimrc

 

## 08. GCC编译器简介

编辑器(如vi、记事本)是指我用它来写程序的（编辑代码），而我们写的代码语句，电脑是不懂的，我们需要把它转成电脑能懂的语句，编译器就是这样的转化工具。就是说，我们用编辑器编写程序，由编译器编译后才可以运行！

编译器是将易于编写、阅读和维护的高级计算机语言翻译为计算机能解读、运行的低级机器语言的程序。

gcc（GNU Compiler Collection，GNU 编译器套件），是由 GNU 开发的编程语言编译器。gcc原本作为GNU操作系统的官方编译器，现已被大多数类Unix操作系统（如Linux、BSD、Mac OS X等）采纳为标准的编译器，gcc同样适用于微软的Windows。

gcc最初用于编译C语言，随着项目的发展gcc已经成为了能够编译C、C++、Java、Ada、fortran、Object C、Object C++、Go语言的编译器大家族。

> 编译命令格式：
>
> gcc [options] file...
>
> g++ [options] file...
>
> - 命令、选项和源文件之间使用空格分隔
> - 一行命令中可以有零个、一个或多个选项
> - 文件名可以包含文件的绝对路径，也可以使用相对路径
> - 如果命令中不包含输出可执行文件的文件名，可执行文件的文件名会自动生成一个默认名，Linux平台为a.out，Windows平台为a.exe

 

## 09. GCC工作流程和常用选项

gcc编译器从拿到一个c源文件到生成一个可执行程序，中间一共经历了四个步骤：

![img](assets/clip_image002.png)

四个步骤并不是gcc独立完成的，而是在内部调用了其他工具，从而完成了整个工作流程：

![img](assets/clip_image002-1527509458588.png)

gcc工作的流程

> deng@itcast:~/share/3rd/1gcc$ ls 1hello.c
>
> 第一步: 进行预处理
>
> deng@itcast:~/share/3rd/1gcc$ gcc -E 1hello.c -o 1hello.i
>
> 第二步: 生成汇编文件
>
> deng@itcast:~/share/3rd/1gcc$ gcc -S 1hello.i -o 1hello.s
>
> 第三步: 生成目标代码
>
> deng@itcast:~/share/3rd/1gcc$ gcc -c 1hello.s -o 1hello.o
>
> 第四步: 生成可以执行文件
>
> deng@itcast:~/share/3rd/1gcc$ gcc 1hello.o -o 1hello 第五步: 执行 deng@itcast:~/share/3rd/1gcc$ ./1hello hello itcast

 

直接将源文件生成一个可以执行文件

> deng@itcast:~/share/3rd/1gcc$ gcc 1hello.c -o 1hello deng@itcast:~/share/3rd/1gcc$ ./1hello hello itcast

如果不指定输出文件名字, gcc编译器会生成一个默认的可以执行a.out

> deng@itcast:~/share/3rd/1gcc$ gcc 1hello.c
> deng@itcast:~/share/3rd/1gcc$ ls 1hello 1hello.c 1hello.i 1hello.o 1hello.s a.out deng@itcast:~/share/3rd/1gcc$ ./a.out
> hello itcast

 

gcc常用选项

| **选项**       | **作用**                   |
| :------------- | :------------------------- |
| -o file        | 指定生成的输出文件名为file |
| -E             | 只进行预处理               |
| -S(大写)       | 只进行预处理和编译         |
| -c(小写)       | 只进行预处理、编译和汇编   |
| -v / --version | 查看gcc版本号              |
| -g             | 包含调试信息               |
| -On n=0~3      | 编译优化，n越大优化得越多  |
| -Wall          | 提示更多警告信息           |
| -D             | 编译时定义宏               |

显示所有的警告信息

> gcc -Wall test.c

将警告信息当做错误处理

> gcc -Wall -Werror test.c

 

测试程序(-D选项)：

```
#include <stdio.h>


int main(void)
{

    printf("SIZE: %d\n", SIZE);

    return 0;
}
```

 

> deng@itcast:~/test$ gcc 2test.c -DSIZE=10
>
> deng@itcast:~/test$ ./a.out
>
> SIZE: 10

 

## 10. 静态连接和动态连接

链接分为两种：**静态链接**、**动态链接**。

**1）静态链接**

静态链接：由链接器在链接时将库的内容加入到可执行程序中。

优点：

- 对运行环境的依赖性较小，具有较好的兼容性

缺点：

- 生成的程序比较大，需要更多的系统资源，在装入内存时会消耗更多的时间
- 库函数有了更新，必须重新编译应用程序

**2）动态链接**

动态链接：连接器在链接时仅仅建立与所需库函数的之间的链接关系，在程序运行时才将所需资源调入可执行程序。

优点：

- 在需要的时候才会调入对应的资源函数
- 简化程序的升级；有着较小的程序体积
- 实现进程之间的资源共享（避免重复拷贝）

缺点：

- 依赖动态库，不能独立运行
- 动态库依赖版本问题严重

**3）静态、动态编译对比**

前面我们编写的应用程序大量用到了标准库函数，系统默认采用动态链接的方式进行编译程序，若想采用静态编译，加入-static参数。

以下是分别采用动态编译、静态编译时文件对比：

测试程序(test.c)如下：

```
#include <stdio.h>

int main(void)
{
    printf("hello world\n");

    return 0;
}
```

编译：

> deng@itcast:~/test$ gcc test.c -o test_share
>
> deng@itcast:~/test$ gcc -static test.c -o test_static

结果对比：

![1527510332615](assets/1527510332615.png)

参考博客：[静态链接库与动态链接库](https://blog.csdn.net/freestyle4568world/article/details/49817799)

 

## 11. 静态库和动态库简介

所谓“程序库”，简单说，就是包含了数据和执行码的文件。其不能单独执行，可以作为其它执行程序的一部分来完成某些功能。

库的存在可以使得程序模块化，可以加快程序的再编译，可以实现代码重用,可以使得程序便于升级。

程序库可分**静态库(static library)**和**共享库(shared library)**。

 

## 12. 静态库制作和使用

静态库可以认为是一些目标代码的集合，是在可执行程序运行前就已经加入到执行码中，成为执行程序的一部分。

按照习惯,一般以“.a”做为文件后缀名。静态库的命名一般分为三个部分：

- 前缀：lib
- 库名称：自己定义即可
- 后缀：.a

所以最终的静态库的名字应该为：**libxxx.a**

**1） 静态库制作**

![img](assets/clip_image002-1527510689190.jpg)

步骤1：将c源文件生成对应的.o文件

> deng@itcast:~/test/3static_lib$ gcc -c add.c -o add.o
> deng@itcast:~/test/3static_lib$ gcc -c sub.c -o sub.o deng@itcast:~/test/3static_lib$ gcc -c mul.c -o mul.o deng@itcast:~/test/3static_lib$ gcc -c div.c -o div.o

步骤2：使用打包工具ar将准备好的.o文件打包为.a文件 libtest.a

> deng@itcast:~/test/3static_lib$ ar -rcs libtest.a add.o sub.o mul.o div.o

**在使用ar工具是时候需要添加参数：rcs**

- r更新
- c创建
- s建立索引

 

**2）静态库使用**

静态库制作完成之后，需要将.a文件和头文件一起发布给用户。

假设测试文件为main.c，静态库文件为libtest.a头文件为head.h

编译命令：

> deng@itcast:~/test/4static_test$ gcc test.c -L./ -I./ -ltest -o test

参数说明：

- -L：表示要连接的库所在目录
- -I./: I(大写i) 表示指定头文件的目录为当前目录
- -l(小写L)：指定链接时需要的库，去掉前缀和后缀

![img](assets/clip_image002-1527510920275.jpg)

## 13. 动态库制作和使用

共享库在程序编译时并不会被连接到目标代码中，而是在程序运行是才被载入。不同的应用程序如果调用相同的库，那么在内存里只需要有一份该共享库的实例，规避了空间浪费问题。

动态库在程序运行是才被载入，也解决了静态库对程序的更新、部署和发布页会带来麻烦。用户只需要更新动态库即可，增量更新。

按照习惯,一般以“.so”做为文件后缀名。共享库的命名一般分为三个部分：

- 前缀：lib
- 库名称：自己定义即可
- 后缀：.so

所以最终的动态库的名字应该为：libxxx.so

![img](assets/clip_image002-1527511145606.jpg)

 

**1）动态库制作**

步骤一：生成目标文件，此时要加编译选项：-fPIC（fpic）

> deng@itcast:~/test/5share_lib$ gcc -fPIC -c add.c
> deng@itcast:~/test/5share_lib$ gcc -fPIC -c sub.c deng@itcast:~/test/5share_lib$ gcc -fPIC -c mul.c deng@itcast:~/test/5share_lib$ gcc -fPIC -c div.c

参数：-fPIC 创建与地址无关的编译程序（pic，position independent code），是为了能够在多个应用程序间共享。

步骤二：生成共享库，此时要加链接器选项: -shared（指定生成动态链接库）

> deng@itcast:~/test/5share_lib$ gcc -shared add.o sub.o mul.o div.o -o libtest.so

步骤三: 通过nm命令查看对应的函数

> deng@itcast:~/test/5share_lib$ nm libtest.so | grep add 00000000000006b0 T add deng@itcast:~/test/5share_lib$ nm libtest.so | grep sub 00000000000006c4 T sub

 

ldd查看可执行文件的依赖的动态库

> deng@itcast:~/share/3rd/2share_test$ ldd test linux-vdso.so.1 => (0x00007ffcf89d4000) libtest.so => /lib/libtest.so (0x00007f81b5612000) libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f81b5248000) /lib64/ld-linux-x86-64.so.2 (0x00005562d0cff000)

**2）动态库测试**

引用动态库编译成可执行文件（跟静态库方式一样）

> deng@itcast:~/test/6share_test$ gcc test.c -L. -I. -ltest (-I. 大写i -ltest 小写L)

然后运行：./a.out，发现竟然报错了！！！

![1527582099959](assets/1527582099959.png)

- 当系统加载可执行代码时候，能够知道其所依赖的库的名字，但是还需要知道绝对路径。此时就需要系统动态载入器(dynamic linker/loader)。
- 对于elf格式的可执行程序，是由ld-linux.so*来完成的，它先后搜索elf文件的 DT_RPATH段 — 环境变量LD_LIBRARY_PATH — /etc/ld.so.cache文件列表 — **/lib/, /usr/lib**目录找到库文件后将其载入内存。

 

**3）如何让系统找到动态库**

- 拷贝自己制作的共享库到/lib或者/usr/lib(不能是/lib64目录)
- 临时设置LD_LIBRARY_PATH：

> export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:库路径

- 永久设置,把export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:库路径，设置到~/.bashrc或者 /etc/profile文件中

  > deng@itcast:~/share/3rd/2share_test$ vim ~/.bashrc
  >
  > 最后一行添加如下内容:
  >
  > export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/deng/share/3rd/2share_test

  使环境变量生效

  > deng@itcast:~/share/3rd/2share_test$ source ~/.bashrc deng@itcast:~/share/3rd/2share_test$ ./test
  > a + b = 20 a - b = 10

- 将其添加到 /etc/ld.so.conf文件中

  编辑/etc/ld.so.conf文件，加入库文件所在目录的路径

  运行sudo ldconfig -v，该命令会重建/etc/ld.so.cache文件

  > deng@itcast:~/share/3rd/2share_test$ sudo vim /etc/ld.so.conf
  >
  > 文件最后添加动态库路径(绝对路径)

  ![1539308885923](assets/1539308885923.png)

  > 使生效
  >
  > deng@itcast:~/share/3rd/2share_test$ sudo ldconfig -v

- 使用符号链接， 但是一定要使用绝对路径

  deng@itcast:~/test/6share_test$ sudo ln -s /home/deng/test/6share_test/libtest.so /lib/libtest.so

 

## 14. GDB调试器

### 14.1 GDB简介

GNU工具集中的调试器是GDB（GNU Debugger），该程序是一个交互式工具，工作在字符模式。

除gdb外，linux下比较有名的调试器还有xxgdb, ddd, kgdb, ups。



GDB主要帮忙你完成下面四个方面的功能：

1. 启动程序，可以按照你的自定义的要求随心所欲的运行程序。
2. 可让被调试的程序在你所指定的调置的断点处停住。（断点可以是条件表达式）
3. 当程序被停住时，可以检查此时你的程序中所发生的事。
4. 动态的改变你程序的执行环境。

 

### 14.2 生成调试信息

一般来说GDB主要调试的是C/C++的程序。要调试C/C++的程序，首先在编译时，我们必须要把调试信息加到可执行文件中。使用编译器（cc/gcc/g++）的 -g 参数可以做到这一点。如：

> gcc -g hello.c -o hello
>
> g++ -g hello.cpp -o hello

如果没有-g，你将看不见程序的函数名、变量名，所代替的全是运行时的内存地址。

 

### 14.3 启动GDB

- 启动gdb：gdb program

  program 也就是你的执行文件，一般在当前目录下。



- 设置运行参数

  set args 可指定运行时参数。（如：set args 10 20 30 40 50 ）

  show args 命令可以查看设置好的运行参数。



- 启动程序

  run： 程序开始执行，如果有断点，停在第一个断点处

  start： 程序向下执行一行。

### 14.3 显示源代码

用list命令来打印程序的源代码。默认打印10行。

Ø list linenum： 打印第linenm行的上下文内容.

Ø list function： 显示函数名为function的函数的源程序。

Ø list： 显示当前行后面的源程序。

Ø list -： 显示当前行前面的源程序。



一般是打印当前行的上5行和下5行，如果显示函数是是上2行下8行，默认是10行，当然，你也可以定制显示的范围，使用下面命令可以设置一次显示源程序的行数。

Ø set listsize count：设置一次显示源代码的行数。

Ø show listsize： 查看当前listsize的设置。

### 14.4 断点操作

**1）简单断点**

break 设置断点，可以简写为b

Ø b 10 设置断点，在源程序第10行

Ø b func 设置断点，在func函数入口处

 

**2）多文件设置断点**

C++中可以使用class::function或function(type,type)格式来指定函数名。

如果有名称空间，可以使用namespace::class::function或者function(type,type)格式来指定函数名。

Ø break filename:linenum -- 在源文件filename的linenum行处停住

Ø break filename:function -- 在源文件filename的function函数的入口处停住

Ø break class::function或function(type,type) -- 在类class的function函数的入口处停住

Ø break namespace::class::function -- 在名称空间为namespace的类class的function函数的入口处停住

**3）查询所有断点**

- info b
- info break
- i break
- i b

### 14.5 条件断点

一般来说，为断点设置一个条件，我们使用if关键词，后面跟其断点条件。

设置一个条件断点：

> b test.c:8 if Value == 5

 

### 14.6 维护断点

1）delete [range...] 删除指定的断点，其简写命令为d。

- 如果不指定断点号，则表示删除所有的断点。range表示断点号的范围（如：3-7）。
- 比删除更好的一种方法是disable停止点，disable了的停止点，GDB不会删除，当你还需要时，enable即可，就好像回收站一样。

2） disable [range...] 使指定断点无效，简写命令是dis。

如果什么都不指定，表示disable所有的停止点。

3） enable [range...] 使无效断点生效，简写命令是ena。

如果什么都不指定，表示enable所有的停止点。

 

### 14.7 调试代码

- run 运行程序，可简写为r
- next 单步跟踪，函数调用当作一条简单语句执行，可简写为n
- step 单步跟踪，函数调进入被调用函数体内，可简写为s
- finish 退出进入的函数
- until 在一个循环体内单步跟踪时，这个命令可以运行程序直到退出循环体,可简写为u。
- continue 继续运行程序，停在下一个断点的位置，可简写为c
- quit 退出gdb，可简写为q

 

### 14.8 数据查看

1）查看运行时数据

print 打印变量、字符串、表达式等的值，可简写为p

p count 打印count的值

 

### 14.9 自动显示

你可以**设置一些自动显示的变量**，当程序停住时，或是在你单步跟踪时，这些变量会自动显示。相关的GDB命令是display。

- display 变量名
- info display -- 查看display设置的自动显示的信息。
- undisplay num（info display时显示的编号）
- delete display dnums… -- 删除自动显示，dnums意为所设置好了的自动显式的编号。如果要同时删除几个，编号可以用空格分隔，如果要删除一个范围内的编号，可以用减号表示（如：2-5）
- disable display dnums…
- enable display dnums…
- disable和enalbe不删除自动显示的设置，而只是让其失效和恢复。



### 14.10 查看修改变量的值

1）ptype width -- 查看变量width的类型

type = double

2）p width -- 打印变量width 的值

$4 = 13

你可以使用set var命令来告诉GDB，width不是你GDB的参数，而是程序的变量名，如：

set var width=47 // 将变量var值设置为47

**在你改变程序变量取值时，最好都使用set var格式的GDB命令**

第3天：
	文件IO常用函数、文件读写原理、进程控制块概念、阻塞、非阻塞概念

第4天：
	文件操作常用函数、目录操作常用函数、重定向

第5天：
	进程控制fork、exec函数族、进程回收wait/waitpid

第6天：
	进程间通信pipe、fifo、mmap

第7天：
	信号集操作函数、信号捕捉、守护进程

第8天：
	线程基本操作、线程回收、线程分离、线程属性修改(了解)

第9天：
	线程同步 [互斥量、读写锁、信号量]、生产者消费者模型

#  学习目标

- 掌握目录遍历相关的函数使用
- 了解进程相关的概念
- 掌握fork/getpid/getppid函数的使用
- 熟练掌握ps/kill命令的使用
- 熟练掌握execl/execlp函数的使用
- 说出什么是孤儿进程和僵尸进程

## 进程和程序 (理解)

程序是存放在存储介质上的一个**可执行文件**，而进程是**程序执行的过程**。进程的状态是变化的，其包括进程的创建、调度和消亡。程序是静态的，进程是动态的。

![1527992375886](file:///C:/Users/12964/Desktop/%E7%AC%AC4%E9%98%B6%E6%AE%B5-Linux%E9%AB%98%E5%B9%B6%E5%8F%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%BC%80%E5%8F%91/Linux%E7%B3%BB%E7%BB%9F%E7%BC%96%E7%A8%8B/Linux%E7%B3%BB%E7%BB%9F%E7%BC%96%E7%A8%8B-%E7%AC%AC05%E5%A4%A9%EF%BC%88%E8%BF%9B%E7%A8%8B%E6%8E%A7%E5%88%B6%EF%BC%89/1-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1527992375886.png)

系统是通过进程去完成一个一个的任务，**进程是管理事务的基本单元。**

进程拥有自己独立的**处理环境**和**系统资源**

## 单道、多道程序设计(了解)

###  单道程序设计

所有进程一个一个排队执行。若A阻塞，B只能等待

### 多道程序设计

相互独立的程序，在管理程序控制之下，相互穿插的运行

在计算机中**时钟中断**即为多道程序设计模型的理论基础。常见CPU为纳秒级，1秒可以执行约10亿条指令

> 1s = 1000ms
>
> 1ms = 1000us
>
> 1us = 1000ns
>
> 1s = 1000000000ns

## 并行和并发(理解)

**并行(parallel)：**指在同一时刻，有多条指令在多个处理器上同时执行。

![1527906658917](file:///C:/Users/12964/Desktop/%E7%AC%AC4%E9%98%B6%E6%AE%B5-Linux%E9%AB%98%E5%B9%B6%E5%8F%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%BC%80%E5%8F%91/Linux%E7%B3%BB%E7%BB%9F%E7%BC%96%E7%A8%8B/Linux%E7%B3%BB%E7%BB%9F%E7%BC%96%E7%A8%8B-%E7%AC%AC05%E5%A4%A9%EF%BC%88%E8%BF%9B%E7%A8%8B%E6%8E%A7%E5%88%B6%EF%BC%89/1-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1527906658917.png)

**并发(concurrency)：**指在同一时刻只能有一条指令执行，但多个进程指令被快速的轮换执行，使得在宏观上具有多个进程同时执行的效果，但在微观上并不是同时执行的，只是把时间分成若干段，使多个进程快速交替的执行。

 ![1527906748430](file:///C:/Users/12964/Desktop/%E7%AC%AC4%E9%98%B6%E6%AE%B5-Linux%E9%AB%98%E5%B9%B6%E5%8F%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%BC%80%E5%8F%91/Linux%E7%B3%BB%E7%BB%9F%E7%BC%96%E7%A8%8B/Linux%E7%B3%BB%E7%BB%9F%E7%BC%96%E7%A8%8B-%E7%AC%AC05%E5%A4%A9%EF%BC%88%E8%BF%9B%E7%A8%8B%E6%8E%A7%E5%88%B6%EF%BC%89/1-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1527906748430.png)

- 并行是两个队列**同时**使用两台咖啡机
- 并发是两个队列**交替**使用一台咖啡机

## MMU(了解)

MMU是Memory Management Unit的缩写，中文名是**内存管理**单元，它是[**中央处理器**](https://baike.baidu.com/item/中央处理器)（CPU）中用来管理[虚拟存储器](https://baike.baidu.com/item/虚拟存储器)、物理存储器的控制线路，同时也负责[虚拟地址](https://baike.baidu.com/item/虚拟地址)映射为[物理地址](https://baike.baidu.com/item/物理地址)，以及提供硬件机制的内存访问授权，多用户多进程操作系统。

![1527907116958](file:///C:/Users/12964/Desktop/%E7%AC%AC4%E9%98%B6%E6%AE%B5-Linux%E9%AB%98%E5%B9%B6%E5%8F%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%BC%80%E5%8F%91/Linux%E7%B3%BB%E7%BB%9F%E7%BC%96%E7%A8%8B/Linux%E7%B3%BB%E7%BB%9F%E7%BC%96%E7%A8%8B-%E7%AC%AC05%E5%A4%A9%EF%BC%88%E8%BF%9B%E7%A8%8B%E6%8E%A7%E5%88%B6%EF%BC%89/1-%E6%95%99%E5%AD%A6%E8%B5%84%E6%96%99/assets/1527907116958.png)

## 进程控制块PCB(了解)

进程运行时，内核为进程每个进程分配一个**PCB**（进程控制块），维护进程相关的信息，Linux内核的进程控制块是task_struct结构体。

在 /usr/src/linux-headers-xxx/include/linux/sched.h 文件中可以查看struct task_struct 结构体定义：

> deng@itcast:~/share$ vim /usr/src/linux-headers-4.10.0-28/include/linux/sched.h
>
> ![image-20240419172127714](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\image-20240419172127714.png)

其内部成员有很多，我们掌握以下部分即可：

- 进程id。每个进程有唯一的id，在C语言中用**pid_t**类型表示，其实就是一个非负整数。
- 进程的状态，有**就绪、运行、挂起、停止**等状态。
- 进程切换时需要**保存和恢复**的一些CPU寄存器。
- 描述虚拟地址空间的信息。//mmu
- 描述控制终端的信息。
- 当前工作目录（Current Working Directory）。
- umask掩码
- 文件描述符表，包含很多指向file结构体的指针。
- 和信号相关的信息
- 用户id和组id
- 会话（Session）和进程组
- 进程可使用资源上限（Resource Limit）

## 进程的状态(重点)

进程状态反映进程执行过程的变化。这些状态随着进程的执行和外界条件的变化而转换。

在三态模型中，进程状态分为三个基本状态，即**运行态，就绪态，阻塞态**。

在五态模型中，进程分为**新建态、终止态，运行态，就绪态，阻塞态**。

![1527908066890](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\1527908066890.png)

**①TASK_RUNNING：**进程正在被CPU执行。当一个进程刚被创建时会处于TASK_RUNNABLE，表示己经准备就绪，正等待被调度。

**②TASK_INTERRUPTIBLE（可中断）：**进程正在睡眠（也就是说它被阻塞）等待某些条件的达成。一旦这些条件达成，内核就会把进程状态设置为运行。处于**此状态的进程也会因为接收到信号而提前被唤醒**，**比如给一个TASK_INTERRUPTIBLE状态的进程发送SIGKILL信号，这个进程将先被唤醒（进入TASK_RUNNABLE状态），然后再响应SIGKILL信号而退出**（变为TASK_ZOMBIE状态），并不会从TASK_INTERRUPTIBLE状态直接退出。

**③TASK_UNINTERRUPTIBLE（不可中断）：**处于等待中的进程，待资源满足时被唤醒，**但不可以由其它进程通过信号或中断唤醒**。由于不接受外来的任何信号，**因此无法用kill杀掉这些处于该状态的进程**。而**TASK_UNINTERRUPTIBLE状态存在的意义就在于**，**内核的某些处理流程是不能被打断的**。如果响应异步信号，程序的执行流程中就会被插入一段用于处理异步信号的流程，于是原有的流程就被中断了，这可能使某些设备陷入不可控的状态。处于TASK_UNINTERRUPTIBLE状态一般总是非常短暂的，通过ps命令基本上不可能捕捉到。

**④TASK_ZOMBIE（僵死）：**表示进程已经结束了，**但是其父进程还没有调用wait4或waitpid()来释放进程描述符**。为了父进程能够获知它的消息，子进程的进程描述符仍然被保留着。一旦父进程调用了wait4()，进程描述符就会被释放。

**⑤TASK_STOPPED（停止）：**进程停止执行。当进程接收到SIGSTOP，SIGTSTP，SIGTTIN，SIGTTOU等信号的时候。此外，**在调试期间接收到任何信号**，都会使进程进入这种状态。**当接收到SIGCONT信号，会重新回到TASK_RUNNABLE**。

如何查看进程状态：

![1527994562159](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\1527994562159.png)

stat中的参数意义如下：

| **参数** | **含义**                               |
| :------- | :------------------------------------- |
| D        | 不可中断 Uninterruptible（usually IO） |
| R        | 正在运行，或在队列中的进程             |
| S(大写)  | 处于休眠状态                           |
| T        | 停止或被追踪                           |
| Z        | 僵尸进程                               |
| W        | 进入内存交换（从内核2.6开始无效）      |
| X        | 死掉的进程                             |
| <        | 高优先级                               |
| N        | 低优先级                               |
| s        | 包含子进程                             |
| +        | 位于前台的进程组                       |

### ps

进程是一个具有一定独立功能的程序，它是**操作系统动态执行的基本单元**

ps命令可以查看进程的详细状况，

| **选项** | **含义**                                 |
| :------- | :--------------------------------------- |
| -a       | 显示终端上的所有进程，包括其他用户的进程 |
| -u       | 显示进程的详细状态                       |
| -x       | 显示没有控制终端的进程                   |
| -w       | 显示加宽，以便显示更多的信息             |
| -r       | 只显示正在运行的进程                     |

ps aux

ps ef

ps -a

![2016-05-29_230200](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\clip_image002-1527436564167.jpg)

###  top

top命令用来**动态显示运行中的进程**,指定的时间间隔更新显示信息

在top命令执行后，可以按下按键得到对显示的结果进行排序：

| **按键** | **含义**                           |
| :------- | :--------------------------------- |
| M        | 根据内存使用量来排序               |
| P        | 根据CPU占有率来排序                |
| T        | 根据进程运行时间的长短来排序       |
| U        | 可以根据后面输入的用户名来筛选进程 |
| K        | 可以根据后面输入的PID来杀死进程。  |
| q        | 退出                               |
| h        | 获得帮助                           |

![2016-05-29_231626](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\clip_image002-1527436598410.jpg)

### kill

kill命令指定进程号的进程，需要配合 ps 使用。

使用格式：

kill [-signal] pid

信号值从0到15，其中9为绝对终止，可以处理一般信号无法终止的进程。

**kill 9133** ：9133 为应用程序所对应的进程号

![20150318112100659](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\clip_image002-1527436647473.jpg)

有些进程不能直接杀死，这时候我们需要加一个参数“ -9 ”，“ -9 ” 代表强制结束：

![20150318112401325](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\clip_image002-1527436664857.jpg)

###  killall

通过进程名字杀死进程

![1527498996963](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\1527498996963.png)

## 进程号和相关函数

每个进程由进程号来标识，其类型为 **pid_t（整型）**，进程号的范围：0～32767。唯一的，但可以重用

接下来，再给大家介绍三个不同的进程号。

**进程号（PID）**：标识进程的一个非负整型数。

**父进程号（PPID）**：任何进程（ 除 init (调用main函数)进程）都是由另一个进程创建

**进程组号（PGID）**：进程组是一个或多个进程的集合。进程组可以接收同一终端的各种信号，关联的进程有一个进程组号（PGID） 。类似于 QQ 群，当前的进程号会当做当前的进程组号

头文件：

```c
#include <sys/types.h>
#include <unistd.h>
```

### getpid函数

```c
pid_t getpid(void);//功能：获取本进程号（PID）
//参数：无
//返回值：本进程号
```

###  getppid函数

```c
pid_t getppid(void);//功能：获取调用此函数的进程的父进程号（PPID）
//返回值：调用此函数的进程的父进程号（PPID）
```

###  getpgid函数

```c
pid_t getpgid(pid_t pid);
//功能：获取进程组号（PGID）
//参数：pid：进程号
//返回值：参数为 0 时返回当前进程组号，否则返回参数指定的进程的进程组号
```

示例程序:

```
int main()
{
    pid_t pid, ppid, pgid;
    pid = getpid();
    printf("pid = %d\n", pid);
    ppid = getppid();
    printf("ppid = %d\n", ppid);
    pgid = getpgid(pid);
    printf("pgid = %d\n", pgid);
    return 0;
}
```

![1527995537071](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\1527995537071.png)

##  进程的创建（重点）

允许一个进程创建子进程（新进程），子进程可再创建新子进程，形成进程树结构模型

```c
#include <sys/types.h>
#include <unistd.h>
pid_t fork(void);
//功能：用于从一个已存在的进程中创建一个新进程
//参数：无
//返回值：成功：子进程中返回 0，父进程中返回子进程 ID。pi
//   失败：返回-1。
//   失败的两个主要原因是：
//        1）当前的进程数已经达到了系统规定的上限，这时 errno 的值被设置为 EAGAIN。
//        2）系统内存不足，这时 errno 的值被设置为 ENOMEM。
```

**示例代码：**

```
int main()
{
    fork();
    printf("id ==== %d\n", getpid());   // 获取进程号  
    return 0;
}
```

**运行结果如下：**

![1527909102449](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\1527909102449.png)

从运行结果，我们可以看出，fork() 之后的打印函数打印了两次，而且打印了两个进程号，这说明，fork() 之后确实创建了一个新的进程

##  父子进程关系

fork() 函数得到的子进程是父进程的一个复制品，它继承了父进程整个进程的地址空间：包括进程上下文（进程执行活动全过程的静态描述）、进程堆栈、打开的文件描述符、信号控制设定、进程优先级、进程组号等。

子进程所独有的只有它的进程号，计时器等（只有小量信息）。因此，使用 fork() 函数的代价是很大的。

![1527909236123](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\1527909236123.png)

一个进程调用 fork() 函数后，系统先新的进程分配资源，例如存储数据和代码的空间。然后把原来的进程的所有值都复制到新的新进程中，只有少数值与原来的进程的值不同。相当于克隆了一个自己。

Linux 的 fork() 使用是通过写时拷贝 (copy- on-write) 实现。写时拷贝是一种可以推迟甚至避免拷贝数据的技术。内核此时并不复制整个进程的地址空间，而是让父子进程共享同一个地址空间。只用在需要写入的时候才会复制地址空间，从而使各个进行拥有各自的地址空间。也就是说，资源的复制是在需要写入的时候才会进行，在此之前，只有以只读方式共享。

**fork之后父子进程共享文件，fork产生的子进程与父进程相同的文件文件描述符指向相同的文件表，引用计数增加，共享文件文件偏移指针。** 

##  区分父子进程

通过 fork() 的返回值，区别父子进程

fork() 函数被调用一次，但返回两次。两次返回的区别是：子进程返回 0，父进程返回新子进程的进程 ID

**测试程序：**

```
int main()
{
    pid_t pid;
    pid = fork();
    if (pid < 0)
    {   // 没有创建成功  
        perror("fork");
        return 0;
    }
    if (0 == pid)
    { // 子进程  
        while (1)
        {
            printf("I am son\n");
            sleep(1);
        }
    }
    else if (pid > 0)
    { // 父进程  
        while (1)
        {
            printf("I am father\n");
            sleep(1);
        }
    }

    return 0;
}

```

运行结果如下：

![1527909577065](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\1527909577065.png)

父子进程各做一件事（各自打印一句话）。我们只是看到只有一份代码，实际上，fork() 以后，有两个地址空间在独立运行着，有点类似于有两个独立的程序（父子进程）在运行着。

> - 在 fork() 之后是父进程先执行还是子进程先执行是不确定的。这取决于内核所使用的调度算法。
> - 在子进程的地址空间里，子进程是从 fork() 这个函数后才开始执行代码。

## 父子进程地址空间

父子进程各自的地址空间是独立的

```
int a = 10;     // 全局变量

int main()
{
    int b = 20; //局部变量
    pid_t pid;
    pid = fork();
    if (pid < 0)
    {   // 没有创建成功
        perror("fork");
    }

    if (0 == pid)
    { // 子进程
        a = 111;
        b = 222;    // 子进程修改其值
        printf("son: a = %d, b = %d\n", a, b);
    }
    else if (pid > 0)
    { // 父进程
        sleep(1);   // 保证子进程先运行
        printf("father: a = %d, b = %d\n", a, b);
    }

    return 0;
}

```

运行结果如下：

通过得知，在子进程修改变量 a，b 的值，并不影响到父进程 a，b 的值。

## 进程相关命令

### ps命令

ps命令可以查看进程的详细状况，常用选项(选项可以不加“-”)如下：

| **选项** | **含义**                                 |
| :------- | :--------------------------------------- |
| -a       | 显示终端上的所有进程，包括其他用户的进程 |
| -u       | 显示进程的详细状态                       |
| -x       | 显示没有控制终端的进程                   |
| -j       | 列出与作业控制相关的信息                 |

显示当前用户下所有进程：**ps aux**

以比较完整的格式显示所有的进程：ps ajx

###  kill命令

命令功能: 发送指定的信号到相应进程。

查看信号编号: kill -l(字母)

![1527909976012](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\1527909976012.png)

有些进程不能直接杀死，这时候我们需要加一个参数“-9”，使用9号信号SIGKILL

杀死进程: kill -SIGKILL/(-9) 89899【进程标识号】

## GDB调试多进程

使用gdb调试的时候，gdb只能跟踪一个进程。可以在fork函数调用之前，通过指令设置gdb调试工具跟踪父进程或者是跟踪子进程。默认跟踪父进程。（**在fork函数调用之前设置**）

- set follow-fork-mode child 设置gdb在fork之后跟踪子进程。
- set follow-fork-mode parent 设置跟踪父进程（默认）。

##  进程退出函数

```c
#include <stdlib.h>
void exit(int status);

#include <unistd.h>
void _exit(int status);
功能：结束调用此函数的进程。
参数：status：返回给父进程的参数（低 8 位有效），至于这个参数是多少根据需要来填写。
返回值：无
```

exit() 和 _exit() 函数功能和用法是一样的，无非时所包含的头文件不一样，还有的区别就是：exit()属于标准库函数，_exit()属于系统调用函数。

![1527910170715](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\1527910170715.png)

## 等待子进程退出函数

### 概述

在每个进程退出的时候，内核释放该进程所有的资源、包括打开的文件、占用的内存等。但是仍然为其保留一定的信息，这些信息主要主要指进程控制块PCB的信息（包括进程号、退出状态、运行时间等）。

父进程可以通过调用wait或waitpid得到它的退出状态同时彻底清除掉这个进程。

wait() 和 waitpid() 函数的功能一样，区别在于，wait() 函数会阻塞，waitpid() 可以设置不阻塞，waitpid() 还可以指定等待哪个子进程结束。

注意：**一次wait或waitpid调用只能清理一个子进程，清理多个子进程应使用循环。**

###  wait函数

```
#include <sys/types.h>
#include <sys/wait.h>

pid_t wait(int *status);
功能：等待任意一个子进程结束，如果任意一个子进程结束了，此函数会回收该子进程的资源。
参数：status : 进程退出时的状态信息。
返回值：成功：已经结束子进程的进程号
      失败： -1
```

调用 wait() 函数的进程会**挂起（阻塞）**，直到它的一个子进程退出或收到一个不能被忽视的信号时才被唤醒(相当于继续往下执行)

若调用进程没有子进程，该函数立即返回；若它的子进程已经结束，该函数同样会立即返回，并且会回收那个早已结束进程的资源。

所以，wait()函数的主要功能为**回收已经结束子进程的资源**

如果参数 status 的值不是 NULL，wait() 就会把子进程退出时的状态取出并存入其中，这是一个整数值（int），指出了子进程是**正常退出还是被非正常结束的**。

这个退出信息在一个 int 中包含了多个字段，直接使用这个值是没有意义的，我们需要用宏定义取出其中的每个字段。

**宏函数可分为如下三组：**

1) WIFEXITED(status)为非0 → 进程正常结束

WEXITSTATUS(status)如上宏为真，使用此宏 → 获取进程退出状态 (exit的参数)

2) WIFSIGNALED(status)为非0 → 进程异常终止

WTERMSIG(status)如上宏为真，使用此宏 → 取得使进程终止的那个信号的编号。

3) WIFSTOPPED(status)为非0 → 进程处于暂停状态

WSTOPSIG(status)如上宏为真，使用此宏 → 取得使进程暂停的那个信号的编号。

WIFCONTINUED(status)为真 → 进程暂停后已经继续运行

### waitpid函数

```c++
#include <sys/types.h>
#include <sys/wait.h>

pid_t waitpid(pid_t pid, int *status, int options);
//功能：等待子进程终止，如果子进程终止了，此函数会回收子进程的资源。
参数：
    pid : 参数 pid 的值有以下几种类型：
      pid > 0  等待进程 ID 等于 pid 的子进程。
      pid = 0  等待同一个进程组中的任何子进程，如果子进程已经加入了别的进程组，waitpid 不会等待它。
      pid = -1 等待任意子进程，此时 waitpid 和 wait 作用一样。
      pid < -1 等待指定进程组中的任何子进程，这个进程组的 ID 等于 pid 的绝对值。
    status : 进程退出时的状态信息。和 wait() 用法一样。
    options : options 提供了一些额外的选项来控制 waitpid()。
            0：同 wait()，阻塞父进程，等待子进程退出。
            WNOHANG：没有任何已经结束的子进程，则立即返回。
            WUNTRACED：如果子进程暂停了则此函数马上返回，并且不予以理会子进程的结束状态。
返回值：
    waitpid() 的返回值比 wait() 稍微复杂一些，一共有 3 种情况：
        1) 当正常返回的时候，waitpid() 返回收集到的已经回收子进程的进程号；
        2) 如果设置了选项 WNOHANG，而调用中 waitpid() 发现没有已退出的子进程可等待，则返回 0；
        3) 如果调用中出错，则返回-1，这时 errno 会被设置成相应的值以指示错误所在，如：当 pid 所对应的子进程不存在，或此进程存在，但不是调用进程的子进程，waitpid() 就会出错返回，这时 errno 被设置为 ECHILD；
```

##  孤儿进程

**父进程运行结束**，但子进程还在运行（未运行结束）的子进程就称为孤儿进程（Orphan Process）。

每当出现一个孤儿进程的时候，内核就把孤儿进程的**父进程设置为 init** ，而 **init 进程会循环地 wait() 它的已经退出的子进程**。这样，当一个孤儿进程凄凉地结束了其生命周期的时候，init 进程就会处理它的一切善后工作。孤儿进程并不会有什么危害。

## 僵尸进程

**进程终止，父进程尚未回收**，子进程残留资源（PCB）存放于内核中，变成僵尸（Zombie）进程。

即如果进程不调用wait() 或 waitpid() 的话， 那么保留的那段信息就不会释放，其进程号就会一直被占用，但是系统所能使用的进程号是有限的，如果大量的产生僵尸进程，将因为没有可用的进程号而导致系统不能产生新的进程

##  进程替换

**概述**

如果我们本来就运行着一个程序（进程），我们如何在这个**进程内部启动一个外部程序**，由**内核将这个外部程序读入内存**，使其执行起来成为一个进程呢？这里我们通过 exec 函数族实现。

exec 指的是一组函数，并不存在 exec() 函数，一共有 6 个：

```c
#include <unistd.h>
extern char **environ;

int execl(const char *path, const char *arg, .../* (char  *) NULL */);
int execlp(const char *file, const char *arg, ... /* (char  *) NULL */);
int execle(const char *path, const char *arg, .../*, (char *) NULL, char * const envp[] */);
int execv(const char *path, char *const argv[]);
int execvp(const char *file, char *const argv[]);
int execvpe(const char *file, char *const argv[], char *const envp[]);
int execve(const char *filename, char *const argv[], char *const envp[]);
```

其中只有 **execve() 是真正意义上的系统调用**，其它都是在此基础上经过包装的库函数。

exec 函数族的作用是**根据指定的文件名或目录名找到可执行文件**，并用它来取代调用进程的内容，换句话说，就是**在调用进程内部执行一个可执行文件**。

进程调用一种 exec 函数时，**该进程完全由新程序替换**，而新程序则从其 main 函数开始执行。因为调用 exec 并不创建新进程，所以前后的进程 ID （当然还有父进程号、进程组号、当前工作目录……）并未改变。exec 只是用另一个新程序替换了当前进程的正文、数据、堆和栈段（进程替换）。

![1527922959390](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\1527922959390.png)

**exec 函数族使用说明**

![1527923035885](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\1527923035885.png)

补充说明：

| l(list)        | 参数地址列表，以空指针结尾               |
| :------------- | :--------------------------------------- |
| v(vector)      | 存有各参数地址的指针数组的地址           |
| p(path)        | 按 PATH 环境变量指定的目录搜索可执行文件 |
| e(environment) | 存有环境变量字符串地址的指针数组的地址   |

exec 函数族中的函数**执行成功后不会返回**，而且，**exec 函数族下面的代码执行不到**。

调用失败，返回 -1，失败后从原程序的调用点接着往下执行。

##  源码包安装(扩展)

**第一步**：生成Makefile和检测当前环境

> deng@itcast:~/tools/valgrind-3.13.0 sudo ./configure

**第二步:** 编译源码 生成可执行文件

> deng@itcast:~/tools/valgrind-3.13.0$ sudo make -j4

**第三步：** 安装

> deng@itcast:~/tools/valgrind-3.13.0$ sudo make install

**第四步：**测试

> deng@itcast:~/tools/valgrind-3.13.0$ valgrind valgrind: no program specified valgrind: Use --help for more information.

## 21. 作业

**1）编写测试程序,测试fork之前打开文件，父子进程之间是否共享文件**

提示：

- 子进程write
- 父进程read

**2）多进程编程**

父进程fork三个子进程：

- 一个调用ps命令
- 一个调用自定义应用程序
- 一个调用会出现段错误的程序

父进程回收三个子进程(waitpid)，并且打印三个子进程的退出状态

**3) 文件操作**

统计出指定目录中普通文件的个数.(递归)

##  总结

#  进程间通信

## 学习目标

- 熟练掌握execl/execlp函数的使用
- 说出什么是孤儿进程和僵尸进程
- 说出并理解管道的读写行为
- 熟练使用pipe进行父子进程间通信
- 熟练使用pipe进行兄弟进程间通信
- 熟练使用fifo进行无血缘关系的进程间通信
- 熟练掌握mmap函数的使用
- 使用mmap进行有血缘关系的进程间通信
- 使用mmap进行无血缘关系的进程间通信

##  进程间通讯概念

进程是一个独立的资源分配单元，不同进程之间的资源是独立的，没有关联，不能在一个进程中直接访问另一个进程的资源。

进程不是孤立的，不同的进程需要进行信息的交互和状态的传递，进程间通信( IPC：Inter Processes Communication )。

进程间通信的目的：

- 数据传输：一个进程需要将它的数据发送给另一个进程。
- 通知事件：一个进程需要向另一个或一组进程发送消息，通知它（它们）发生了某种事件（如进程终止时要通知父进程）。
- 资源共享：多个进程之间共享同样的资源。为了做到这一点，需要内核提供互斥和同步机制。
- 进程控制：有些进程希望完全控制另一个进程的执行（如 Debug 进程），此时控制进程希望能够拦截另一个进程的所有陷入和异常，并能够及时知道它的状态改变。

**Linux 操作系统支持的主要进程间通信的通信机制：**

![1527923816604](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\1527923816604.png)                                                                                                                                                                                                                                                                                                                                                               

## 无名管道

###  概述

管道也叫无名管道，它是是 UNIX 系统 IPC（进程间通信） 的最古老形式，所有的 UNIX 系统都支持

1) 半双工，数据在同一时刻只能在一个方向上流动。
2) 数据只能从管道的一端写入，从另一端读出。
3) 写入管道中的数据遵循先入先出的规则。
4) 管道所传送的数据是无格式的，这要求管道的**读出方与写入方**必须事**先约定好数据的格式**，如多少字节算一个消息等。
5) 管道不是普通的文件，不属于某个文件系统，其只存在于**内存**中。
6) 管道在内存中对应一个缓冲区。不同的系统其大小不一定相同。
7) 从管道读数据是一次性操作，数据一旦被读走，它就从管道中被抛弃，释放空间以便写更多的数据。
8) 管道没有名字，**只能在具有公共祖先的进程**（父进程与子进程，或者两个兄弟进程，具有亲缘关系）之间使用。

管道是一种特殊类型的文件，在应用层体现为两个打开的文件描述符。

![1527924156395](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\1527924156395.png)

### pipe函数

```c
#include <unistd.h>
int pipe(int pipefd[2]);
功能：创建无名管道。
参数：
    pipefd : 为 int 型数组的首地址，其存放了管道的文件描述符 pipefd[0]、pipefd[1]。
    当一个管道建立时，它会创建两个文件描述符 fd[0] 和 fd[1]。其中 fd[0] 固定用于读管道，而 fd[1] 固定用于写管道。一般文件 I/O的函数都可以用来操作管道(lseek() 除外)。
返回值：
    成功：0
    失败：-1
```

下面我们写这个一个例子，子进程通过无名管道给父进程传递一个字符串数据：

```c
int main()
{
    int fd_pipe[2] = { 0 };
    pid_t pid;
    if (pipe(fd_pipe) < 0)
    {// 创建管道
        perror("pipe");
    }
    pid = fork(); // 创建进程
    if (pid == 0)
    { // 子进程
        char buf[] = "I am mike";
        // 往管道写端写数据
        write(fd_pipe[1], buf, strlen(buf));

        _exit(0);
    }
    else if (pid > 0)
    {// 父进程
        wait(NULL); // 等待子进程结束，回收其资源
        char str[50] = { 0 };
        // 从管道里读数据
        read(fd_pipe[0], str, sizeof(str));

        printf("str=[%s]\n", str); // 打印数据
    }
    return 0;
}
```

###  管道的读写特点

使用管道需要注意以下4种特殊情况（假设都是阻塞I/O操作，没有设置O_NONBLOCK标志）：

1) 如果所有指向管道写端的文件描述符都关闭了（管道写端引用计数为0），而仍然有进程从管道的读端读数据，那么管道中剩余的数据都被读取后，再次read会返回0，就像读到文件末尾一样。
2) 如果有指向管道写端的文件描述符没关闭（管道写端引用计数大于0），而持有管道写端的进程也没有向管道中写数据，这时有进程从管道读端读数据，那么管道中剩余的数据都被读取后，再次read会阻塞，直到管道中有数据可读了才读取数据并返回。
3) 如果所有指向管道读端的文件描述符都关闭了（管道读端引用计数为0），这时有进程向管道的写端write，那么该进程会收到信号SIGPIPE，通常会导致进程异常终止。当然也可以对SIGPIPE信号实施捕捉，不终止进程。具体方法信号章节详细介绍。
4) 如果有指向管道读端的文件描述符没关闭（管道读端引用计数大于0），而持有管道读端的进程也没有从管道中读数据，这时有进程向管道写端写数据，那么在管道被写满时再次write会阻塞，直到管道中有空位置了才写入数据并返回。

**总结：**

**读管道：**

Ø 管道中有数据，read返回实际读到的字节数。

Ø 管道中无数据：

u 管道写端被全部关闭，read返回0 (相当于读到文件结尾)

u 写端没有全部被关闭，read阻塞等待(不久的将来可能有数据递达，此时会让出cpu)

**写管道：**

Ø 管道读端全部被关闭， 进程异常终止(也可使用捕捉SIGPIPE信号，使进程终止)

Ø 管道读端没有全部关闭：

u 管道已满，write阻塞。

u 管道未满，write将数据写入，并返回实际写入的字节数。

### 设置为非阻塞的方法

设置方法：

```c
//获取原来的flags
int flags = fcntl(fd[0], F_GETFL);
// 设置新的flags
flag |= O_NONBLOCK;
// flags = flags | O_NONBLOCK;
fcntl(fd[0], F_SETFL, flags);
```

结论： 如果写端没有关闭，读端设置为非阻塞， 如果没有数据，直接返回-1。

### 查看管道缓冲区命令

可以使用ulimit -a 命令来查看当前系统中创建管道文件所对应的内核缓冲区大小。

![1528094380143](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\1528094380143.png)

### 查看管道缓冲区函数

```c
#include <unistd.h>

long fpathconf(int fd, int name);
功能：该函数可以通过name参数查看不同的属性值
参数：
    fd：文件描述符
    name：
        _PC_PIPE_BUF，查看管道缓冲区大小
        _PC_NAME_MAX，文件名字字节数的上限
返回值：
    成功：根据name返回的值的意义也不同。
    失败： -1
```

示例：

```c
int main()
{
    int fd[2];
    int ret = pipe(fd);
    if (ret == -1)
    {
        perror("pipe error");
        exit(1);
    }

    long num = fpathconf(fd[0], _PC_PIPE_BUF);
    printf("num = %ld\n", num);

    return 0;
}
```

## 有名管道

### 概述

命名管道（有名管道）（FIFO）不同于无名管道之处在于它**提供了一个路径名与之关联**，以 FIFO 的文件形式存在于文件系统中，这样，即使与 FIFO 的创建进程不存在亲缘关系的进程，**只要可以访问该路径**，就能够彼此通过 FIFO 相互通信 

命名管道（FIFO)和无名管道（pipe）有一些特点是相同的，不一样的地方在于：

1) FIFO 在文件系统中作为一个特殊的文件而存在，但 FIFO 中的内容却存放在**内存**中。
2) 当使用 FIFO 的进程退出后，FIFO 文件将继续保存在文件系统中以便以后使用。
3) FIFO 有名字，不相关的进程可以通过打开命名管道进行通信。

### 通过命令创建有名管道

![1528095132062](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\1528095132062.png)

### 4.3 通过函数创建有名管道

```c
#include <sys/types.h>
#include <sys/stat.h>

int mkfifo(const char *pathname, mode_t mode);
功能：
    命名管道的创建。
参数：
    pathname : 普通的路径名，也就是创建后 FIFO 的名字。
    mode : 文件的权限，与打开普通文件的 open() 函数中的 mode 参数相同。(0666)
返回值：
    成功：0   状态码
    失败：如果文件已经存在，则会出错且返回 -1。
```

### 有名管道读写操作

一旦使用mkfifo创建了一个FIFO，就可以使用open打开它，常见的文件I/O函数都可用于fifo。如：close、read、write、unlink等。

FIFO严格遵循先进先出（first in first out），对管道及FIFO的读总是从开始处返回数据，对它们的写则把数据添加到末尾。**它们不支持诸如lseek()等文件定位操作。**

```
//进行1，写操作
int fd = open("my_fifo", O_WRONLY);  

char send[100] = "Hello Mike";
write(fd, send, strlen(send));

//进程2，读操作
int fd = open("my_fifo", O_RDONLY);//等着只写  

char recv[100] = { 0 };
//读数据，命名管道没数据时会阻塞，有数据时就取出来  
read(fd, recv, sizeof(recv));
printf("read from my_fifo buf=[%s]\n", recv);
```

### 有名管道注意事项

1) 一个为只读而打开一个管道的进程会阻塞直到另外一个进程为只写打开该管道

2）一个为只写而打开一个管道的进程会阻塞直到另外一个进程为只读打开该管道

**读管道：**

Ø 管道中有数据，read返回实际读到的字节数。

Ø 管道中无数据：

u 管道写端被全部关闭，read返回0 (相当于读到文件结尾)

u 写端没有全部被关闭，read阻塞等待

**写管道：**

Ø 管道读端全部被关闭， 进程异常终止(也可使用捕捉SIGPIPE信号，使进程终止)

Ø 管道读端没有全部关闭：

u 管道已满，write阻塞。

u 管道未满，write将数据写入，并返回实际写入的字节数。

## 共享存储映射

### 5.1 概述

存储映射I/O (Memory-mapped I/O) 使一个**磁盘文件与存储空间**中的一个**缓冲区**相映射。

![1527925077595](C:\Users\12964\AppData\Roaming\Typora\typora-user-images\1527925077595.png)

于是当从缓冲区中取数据，就相当于读文件中的相应字节。于此类似，将数据存入缓冲区，则相应的字节就自动写入文件。这样，就可在不适用read和write函数的情况下，使用**地址（指针）完成I/O操作**。

**共享内存可以说是最有用的进程间通信方式**，也是最快的IPC形式, 因为进程可以直接读写内存，而不需要任何数据的拷贝。

### 存储映射函数

(1) mmap函数

```c
#include <sys/mman.h>

void *mmap(void *addr, size_t length, int prot, int flags, int fd, off_t offset);
功能:
    一个文件或者其它对象映射进内存
参数：
    addr :  指定映射的起始地址, 通常设为NULL, 由系统指定
    length：映射到内存的文件长度
    prot：  映射区的保护方式, 最常用的 :
        a) 读：PROT_READ
        b) 写：PROT_WRITE
        c) 读写：PROT_READ | PROT_WRITE
    flags：  映射区的特性, 可以是
        a) MAP_SHARED : 写入映射区的数据会复制回文件, 且允许其他映射该文件的进程共享。
        b) MAP_PRIVATE : 对映射区的写入操作会产生一个映射区的复制(copy - on - write), 对此区域所做的修改不会写回原文件。
    fd：由open返回的文件描述符, 代表要映射的文件。
    offset：以文件开始处的偏移量, 必须是4k的整数倍, 通常为0, 表示从文件头开始映射
返回值：
    成功：返回创建的映射区首地址
    失败：MAP_FAILED宏
```

**关于mmap函数的使用总结：**

1) 第一个参数写成NULL
2) 第二个参数要映射的文件大小 > 0
3) 第三个参数：PROT_READ 、PROT_WRITE
4) 第四个参数：MAP_SHARED 或者 MAP_PRIVATE
5) 第五个参数：打开的文件对应的文件描述符
6) 第六个参数：4k的整数倍，通常为0

(2) munmap函数

```c
#include <sys/mman.h>
int munmap(void *addr, size_t length);
功能：
    释放内存映射区
参数：
    addr：使用mmap函数创建的映射区的首地址
    length：映射区的大小
返回值：
    成功：0
    失败：-1
```

### 注意事项

1) 创建映射区的过程中，隐含着一次对映射文件的读操作。
2) 当MAP_SHARED时，要求：映射区的权限应 <=文件打开的权限(出于对映射区的保护)。而MAP_PRIVATE则无所谓，因为mmap中的权限是对内存的限制。
3) 映射区的释放与文件关闭无关。只要映射建立成功，文件可以立即关闭。
4) 特别注意，当映射文件大小为0时，不能创建映射区。所以，用于映射的文件必须要有实际大小。mmap使用时常常会出现总线错误，通常是由于共享文件存储空间大小引起的。
5) munmap传入的地址一定是mmap的返回地址。坚决杜绝指针++操作。
6) 如果文件偏移量必须为4K的整数倍。
7) mmap创建映射区出错概率非常高，一定要检查返回值，确保映射区建立成功再进行后续操作。

### 共享映射的方式操作文件

参考示例：

```c
    int fd = open("xxx.txt", O_RDWR); //读写文件
    int len = lseek(fd, 0, SEEK_END);   //获取文件大小

    //一个文件映射到内存，ptr指向此内存
    void * ptr = mmap(NULL, len, PROT_READ | PROT_WRITE, MAP_SHARED, fd, 0);
    if (ptr == MAP_FAILED)
    {
        perror("mmap error");
        exit(1);
    }

    close(fd); //关闭文件

    char buf[4096];
    printf("buf = %s\n", (char*)ptr); // 从内存中读数据，等价于从文件中读取内容

    strcpy((char*)ptr, "this is a test");//写内容

    int ret = munmap(ptr, len);
    if (ret == -1)
    {
        perror("munmap error");
        exit(1);
    }
```

###  共享映射实现父子进程通信

参考示例：

```c
    int fd = open("xxx.txt", O_RDWR);// 打开一个文件
    int len = lseek(fd, 0, SEEK_END);//获取文件大小

    // 创建内存映射区
    void *ptr = mmap(NULL, len, PROT_READ | PROT_WRITE, MAP_SHARED, fd, 0);
    if (ptr == MAP_FAILED)
    {
        perror("mmap error");
        exit(1);
    }
    close(fd); //关闭文件

    // 创建子进程
    pid_t pid = fork();
    if (pid == 0) //子进程
    {
        sleep(1); //演示，保证父进程先执行

        // 读数据
        printf("%s\n", (char*)ptr);
    }
    else if (pid > 0) //父进程
    {
        // 写数据
        strcpy((char*)ptr, "i am u father!!");

        // 回收子进程资源
        wait(NULL);
    }

    // 释放内存映射区
    int ret = munmap(ptr, len);
    if (ret == -1)
    {
        perror("munmap error");
        exit(1);
    } 
```

###  匿名映射实现父子进程通信

通过使用我们发现，使用映射区来完成文件读写操作十分方便，父子进程间通信也较容易。但缺陷是，每次创建映射区一定要依赖一个文件才能实现。

通常为了建立映射区要open一个temp文件，创建好了再unlink、close掉，比较麻烦。 可以直接使用匿名映射来代替。

其实Linux系统给我们提供了创建匿名映射区的方法，无需依赖一个文件即可创建映射区。同样需要借助标志位参数flags来指定。

使用**MAP_ANONYMOUS (或MAP_ANON)**。

```
int *p = mmap(NULL, 4, PROT_READ|PROT_WRITE, MAP_SHARED|MAP_ANONYMOUS, -1, 0);
```

- 4"随意举例，该位置表示映射区大小，可依实际需要填写。
- MAP_ANONYMOUS和MAP_ANON这两个宏是Linux操作系统特有的宏。在类Unix系统中如无该宏定义，可使用如下两步来完成匿名映射区的建立。

程序示例：

```c
// 创建匿名内存映射区
    int len = 4096;
    void *ptr = mmap(NULL, len, PROT_READ | PROT_WRITE, MAP_SHARED | MAP_ANON, -1, 0);
    if (ptr == MAP_FAILED)
    {
        perror("mmap error");
        exit(1);
    }

    // 创建子进程
    pid_t pid = fork();
    if (pid > 0) //父进程
    {
        // 写数据
        strcpy((char*)ptr, "hello mike!!");
        // 回收
        wait(NULL);
    }
    else if (pid == 0)//子进程
    {
        sleep(1);
        // 读数据
        printf("%s\n", (char*)ptr);
    }

    // 释放内存映射区
    int ret = munmap(ptr, len);
    if (ret == -1)
    {
        perror("munmap error");
        exit(1);
    }
```

 

## 作业

**6.1 使用多进程的方式改写聊天程序(有名管道)**

16mkfifo_room

**6.2 思考使用存储映射实现不同进程之间通信**

mmap munmap

**2）多进程编程**

父进程fork三个子进程：

- 一个调用ps命令
- 一个调用自定义应用程序
- 一个调用会出现段错误的程序

父进程回收三个子进程(waitpid)，并且打印三个子进程的退出状态 

练习:

创建一个子进程, 子进程执行ls -l /home命令, 父进程等待子进程结束.(15min)

## 总结

# 信号

##  学习目标

- 了解信号中的基本概念
- 熟练使用信号相关的函数
- 了解内核中的阻塞信号集和未决信号集作用
- 参考文档使用信号集操作相关函数
- 熟练使用信号捕捉函数signal
- 熟练使用信号捕捉函数sigaction
- 熟练掌握使用信号完成子进程的回收

##  信号的概述

**信号的概念**

信号是 Linux 进程间通信的**最古老**的方式。信号是软件中断，它是在软件层次上对中断机制的一种模拟，是一种异步通信的方式 。信号可以导致一个正在运行的进程被另一个正在运行的异步进程中断，转而处理某一个突发事件。

“中断”在我们生活中经常遇到，譬如，我正在房间里打游戏，突然送快递的来了，把正在玩游戏的我给“中断”了，我去签收快递( 处理中断 )，处理完成后，再继续玩我的游戏。

这里我们学习的“信号”就是属于这么一种“中断”。我们在终端上敲“Ctrl+c”，就产生一个“中断”，相当于产生一个信号，接着就会处理这么一个“中断任务”（默认的处理方式为中断当前进程）。

 

**信号的特点**

- 简单
- 不能携带大量信息
- 满足某个特设条件才发送

 

信号可以直接进行用户空间进程和内核空间进程的交互，内核进程可以利用它来通知用户空间进程发生了哪些系统事件。

一个完整的信号周期包括三个部分：信号的产生，信号在进程中的注册，信号在进程中的注销，执行信号处理函数。如下图所示：

![1527928644452](assets/1527928644452.png)

注意：这里信号的产生，注册，注销时信号的内部机制，而不是信号的函数实现。

## 03. 信号的编号(了解)

1）信号编号：

Unix早期版本就提供了信号机制，但不可靠，信号可能丢失。Berkeley 和 AT&T都对信号模型做了更改，增加了可靠信号机制。但彼此不兼容。POSIX.1对可靠信号例程进行了标准化。

Linux 可使用命令：kill -l（"l" 为字母），查看相应的信号。

![1527928772368](assets/1527928772368.png)

不存在编号为0的信号。其中1-31号信号称之为常规信号（也叫普通信号或标准信号），34-64称之为实时信号，驱动编程与硬件相关。名字上区别不大。而前32个名字各不相同。

 

2） Linux常规信号一览表 :

| **编号** | **信号**             | **对应事件**                                                 | **默认动作**               |
| :------- | :------------------- | :----------------------------------------------------------- | :------------------------- |
| 1        | SIGHUP               | 用户退出shell时，由该shell启动的所有进程将收到这个信号       | 终止进程                   |
| 2        | **SIGINT**           | 当用户按下了**<Ctrl+C>**组合键时，用户终端向正在运行中的由该终端启动的程序发出此信号 | 终止进程                   |
| 3        | **SIGQUIT**          | 用户按下**<ctrl+\>**组合键时产生该信号，用户终端向正在运行中的由该终端启动的程序发出些信号 | 终止进程                   |
| 4        | SIGILL               | CPU检测到某进程执行了非法指令                                | 终止进程并产生core文件     |
| 5        | SIGTRAP              | 该信号由断点指令或其他 trap指令产生                          | 终止进程并产生core文件     |
| 6        | SIGABRT              | 调用abort函数时产生该信号                                    | 终止进程并产生core文件     |
| 7        | SIGBUS               | 非法访问内存地址，包括内存对齐出错                           | 终止进程并产生core文件     |
| 8        | SIGFPE               | 在发生致命的运算错误时发出。不仅包括浮点运算错误，还包括溢出及除数为0等所有的算法错误 | 终止进程并产生core文件     |
| 9        | SIGKILL              | 无条件终止进程。本信号不能被忽略，处理和阻塞                 | 终止进程，可以杀死任何进程 |
| 10       | SIGUSE1              | 用户定义的信号。即程序员可以在程序中定义并使用该信号         | 终止进程                   |
| 11       | **SIGSEGV**          | 指示进程进行了无效内存访问(段错误)                           | 终止进程并产生core文件     |
| 12       | SIGUSR2              | 另外一个用户自定义信号，程序员可以在程序中定义并使用该信号   | 终止进程                   |
| 13       | **SIGPIPE**          | Broken pipe向一个没有读端的管道写数据                        | 终止进程                   |
| 14       | SIGALRM              | 定时器超时，超时的时间 由系统调用alarm设置                   | 终止进程                   |
| 15       | SIGTERM              | 程序结束信号，与SIGKILL不同的是，该信号可以被阻塞和终止。通常用来要示程序正常退出。执行shell命令Kill时，缺省产生这个信号 | 终止进程                   |
| 16       | SIGSTKFLT            | Linux早期版本出现的信号，现仍保留向后兼容                    | 终止进程                   |
| 17       | **SIGCHLD**          | 子进程结束时，父进程会收到这个信号                           | 忽略这个信号               |
| 18       | SIGCONT              | 如果进程已停止，则使其继续运行                               | 继续/忽略                  |
| 19       | SIGSTOP              | 停止进程的执行。信号不能被忽略，处理和阻塞                   | 为终止进程                 |
| 20       | SIGTSTP              | 停止终端交互进程的运行。按下<ctrl+z>组合键时发出这个信号     | 暂停进程                   |
| 21       | SIGTTIN              | 后台进程读终端控制台                                         | 暂停进程                   |
| 22       | SIGTTOU              | 该信号类似于SIGTTIN，在后台进程要向终端输出数据时发生        | 暂停进程                   |
| 23       | SIGURG               | 套接字上有紧急数据时，向当前正在运行的进程发出些信号，报告有紧急数据到达。如网络带外数据到达 | 忽略该信号                 |
| 24       | SIGXCPU              | 进程执行时间超过了分配给该进程的CPU时间 ，系统产生该信号并发送给该进程 | 终止进程                   |
| 25       | SIGXFSZ              | 超过文件的最大长度设置                                       | 终止进程                   |
| 26       | SIGVTALRM            | 虚拟时钟超时时产生该信号。类似于SIGALRM，但是该信号只计算该进程占用CPU的使用时间 | 终止进程                   |
| 27       | SGIPROF              | 类似于SIGVTALRM，它不公包括该进程占用CPU时间还包括执行系统调用时间 | 终止进程                   |
| 28       | SIGWINCH             | 窗口变化大小时发出                                           | 忽略该信号                 |
| 29       | SIGIO                | 此信号向进程指示发出了一个异步IO事件                         | 忽略该信号                 |
| 30       | SIGPWR               | 关机                                                         | 终止进程                   |
| 31       | SIGSYS               | 无效的系统调用                                               | 终止进程并产生core文件     |
| 34~64    | SIGRTMIN ～ SIGRTMAX | LINUX的实时信号，它们没有固定的含义（可以由用户自定义）      | 终止进程                   |

## 04. 信号四要素

每个信号必备4要素，分别是：

1）编号 2）名称 3）事件 4）默认处理动作

可通过**man 7 signal**查看帮助文档获取：

![1527928967909](assets/1527928967909.png)

在标准信号中，有一些信号是有三个“Value”，第一个值通常对alpha和sparc架构有效，中间值针对x86、arm和其他架构，最后一个应用于mips架构。一个‘-’表示在对应架构上尚未定义该信号。

不同的操作系统定义了不同的系统信号。因此有些信号出现在Unix系统内，也出现在Linux中，而有的信号出现在FreeBSD或Mac OS中却没有出现在Linux下。这里我们只研究Linux系统中的信号。

 

 

Action为默认动作：

- Term：终止进程
- Ign： 忽略信号 (默认即时对该种信号忽略操作)
- Core：终止进程，生成Core文件。(查验死亡原因，用于gdb调试)
- Stop：停止（暂停）进程
- Cont：继续运行进程

注意通过man 7 signal命令查看帮助文档，其中可看到 : The signals **SIGKILL** and **SIGSTOP** cannot be caught, blocked, or ignored.

这里特别强调了**9) SIGKILL** **和19) SIGSTOP信号，不允许忽略和捕捉，只能执行默认动作。甚至不能将其设置为阻塞。**

另外需清楚，只有每个信号所对应的事件发生了，该信号才会被递送(但不一定递达)，不应乱发信号！！

 

## 05. 信号的状态

 

**1) 产生**

a) 当用户按某些终端键时，将产生信号。

终端上按“Ctrl+c”组合键通常产生中断信号 SIGINT

终端上按“Ctrl+\”键通常产生中断信号 SIGQUIT

终端上按“Ctrl+z”键通常产生中断信号 SIGSTOP 等。

b) 硬件异常将产生信号。

除数为 0，无效的内存访问等。这些情况通常由硬件检测到，并通知内核，然后内核产生适当的信号发送给相应的进程。

c) 软件异常将产生信号。

当检测到某种软件条件已发生(如：定时器alarm)，并将其通知有关进程时，产生信号。

d) 调用系统函数(如：kill、raise、abort)将发送信号。

注意：接收信号进程和发送信号进程的所有者必须相同，或发送信号进程的所有者必须是超级用户。

e) 运行 kill /killall命令将发送信号。

此程序实际上是使用 kill 函数来发送信号。也常用此命令终止一个失控的后台进程。

 

**2) 未决状态：没有被处理**

**3) 递达状态：信号被处理了**

 

## 06. 阻塞信号集和未决信号集

信号的实现手段导致信号有很强的延时性，但对于用户来说，时间非常短，不易察觉。

Linux内核的进程控制块PCB是一个结构体，task_struct, 除了包含进程id，状态，工作目录，用户id，组id，文件描述符表，还包含了信号相关的信息，主要指**阻塞信号集和未决信号集**。

**6.1 阻塞信号集(信号屏蔽字)**

将某些信号加入集合，对他们设置屏蔽，当屏蔽x信号后，再收到该信号，该信号的处理将推后(处理发生在解除屏蔽后)。

**6.2 未决信号集**

信号产生，未决信号集中描述该信号的位立刻翻转为1，表示信号处于未决状态。当信号被处理对应位翻转回为0。这一时刻往往非常短暂。

信号产生后由于某些原因(主要是阻塞)不能抵达。这类信号的集合称之为未决信号集。在屏蔽解除前，信号一直处于未决状态。

 

## 07. 信号产生函数

### 7.1 kill函数

```
#include <sys/types.h>
#include <signal.h>

int kill(pid_t pid, int sig);
功能：给指定进程发送指定信号(不一定杀死)

参数：
    pid : 取值有 4 种情况 :
        pid > 0:  将信号传送给进程 ID 为pid的进程。
        pid = 0 :  将信号传送给当前进程所在进程组中的所有进程。
        pid = -1 : 将信号传送给系统内所有的进程。
        pid < -1 : 将信号传给指定进程组的所有进程。这个进程组号等于 pid 的绝对值。
    sig : 信号的编号，这里可以填数字编号，也可以填信号的宏定义，可以通过命令 kill - l("l" 为字母)进行相应查看。不推荐直接使用数字，应使用宏名，因为不同操作系统信号编号可能不同，但名称一致。

返回值：
    成功：0
    失败：-1
```

super用户(root)可以发送信号给任意用户，普通用户是不能向系统用户发送信号的。

kill -9 (root用户的pid) 是不可以的。同样，普通用户也不能向其他普通用户发送信号，终止其进程。 只能向自己创建的进程发送信号。

普通用户基本规则是：发送者实际或有效用户ID == 接收者实际或有效用户ID

程序示例:

```
int main()
{
    pid_t pid = fork();
    if (pid == 0)
    {//子进程
        int i = 0;
        for (i = 0; i<5; i++)
        {
            printf("in son process\n");
            sleep(1);
        }
    }
    else
    {//父进程
        printf("in father process\n");
        sleep(2);
        printf("kill sub process now \n");
        kill(pid, SIGINT);
    }

    return 0;
}
```

 

### 7.2 raise函数

```
#include <signal.h>

int raise(int sig);
功能：给当前进程发送指定信号(自己给自己发)，等价于 kill(getpid(), sig)
参数：
    sig：信号编号
返回值：
    成功：0
    失败：非0值
```

 

### 7.3 abort函数

```
#include <stdlib.h>

void abort(void);
功能：给自己发送异常终止信号 6) SIGABRT，并产生core文件，等价于kill(getpid(), SIGABRT);

参数：无

返回值：无

```

 

### 7.4 alarm函数(闹钟)

```
#include <unistd.h>

unsigned int alarm(unsigned int seconds);
功能：
    设置定时器(闹钟)。在指定seconds后，内核会给当前进程发送14）SIGALRM信号。进程收到该信号，默认动作终止。每个进程都有且只有唯一的一个定时器。
    取消定时器alarm(0)，返回旧闹钟余下秒数。
参数：
    seconds：指定的时间，以秒为单位
返回值：
    返回0或剩余的秒数

```

定时，与进程状态无关(自然定时法)！就绪、运行、挂起(阻塞、暂停)、终止、僵尸……无论进程处于何种状态，alarm都计时。

测试程序:

```
int main()
{
    int seconds = 0;

    seconds = alarm(5);
    printf("seconds = %d\n", seconds);

    sleep(2);
    seconds = alarm(5);
    printf("seconds = %d\n", seconds);

    while (1);
    return 0;
}
```

 

### 7.5 setitimer函数（定时器）

```
#include <sys/time.h>

int setitimer(int which,  const struct itimerval *new_value, struct itimerval *old_value);
功能：
    设置定时器(闹钟)。 可代替alarm函数。精度微秒us，可以实现周期定时。
参数：
    which：指定定时方式
        a) 自然定时：ITIMER_REAL → 14）SIGALRM计算自然时间
        b) 虚拟空间计时(用户空间)：ITIMER_VIRTUAL → 26）SIGVTALRM  只计算进程占用cpu的时间
        c) 运行时计时(用户 + 内核)：ITIMER_PROF → 27）SIGPROF计算占用cpu及执行系统调用的时间
    new_value：struct itimerval, 负责设定timeout时间
        struct itimerval {
            struct timerval it_interval; // 闹钟触发周期
            struct timerval it_value;    // 闹钟触发时间
        };
        struct timeval {
            long tv_sec;            // 秒
            long tv_usec;           // 微秒
        }
        itimerval.it_value： 设定第一次执行function所延迟的秒数 
        itimerval.it_interval：  设定以后每几秒执行function

    old_value： 存放旧的timeout值，一般指定为NULL
返回值：
    成功：0
    失败：-1
```

示例程序：

```
void myfunc(int sig)
{
    printf("hello\n");
}

int main()
{
    struct itimerval new_value;

    //定时周期
    new_value.it_interval.tv_sec = 1;
    new_value.it_interval.tv_usec = 0;

    //第一次触发的时间
    new_value.it_value.tv_sec = 2;
    new_value.it_value.tv_usec = 0;

    signal(SIGALRM, myfunc); //信号处理
    setitimer(ITIMER_REAL, &new_value, NULL); //定时器设置

    while (1);

    return 0;
}

```

 

## 08. 信号集

### 8.1 信号集概述

在PCB中有两个非常重要的信号集。一个称之为“阻塞信号集”，另一个称之为“未决信号集”。

这两个信号集都是内核使用**位图机制**来实现的。但操作系统不允许我们直接对其进行位操作。而需自定义另外一个集合，借助信号集操作函数来对PCB中的这两个信号集进行修改。

![1527930344052](assets/1527930344052.png)

 

### 8.2 自定义信号集函数

为了方便对多个信号进行处理，一个用户进程常常需要对多个信号做出处理，在 Linux 系统中引入了信号集（信号的集合）。

这个信号集有点类似于我们的 QQ 群，一个个的信号相当于 QQ 群里的一个个好友。

信号集是一个能表示多个信号的数据类型，sigset_t set，set即一个信号集。既然是一个集合，就需要对集合进行添加/删除等操作。

相关函数说明如下：

```
#include <signal.h>  

int sigemptyset(sigset_t *set);       //将set集合置空
int sigfillset(sigset_t *set)；          //将所有信号加入set集合
int sigaddset(sigset_t *set, int signo);  //将signo信号加入到set集合
int sigdelset(sigset_t *set, int signo);   //从set集合中移除signo信号
int sigismember(const sigset_t *set, int signo); //判断信号是否存在
```

除sigismember外，其余操作函数中的set均为传出参数。sigset_t类型的本质是位图。但不应该直接使用位操作，而应该使用上述函数，保证跨系统操作有效。

 

示例程序:

```
int main()
{
    sigset_t set;   // 定义一个信号集变量
    int ret = 0;

    sigemptyset(&set); // 清空信号集的内容

    // 判断 SIGINT 是否在信号集 set 里
    // 在返回 1， 不在返回 0
    ret = sigismember(&set, SIGINT);
    if (ret == 0)
    {
        printf("SIGINT is not a member of set \nret = %d\n", ret);
    }

    sigaddset(&set, SIGINT); // 把 SIGINT 添加到信号集 set
    sigaddset(&set, SIGQUIT);// 把 SIGQUIT 添加到信号集 set

    // 判断 SIGINT 是否在信号集 set 里
    // 在返回 1， 不在返回 0
    ret = sigismember(&set, SIGINT);
    if (ret == 1)
    {
        printf("SIGINT is a member of set \nret = %d\n", ret);
    }

    sigdelset(&set, SIGQUIT); // 把 SIGQUIT 从信号集 set 移除

    // 判断 SIGQUIT 是否在信号集 set 里
    // 在返回 1， 不在返回 0
    ret = sigismember(&set, SIGQUIT);
    if (ret == 0)
    {
        printf("SIGQUIT is not a member of set \nret = %d\n", ret);
    }

    return 0;
}
```

 

### 8.3 sigprocmask函数

信号阻塞集也称信号屏蔽集、信号掩码。每个进程都有一个阻塞集，创建子进程时子进程将继承父进程的阻塞集。信号阻塞集用来描述哪些信号递送到该进程的时候被阻塞（在信号发生时记住它，直到进程准备好时再将信号通知进程）。

所谓阻塞并不是禁止传送信号, 而是暂缓信号的传送。若将被阻塞的信号从信号阻塞集中删除，且对应的信号在被阻塞时发生了，进程将会收到相应的信号。

我们可以通过 sigprocmask() 修改当前的信号掩码来改变信号的阻塞情况。

```
#include <signal.h>

int sigprocmask(int how, const sigset_t *set, sigset_t *oldset);
功能：
    检查或修改信号阻塞集，根据 how 指定的方法对进程的阻塞集合进行修改，新的信号阻塞集由 set 指定，而原先的信号阻塞集合由 oldset 保存。

参数：
    how : 信号阻塞集合的修改方法，有 3 种情况：
        SIG_BLOCK：向信号阻塞集合中添加 set 信号集，新的信号掩码是set和旧信号掩码的并集。相当于 mask = mask|set。
        SIG_UNBLOCK：从信号阻塞集合中删除 set 信号集，从当前信号掩码中去除 set 中的信号。相当于 mask = mask & ~ set。
        SIG_SETMASK：将信号阻塞集合设为 set 信号集，相当于原来信号阻塞集的内容清空，然后按照 set 中的信号重新设置信号阻塞集。相当于mask = set。
    set : 要操作的信号集地址。
        若 set 为 NULL，则不改变信号阻塞集合，函数只把当前信号阻塞集合保存到 oldset 中。
    oldset : 保存原先信号阻塞集地址

返回值：
    成功：0，
    失败：-1，失败时错误代码只可能是 EINVAL，表示参数 how 不合法。
```

 

### 8.4 sigpending函数

```
#include <signal.h>

int sigpending(sigset_t *set);
功能：读取当前进程的未决信号集
参数：
    set：未决信号集
返回值：
    成功：0
    失败：-1

```

示例程序:

```
int main()
{
    // 自定义信号集
    sigset_t myset, old;
    sigemptyset(&myset);// 清空　－》　０

    // 添加要阻塞的信号
    sigaddset(&myset, SIGINT);
    sigaddset(&myset, SIGQUIT);
    sigaddset(&myset, SIGKILL);

    // 自定义信号集设置到内核中的阻塞信号集
    sigprocmask(SIG_BLOCK, &myset, &old);

    sigset_t pend;
    int i = 0;
    while (1)
    {
        // 读内核中的未决信号集的状态
        sigpending(&pend);
        for (int i = 1; i<32; ++i)
        {
            if (sigismember(&pend, i))
            {
                printf("1");
            }
            else if (sigismember(&pend, i) == 0)
            {
                printf("0");
            }
        }
        printf("\n");
        sleep(1);
        i++;

        // 10s之后解除阻塞
        if (i > 10)
        {
            // sigprocmask(SIG_UNBLOCK, &myset, NULL);
            sigprocmask(SIG_SETMASK, &old, NULL);
        }
    }

    return 0;
}
```

 

## 09. 信号捕捉

### 9.1 信号处理方式

一个进程收到一个信号的时候，可以用如下方法进行处理：

1）执行系统默认动作

对大多数信号来说，系统默认动作是用来终止该进程。

2）忽略此信号(丢弃)

接收到此信号后没有任何动作。

3）执行自定义信号处理函数(捕获)

用用户定义的信号处理函数处理该信号。

【注意】：SIGKILL 和 SIGSTOP 不能更改信号的处理方式，因为它们向用户提供了一种使进程终止的可靠方法。

 

内核实现信号捕捉过程：

![1527931072795](assets/1527931072795.png)

 

### 9.2 signal函数

```
#include <signal.h>

typedef void(*sighandler_t)(int);
sighandler_t signal(int signum, sighandler_t handler);
功能：
    注册信号处理函数（不可用于 SIGKILL、SIGSTOP 信号），即确定收到信号后处理函数的入口地址。此函数不会阻塞。

参数：
    signum：信号的编号，这里可以填数字编号，也可以填信号的宏定义，可以通过命令 kill - l("l" 为字母)进行相应查看。
    handler : 取值有 3 种情况：
          SIG_IGN：忽略该信号
          SIG_DFL：执行系统默认动作
          信号处理函数名：自定义信号处理函数，如：func
          回调函数的定义如下：
            void func(int signo)
            {
                // signo 为触发的信号，为 signal() 第一个参数的值
            }

返回值：
    成功：第一次返回 NULL，下一次返回此信号上一次注册的信号处理函数的地址。如果需要使用此返回值，必须在前面先声明此函数指针的类型。
    失败：返回 SIG_ERR
```

该函数由ANSI定义，由于历史原因在不同版本的Unix和不同版本的Linux中可能有不同的行为。因此应该尽量避免使用它，取而代之使用sigaction函数。

 

示例程序:

```
// 信号处理函数
void signal_handler(int signo)
{
    if (signo == SIGINT)
    {
        printf("recv SIGINT\n");
    }
    else if (signo == SIGQUIT)
    {
        printf("recv SIGQUIT\n");
    }
}

int main()
{
    printf("wait for SIGINT OR SIGQUIT\n");

    /* SIGINT: Ctrl+c ; SIGQUIT: Ctrl+\ */
    // 信号注册函数
    signal(SIGINT, signal_handler);
    signal(SIGQUIT, signal_handler);

    while (1); //不让程序结束

    return 0;
}

```

 

### 9.3 sigaction函数

```
#include <signal.h>

int sigaction(int signum, const struct sigaction *act, struct sigaction *oldact);
功能：
    检查或修改指定信号的设置（或同时执行这两种操作）。

参数：
    signum：要操作的信号。
    act：   要设置的对信号的新处理方式（传入参数）。
    oldact：原来对信号的处理方式（传出参数）。

    如果 act 指针非空，则要改变指定信号的处理方式（设置），如果 oldact 指针非空，则系统将此前指定信号的处理方式存入 oldact。

返回值：
    成功：0
    失败：-1
```

**struct sigaction结构体：**

```
struct sigaction {
    void(*sa_handler)(int); //旧的信号处理函数指针
    void(*sa_sigaction)(int, siginfo_t *, void *); //新的信号处理函数指针
    sigset_t   sa_mask;      //信号阻塞集
    int        sa_flags;     //信号处理的方式
    void(*sa_restorer)(void); //已弃用
};
```

1) sa_handler、sa_sigaction：信号处理函数指针，和 signal() 里的函数指针用法一样，应根据情况给sa_sigaction、sa_handler 两者之一赋值，其取值如下：

a) SIG_IGN：忽略该信号

b) SIG_DFL：执行系统默认动作

c) 处理函数名：自定义信号处理函数

2) sa_mask：信号阻塞集，在信号处理函数执行过程中，临时屏蔽指定的信号。
3) sa_flags：用于指定信号处理的行为，通常设置为0，表使用默认属性。它可以是一下值的“按位或”组合：

Ø SA_RESTART：使被信号打断的系统调用自动重新发起（已经废弃）

Ø SA_NOCLDSTOP：使父进程在它的子进程暂停或继续运行时不会收到 SIGCHLD 信号。

Ø SA_NOCLDWAIT：使父进程在它的子进程退出时不会收到 SIGCHLD 信号，这时子进程如果退出也不会成为僵尸进程。

Ø SA_NODEFER：使对信号的屏蔽无效，即在信号处理函数执行期间仍能发出这个信号。

Ø SA_RESETHAND：信号处理之后重新设置为默认的处理方式。

Ø SA_SIGINFO：使用 sa_sigaction 成员而不是 sa_handler 作为信号处理函数。

 

**信号处理函数:**

```
void(*sa_sigaction)(int signum, siginfo_t *info, void *context);
参数说明：
    signum：信号的编号。
    info：记录信号发送进程信息的结构体。
    context：可以赋给指向 ucontext_t 类型的一个对象的指针，以引用在传递信号时被中断的接收进程或线程的上下文。

```

 

示例程序:

```
void myfunc(int sig)
{
    printf("hello signal: %d\n", sig);
    sleep(5);
    printf("wake up .....\n");
}

int main()
{
    // 注册信号捕捉函数
    struct sigaction act;
    act.sa_flags = 0;
    act.sa_handler = myfunc;
    // 设置临时屏蔽的信号
    sigemptyset(&act.sa_mask);  // 清空
    // ctrl + 反斜杠
    sigaddset(&act.sa_mask, SIGQUIT);

    sigaction(SIGINT, &act, NULL); //注册信号

    while (1);

    return 0;
}
```

 

### 9.4 **sigqueue** 函数(了解)

```
#include <signal.h>

int sigqueue(pid_t pid, int sig, const union sigval value);
功能：
    给指定进程发送信号。
参数：
    pid : 进程号。
    sig : 信号的编号。
    value : 通过信号传递的参数。
        union sigval 类型如下：
            union sigval
            {
                int   sival_int;
                void *sival_ptr;
            };
返回值：
    成功：0
    失败：-1

```

 

向指定进程发送指定信号的同时，携带数据。但如传地址，需注意，不同进程之间虚拟地址空间各自独立，将当前进程地址传递给另一进程没有实际意义。

下面我们做这么一个例子，一个进程在发送信号，一个进程在接收信号的发送。

发送信号示例代码如下：

```
/*******************************************************
*功能：     发 SIGINT 信号及信号携带的值给指定的进程
*参数：        argv[1]：进程号 argv[2]：待发送的值（默认为100）
*返回值：   0
********************************************************/
int main()
{
    if (argc >= 2)
    {
        pid_t pid, pid_self;
        union sigval tmp;

        pid = atoi(argv[1]); // 进程号
        if (argc >= 3)
        {
            tmp.sival_int = atoi(argv[2]);
        }
        else
        {
            tmp.sival_int = 100;
        }

        // 给进程 pid，发送 SIGINT 信号，并把 tmp 传递过去
        sigqueue(pid, SIGINT, tmp);

        pid_self = getpid(); // 进程号
        printf("pid = %d, pid_self = %d\n", pid, pid_self);
    }

    return 0;
}
```

接收信号示例代码如下：

```
// 信号处理回调函数
void signal_handler(int signum, siginfo_t *info, void *ptr)
{
    printf("signum = %d\n", signum); // 信号编号
    printf("info->si_pid = %d\n", info->si_pid); // 对方的进程号
    printf("info->si_sigval = %d\n", info->si_value.sival_int); // 对方传递过来的信息
}

int main()
{
    struct sigaction act, oact;

    act.sa_sigaction = signal_handler; //指定信号处理回调函数
    sigemptyset(&act.sa_mask); // 阻塞集为空
    act.sa_flags = SA_SIGINFO; // 指定调用 signal_handler

    // 注册信号 SIGINT
    sigaction(SIGINT, &act, &oact);

    while (1)
    {
        printf("pid is %d\n", getpid()); // 进程号

        pause(); // 捕获信号，此函数会阻塞
    }

    return 0;
}

```

两个终端分别编译代码，一个进程接收，一个进程发送，运行结果如下：

![1527931650109](assets/1527931650109.png)

 

 

## 10. 不可重入、可重入函数

如果有一个函数不幸被设计成为这样：那么不同任务调用这个函数时可能修改其他任务调用这个函数的数据，从而导致不可预料的后果。这样的函数是不安全的函数，也叫不可重入函数。

 

满足下列条件的函数多数是不可重入（不安全）的：

- 函数体内使用了静态的数据结构；
- 函数体内调用了malloc() 或者 free() 函数(谨慎使用堆)；
- 函数体内调用了标准 I/O 函数。

 

相反，肯定有一个安全的函数，这个安全的函数又叫可重入函数。那么什么是可重入函数呢？所谓可重入是指一个可以被多个任务调用的过程，任务在调用时不必担心数据是否会出错。

 

保证函数的可重入性的方法：

- 在写函数时候尽量使用局部变量（例如寄存器、栈中的变量）；
- 对于要使用的全局变量要加以保护（如采取关中断、信号量等互斥方法），这样构成的函数就一定是一个可重入的函数。

 

Linux常见的可重入函数：

![1527931811952](assets/1527931811952.png)

**注意：信号处理函数应该为可重入函数。**

 

## 11. SIGCHLD信号

### 11.1 SIGCHLD信号产生的条件

1) 子进程终止时
2) 子进程接收到SIGSTOP信号停止时
3) 子进程处在停止态，接受到SIGCONT后唤醒时

 

### 11.2 如何避免僵尸进程

1) 最简单的方法，父进程通过 wait() 和 waitpid() 等函数等待子进程结束，但是，这会导致父进程挂起。
2) 如果父进程要处理的事情很多，不能够挂起，通过 signal() 函数人为处理信号 SIGCHLD ， 只要有子进程退出自动调用指定好的回调函数，因为子进程结束后， 父进程会收到该信号 SIGCHLD ，可以在其回调函数里调用 wait() 或 waitpid() 回收。

示例程序:

```
void sig_child(int signo)
{
    pid_t  pid;

    //处理僵尸进程, -1 代表等待任意一个子进程, WNOHANG代表不阻塞
    while ((pid = waitpid(-1, NULL, WNOHANG)) > 0)
    {
        printf("child %d terminated.\n", pid);
    }
}

int main()
{
    pid_t pid;

    // 创建捕捉子进程退出信号
    // 只要子进程退出，触发SIGCHLD，自动调用sig_child()
    signal(SIGCHLD, sig_child);

    pid = fork();   // 创建进程
    if (pid < 0)
    { // 出错
        perror("fork error:");
        exit(1);
    }
    else if (pid == 0)
    { // 子进程
        printf("I am child process,pid id %d.I am exiting.\n", getpid());
        exit(0);
    }
    else if (pid > 0)
    { // 父进程
        sleep(2);   // 保证子进程先运行
        printf("I am father, i am exited\n\n");
        system("ps -ef | grep defunct"); // 查看有没有僵尸进程
    }

    return 0;
}

```

 

3）如果父进程不关心子进程什么时候结束，那么可以用signal（SIGCHLD, SIG_IGN）通知内核，自己对子进程的结束不感兴趣，父进程忽略此信号，那么子进程结束后，内核会回收， 并不再给父进程发送信号。

示例程序:

```
int main()
{
    pid_t pid;

    // 忽略子进程退出信号的信号
    // 那么子进程结束后，内核会回收， 并不再给父进程发送信号
    signal(SIGCHLD, SIG_IGN);

    pid = fork();   // 创建进程

    if (pid < 0)
    { // 出错
        perror("fork error:");
        exit(1);
    }
    else if (pid == 0)
    { // 子进程
        printf("I am child process,pid id %d.I am exiting.\n", getpid());
        exit(0);

    }
    else if (pid > 0)
    { // 父进程
        sleep(2);   // 保证子进程先运行
        printf("I am father, i am exited\n\n");
        system("ps -ef | grep defunct"); // 查看有没有僵尸进程
    }

    return 0;
}

```

 

## 12. 作业

**1. 实现类似ps aux | grep "bash"功能**

提示: 使用多进程 和execl函数 dup2函数

 

## 13. 总结

# 线程

## 01. 学习目标

- 了解终端的概念
- 了解进程组的概念
- 了解会话概念
- 熟练掌握守护进程创建
- 了解线程优缺点和基本概念
- 熟练掌握线程基本操作函数
- 了解线程属性的设置

 

- 说出守护进程的特点
- 独立完成守护进程的创建
- 独立实现多个线程的创建
- 独立实现线程的退出和资源回收
- 独立实现线程的取消(杀死线程)
- 使用线程属性设置线程分离

## 02. 终端的概念(了解)

在UNIX系统中，用户通过终端登录系统后得到一个Shell进程，这个终端成为Shell进程的控制终端（Controlling Terminal），进程中，控制终端是保存在PCB中的信息，而fork会复制PCB中的信息，因此由Shell进程启动的其它进程的控制终端也是这个终端。

默认情况下（没有重定向），每个进程的标准输入、标准输出和标准错误输出都指向控制终端，进程从标准输入读也就是读用户的键盘输入，进程往标准输出或标准错误输出写也就是输出到显示器上。

信号中还讲过，在控制终端输入一些特殊的控制键可以给前台进程发信号，例如Ctrl+C表示SIGINT，Ctrl+\表示SIGQUIT。

 

函数说明：

```
#include <unistd.h>

char *ttyname(int fd);
功能：由文件描述符查出对应的文件名
参数：
    fd：文件描述符
返回值：
    成功：终端名
    失败：NULL
```

 

下面我们借助ttyname函数，通过实验看一下各种不同的终端所对应的设备文件名：

```
int main()
{
    printf("fd 0: %s\n", ttyname(0));
    printf("fd 1: %s\n", ttyname(1));
    printf("fd 2: %s\n", ttyname(2));

    return 0;
}

```

 

## 03. 进程组概念(理解)

### 3.1 进程组概述

进程组，也称之为作业。BSD于1980年前后向Unix中增加的一个新特性。**代表一个或多个进程的集合。**

每个进程都属于一个进程组。在waitpid函数和kill函数的参数中都曾使用到。操作系统设计的进程组的概念，是为了简化对多个进程的管理。

当父进程，创建子进程的时候，默认子进程与父进程属于同一进程组。进程组ID为第一个进程ID(组长进程)。所以，组长进程标识：其进程组ID为其进程ID



可以使用**kill -SIGKILL -进程组ID**(负的)来将整个进程组内的进程全部杀死：

![1528119946594](assets/1528119946594.png)

组长进程可以创建一个进程组，创建该进程组中的进程，然后终止。只要进程组中有一个进程存在，进程组就存在，与组长进程是否终止无关。

进程组生存期：进程组创建到最后一个进程离开(终止或转移到另一个进程组)。

一个进程可以为自己或子进程设置进程组ID。

 

### 3.2 相关函数说明

```
#include <unistd.h>

pid_t getpgrp(void);                 /* POSIX.1 version */
功能：获取当前进程的进程组ID
参数：无
返回值：总是返回调用者的进程组ID

pid_t getpgid(pid_t pid);
功能：获取指定进程的进程组ID
参数：
    pid：进程号，如果pid = 0，那么该函数作用和getpgrp一样
返回值：
    成功：进程组ID
    失败：-1

int setpgid(pid_t pid, pid_t pgid);
功能：
    改变进程默认所属的进程组。通常可用来加入一个现有的进程组或创建一个新进程组。
参数：
    将参1对应的进程，加入参2对应的进程组中
返回值：
    成功：0
    失败：-1
```

 

## 04. 会话(了解)

### 4.1 会话概念

会话是一个或多个进程组的集合。

- 一个会话可以有一个控制终端。这通常是终端设备或伪终端设备；
- 建立与控制终端连接的会话首进程被称为控制进程；
- 一个会话中的几个进程组可被分为一个前台进程组以及一个或多个后台进程组；
- 如果一个会话有一个控制终端，则它有一个前台进程组，其它进程组为后台进程组；
- 如果终端接口检测到断开连接，则将挂断信号发送至控制进程（会话首进程）。

![1528120442841](assets/1528120442841.png)

 

### 4.2 创建会话注意事项

1) 调用进程不能是进程组组长，该进程变成新会话首进程(session header)
2) 该调用进程是组长进程，则出错返回
3) 该进程成为一个新进程组的组长进程
4) 需有root权限(ubuntu不需要)
5) 新会话丢弃原有的控制终端，该会话没有控制终端
6) 建立新会话时，先调用fork, 父进程终止，子进程调用setsid



### 4.3 API函数介绍

getsid函数：

```
#include <unistd.h>

pid_t getsid(pid_t pid);
功能：获取进程所属的会话ID
参数：
    pid：进程号，pid为0表示查看当前进程session ID
返回值：
    成功：返回调用进程的会话ID
    失败：-1
```

组长进程不能成为新会话首进程，新会话首进程必定会成为组长进程。

setsid函数：

```
#include <unistd.h>

pid_t setsid(void);
功能：
    创建一个会话，并以自己的ID设置进程组ID，同时也是新会话的ID。调用了setsid函数的进程，既是新的会长，也是新的组长。
参数：无
返回值：
    成功：返回调用进程的会话ID
    失败：-1

```

 

## 05. 守护进程(重点)

### 5.1 守护进程介绍

守护进程（Daemon Process），也就是通常说的 Daemon 进程（精灵进程），是 Linux 中的后台服务进程。它是一个生存期较长的进程，通常独立于控制终端并且周期性地执行某种任务或等待处理某些发生的事件。一般采用以d结尾的名字。

守护进程是个特殊的孤儿进程，这种进程脱离终端，为什么要脱离终端呢？之所以脱离于终端是为了避免进程被任何终端所产生的信息所打断，其在执行过程中的信息也不在任何终端上显示。由于在 Linux 中，每一个系统与用户进行交流的界面称为终端，每一个从此终端开始运行的进程都会依附于这个终端，这个终端就称为这些进程的控制终端，当控制终端被关闭时，相应的进程都会自动关闭。

Linux 的大多数服务器就是用守护进程实现的。比如，Internet 服务器 inetd，Web 服务器 httpd 等。

### 5.2 守护进程模型

1) 创建子进程，父进程退出(必须)

- 所有工作在子进程中进行形式上脱离了控制终端
- 在子进程中创建新会话(必须)

- setsid()函数
- 使子进程完全独立出来，脱离控制
- 改变当前目录为根目录(不是必须)

- chdir()函数
- 防止占用可卸载的文件系统
- 也可以换成其它路径
- 重设文件权限掩码(不是必须)

- umask()函数
- 防止继承的文件创建屏蔽字拒绝某些权限
- 增加守护进程灵活性
- 关闭文件描述符(不是必须)

- 继承的打开文件不会用到，浪费系统资源，无法卸载
- 开始执行守护进程核心工作(必须)

守护进程退出处理程序模型

### 5.3 守护进程参考代码

写一个守护进程, 每隔2s获取一次系统时间, 将这个时间写入到磁盘文件：

```
/*
* time_t rawtime;
* time ( &rawtime  ); --- 获取时间，以秒计，从1970年1月一日起算，存于rawtime
* localtime ( &rawtime  ); //转为当地时间，tm 时间结构
* asctime() // 转为标准ASCII时间格式：
*/
void write_time(int num)
{
    time_t rawtime;
    struct tm * timeinfo;
    // 获取时间
    time(&rawtime);
#if 0
    // 转为本地时间
    timeinfo = localtime(&rawtime);
    // 转为标准ASCII时间格式
    char *cur = asctime(timeinfo);
#else
    char* cur = ctime(&rawtime);
#endif

    // 将得到的时间写入文件中
    int fd = open("/home/edu/timelog.txt", O_RDWR | O_CREAT | O_APPEND, 0664);
    if (fd == -1)
    {
        perror("open error");
        exit(1);
    }
    // 写文件
    int ret = write(fd, cur, strlen(cur) + 1);
    if (ret == -1)
    {
        perror("write error");
        exit(1);
    }
    // 关闭文件
    close(fd);
}

int main(int argc, const char* argv[])
{
    pid_t pid = fork();
    if (pid == -1)
    {
        perror("fork error");
        exit(1);
    }

    if (pid > 0)
    {
        // 父进程退出
        exit(1);
    }
    else if (pid == 0)
    {
        // 子进程
        // 提升为会长，同时也是新进程组的组长
        setsid();

        // 更改进程的执行目录
        chdir("/home/edu");

        // 更改掩码
        umask(0022);

        // 关闭文件描述符
        close(STDIN_FILENO);
        close(STDOUT_FILENO);
        close(STDERR_FILENO);

        // 注册信号捕捉函数
        //先注册，再定时
        struct sigaction sigact;
        sigact.sa_flags = 0;
        sigemptyset(&sigact.sa_mask);
        sigact.sa_handler = write_time;
        sigaction(SIGALRM, &sigact, NULL);

        // 设置定时器
        struct itimerval act;
        // 定时周期
        act.it_interval.tv_sec = 2;
        act.it_interval.tv_usec = 0;
        // 设置第一次触发定时器时间
        act.it_value.tv_sec = 2;
        act.it_value.tv_usec = 0;
        // 开始计时
        setitimer(ITIMER_REAL, &act, NULL);

        // 防止子进程退出
        while (1);
    }

    return 0;
}
```

 

## 06. 线程简介

### 6.1 线程概念

在许多经典的操作系统教科书中，总是把进程定义为程序的执行实例，它并不执行什么, 只是维护应用程序所需的各种资源，而线程则是真正的执行实体。

所以，线程是轻量级的进程（LWP：light weight process），在Linux环境下线程的本质仍是进程。

为了让进程完成一定的工作，进程必须至少包含一个线程。

![1528121100232](assets/1528121100232.png)

 

进程，直观点说，保存在硬盘上的程序运行以后，会在内存空间里形成一个独立的内存体，这个内存体有自己的地址空间，有自己的堆，上级挂靠单位是操作系统。操作系统会以进程为单位，分配系统资源，所以我们也说，**进程是CPU分配资源的最小单位**。

线程存在与进程当中(进程可以认为是线程的容器)，是操作系统调度执行的最小单位。说通俗点，线程就是干活的。

进程是具有一定独立功能的程序关于某个数据集合上的一次运行活动，进程是系统进行资源分配和调度的一个独立单位。

线程是进程的一个实体，是 CPU 调度和分派的基本单位，它是比进程更小的能独立运行的基本单位。线程自己基本上不拥有系统资源，只拥有一点在运行中必不可少的资源（如程序计数器，一组寄存器和栈），但是它可与同属一个进程的其他的线程共享进程所拥有的全部资源。

如果说进程是一个资源管家，负责从主人那里要资源的话，那么线程就是干活的苦力。一个管家必须完成一项工作，就需要最少一个苦力，也就是说，一个进程最少包含一个线程，也可以包含多个线程。苦力要干活，就需要依托于管家，所以说一个线程，必须属于某一个进程。

进程有自己的地址空间，线程使用进程的地址空间，也就是说，进程里的资源，线程都是有权访问的，比如说堆啊，栈啊，静态存储区什么的。

 

> 进程是操作系统分配资源的最小单位
>
> 线程是操作系统调度的最小单位



### 6.2 线程函数列表安装

命令：

> sudo apt-get install manpages-posix-dev

【说明】manpages-posix-dev 包含 POSIX 的 header files 和 library calls 的用法

查看：

> man -k pthread

 

### 6.3 NPTL

当 Linux 最初开发时，在内核中并不能真正支持线程。但是它的确可以通过 clone() 系统调用将进程作为可调度的实体。这个调用创建了调用进程（calling process）的一个拷贝，这个拷贝与调用进程共享相同的地址空间。LinuxThreads 项目使用这个调用来完全在用户空间模拟对线程的支持。不幸的是，这种方法有一些缺点，尤其是在信号处理、调度和进程间同步原语方面都存在问题。另外，这个线程模型也不符合 POSIX 的要求。

要改进 LinuxThreads，非常明显我们需要内核的支持，并且需要重写线程库。有两个相互竞争的项目开始来满足这些要求。一个包括 IBM 的开发人员的团队开展了 NGPT（Next-Generation POSIX Threads）项目。同时，Red Hat 的一些开发人员开展了 NPTL 项目。NGPT 在 2003 年中期被放弃了，把这个领域完全留给了 NPTL。

NPTL，或称为 Native POSIX Thread Library，是 Linux 线程的一个新实现，它克服了 LinuxThreads 的缺点，同时也符合 POSIX 的需求。与 LinuxThreads 相比，它在性能和稳定性方面都提供了重大的改进。

查看当前pthread库版本：getconf GNU_LIBPTHREAD_VERSION

![1528121402843](assets/1528121402843.png)

### 6.4 线程的特点

类Unix系统中，早期是没有“线程”概念的，80年代才引入，借助进程机制实现出了线程的概念。

 

因此在这类系统中，进程和线程关系密切：

1) 线程是轻量级进程(light-weight process)，也有PCB，创建线程使用的底层函数和进程一样，都是clone
2) 从内核里看进程和线程是一样的，都有各自不同的PCB.
3) 进程可以蜕变成线程
4) 在linux下，线程最是小的执行单位；进程是最小的分配资源单位

![1528121496711](assets/1528121496711.png)

查看指定进程的LWP号：

> ps  -Lf  pid

实际上，无论是创建进程的fork，还是创建线程的pthread_create，底层实现都是调用同一个内核函数 clone 。

Ø 如果复制对方的地址空间，那么就产出一个“进程”；

Ø 如果共享对方的地址空间，就产生一个“线程”。

Linux内核是不区分进程和线程的, 只在用户层面上进行区分。所以，线程所有操作函数 pthread_* 是库函数，而非系统调用。

 

### 6.5 线程共享资源

1) 文件描述符表
2) 每种信号的处理方式
3) 当前工作目录
4) 用户ID和组ID

内存地址空间 (.text/.data/.bss/heap/共享库)

### 6.6 线程非共享资源

1) 线程id
2) 处理器现场和栈指针(内核栈)
3) 独立的栈空间(用户空间栈)
4) errno变量
5) 信号屏蔽字
6) 调度优先级

 

### 6.7 线程的优缺点

**优点：**

Ø 提高程序并发性

Ø 开销小

Ø 数据通信、共享数据方便



**缺点：**

Ø 库函数，不稳定

Ø 调试、编写困难、gdb不支持

Ø 对信号支持不好

优点相对突出，缺点均不是硬伤。Linux下由于实现方法导致进程、线程差别不是很大。

 

## 07. 线程常用操作

### 7.1 线程号

就像每个进程都有一个进程号一样，每个线程也有一个线程号。进程号在整个系统中是唯一的，但线程号不同，线程号只在它所属的进程环境中有效。

进程号用 pid_t 数据类型表示，是一个非负整数。线程号则用 pthread_t 数据类型来表示，Linux 使用无符号长整数表示。

有的系统在实现pthread_t 的时候，用一个结构体来表示，所以在可移植的操作系统实现不能把它做为整数处理。

 

pthread_self函数：

```
#include <pthread.h>

pthread_t pthread_self(void);
功能：
    获取线程号。
参数：
    无
返回值：
    调用线程的线程 ID 。
    
```

 

pthread_equal函数:

```
int pthread_equal(pthread_t t1, pthread_t t2);
功能：
    判断线程号 t1 和 t2 是否相等。为了方便移植，尽量使用函数来比较线程 ID。
参数：
    t1，t2：待判断的线程号。
返回值：
    相等：  非 0
    不相等：0
```

参考程序：

```
int main()
{
    pthread_t thread_id;

    thread_id = pthread_self(); // 返回调用线程的线程ID
    printf("Thread ID = %lu \n", thread_id);

    if (0 != pthread_equal(thread_id, pthread_self()))
    {
        printf("Equal!\n");
    }
    else
    {
        printf("Not equal!\n");
    }

    return 0;
}
```

【注意】线程函数的程序在 pthread 库中，故链接时要加上参数 -lpthread。

### 7.2 线程的创建

pthread_create函数：

```
#include <pthread.h>

int pthread_create(pthread_t *thread,
            const pthread_attr_t *attr,
            void *(*start_routine)(void *),
            void *arg );
功能：
    创建一个线程。
参数：
    thread：线程标识符地址。
    attr：线程属性结构体地址，通常设置为 NULL。
    start_routine：线程函数的入口地址。
    arg：传给线程函数的参数。
返回值：
    成功：0
    失败：非 0
```

在一个线程中调用pthread_create()创建新的线程后，当前线程从pthread_create()返回继续往下执行，而新的线程所执行的代码由我们传给pthread_create的函数指针start_routine决定。

由于pthread_create的错误码不保存在errno中，因此不能直接用perror()打印错误信息，可以先用strerror()把错误码转换成错误信息再打印。

 

参考程序：

```
// 回调函数
void *thread_fun(void * arg)
{
    sleep(1);
    int num = *((int *)arg);
    printf("int the new thread: num = %d\n", num);

    return NULL;
}

int main()
{
    pthread_t tid;
    int test = 100;

    // 返回错误号
    int ret = pthread_create(&tid, NULL, thread_fun, (void *)&test);
    if (ret != 0)
    {
        printf("error number: %d\n", ret);
        // 根据错误号打印错误信息
        printf("error information: %s\n", strerror(ret));
    }

    while (1);

    return 0;
}
```

 

### 7.3 线程资源回收

pthread_join函数：

```
#include <pthread.h>

int pthread_join(pthread_t thread, void **retval);
功能：
    等待线程结束（此函数会阻塞），并回收线程资源，类似进程的 wait() 函数。如果线程已经结束，那么该函数会立即返回。
参数：
    thread：被等待的线程号。
    retval：用来存储线程退出状态的指针的地址。
返回值：
    成功：0
    失败：非 0

```

 

参考程序：

```
void *thead(void *arg)
{
    static int num = 123; //静态变量

    printf("after 2 seceonds, thread will return\n");
    sleep(2);

    return &num;
}

int main()
{
    pthread_t tid;
    int ret = 0;
    void *value = NULL;

    // 创建线程
    pthread_create(&tid, NULL, thead, NULL);


    // 等待线程号为 tid 的线程，如果此线程结束就回收其资源
    // &value保存线程退出的返回值
    pthread_join(tid, &value);

    printf("value = %d\n", *((int *)value));

    return 0;
}
```

调用该函数的线程将挂起等待，直到id为thread的线程终止。thread线程以不同的方法终止，通过pthread_join得到的终止状态是不同的，总结如下：

1) 如果thread线程通过return返回，retval所指向的单元里存放的是thread线程函数的返回值。
2) 如果thread线程被别的线程调用pthread_cancel异常终止掉，retval所指向的单元里存放的是常数PTHREAD_CANCELED。
3) 如果thread线程是自己调用pthread_exit终止的，retval所指向的单元存放的是传给pthread_exit的参数。

 

### 7.4 线程分离

一般情况下，线程终止后，其终止状态一直保留到其它线程调用pthread_join获取它的状态为止。但是线程也可以被置为detach状态，这样的线程一旦终止就立刻回收它占用的所有资源，而不保留终止状态。

不能对一个已经处于detach状态的线程调用pthread_join，这样的调用将返回EINVAL错误。也就是说，如果已经对一个线程调用了pthread_detach就不能再调用pthread_join了。

 

pthread_detach函数：

```
#include <pthread.h>

int pthread_detach(pthread_t thread);
功能：
    使调用线程与当前进程分离，分离后不代表此线程不依赖与当前进程，线程分离的目的是将线程资源的回收工作交由系统自动来完成，也就是说当被分离的线程结束之后，系统会自动回收它的资源。所以，此函数不会阻塞。
参数：
    thread：线程号。
返回值：
    成功：0
    失败：非0
```

 

### 7.5 线程退出

在进程中我们可以调用exit函数或_exit函数来结束进程，在一个线程中我们可以通过以下三种在不终止整个进程的情况下停止它的控制流。

- 线程从执行函数中返回。
- 线程调用pthread_exit退出线程。
- 线程可以被同一进程中的其它线程取消。

 

pthread_exit函数：

```
#include <pthread.h>

void pthread_exit(void *retval);
功能：
    退出调用线程。一个进程中的多个线程是共享该进程的数据段，因此，通常线程退出后所占用的资源并不会释放。
参数：
    retval：存储线程退出状态的指针。
返回值：无  

```

参考程序:

```
void *thread(void *arg)
{
    static int num = 123; //静态变量
    int i = 0;
    while (1)
    {
        printf("I am runing\n");
        sleep(1);
        i++;
        if (i == 3)
        {
            pthread_exit((void *)&num);
            // return &num;
        }
    }

    return NULL;
}

int main(int argc, char *argv[])
{
    int ret = 0;
    pthread_t tid;
    void *value = NULL;

    pthread_create(&tid, NULL, thread, NULL);


    pthread_join(tid, &value);
    printf("value = %d\n", *(int *)value);

    return 0;
}

```

### 7.6 线程取消

```
#include <pthread.h>

int pthread_cancel(pthread_t thread);
功能：
    杀死(取消)线程
参数：
    thread : 目标线程ID。
返回值：
    成功：0
    失败：出错编号

```

注意：线程的取消并不是实时的，而又一定的延时。需要等待线程到达某个取消点(检查点)。

类似于玩游戏存档，必须到达指定的场所(存档点，如：客栈、仓库、城里等)才能存储进度。

杀死线程也不是立刻就能完成，必须要到达取消点。

取消点：是线程检查是否被取消，并按请求进行动作的一个位置。通常是一些系统调用creat，open，pause，close，read，write..... 执行命令**man 7 pthreads**可以查看具备这些取消点的系统调用列表。

可粗略认为一个系统调用(进入内核)即为一个取消点。

参考程序:

```
void *thread_cancel(void *arg)
{
    while (1)
    {
        pthread_testcancel(); //设置取消点
    }
    return NULL;
}

int main()
{
    pthread_t tid;
    pthread_create(&tid, NULL, thread_cancel, NULL); //创建线程

    sleep(3);                   //3秒后
    pthread_cancel(tid); //取消tid线程

    pthread_join(tid, NULL);

    return 0;
}

```

 

## 08. 线程属性（了解）

### 8.1 概述

Linux下线程的属性是可以根据实际项目需要，进行设置，之前我们讨论的线程都是采用线程的默认属性，默认属性已经可以解决绝大多数开发时遇到的问题。

如我们对程序的性能提出更高的要求那么需要设置线程属性，比如可以通过设置线程栈的大小来降低内存的使用，增加最大线程个数。

```
typedef struct
{
    int             etachstate;     //线程的分离状态
    int             schedpolicy;    //线程调度策略
    struct sched_param  schedparam; //线程的调度参数
    int             inheritsched;   //线程的继承性
    int             scope;      //线程的作用域
    size_t          guardsize;  //线程栈末尾的警戒缓冲区大小
    int             stackaddr_set; //线程的栈设置
    void*           stackaddr;  //线程栈的位置
    size_t          stacksize;  //线程栈的大小
} pthread_attr_t;
```

主要结构体成员：

1) 线程分离状态
2) 线程栈大小（默认平均分配）
3) 线程栈警戒缓冲区大小（位于栈末尾）
4) 线程栈最低地址



属性值不能直接设置，须使用相关函数进行操作，初始化的函数为pthread_attr_init，这个函数必须在pthread_create函数之前调用。之后须用pthread_attr_destroy函数来释放资源。

线程属性主要包括如下属性：作用域（scope）、栈尺寸（stack size）、栈地址（stack address）、优先级（priority）、分离的状态（detached state）、调度策略和参数（scheduling policy and parameters）。默认的属性为非绑定、非分离、缺省的堆栈、与父进程同样级别的优先级。

### 8.2 线程属性初始化和销毁

```
#include <pthread.h>

int pthread_attr_init(pthread_attr_t *attr);
功能：
    初始化线程属性函数，注意：应先初始化线程属性，再pthread_create创建线程
参数：
    attr：线程属性结构体
返回值：
    成功：0
    失败：错误号

int pthread_attr_destroy(pthread_attr_t *attr);
功能：
    销毁线程属性所占用的资源函数
参数：
    attr：线程属性结构体
返回值：
    成功：0
    失败：错误号
```

### 8.3 线程分离状态

线程的分离状态决定一个线程以什么样的方式来终止自己。

- 非分离状态：线程的默认属性是非分离状态，这种情况下，原有的线程等待创建的线程结束。只有当pthread_join()函数返回时，创建的线程才算终止，才能释放自己占用的系统资源。
- 分离状态：分离线程没有被其他的线程所等待，自己运行结束了，线程也就终止了，马上释放系统资源。应该根据自己的需要，选择适当的分离状态。

相关函数：

```
#include <pthread.h>

int pthread_attr_setdetachstate(pthread_attr_t *attr, int detachstate);
功能：设置线程分离状态
参数：
    attr：已初始化的线程属性
    detachstate：    分离状态
        PTHREAD_CREATE_DETACHED（分离线程）
        PTHREAD_CREATE_JOINABLE（非分离线程）
返回值：
    成功：0
    失败：非0

int pthread_attr_getdetachstate(const pthread_attr_t *attr, int *detachstate);
功能：获取线程分离状态
参数：
    attr：已初始化的线程属性
    detachstate：    分离状态
        PTHREAD_CREATE_DETACHED（分离线程）
        PTHREAD _CREATE_JOINABLE（非分离线程）
返回值：
    成功：0
    失败：非0

```

这里要注意的一点是，如果设置一个线程为分离线程，而这个线程运行又非常快，它很可能在pthread_create函数返回之前就终止了，它终止以后就可能将线程号和系统资源移交给其他的线程使用，这样调用pthread_create的线程就得到了错误的线程号。

要避免这种情况可以采取一定的同步措施，最简单的方法之一是可以在被创建的线程里调用pthread_cond_timedwait函数，让这个线程等待一会儿，留出足够的时间让函数pthread_create返回。

设置一段等待时间，是在多线程编程里常用的方法。但是注意不要使用诸如wait()之类的函数，它们是使整个进程睡眠，并不能解决线程同步的问题。

### 8.4 线程栈地址

POSIX.1定义了两个常量来检测系统是否支持栈属性：

- _POSIX_THREAD_ATTR_STACKADDR
- _POSIX_THREAD_ATTR_STACKSIZE

也可以给sysconf函数传递来进行检测：

- _SC_THREAD_ATTR_STACKADDR
- _SC_THREAD_ATTR_STACKSIZE

当进程栈地址空间不够用时，指定新建线程使用由malloc分配的空间作为自己的栈空间。通过pthread_attr_setstack和pthread_attr_getstack两个函数分别设置和获取线程的栈地址。

```
#include <pthread.h>

int pthread_attr_setstack(pthread_attr_t *attr, void *stackaddr,  size_t stacksize);
功能：设置线程的栈地址
参数：
    attr：指向一个线程属性的指针
    stackaddr：内存首地址
    stacksize：返回线程的堆栈大小
返回值：
    成功：0
    失败：错误号

int pthread_attr_getstack(const pthread_attr_t *attr, void **stackaddr,  size_t *stacksize);
功能：获取线程的栈地址
参数：
    attr：指向一个线程属性的指针
    stackaddr：返回获取的栈地址
    stacksize：返回获取的栈大小
返回值：
    成功：0
    失败：错误号

```

 

### 8.5 线程栈大小

当系统中有很多线程时，可能需要减小每个线程栈的默认大小，防止进程的地址空间不够用,当线程调用的函数会分配很大的局部变量或者函数调用层次很深时，可能需要增大线程栈的默认大小。

```
#include <pthread.h>

int pthread_attr_setstacksize(pthread_attr_t *attr, size_t stacksize);
功能：设置线程的栈大小
参数：
    attr：指向一个线程属性的指针
    stacksize：线程的堆栈大小
返回值：
    成功：0
    失败：错误号

int pthread_attr_getstacksize(const pthread_attr_t *attr, size_t *stacksize);
功能：获取线程的栈大小
参数： 
    attr：指向一个线程属性的指针
    stacksize：返回线程的堆栈大小
返回值：
    成功：0
    失败：错误号

```

 

### 8.6 综合参考程序

```
#define SIZE 0x100000

void *th_fun(void *arg)
{
    while (1)
    {
        sleep(1);
    }
}

int main()
{
    pthread_t tid;
    int err, detachstate, i = 1;

    pthread_attr_t attr;
    size_t stacksize;
    void *stackaddr;

    pthread_attr_init(&attr);  //线程属性初始化
    pthread_attr_getstack(&attr, &stackaddr, &stacksize); //获取线程的栈地址
    pthread_attr_getdetachstate(&attr, &detachstate);           //获取线程分离状态

    if (detachstate == PTHREAD_CREATE_DETACHED)
    {
        printf("thread detached\n");
    }
    else if (detachstate == PTHREAD_CREATE_JOINABLE)
    {
        printf("thread join\n");
    }
    else
    {
        printf("thread unknown\n");
    }
        
    pthread_attr_setdetachstate(&attr, PTHREAD_CREATE_DETACHED); //设置分离状态

    while (1) 
    {
        stackaddr = malloc(SIZE);
        if (stackaddr == NULL) 
        {
            perror("malloc");
            exit(1);
        }

        stacksize = SIZE;
        pthread_attr_setstack(&attr, stackaddr, stacksize); //设置线程的栈地址
        err = pthread_create(&tid, &attr, th_fun, NULL); //创建线程
        if (err != 0) 
        {
            printf("%s\n", strerror(err));
            exit(1);
        }
        printf("%d\n", i++);
    }

    pthread_attr_destroy(&attr); //销毁线程属性所占用的资源函数

    return 0;
}
```

### 8.7 线程使用注意事项

1) 主线程退出其他线程不退出，主线程应调用pthread_exit
2) 避免僵尸线程

a) pthread_join

b) pthread_detach

c) pthread_create指定分离属性

被join线程可能在join函数返回前就释放完自己的所有内存资源，所以不应当返回被回收线程栈中的值;

3) malloc和mmap申请的内存可以被其他线程释放
4) 应避免在多线程模型中调用fork，除非马上exec，子进程中只有调用fork的线程存在，其他线程t在子进程中均pthread_exit
5) 信号的复杂语义很难和多线程共存，应避免在多线程引入信号机制

 

## 09. 作业

1） 创建两个子线程， 第一个子线程输出所有的大写字母(A-Z)，第二个子线程输出所有小写字母(a-z)，每输出一个字母都要睡眠(usleep)。 100ms

 

## 10. 总结

#  线程同步

## 02. 学习目标

- 熟练掌握互斥量的使用
- 说出什么叫死锁以及解决方案
- 熟练掌握读写锁的使用
- 熟练掌握条件变量的使用
- 熟练掌握条件变量实现生产消费者模型
- 熟练掌握信号量实现生产消费者模型

 

## 03. 互斥锁

### 3.1 同步与互斥概述

现代操作系统基本都是多任务操作系统，即同时有大量可调度实体在运行。在多任务操作系统中，同时运行的多个任务可能：

- 都需要访问/使用同一种资源
- 多个任务之间有依赖关系，某个任务的运行依赖于另一个任务

这两种情形是多任务编程中遇到的最基本的问题，也是多任务编程中的核心问题，同步和互斥就是用于解决这两个问题的。

**互斥：**是指散步在不同任务之间的若干程序片断，当某个任务运行其中一个程序片段时，其它任务就不能运行它们之中的任一程序片段，只能等到该任务运行完这个程序片段后才可以运行。最基本的场景就是：一个公共资源同一时刻只能被一个进程或线程使用，多个进程或线程不能同时使用公共资源。



**同步：**是指散步在不同任务之间的若干程序片断，它们的运行必须严格按照规定的某种先后次序来运行，这种先后次序依赖于要完成的特定的任务。最基本的场景就是：两个或两个以上的进程或线程在运行过程中协同步调，按预定的先后次序运行。比如 A 任务的运行依赖于 B 任务产生的数据。

显然，同步是一种更为复杂的互斥，而互斥是一种特殊的同步。也就是说互斥是两个任务之间不可以同时运行，他们会相互排斥，必须等待一个线程运行完毕，另一个才能运行，而同步也是不能同时运行，但他是必须要按照某种次序来运行相应的线程（也是一种互斥）！因此互斥具有唯一性和排它性，但互斥并不限制任务的运行顺序，即任务是无序的，而同步的任务之间则有顺序关系。

### 3.2 为什么需要互斥锁

在多任务操作系统中，同时运行的多个任务可能都需要使用同一种资源。这个过程有点类似于，公司部门里，我在使用着打印机打印东西的同时（还没有打印完），别人刚好也在此刻使用打印机打印东西，如果不做任何处理的话，打印出来的东西肯定是错乱的。

下面我们用程序模拟一下这个过程，线程一需要打印“ hello ”，线程二需要打印“ world ”，不加任何处理的话，打印出来的内容会错乱：

测试程序：

```
// 打印机，公共资源
void printer(char *str)
{
    while (*str != '\0')
    {
        putchar(*str);
        fflush(stdout);
        str++;
        sleep(1);
    }
    printf("\n");
}

// 线程一
void *thread_fun_1(void *arg)
{
    char *str = "hello";
    printer(str); //打印
}

// 线程二
void *thread_fun_2(void *arg)
{
    char *str = "world";
    printer(str); //打印
}

int main()
{
    pthread_t tid1, tid2;

    // 创建 2 个线程
    pthread_create(&tid1, NULL, thread_fun_1, NULL);
    pthread_create(&tid2, NULL, thread_fun_2, NULL);

    // 等待线程结束，回收其资源
    pthread_join(tid1, NULL);
    pthread_join(tid2, NULL);

    return 0;
}
```

运行结果如下：

 

实际上，打印机是有做处理的，我在打印着的时候别人是不允许打印的，只有等我打印结束后别人才允许打印。这个过程有点类似于，把打印机放在一个房间里，给这个房间安把锁，这个锁默认是打开的。当 A 需要打印时，他先过来检查这把锁有没有锁着，没有的话就进去，同时上锁在房间里打印。而在这时，刚好 B 也需要打印，B 同样先检查锁，发现锁是锁住的，他就在门外等着。而当 A 打印结束后，他会开锁出来，这时候 B 才进去上锁打印。

 

### 3.3 互斥锁Mutex介绍

而在线程里也有这么一把锁：互斥锁（mutex），也叫互斥量，互斥锁是一种简单的加锁的方法来控制对共享资源的访问，互斥锁只有两种状态,即**加锁**( lock )和**解锁**( unlock )。



互斥锁的操作流程如下：

1）在访问共享资源后临界区域前，对互斥锁进行加锁。

2）在访问完成后释放互斥锁导上的锁。

3）对互斥锁进行加锁后，任何其他试图再次对互斥锁加锁的线程将会被阻塞，直到锁被释放。



互斥锁的数据类型是： pthread_mutex_t。

 

安装对应帮助手册：

> deng@itcast:~$ sudo apt-get install manpages-posix-dev

### 3.4 **pthread_mutex_init** 函数

初始化互斥锁：

```
#include <pthread.h>

int pthread_mutex_init(pthread_mutex_t *restrict mutex,
    const pthread_mutexattr_t *restrict attr);
功能：
    初始化一个互斥锁。
参数：
    mutex：互斥锁地址。类型是 pthread_mutex_t 。
    attr：设置互斥量的属性，通常可采用默认属性，即可将 attr 设为 NULL。

    可以使用宏 PTHREAD_MUTEX_INITIALIZER 静态初始化互斥锁，比如：
    pthread_mutex_t  mutex = PTHREAD_MUTEX_INITIALIZER;

这种方法等价于使用 NULL 指定的 attr 参数调用 pthread_mutex_init() 来完成动态初始化，不同之处在于 PTHREAD_MUTEX_INITIALIZER 宏不进行错误检查。

返回值：
    成功：0，成功申请的锁默认是打开的。
    失败：非 0 错误码
```



> restrict，C语言中的一种类型[限定符](https://baike.baidu.com/item/限定符/1924249)（Type Qualifiers），用于告诉编译器，对象已经被指针所引用，不能通过除该指针外所有其他直接或间接的方式修改该对象的内容。

 

### 3.5 pthread_mutex_destroy函数

```
#include <pthread.h>

int pthread_mutex_destroy(pthread_mutex_t *mutex);
功能：
    销毁指定的一个互斥锁。互斥锁在使用完毕后，必须要对互斥锁进行销毁，以释放资源。
参数：
    mutex：互斥锁地址。
返回值：
    成功：0
    失败：非 0 错误码
```

 

### 3.6 pthread_mutex_lock函数

```
#include <pthread.h>

int pthread_mutex_lock(pthread_mutex_t *mutex);
功能：
    对互斥锁上锁，若互斥锁已经上锁，则调用者阻塞，直到互斥锁解锁后再上锁。
参数：
    mutex：互斥锁地址。
返回值：
    成功：0
    失败：非 0 错误码

int pthread_mutex_trylock(pthread_mutex_t *mutex);
   调用该函数时，若互斥锁未加锁，则上锁，返回 0；
   若互斥锁已加锁，则函数直接返回失败，即 EBUSY。

```

 

### 3.7 pthread_mutex_unlock函数

```
#include <pthread.h>

int pthread_mutex_unlock(pthread_mutex_t *mutex);
功能：
    对指定的互斥锁解锁。
参数：
    mutex：互斥锁地址。
返回值：
    成功：0
    失败：非0错误码

```

 

### 3.8 测试程序

```
pthread_mutex_t mutex; //互斥锁

// 打印机
void printer(char *str)
{
    pthread_mutex_lock(&mutex); //上锁
    while (*str != '\0')
    {
        putchar(*str);
        fflush(stdout);
        str++;
        sleep(1);
    }
    printf("\n");
    pthread_mutex_unlock(&mutex); //解锁
}

// 线程一
void *thread_fun_1(void *arg)
{
    char *str = "hello";
    printer(str); //打印
}

// 线程二
void *thread_fun_2(void *arg)
{
    char *str = "world";
    printer(str); //打印
}

int main(void)
{
    pthread_t tid1, tid2;

    pthread_mutex_init(&mutex, NULL); //初始化互斥锁

    // 创建 2 个线程
    pthread_create(&tid1, NULL, thread_fun_1, NULL);
    pthread_create(&tid2, NULL, thread_fun_2, NULL);

    // 等待线程结束，回收其资源
    pthread_join(tid1, NULL);
    pthread_join(tid2, NULL);

    pthread_mutex_destroy(&mutex); //销毁互斥锁

    return 0;
}
```

 

### 3.9 死锁（DeadLock）

**1）什么是死锁**

死锁是指两个或两个以上的进程在执行过程中，由于竞争资源或者由于彼此通信而造成的一种阻塞的现象，若无外力作用，它们都将无法推进下去。此时称系统处于死锁状态或系统产生了死锁，这些永远在互相等待的进程称为死锁进程。

 

**2）死锁引起的原因**

竞争不可抢占资源引起死锁

也就是我们说的第一种情况，而这都在等待对方占有的不可抢占的资源。

竞争可消耗资源引起死锁

有p1，p2，p3三个进程，p1向p2发送消息并接受p3发送的消息，p2向p3发送消息并接受p1的消息，p3向p1发送消息并接受p2的消息，如果设置是先接到消息后发送消息，则所有的消息都不能发送，这就造成死锁。

进程推进顺序不当引起死锁

有进程p1，p2，都需要资源A，B，本来可以p1运行A --> p1运行B --> p2运行A --> p2运行B，但是顺序换了，p1运行A时p2运行B，容易发生第一种死锁。互相抢占资源。

**3）死锁的必要条件**

互斥条件

某资源只能被一个进程使用，其他进程请求该资源时，只能等待，直到资源使用完毕后释放资源。

请求和保持条件

程序已经保持了至少一个资源，但是又提出了新要求，而这个资源被其他进程占用，自己占用资源却保持不放。

不可抢占条件

进程已获得的资源没有使用完，不能被抢占。

循环等待条件

必然存在一个循环链。

**4）处理死锁的思路**

预防死锁

破坏死锁的四个必要条件中的一个或多个来预防死锁。

避免死锁

和预防死锁的区别就是，在资源动态分配过程中，用某种方式防止系统进入不安全的状态。

检测死锁

运行时出现死锁，能及时发现死锁，把程序解脱出来

解除死锁

发生死锁后，解脱进程，通常撤销进程，回收资源，再分配给正处于阻塞状态的进程。

**5）预防死锁的方法**

***破坏请求和保持条件\***

协议1：

所有进程开始前，必须一次性地申请所需的所有资源，这样运行期间就不会再提出资源要求，破坏了请求条件，即使有一种资源不能满足需求，也不会给它分配正在空闲的资源，这样它就没有资源，就破坏了保持条件，从而预防死锁的发生。

协议2：

允许一个进程只获得初期的资源就开始运行，然后再把运行完的资源释放出来。然后再请求新的资源。

***破坏不可抢占条件\***

当一个已经保持了某种不可抢占资源的进程，提出新资源请求不能被满足时，它必须释放已经保持的所有资源，以后需要时再重新申请。

***破坏循环等待条件\***

对系统中的所有资源类型进行线性排序，然后规定每个进程必须按序列号递增的顺序请求资源。假如进程请求到了一些序列号较高的资源，然后有请求一个序列较低的资源时，必须先释放相同和更高序号的资源后才能申请低序号的资源。多个同类资源必须一起请求。

 

## 04. 读写锁

### 4.1 读写锁概述

当有一个线程已经持有互斥锁时，互斥锁将所有试图进入临界区的线程都阻塞住。但是考虑一种情形，当前持有互斥锁的线程只是要读访问共享资源，而同时有其它几个线程也想读取这个共享资源，但是由于互斥锁的排它性，所有其它线程都无法获取锁，也就无法读访问共享资源了，但是实际上多个线程同时读访问共享资源并不会导致问题。

在对数据的读写操作中，更多的是读操作，写操作较少，例如对数据库数据的读写应用。为了满足当前能够允许多个读出，但只允许一个写入的需求，线程提供了**读写锁**来实现。

 

读写锁的特点如下：

1）如果有其它线程读数据，则允许其它线程执行读操作，但不允许写操作。

2）如果有其它线程写数据，则其它线程都不允许读、写操作。



读写锁分为读锁和写锁，规则如下：

1）如果某线程申请了读锁，其它线程可以再申请读锁，但不能申请写锁。

2）如果某线程申请了写锁，其它线程不能申请读锁，也不能申请写锁。

 

POSIX 定义的读写锁的数据类型是： pthread_rwlock_t。

 

### 4.2 pthread_rwlock_init函数

```
#include <pthread.h>

int pthread_rwlock_init(pthread_rwlock_t *restrict rwlock,
    const pthread_rwlockattr_t *restrict attr);
功能：
    用来初始化 rwlock 所指向的读写锁。

参数：
    rwlock：指向要初始化的读写锁指针。
    attr：读写锁的属性指针。如果 attr 为 NULL 则会使用默认的属性初始化读写锁，否则使用指定的 attr 初始化读写锁。

    可以使用宏 PTHREAD_RWLOCK_INITIALIZER 静态初始化读写锁，比如：
    pthread_rwlock_t my_rwlock = PTHREAD_RWLOCK_INITIALIZER;

    这种方法等价于使用 NULL 指定的 attr 参数调用 pthread_rwlock_init() 来完成动态初始化，不同之处在于PTHREAD_RWLOCK_INITIALIZER 宏不进行错误检查。

返回值：
    成功：0，读写锁的状态将成为已初始化和已解锁。
    失败：非 0 错误码。

```

 

### 4.3 pthread_rwlock_destroy函数

```
#include <pthread.h>

int pthread_rwlock_destroy(pthread_rwlock_t *rwlock);
功能：
    用于销毁一个读写锁，并释放所有相关联的资源（所谓的所有指的是由 pthread_rwlock_init() 自动申请的资源） 。
参数：
    rwlock：读写锁指针。
返回值：
    成功：0
    失败：非 0 错误码

```

 

### 4.4 pthread_rwlock_rdlock函数

```
#include <pthread.h>

int pthread_rwlock_rdlock(pthread_rwlock_t *rwlock);
功能：
    以阻塞方式在读写锁上获取读锁（读锁定）。
    如果没有写者持有该锁，并且没有写者阻塞在该锁上，则调用线程会获取读锁。
    如果调用线程未获取读锁，则它将阻塞直到它获取了该锁。一个线程可以在一个读写锁上多次执行读锁定。
    线程可以成功调用 pthread_rwlock_rdlock() 函数 n 次，但是之后该线程必须调用 pthread_rwlock_unlock() 函数 n 次才能解除锁定。
参数：
    rwlock：读写锁指针。
返回值：
    成功：0
    失败：非 0 错误码

int pthread_rwlock_tryrdlock(pthread_rwlock_t *rwlock);
   用于尝试以非阻塞的方式来在读写锁上获取读锁。
   如果有任何的写者持有该锁或有写者阻塞在该读写锁上，则立即失败返回。

```

 

### 4.5 pthread_rwlock_wrlock函数

```
#include <pthread.h>

int pthread_rwlock_wrlock(pthread_rwlock_t *rwlock);
功能：
    在读写锁上获取写锁（写锁定）。
    如果没有写者持有该锁，并且没有写者读者持有该锁，则调用线程会获取写锁。
    如果调用线程未获取写锁，则它将阻塞直到它获取了该锁。
参数：
    rwlock：读写锁指针。
返回值：
    成功：0
    失败：非 0 错误码

int pthread_rwlock_trywrlock(pthread_rwlock_t *rwlock);
   用于尝试以非阻塞的方式来在读写锁上获取写锁。
   如果有任何的读者或写者持有该锁，则立即失败返回。

```

 

### 4.6 pthread_rwlock_unlock函数

```
#include <pthread.h>

int pthread_rwlock_unlock(pthread_rwlock_t *rwlock);
功能：
    无论是读锁或写锁，都可以通过此函数解锁。
参数：
    rwlock：读写锁指针。
返回值：
    成功：0
    失败：非 0 错误码

```

 

### 4.7 测试程序示例

下面是一个使用读写锁来实现 4 个线程读写一段数据是实例。

在此示例程序中，共创建了 4 个线程，其中两个线程用来写入数据，两个线程用来读取数据。当某个线程读操作时，其他线程允许读操作，却不允许写操作；当某个线程写操作时，其它线程都不允许读或写操作。

```
pthread_rwlock_t rwlock; //读写锁
int num = 1;

//读操作，其他线程允许读操作，却不允许写操作
void *fun1(void *arg)
{
    while (1)
    {
        pthread_rwlock_rdlock(&rwlock);
        printf("read num first===%d\n", num);
        pthread_rwlock_unlock(&rwlock);
        sleep(1);
    }
}

//读操作，其他线程允许读操作，却不允许写操作
void *fun2(void *arg)
{
    while (1)
    {
        pthread_rwlock_rdlock(&rwlock);
        printf("read num second===%d\n", num);
        pthread_rwlock_unlock(&rwlock);
        sleep(2);
    }
}

//写操作，其它线程都不允许读或写操作
void *fun3(void *arg)
{
    while (1)
    {

        pthread_rwlock_wrlock(&rwlock);
        num++;
        printf("write thread first\n");
        pthread_rwlock_unlock(&rwlock);
        sleep(2);
    }
}

//写操作，其它线程都不允许读或写操作
void *fun4(void *arg)
{
    while (1)
    {

        pthread_rwlock_wrlock(&rwlock);
        num++;
        printf("write thread second\n");
        pthread_rwlock_unlock(&rwlock);
        sleep(1);
    }
}

int main()
{
    pthread_t ptd1, ptd2, ptd3, ptd4;

    pthread_rwlock_init(&rwlock, NULL);//初始化一个读写锁

    //创建线程
    pthread_create(&ptd1, NULL, fun1, NULL);
    pthread_create(&ptd2, NULL, fun2, NULL);
    pthread_create(&ptd3, NULL, fun3, NULL);
    pthread_create(&ptd4, NULL, fun4, NULL);

    //等待线程结束，回收其资源
    pthread_join(ptd1, NULL);
    pthread_join(ptd2, NULL);
    pthread_join(ptd3, NULL);
    pthread_join(ptd4, NULL);

    pthread_rwlock_destroy(&rwlock);//销毁读写锁

    return 0;
}

```

 

## 05. 条件变量

### 5.1 条件变量概述

与互斥锁不同，条件变量是用来等待而不是用来上锁的，**条件变量本身不是锁**！

条件变量用来自动阻塞一个线程，直到某特殊情况发生为止。通常条件变量和互斥锁同时使用。

条件变量的两个动作：

- 条件不满, 阻塞线程
- 当条件满足, 通知阻塞的线程开始工作

条件变量的类型: pthread_cond_t。

 

### 5.2 pthread_cond_init函数

```
#include <pthread.h>

int pthread_cond_init(pthread_cond_t *restrict cond,
    const pthread_condattr_t *restrict attr);
功能：
    初始化一个条件变量
参数：
    cond：指向要初始化的条件变量指针。
    attr：条件变量属性，通常为默认值，传NULL即可
        也可以使用静态初始化的方法，初始化条件变量：
        pthread_cond_t cond = PTHREAD_COND_INITIALIZER;
返回值：
    成功：0
    失败：非0错误号

```

 

### 5.3 pthread_cond_destroy函数

```
#include <pthread.h>

int pthread_cond_destroy(pthread_cond_t *cond);
功能：
    销毁一个条件变量
参数：
    cond：指向要初始化的条件变量指针
返回值：
    成功：0
    失败：非0错误号

```

 

### 5.4 pthread_cond_wait函数

```
#include <pthread.h>

int pthread_cond_wait(pthread_cond_t *restrict cond,
    pthread_mutex_t *restrict mutex);
功能：
    阻塞等待一个条件变量
    a) 阻塞等待条件变量cond（参1）满足
    b) 释放已掌握的互斥锁（解锁互斥量）相当于pthread_mutex_unlock(&mutex);
            a) b) 两步为一个原子操作。
    c) 当被唤醒，pthread_cond_wait函数返回时，解除阻塞并重新申请获取互斥锁pthread_mutex_lock(&mutex);

参数：
    cond：指向要初始化的条件变量指针
    mutex：互斥锁

返回值：
    成功：0
    失败：非0错误号

int pthread_cond_timedwait(pthread_cond_t *restrict cond,
    pthread_mutex_t *restrict mutex,
    const struct
                           .*restrict abstime);
功能：
    限时等待一个条件变量

参数：
    cond：指向要初始化的条件变量指针
    mutex：互斥锁
    abstime：绝对时间

返回值：
    成功：0
    失败：非0错误号

```

abstime补充说明：

```
struct timespec {
    time_t tv_sec;      /* seconds */ // 秒
    long   tv_nsec; /* nanosecondes*/ // 纳秒
}

time_t cur = time(NULL);        //获取当前时间。
struct timespec t;              //定义timespec 结构体变量t
t.tv_sec = cur + 1;             // 定时1秒
pthread_cond_timedwait(&cond, &t);

```

 

### 5.5 pthread_cond_signal函数

唤醒至阻塞在条件变量上的线程

```
#include <pthread.h>

int pthread_cond_signal(pthread_cond_t *cond);
功能：
    唤醒至少一个阻塞在条件变量上的线程
参数：
    cond：指向要初始化的条件变量指针
返回值：
    成功：0
    失败：非0错误号

int pthread_cond_broadcast(pthread_cond_t *cond);
功能：
    唤醒全部阻塞在条件变量上的线程
参数：
    cond：指向要初始化的条件变量指针
返回值：
    成功：0
    失败：非0错误号

```

 

### 5.6 生产者消费者条件变量模型

线程同步典型的案例即为生产者消费者模型，而借助条件变量来实现这一模型，是比较常见的一种方法。

假定有两个线程，一个模拟生产者行为，一个模拟消费者行为。两个线程同时操作一个共享资源（一般称之为汇聚），生产向其中添加产品，消费者从中消费掉产品。

```
// 节点结构
typedef struct node
{
    int data;
    struct node* next;
}Node;

// 永远指向链表头部的指针
Node* head = NULL;

// 线程同步 - 互斥锁
pthread_mutex_t mutex;
// 阻塞线程 - 条件变量类型的变量
pthread_cond_t cond;

// 生产者
void* producer(void* arg)
{
    while (1)
    {
        // 创建一个链表的节点
        Node* pnew = (Node*)malloc(sizeof(Node));
        // 节点的初始化
        pnew->data = rand() % 1000; // 0-999

        // 使用互斥锁保护共享数据
        pthread_mutex_lock(&mutex);
        // 指针域
        pnew->next = head;
        head = pnew;
        printf("====== produce: %lu, %d\n", pthread_self(), pnew->data);
        pthread_mutex_unlock(&mutex);

        // 通知阻塞的消费者线程，解除阻塞
        pthread_cond_signal(&cond);

        sleep(rand() % 3);
    }
    return NULL;
}

void* customer(void* arg)
{
    while (1)
    {
        pthread_mutex_lock(&mutex);
        // 判断链表是否为空
        if (head == NULL)
        {
            // 线程阻塞
            // 该函数会对互斥锁解锁
            pthread_cond_wait(&cond, &mutex);
            // 解除阻塞之后，对互斥锁做加锁操作
        }
        // 链表不为空 - 删掉一个节点 - 删除头结点
        Node* pdel = head;
        head = head->next;
        printf("------ customer: %lu, %d\n", pthread_self(), pdel->data);
        free(pdel);
        pthread_mutex_unlock(&mutex);
    }
    return NULL;
}

int main(int argc, const char* argv[])
{
    pthread_t p1, p2;
    // init
    pthread_mutex_init(&mutex, NULL);
    pthread_cond_init(&cond, NULL);

    // 创建生产者线程
    pthread_create(&p1, NULL, producer, NULL);
    // 创建消费者线程
    pthread_create(&p2, NULL, customer, NULL);

    // 阻塞回收子线程
    pthread_join(p1, NULL);
    pthread_join(p2, NULL);

    pthread_mutex_destroy(&mutex);
    pthread_cond_destroy(&cond);

    return 0;
}

```

 

### 5.7 条件变量的优缺点

相较于mutex而言，条件变量可以减少竞争。

如直接使用mutex，除了生产者、消费者之间要竞争互斥量以外，消费者之间也需要竞争互斥量，但如果汇聚（链表）中没有数据，消费者之间竞争互斥锁是无意义的。

有了条件变量机制以后，只有生产者完成生产，才会引起消费者之间的竞争。提高了程序效率。

 

## 06. 信号量

### 6.1 信号量概述

信号量广泛用于进程或线程间的同步和互斥，信号量本质上是一个非负的整数计数器，它被用来控制对公共资源的访问。

编程时可根据操作信号量值的结果判断是否对公共资源具有访问的权限，当信号量值大于 0 时，则可以访问，否则将阻塞。

PV 原语是对信号量的操作，一次 P 操作使信号量减１，一次 V 操作使信号量加１。

信号量主要用于进程或线程间的同步和互斥这两种典型情况。

信号量数据类型为：sem_t。

 

信号量用于互斥：

![1528181665768](assets/1528181665768.png)

信号量用于同步：

![1528181692967](assets/1528181692967.png)

 

### 6.2 sem_init函数

初始化信号量:

```
#include <semaphore.h>

int sem_init(sem_t *sem, int pshared, unsigned int value);
功能：
    创建一个信号量并初始化它的值。一个无名信号量在被使用前必须先初始化。
参数：
    sem：信号量的地址。
    pshared：等于 0，信号量在线程间共享（常用）；不等于0，信号量在进程间共享。
    value：信号量的初始值。
返回值：
    成功：0
    失败： - 1

```

 

### 6.3 sem_destroy函数

销毁信号量：

```
#include <semaphore.h>

int sem_destroy(sem_t *sem);
功能：
    删除 sem 标识的信号量。
参数：
    sem：信号量地址。
返回值：
    成功：0
    失败： - 1


```

 

### 6.4 信号量P操作（减1）

```
#include <semaphore.h>

int sem_wait(sem_t *sem);
功能：
    将信号量的值减 1。操作前，先检查信号量（sem）的值是否为 0，若信号量为 0，此函数会阻塞，直到信号量大于 0 时才进行减 1 操作。
参数：
    sem：信号量的地址。
返回值：
    成功：0
    失败： - 1

int sem_trywait(sem_t *sem);
   以非阻塞的方式来对信号量进行减 1 操作。
   若操作前，信号量的值等于 0，则对信号量的操作失败，函数立即返回。

int sem_timedwait(sem_t *sem, const struct timespec *abs_timeout);
   限时尝试将信号量的值减 1
   abs_timeout：绝对时间

```

abs_timeout补充说明：

```
struct timespec {
    time_t tv_sec;      /* seconds */ // 秒
    long   tv_nsec; /* nanosecondes*/ // 纳秒
}

time_t cur = time(NULL);        //获取当前时间。
struct timespec t;              //定义timespec 结构体变量t
t.tv_sec = cur + 1;             // 定时1秒
sem_timedwait(&cond, &t);

```

 

### 6.5 信号量V操作（加1）

```
#include <semaphore.h>

int sem_post(sem_t *sem);
功能：
    将信号量的值加 1 并发出信号唤醒等待线程（sem_wait()）。
参数：
    sem：信号量的地址。
返回值：
    成功：0
    失败：-1

```

 

### 6.6 获取信号量的值

```
#include <semaphore.h>

int sem_getvalue(sem_t *sem, int *sval);
功能：
    获取 sem 标识的信号量的值，保存在 sval 中。
参数：
    sem：信号量地址。
    sval：保存信号量值的地址。
返回值：
    成功：0
    失败：-1

```

 

### 6.7 程序示例

```
sem_t sem; //信号量

void printer(char *str)
{
    sem_wait(&sem);//减一
    while (*str)
    {
        putchar(*str);
        fflush(stdout);
        str++;
        sleep(1);
    }
    printf("\n");

    sem_post(&sem);//加一
}

void *thread_fun1(void *arg)
{
    char *str1 = "hello";
    printer(str1);
}

void *thread_fun2(void *arg)
{
    char *str2 = "world";
    printer(str2);
}

int main(void)
{
    pthread_t tid1, tid2;

    sem_init(&sem, 0, 1); //初始化信号量，初始值为 1

    //创建 2 个线程
    pthread_create(&tid1, NULL, thread_fun1, NULL);
    pthread_create(&tid2, NULL, thread_fun2, NULL);

    //等待线程结束，回收其资源
    pthread_join(tid1, NULL);
    pthread_join(tid2, NULL);

    sem_destroy(&sem); //销毁信号量

    return 0;
}
```

 

## 07. 作业

1) 实现信号量版本的生产者和消费者模型

 

## 08. 扩展

自旋锁

> int pthread_spin_destroy(pthread_spinlock_t *lock);
>
> int pthread_spin_init(pthread_spinlock_t *lock, int pshared);

 

屏障

 

信号量：

> int semget(key_t key, int nsems, int semflg);

 

## 09. 练习

哲学家就餐问题参考代码

```
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <string.h>
#include <pthread.h>

pthread_mutex_t mutex[5];

void* dine(void* arg)
{
    int num = (int)arg;
    int left, right;

    if(num < 4)
    {
        // 前４个人，右手拿自己筷子
        right = num;
        left = num+1;
    }
    else if(num == 4)
    {
        // 最后一个人，右手拿别人筷子
        right = 0;
        left = num;
    }

    // 吃饭
    while(1)
    {
        // 右手加锁
        pthread_mutex_lock(&mutex[right]);
        // 尝试抢左手筷子
        if(pthread_mutex_trylock(&mutex[left]) == 0)
        {
            // 吃面。。。
            printf("%c 正在吃面。。。。。。\n", num+'A');
            // 吃完放筷子
            pthread_mutex_unlock(&mutex[left]);
        }
        // 解锁
        pthread_mutex_unlock(&mutex[right]);
        sleep(rand()%5);
    }
}

int main(int argc, const char* argv[])
{
    pthread_t p[5];

    for(int i=0; i<5; ++i)
    {
        pthread_mutex_init(&mutex[i], NULL);
    }

    for(int i=0; i<5; ++i)
    {
        pthread_create(&p[i], NULL, dine, (void*)i);
    }

    for(int i=0; i<5; ++i)
    {
        pthread_join(p[i], NULL);
    }
    
    for(int i=0; i<5; ++i)
    {
        pthread_mutex_destroy(&mutex[i]);
    }
    
    return 0;
}

```

 

## 10. 总结

互斥锁

死锁

读写锁

条件变量

信号量

 

 

 

 