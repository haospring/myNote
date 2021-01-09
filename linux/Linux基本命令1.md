# Linux基本命令1

## 定义别名

使用短的字符串代替长的字符串

~~~shell
#使用alias
alias cdnet="cd /etc/sysconfig/network-scripts"
#将文件写进磁盘
cd /root
#只在本用户生效
vim .bashrc
#全部用户生效，不建议
vim /etc/bashrc
alias cdnet='cd /etc/sysconfig/networdk-scripts'
#将文件写进磁盘后强制生效，免去重启
source .bashrc
~~~

alias --- 内部 --- hash --- 外部

~~~ shell
#删除别名,只在内存中生效
unalias cdnet
#查看所有别名
alias

~~~

## 两天的指令

~~~shell
alias
cat
cp
#ctrl+l
clear
exit
enable
echo $SHELL
halt
hash
hostname
init
id -u
#ctrl+d
logout
connectin modify ens33 connection.autoconnect yes
nano /etc/profile.d/env.sh
PS1="\[e[1;33m\][\u@\h \w]\\$\[e[0m\]"
poweroff
reboot
type
unalias
alias
which
whereis
who
whoami
~~~

## 日期和时间

~~~shell
#显示操作系统时间
date
#显示硬件时间
clock
#显示日历
cal
cal -y
#更改系统时间，月日时分年秒
date MMDDHHmmYYYY.ss
#-w,--systohc以系统时间为准校正硬件时间
clock -w
#-s,--hctosys以硬件时间为准校正系统时间
clock -s
#centos7调整时区
timedatectl set-timezone Asia/Shanghai
#显示所有时区
timedatectl list-timezones
~~~

## 关机

~~~shell
#关机：halt，poweroff
#重启：reboot
#-f：强制，不调用shutdown
#-p:切断电源
#关机或重启：shutdown
#shutdown [OPTION]...[TIME][MESSAGE]
#-r：reboot
#-h:halt
#-c：cancel
~~~

[视频链接](https://edu.aliyun.com/lesson_1726_13995?spm=5176.8764728.0.0.36c65350zQhsP1#_13995)









