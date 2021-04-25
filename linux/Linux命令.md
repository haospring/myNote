# Linux命令

## 一、目录相关的命令

所有用户都能直接使用命令，是因为在PATH中将命令所在的目录进行配置

![PATH](Linux%E5%9B%BE%E7%89%87/PATH.jpg)

如果要把/root目录配置到PATH中，可以通过

~~~shell
PATH="${PATH}:/root"
~~~

目录与目录之间用`：`分开，${PATH}代表的是PATH的所有内容

### 1.1 pwd（print work directory）

功能描述：显示当前工作目录的绝对路径 

~~~shell
[root@izbp1adurb6tc9s27c82y5z usr]# pwd
# 显示当前目录的真是目录，即显示软链接所链接到的目录
# e.g.当前是在/var/mail目录下，但是这个目录是链接到/usr/spool/mail下的
# 下面的指令显示的是/usr/spool/mail的目录
pwd -P
~~~

### 1.2 ls（list files）

语法：ls [选项] [目录或文件]

描述：列出目录下的文件

选项：

- -a（--all）：显示全部文件及目录，包括隐藏文件（以.开头的文件） 
- -d：仅显示目录名，不显示目录下的内容列表
- -h：人性化显示
- -l：long长数据串列出，包含文件的属性和权限
- -r：将文件以相反次序显示（原定依英文字母次序）
- -t：将文件依建立时间的先后次序列出
- -A：同a，但不列出"."和".."
- -F：在列出的文件名称后加一个符号，可执行文件后加"*"，目录加"/"
- -R：若目录下有文件，则其下文件也列出

~~~shell
ls -altF
ls -R
ll
~~~

### 1.3 cd（change directory）

语法：cd [选项] [目录名称]

描述：切换到指定目录，以/开头的表示绝对路径

- cd				    绝对路径或相对路径（跳转到指定目录）

- cd或cd ~		 返回当前用户家目录

- cd -				  返回上一次所在的目录

- cd ..				 返回当前目录的上一级目录

- cd .				  当前目录

### 1.4 mkdir（make directory）

语法：mkdir [选项] 目录名称

描述：创建指定目录

选项：

- -p：parents，创建多层目录
- -m：强制指定目录权限

~~~shell
[root@izbp1adurb6tc9s27c82y5z ~]# mkdir /usr/test/
[root@izbp1adurb6tc9s27c82y5z test]# mkdir -p /usr/test2/test3
# 创建目录test04并设置其权限为754
mkdir -m 754 test04
~~~

### 1.5 rmdir（remove directory）

语法：rmdir [选项] 目录名称

描述：删除空的目录

选项：

- -p：当子目录被删除时，如果父目录也为空，则将父目录也删除

~~~shell
# 切换到haospring的家目录
cd ~haospring
# 创建两个空目录
mkdir -p test/test2
# 删除test2目录，如果删除test2后test为空，则将test也删除
rmdir -p test/test2

~~~



### 1.6 cp（copy file）

语法：cp 源目录或文件 目标目录或文件

描述：复制目录或文件，cp复制时会默认修改文件的权限，所以赋值配置文件时要加上-a，复制文件的所有属性

选项：

- -a：保留链接、文件属性，并赋值目录下的所有内容，相当于`-dr --preserve=all`（常用）

- -d：若源文件为链接文件的属性，则复制链接文件属性而非文件本身

- -p：连同文件的属性（权限、用户、时间）一起复制过去，而非使用默认属性（备份常用）

- -r：recursive，递归复制整个文件夹（常用）

- -f：覆盖已经存在的目标文件而不给出提示

- -i：覆盖前提示是否要覆盖（ 常用）

- -l：不复制文件，只是生成链接文件

~~~xml
[haospring@izbp1adurb6tc9s27c82y5z ~]$ cp -rp test test2
~~~

### 1.7 mv（move file）

语法：mv [选项] 源文件 目标目录

描述：移动文件或重命名文件

选项：

