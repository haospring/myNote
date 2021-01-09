# Linux

## 分区挂载

为分区分配一个目录，称为挂载（mount）

windows也可以把某一个分区挂载到另一个分区的其中一个目录上

## 磁盘分区

### Windows分区

1. 主分区:每个磁盘最多四个主分区，只能有一个活动区（启动），用于系统引导。编号：1-4
2. 扩展分区：每个磁盘最多一个扩展分区，用于划分更小的分区。扩展+主分区<=4 。编号：1-4
3. 逻辑分区：扩展分区可以分为多个逻辑分区

### Linux分区规划

/	根分区，预留足够空间，后期无法增加

/boot	存放引导数据的分区	几百M够用，1G绰绰有余

~~~ shell
#查看指定目录所占空间
du -sh /boot	
~~~

/swap	交换分区，一般是物理内存的两倍，当内存不足时，将硬盘作为内存使用。

## 关机

~~~shell
#重启
reboot
#关机
shutdown -h now
poweroff
halt
~~~

## 查看硬盘及分区信息
~~~ shell
#查看硬盘
lsblk 				block
fdisk -l /dev/sda
#查看内存大小
cat /proc/meminfo
#查看硬盘分区大小
cat /proc/partitions
#查看内存和交换分区
free
free -h
~~~

![tupain](https://raw.githubusercontent.com/haospring/springPic/main/img/Snipaste_2020-10-06_10-20-52.jpg)
## 进制转换

十进制——>二进制		n/2，取余数的倒值

二进制——>十进制		每个位上的数字乘以2^n相加

十进制——>十六进制	n/16，取余数的倒值

十六进制——>十进制	每个位上的数字乘以16^n相加

十六进制——>二进制	先把十六进制转为十进制，然后由十进制转为二进制

linux终端进制转换命令：

~~~shell
bc
#输入值为二进制
ibase=2
#输出值为二进制
obase=2
~~~

## 指令

~~~shell
#显示当前所在目录
pwd
#计算iso文件的值是否和官方给定的值相同，以此判断文件是或否损坏
sha1sum /dev/sr0
~~~

超级用户显示为#，普通用户显示为$

## 本期视频地址

[阿里云大学](https://edu.aliyun.com/lesson_1725_13992?spm=5176.10731542.0.0.6e4f1860D1zQEf#_13992)





​	