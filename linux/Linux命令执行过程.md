# Linux命令执行过程

## 内部命令

执行速度快

不同的shell可能有不同的内部命令

~~~shell
#显示内部命令
help
enable
#查看命令是否时内部命令
type pwd
type help
#禁用某个内部命令
enable -n pwd
#启用命令
enable pwd
#显示所有禁用的命令
enable -n
#显示命令的内部外部
type -a pwd
~~~



## 外部命令

执行速度慢，表现为磁盘上的路径

外部命令比内部命令的数量多

命令执行顺序：内部命令>hash表（记录外部命令的路径）>外部命令

~~~ shell
#显示外部命令的路径
which init
type init
#显示外部命令的路径及其配置文件、是说明文档路径
whereis init
~~~

[视频链接](https://edu.aliyun.com/lesson_1725_13994?spm=5176.8764728.0.0.f51f1860uK4GoR#_13994)