- -i：如果指定移动的源目录或文件与目标的目录或文件同名，提示是否覆盖旧文件

- -f：不提示，直接覆盖

- -n：不覆盖

- -u：当源文件比目标文件新或者目标文件不存在时，才执行移动

~~~shell
mv /usr/test /usr/test2
mkdir /usr/test3
mv /usr/test2 /usr/test3
~~~

### 1.8 rm（remove）

语法：rm [选项] 文件或目录

描述：删除文件及目录，支持通配符，在CentOS7中rm默认加入了`-i`这个选项，可以通过`\rm`的方式忽略掉alias的指定选项

选项：

- -f：force强制删除，不提示

- -r：递归执行

- -i：提示是否删除

## 二、文件相关命令

### 2.1 touch

语法：touch [选项] 文件名

描述：修改文件或目录的时间属性，若文件不存在，则创建一个新文件

选项：

- a 改变档案的读取时间记录。

- m 改变档案的修改时间记录。

- c 假如目的档案不存在，不会建立新的档案。

- r 使用参考档的时间记录。

- d 设定时间与日期，可以使用各种不同的格式。

- t 设定档案的时间记录，格式与 date 指令相同。

~~~shell
# 创建两个文件
touch program file
# 创建一个带空格的文件名
touch "program file"
~~~

查看文件的修改、读取、建立时间，默认情况下ls显示的是文件的mtime（上次修改的时间）

![查看文件的建立、读取、更新时间](Linux%E5%9B%BE%E7%89%87/%E6%96%87%E4%BB%B6%E5%BB%BA%E7%AB%8B%E6%97%B6%E9%97%B4.jpg)

### 2.2 echo

语法：echo 字符串

描述：用于字符串的输出

1. 显示普通字符串

~~~shell
[root@izbp1adurb6tc9s27c82y5z usr]# echo It is a test
It is a test
[root@izbp1adurb6tc9s27c82y5z usr]# echo "It is a test"
It is a test
~~~

2. 显示转义字符

~~~shell
[root@izbp1adurb6tc9s27c82y5z usr]# echo "\"It is a test\""
"It is a test"
~~~

3. 显示结果定向到文件

~~~shell
echo 表示追加到文件末尾 >> java.txt
echo 可以创建新的文件或将文件覆盖原文件内容 > java.txt
~~~

4. 显示命令执行结果

~~~shell
[root@izbp1adurb6tc9s27c82y5z usr]# echo `date`
Sat Dec 12 11:38:39 CST 2020
~~~

### 2.3 cat、tac

语法：cat [选项] 文件名

描述：cat由第一行开始显示文件内容，tac有最后一行开始显示文件内容

选项：

- -n 或 --number：由 1 开始对所有输出的行数编号。

- -b 或 --number-nonblank：和 -n 相似，只不过对于空白行不编号。

- -s 或 --squeeze-blank：当遇到有连续两行以上的空白行，就代换为一行的空白行。

- -v 或 --show-nonprinting：使用 ^ 和 M- 符号，除了 LFD 和 TAB 之外。

- -E 或 --show-ends : 在每行结束处显示 $。

- -T 或 --show-tabs: 将 TAB 字符显示为 ^I。

- -A, --show-all：等价于 -vET。

- -e：等价于"-vE"选项。

- -t：等价于"-vT"选项。

~~~shell
cat /proc/version
uname -a

cat /etc/redhat-release
~~~

### 2.4 more

语法：more [选项] 文件

描述：类似于cat，不过是一页一页的显示，使用空格翻页；使用b返回一页显示，对管道无用

- -num 一次显示的行数
- -d 提示使用者，在画面下方显示 [Press space to continue, 'q' to quit.] ，如果使用者按错键，则会显示 [Press 'h' for instructions.] 而不是 '哔' 声
- -f 计算行数时，以实际上的行数，而非自动换行过后的行数（有些单行字数太长的会被扩展为两行或两行以上）
- -s 当遇到有连续两行以上的空白行，就代换为一行的空白行
- +num 从第 num 行开始显示

