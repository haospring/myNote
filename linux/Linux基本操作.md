# Linux基本操作

## 切换运行模式

只能由管理员权限进行

~~~ shell
#切换到命令行模式
init 3
#切换到桌面模式
init 5
#查看前一个和当前的运行模式
runlevel
#startx切换到桌面不需要登录
startx

#reboot
init 6
#关机: poweroff / halt / shutdown
init 0
~~~

~~~ shell
#临时打开命令行
ctrl + alt + F2
#临时打开桌面
ctrl + alt + F1
#命令行查看当前在F几
tty
#chvt n可以起到ctrl+alt+Fn的效果
chvt 2
chvt 1
~~~

## 用户相关

~~~shell
#查看当前用户
whoami
#查看用户uid，uid为0的是超级用户，不为0的是普通用户
id -u
~~~

## 版本信息

~~~ shell
#查看当前centos的版本
cat /etc/centos-release
#查看系统版本，centos需要安装软件才能使用
lsb_release -a
#查看内核版本
uname -r
cat /proc/v
~~~

## 查看硬件设备

~~~shell
#查看cpu
lscpu
#查看内存大小
free -hm
# 查看内存信息
cat /proc/meminfo
#查看硬盘
lsblk
fdisk -l /dev/sdq
cat /proc/partitions
#查看网卡
#centos7
mii-tool ens33
#centos6
mii-tool eth0
~~~

## Linux目录

**/bin**：
bin 是 Binaries (二进制文件) 的缩写, 这个目录存放着最经常使用的命令。

**/boot：**
这里存放的是启动 Linux 时使用的一些核心文件，包括一些连接文件以及镜像文件。

**/dev ：**
dev 是 Device(设备) 的缩写, 该目录下存放的是 Linux 的外部设备，在 Linux 中访问设备的方式和访问文件的方式是相同的。

**/etc：**
etc 是 Etcetera(等等) 的缩写,这个目录用来存放所有的系统管理所需要的配置文件和子目录。

**/home**：
用户的主目录，在 Linux 中，每个用户都有一个自己的目录，一般该目录名是以用户的账号命名的。

**/lib**：
lib 是 Library(库) 的缩写这个目录里存放着系统最基本的动态连接共享库，其作用类似于 Windows 里的 DLL 文件。几乎所有的应用程序都需要用到这些共享库。

**/lost+found**
这个目录一般情况下是空的，当系统非法关机后，这里就存放了一些文件。

**/media**：
linux 系统会自动识别一些设备，例如U盘、光驱等等，当识别后，Linux 会把识别的设备挂载到这个目录下。

**/mnt**：
系统提供该目录是为了让用户临时挂载别的文件系统的，我们可以将光驱挂载在 /mnt/ 上，然后进入该目录就可以查看光驱里的内容了。

**/opt**：
opt 是 optional(可选) 的缩写，这是给主机额外安装软件所摆放的目录。比如你安装一个ORACLE数据库则就可以放到这个目录下。默认是空的。

**/proc**：
proc 是 Processes(进程) 的缩写，/proc 是一种伪文件系统（也即虚拟文件系统），存储的是当前内核运行状态的一系列特殊文件，这个目录是一个虚拟的目录，它是系统内存的映射，我们可以通过直接访问这个目录来获取系统信息。

**/root**：
该目录为系统管理员，也称作超级权限者的用户主目录。

**/sbin**：
s 就是 Super User 的意思，是 Superuser Binaries (超级用户的二进制文件) 的缩写，这里存放的是系统管理员使用的系统管理程序。

**/selinux**：
 这个目录是 Redhat/CentOS 所特有的目录，Selinux 是一个安全机制，类似于 windows 的防火墙，但是这套机制比较复杂，这个目录就是存放selinux相关的文件的。

**/srv**：
 该目录存放一些服务启动之后需要提取的数据。

**/sys**：
sysfs 文件系统集成了下面3种文件系统的信息：针对进程信息的 proc 文件系统、针对设备的 devfs 文件系统以及针对伪终端的 devpts 文件系统。
该文件系统是内核设备树的一个直观反映。
当一个内核对象被创建的时候，对应的文件和目录也在内核对象子系统中被创建。

**/tmp**：
tmp 是 temporary(临时) 的缩写这个目录是用来存放一些临时文件的。

**/usr**：
 usr 是 unix shared resources(共享资源) 的缩写，这是一个非常重要的目录，用户的很多应用程序和文件都放在这个目录下，类似于 windows 下的 program files 目录。

**/usr/bin：**
系统用户使用的应用程序。

**/usr/sbin：**
超级用户使用的比较高级的管理程序和系统守护程序。

**/usr/src：**
内核源代码默认的放置目录。

**/var**：
var 是 variable(变量) 的缩写，这个目录中存放着在不断扩充着的东西，我们习惯将那些经常被修改的目录放在这个目录下。包括各种日志文件。

**/run**：
是一个临时文件系统，存储系统启动以来的信息。当系统重启时，这个目录下的文件应该被删掉或清除。如果你的系统上有 /var/run 目录，应该让它指向 run。

[链接地址](https://www.runoob.com/linux/linux-system-contents.html)

## shell

~~~shell
#显示当前使用的shell
echo $SHELL
echo ${SHELL}
#显示当前系统使用的所有shell
cat -/etc/shells
~~~

## 快捷键

ctr+l等价于clear，清屏

## 主机名

~~~shell
#查看主机名
hostname
#查看命令行用户名和主机名的颜色
echo $PS1
#临时改变颜色，重启恢复
PS1="\[\e[44;33m\][\u@\h \w]\\$\[\e[0m]"
#44背景颜色;33字体颜色;0m颜色中止
#永久保存
vim /etc/profile.d/env.sh
#将下面一句话复制粘贴上去
PS1="\[\e[36m\][\u@\h \w]\\$\[\e[0m]"
#\e\033两个相等，实现颜色设置
#\u当前用户
#\h主机名简称
#\H主机名
#\w当前工作目录
#\W当前工作目录基名
#\t24小时制时间格式
#\T12小时制时间格式
#\!命令李老师数
#\#开机后命令历史数
~~~