**常用操作命令**

- Enter 向下n行，需要定义。默认为1行
- Ctrl+F 向下滚动一屏
- Space 向下滚动一屏
- Ctrl+B 返回上一屏
- = 输出当前行的行号
- ：f 输出文件名和当前行的行号
- V 调用vi编辑器
- !命令调用Shell，并执行命令
- q 退出more
- /字符串：代表在这个现实的内容当中，向下查找字符串这个关键词

### 2.5 less

语法：less [选项] 文件

描述：查看文件内容，可以通过/要搜索的字符，来在该文件中搜索指定字符

- 空格键：向下翻动一页
- pagedown：向下翻动一页
- pageup：向上翻动一页
- /字符串：向下查找字符串
- ?字符串：向上查找字符串
- n：重复前一个查找（与/或?有关）
- N：反向的重复前一个查找（与/或?有关）
- g：前进到这个数据的第一行
- G：前见到这个数据的最后一行去（注意大小写）
- q：离开less这个程序

~~~shell
less /etc/services
/tcp
~~~

### 2.6 head

语法：head [选项] 文件

描述：查看文件内容，只看头几行

选项：

- -n：查看头n行

如果-n后的数字为负数，则表示不显示后n行

~~~shell
# CentOS7的/etc/man_db.conf一共131行，使用-n -100，则只显示前31行，后100行不显示
head -n -100 /etc/man_db.conf
~~~

### 2.7 tail

语法：tail [选项] 文件

描述：查看文件内容，只查看文件末尾几行

选项：

- -n：末尾几行
- -f：follow输出文件修改的内容，用于追踪文件修改，不断刷新

-n +数字表示显示n行后的数据

~~~shell
# 显示100行以后的数据
tail -n +100 /etc/man_db.conf
~~~

~~~shell
# 显示/etc/man_db.conf的第11-20行
# 先使用head -n 20获取前20行
# 然后使用tail -n 10获取后10行
head -n 20 /etc/man_db.conf | tail -n 10
~~~

~~~shell
# 承上，在显示第11-20数据的时候显示行号
cat -n /etc/man_db.conf | head -n 20 | tail -n 10
~~~

### 2.8 wc

语法：wc [选项] 文本

描述：统计指定文本的行数、字数、字节数

选项：

- -l：lines显示行数
- -w：显示单词数
- -c：显示字节数

### 2.9 file

语法：file [选项] 文件

描述：用于查看文件类型

### 2.10 wget

语法：wget [选项] [url地址]

描述：下载网络文件

选项：

- -b：background后台下载
- -P：directory-prefix下载到指定目录
- -t：tries最大尝试次数
- -c：continue断d点续传
- -p：page-requisites下载页面所有内容，包括图片、视频等
- -r：recursive递归下载

### 2.11 链接ln（link）

语法：ln [选项] [源文件] [目标文件]

描述：生成链接文件

选项：

- -s：创建软链接
- 不加s：创建硬链接

软链接：文件是l开头，类似于windows的快捷方式，指向源文件

硬链接：文件是-开头，类似于复制粘贴的效果，但是可以实现同步更新，不能指向目录

### 2.12

语法：od 选项 参数

描述：读取二进制文件，不会产生乱码的情况

选项：

- -t：后面可以接各种[类型（type）]的输出，例如
  - a			  利用默认的字符来输出
  - c              使用ASCII字符来输出
  - d[size]     利用十进制来输出数据，每个整数占用size Bytes
  - f[size]      利用浮点制来输出数据，每个整数占用size Bytes
  - o[size]     利用八进制来输出数据，每个整数占用size Bytes
  - x[size]     利用十六进制来输出数据，每个整数占用size Bytes

~~~shell
# 将/etc/issue这个文件的内容以八进制列出存储值与ASCII的对照表
od -t oCc /etc/issue
# 查看password的ASCII码
echo password | od -t oCc
~~~

![od](Linux%E5%9B%BE%E7%89%87/od.jpg)

## 三、查找命令

### 3.1 find

语法：find [搜索范围] [选项] [匹配条件]

描述：查找文件或目录

选项：

- -name：按文件名查找
- -user：按文件拥有者查找
- -size：按文件大小查找（+n大于，-n小于，n等于）

~~~shell
find / -name HelloWorld.java
~~~

### 3.2 grep

语法：grep [选项] 查找内容 源文件

描述：在文件内搜索字符串匹配的行并输出

选项：

- -c：count只输出匹配行的计数
- -n：line-number显示匹配行及行号

~~~shell
grep -n public HelloWorld.java
~~~

### 3.3 which

语法：which [选项] 命令

描述：搜索命令所在目录及别名信息

~~~shell
which echo
~~~

## 四、日期命令

### 4.1 date

语法：date [选项] [格式]

描述：显示或设置时间

选项：

- -s：set以字符串格式设置时间

格式（区分大小写）：

+%Y：显示当前年份

+%m：显示当前月份

+%d：显示当前是哪一天

+%H：显示当前小时（0-23）

+%I：显示当前小时（10-12）

+%M：显示当前分钟

+%S：显示当前秒数

~~~shell
[haospring@izbp1adurb6tc9s27c82y5z root]$ date +%Y/%m/%d
2020/12/30
[root@izbp1adurb6tc9s27c82y5z usr]# date "+%Y-%m-%d %H:%M:%S"
2020-12-13 15:01:05
~~~

### 4.2 cal

语法：cal [options] [[[day] month] year]

描述：显示日期

- -3显示上一月，当前月和下一月
- -s, --sunday，以周日作为一周的开始
- -m, --monday，以周一作为一周的开始
-  -y, --year ，显示指定的年

~~~shell
# 显示日月年对应的日历
cal 30 12 2020
# 显示整年的日历
cal 2021
cal -y 2021
# 显示当前月日历
cal
~~~

## 五、进程线程命令

### 5.1 ps

语法：ps [选项]

描述：查看系统中所有进程

- -A 列出所有的进程
- -w 显示加宽可以显示较多的资讯
- -au 显示较详细的资讯
- -aux 显示所有包含其他使用者的行程
- aux输出格式 :
- USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND

~~~shell
ps -aux
ps -aux | grep mysql
~~~

### 5.2 top

语法：top [选项]

描述：查看系统的健康状态

选项：

- -d 秒数：Delay-time，指定top命令每隔几秒更新，默认是3秒
- -i：idie-process，使top命令不显示任何闲置或者僵死进程
- -p：Monitor-PIDs，通过指定监控进程PID来仅仅监控某个进程
- -s：secure-mode，使top在安全模式运行，去除交互命令所带来的潜在危险
- -n：更新的次数，完成后退出top

~~~shell
top -d 2 -i - n 5
~~~

### 5.3 kill

语法：kill [选项] 进程id

描述：终止某个指定pid的服务进程

选项：

- 1 (HUP)：重新加载进程。
- 9 (KILL)：杀死一个进程。
- 15 (TERM)：正常停止一个进程。

## 六 、打包压缩

### 6.1 tar

语法：tar [选项] 包名.tar.gz 待打包的内容

描述：打包目录，压缩后的文件格式为.tar.gz

选项：

- -c：create生成.tar打包文件
- -x：entract解包.tar文件
- -v：verbose显示详细信息
- -f：file指定压缩后的文件名
- -z：打包同时压缩
- -C：解压到指定目录

压缩文件

~~~shell
tar -zcvf test.tar test.conf
~~~

解压缩文件

~~~shell
tar -zxvf test test.tar.gz
tar -zxvf test.tar -C /root
~~~

### 6.2 zip和unzip

语法：zip [选项] 包名.zip 待压缩内容

解压：uzip 包名.zip

描述：压缩文件和目录，Windows和linux通用且可以压缩目录并保留原文件

选项：

- -r：递归压缩目录

~~~shell
zip test.zip test.conf test.tar
unzip test.zip
~~~

## 七、系统状态检测的命令

### 7.1 ifconfig

语法：ifconfig [网络设备] [参数]

描述：获取网卡配置和网络状态信息

~~~shell
ifconfig
~~~

### 7.2 netstat

语法：netstat [参数]

描述：显示整个系统目前网络情况，比如目前的链接、数据包传递数据、路由表内容等

~~~shell
netstat -nplt
~~~

### 7.3 uname

语法：uname [选项]

描述：查看系统内核和系统版本等信息

选项：

- -a或--all 　显示全部的信息。
- -m或--machine 　显示电脑类型。
- -n或-nodename 　显示在网络上的主机名称。
- -r或--release 　显示操作系统的发行编号。
- -s或--sysname 　显示操作系统名称。
- -v 　显示操作系统的版本。
- --help 　显示帮助。
- --version 　显示版本信息。

~~~shell
uname -a
uname --version
~~~

### 7.4 uptime

语法：uptime [选项]

描述：查看系统的负载信息，可以显示当前系统时间、系统已运行时间、启动终端数量以及平均负载值等信息。负载值越高，压力越大，负载值越低越好，尽量不超过1，生产环境不超过5

### 7.5 free

 语法：free [选项]

描述：显示当前系统中内存的使用信息

选项：

- -m：megabytes以兆字节显示
- -h：human带单位输出

~~~shell
free -mh
~~~

### 7.6 who

语法：who [选项]

描述：查看当前登入主机的用户终端信息

~~~shell
who
~~~

### 7.7 whoami

语法：whoami

描述：查看当前的使用者

### 7.8 last

语法：last [选项]

描述：显示用户最近登录信息

- -num 展示前 num 个

### 7.9 history

语法：history [选项]

描述：显示历史执行过的命令

选项：

- -c：清楚所有历史记录，但是.bash_history文件内容不会被删除

~~~shell
history -c
~~~

## 八、关机命令

### 8.1 reboot

语法：reboot [选项]

描述：重启，等同于shutdown -r now

### 8.2 poweroff

语法：poweroff [选项]

描述：关闭系统

### 8.3 halt

语法：halt [选项]

描述：若系统的 runlevel 为 0 或 6 ，则Linux halt命令关闭系统，否则以 shutdown 指令（加上 -h 参数）来取代。

### 8.4 shutdown

语法：shutdown [选项] [时间]

描述：关机，centos7之前需要加上时间，centos7后不加时间默认是一分钟后关机

选项：

- -H：--halt 关机
- -P：--poweroff 关机
- -r：--reboot 重启
- -h：将系统的服务停掉后，立即关机
- -k：不是真的关机，只是发送警告信息出去
- -c：取消已经在进行的shutdown命令内容
- 时间：指定系统关机的时间，默认1分钟

~~~shell
# 立即关机，now相当于0
shutdown -h now
# 10分钟后关机，并通知在线用户
shutdown -h 10 "10分钟后关机，请做好准备"
# 10分钟后重启
shutdown -r 10
# 取消关机操作
shutdown -c
~~~

### 8.5 sync

将内存中的数据写入到磁盘中

reboot、shutdown、halt都内置了sync，但是建议多用

## 九、权限管理

==所有的用户信息都保存在：/etc/passwd文件里==

==所有的组信息都保存在：/etc/group文件里==

==用户密码都保存在：/etc/shadow里，且是加密的==

无论什么管理权限都不能直接查看用户密码，如果用户密码遗忘，可以使用root账户通过`passwd 用户名`修改

### 9.1 添加用户

创建用户完毕后，必须修改密码否则无法登陆

~~~shell
# useradd 用户名
# passwd 用户名
# 输入密码
[root@izbp1adurb6tc9s27c82y5z ~]# useradd haospring
[root@izbp1adurb6tc9s27c82y5z ~]# passwd haospring
Changing password for user haospring.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
~~~

切换用户

~~~shell
# 切换到haospring用户
su haospring
# 切换到root用户
su root
~~~

查看用户的信息

~~~shell
[root@izbp1adurb6tc9s27c82y5z ~]# id haospring
uid=1004(haospring) gid=1004(haospring) groups=1004(haospring)
~~~

创建组

~~~shell
# groupadd 组名
groupadd test
~~~

新建用户同时增加工作组

~~~shell
# useradd -g 组名 用户名
useradd -g test hcs
passwd hcs
~~~

### 9.2 修改用户

usermod

- -c<备注> 　修改用户帐号的备注文字。
- -d<登入目录> 　修改用户登入时的目录。
- -e<有效期限> 　修改帐号的有效期限。
- -f<缓冲天数> 　修改在密码过期后多少天即关闭该帐号。
- -g<群组> 　修改用户所属的群组。
- -G<群组> 　修改用户所属的附加群组。
- -l<帐号名称> 　修改用户帐号名称。
- -L 　锁定用户密码，使密码无效。
- -s<shell> 　修改用户登入后所使用的shell。
- -u<uid> 　修改用户ID。
- -U 　解除密码锁定。

~~~shell
# 修改用户所在组
usermod -g test haospring
~~~

### 9.3 删除用户账号

~~~shell
# 删除账户
# userdel 用户名
# 删除组
# groupdel 组名 
userdel hcs
groupdel test2
~~~

### 9.3 文件权限

~~~shell
drwxr-xr-x   9 root  root       4096 Nov 26 14:38 apache-tomcat-8.5.60
# drwxr-xr-x，第一位表示文件类型
# 后面三个一组，分别是u（user），g（group），o（other）
# 9 引用计数，表示文件被引用过多少次
# root root	文件所有者，所有者所在的组
# 最后修改时间，一般是创建的事件
~~~

| 文件类型 |  文件拥有者的权限  | 此群组账号的权限 | 其他人的权限 |
| :------: | :----------------: | :--------------: | :----------: |
|    d     |        rwx         |       r-x        |     r-x      |
|  文件夹  | 可读、可写、可执行 |   可读、可执行   | 可读、可执行 |

~~~shell
-		文件
d		目录（文件夹）
l		软链接文件
b		设备文件里面的可供存储的周边设备（可按块随机读写的设备）
c		设备文件里面的串行端口设备，例如键盘、鼠标（一次性读取设备）
~~~

### 9.4 改变文件权限

**chmod：修改文件权限**

**chgrp：修改文件所在组**

**chown：修改文件所有者**

~~~shell
# 修改文件所属用户的同时修改文件所属组
chown haospring:user test.txt
# 只修改文件所属的组
chown :user test.txt
# 用户名和组名之间也可以用.分割
chown haospring.user test.txt
chown .user test.txt

#使用chgrp修改文件所属组
chgrp user test.txt
~~~

**+：加入**

**-：移除**

**=：设置**

给三种身份都添加执行的权限

~~~shell
chmod +x 文件名
~~~

等价于

~~~shell
chmod a+x 文件名
~~~

a表示all，可以用u、g、o替换

去掉某个用户的可写权限

~~~shell
chmod u-w 文件名
~~~

~~~shell
chmod u=rw,go=r HelloWorld.java
~~~

### 9.5 目录权限

r：用户对目录具有查看目录结构的权限，可以使用ls

w：用户具有改动目录结构的权限（新增、删除、改名、移动该目录下的文件和目录）

x：用户可以进入该目录（/root目录，其他用户无法查看、修改、进入）

不具备x权限是无法使用该目录下的命令的

### 9.6 数字形式改变文件权限

读取权限：r或4

写入权限：w或2

执行权限：x或1

可读可写可执行：rwx=4+2+1=7

可读可写不可执行：rw=4+2=6

可读不可写可执行：rx=4+1=5

600、644、700、755、711

~~~shell
chmod 777 HelloWorld.java
chmod 644 HelloWorld.java
~~~

修改文件的拥有者

chown user[:group] file

~~~shell
chown haospring:test HelloWorld.java
~~~

### 9.7 SUID、SGID、SBIT

文件除了r、w、x的权限外，还有s和t的全新

#### 9.7.1 SUID

![SUID](Linux%E5%9B%BE%E7%89%87/SUID.jpg)

当**文件拥有者的x位**上是s时，代表SUID的权限（Set UID），可**暂时**获得root的权限，只能用在**二进制程序**上，对目录和shell脚本无效

例：所有的用户名和密码都存放在/etc/shadow文件里，只有root用户可以读取修改这个文件的内容，但是普通用户使用passwd修改自己的密码，会把修改后的密码写入到这个文件中，是因为passwd这个命令具有SUID的权限，可以暂时获得该文件的拥有者的权限（root）

- SUID权限仅对二进制程序有效
- 执行者对于该程序需要具有x的可执行权限
- 本权限仅在执行该程序的过程中有效
- 执行者将具有该程序拥有者的权限

#### 9.7.2 SGID

当**文件用户组的x位上**是s时，代表SGUID的权限（Set GID）

![SGID](Linux%E5%9B%BE%E7%89%87/SGID.jpg)

当文件具有SGID的权限时，可以获得文件所属组的权限，SGID在目录上也有效

- SGID对二进制程序有用
- 程序执行着对于该程序来说，需具备x的权限
- 执行者在执行的过程中将会获得该程序用户组的支持

**SGID在目录上**

- 用户若对于此目录具有r与x的权限时，该用户能够进入此目录
- 用户在此目录下的有效用户组将会变成该目录的用户组
- 用途：若用户在此目录下具有w的权限，则用户所建立的新文件，该新文件的用户组与此目录的用户组相同

#### 9.7.3 SBIT

这个Sticky Bit（SBIT）只针对目录有效

- 当用户对于此目录具有w、x权限，即具有写入的权限
- 当用户在该目录下建立文件或目录时，仅有自己与root才有权利删除该文件

#### 9.7.4 设置权限

4为SUID

2为SGID

1为SBIT

在权限前加上数字可以设置这三个权限

~~~shell
# 给权限为755的文件加上SUID的权限
chmod 4755 filename
~~~

### 9.8 文件种类与扩展名

Linux的文件是否可以执行与文件扩展名无关

和文件前面的十个权限有关

当文件权限为x表示该文件有执行的能力，但是能不能执行成功需要根据文件的内容

e.g. 将文件`/usr/bin/cat`的权限去掉x，则该文件不能被使用

~~~shell
# 去掉cat文件的可执行权限
chmod a-x /usr/bin/cat
# 使用cat会提示权限不够
cat test.txt
# -bash: /usr/bin/cat: 权限不够
~~~

## 十、权限提升

sudo命令

把用户加到wheel组后才能使用sudo命令

~~~shell
usermod -G wheel haospring
sudo touch haospring.txt
~~~

## 十一、配置jdk

~~~shell
# 配置环境变量，所有的环境变量配置都在该文件中
vim /etc/profile
# 创建JAVA_HOME
export JAVA_HOME=/usr/jdk1.8.0_271
# 将JAVA_HOME的配置放在所有的配置前面
export PATH=$JAVA_HOME/bin:$PATH
# jdk8后可以选择不配置CLASSPATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
~~~

配置完成后加载配置

~~~shell
source /etc/profile
~~~

## 十二、安装软件

### yum语法

yum [options] [command] [package]

选项：

- -y：全部默认为yes
- -h：帮助
- -q：不显示安装的过程

command：要进行的操作

package：安装的包名

### 常用命令

1. 列出所有可更新的软件清单命令：yum check-update
2. 更新所有软件命令：yum update
3. 仅安装指定的软件命令：yum install <package_name>
4. 仅更新指定的软件命令：yum update <package_name>
5. 列出所有可安装的软件清单命令：yum list
6. 删除软件包命令：yum remove <package_name>
7. 查找软件包命令：yum search <keyword>
8. 清楚缓存命令：
   1. yum clean packages：清除缓存目录下的软件包
   2. yum clean headers：清除缓存目录下的headers
   3. yum clean oldheaders：清除缓存目录下的旧的headers
   4. yum clean,yum clean all(=yum clean packages;yum clean oldheaders)：清除缓存目录下的软件包及旧的headers

### 换yum源

~~~shell
# 找到yum源所在位置
cd /etc/yun.repos.d
# 备份
mv CentOS-Base.repo CentOS-Base-aliyun.repo.backup
# 下载网易yum源
wget http://mirrors.163.com/.help/CentOS7-Base-163.repo
# 将网易源修改为
mv CentOS7-Base-163.repo CentOS-Base.repo
# 生成缓存
yum clean all
yum makecache
~~~

### 安装rpm软件包

rpm -ivh [package]

i：install

v：显示详细信息

h：套件安装时列出标记

## 安装mysql（不详细）

CentOS自带mariadb，所以需要先删除它，才能安装mysql

~~~shell
# 查找mariadb是否存在
rpm -qa | grep mariadb
# 删除mariadb
rpm -y remove mariadb名
~~~

启动

~~~shell
# 开启服务
systemctl start mysqld
# 开机启动服务
systemctl enable mysqld
# 查看服务状态
systemctl status mysqld
# 停止服务
systemctl stop mysqld
# 重启服务
systemctl restart mysqld
# 停止开机启动
systemctl disable mysqld
~~~

找到mysql的临时密码

~~~shell
grep "password" /var/log/mysqld.log
~~~

修改密码

~~~mysql
# 方式一：
set password for root@localhost=password('密码');
# 方式二：
alter user 'root'@'localhost' identified by '密码';
~~~

密码过于简单会报错，强行设置简单密码

~~~shell
# 设置密码要求
set global validate_password_policy=0;
# 密码长度最短为1
set global validate_password_length=1;
~~~

修改密码后刷新权限

~~~mysql
flush privileges;
~~~

## 十三、计算器

bc，默认输出为整数

^：指数

%：取余

quit：退出计算器

~~~shell
# 通过scale=number得到小数
1/3
0
# 加上scale
scale=3
1/3
.333
~~~

## 十四、热键

## 14.1 Tab

命令补全、文件补齐

~~~shell
# g[tab][tab]
# 列出所有以g开头的命令
~~~

### 14.2 Ctrl+c

结束正在执行的命令

### 14.3 Ctrl+d

结束键盘输入，类似于exit的功能

### 14.4 Shift+PageUp shift+PageDown

上一页，下一页

## 十五、帮助

### 15.1 --help

--help，多数命令都支持--help

~~~shell
# 例：
ls --help
# 例外：
help pwd
~~~

### 15.2 man page

man：manual，详细的命令操作说明

man date

/string：向下查找string

?string：向上查找string

n：继续下一个查找

N：反向查找

q：结束查找

### 15.3 info page

### 15.4 /usr/share/doc

## 十六、内部命令和外部命令

### 内部命令

内部命令实际上是shell程序的一部分，通常在linux系统加载运行时shell就被加载并驻留在系统内存中。

执行速度比外部命令快，因为解析内部命令shell不需要创建子进程

### 外部命令

外部命令是linux系统中的使用程序部分，在系统加载时并不随系统一起被加载到内存中，而是在需要时才将其调用到内存中

通常放在/bin、/usr/bin中

echo $PATH可以打印外部命令的存储路径，如：ls、vi

type指令可以分辨内部命令和外部命令

~~~shell
[root@izbp1adurb6tc9s27c82y5z ~]# type cd
cd is a shell builtin
[root@izbp1adurb6tc9s27c82y5z ~]# type mkdir
mkdir is hashed (/usr/bin/mkdir)
echo $PATH mkdir
~~~

