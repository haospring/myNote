### Ubuntu20.04 反编译

反编译三件套：apktool、dex2jar、jd-gui



#### 环境配置

##### 下载链接

[apktool: https://ibotpeaches.github.io/Apktool/](https://ibotpeaches.github.io/Apktool/)

[dex2jar: https://sourceforge.net/projects/dex2jar/](https://sourceforge.net/projects/dex2jar/)

[jd-gui: http://java-decompiler.github.io/](http://java-decompiler.github.io/)

##### 安装 apktool

1. 下载 apktool 脚本文件，下载 apktool_x.x.x.jar 文件
2. 将两个文件放到同一个目录下，并把 apktool_x.x.x.jar 的文件名改为 apktool.jar
3. 给这两个文件加上可执行权限

~~~shell
sudo chmod a+x apktool
sudo chmod a+x apktool.jar
~~~

4. 将这两个文件放到 `/usr/local/bin` 路径下
5. 执行命令 `apktool d xxx.apk` 反编译 apk ，得到目录如下

 ![apktool反编译](/home/haospring/Documents/MyGithub/myNote/12_questions&solve/ubuntu20%E5%8F%8D%E7%BC%96%E8%AF%91apk.assets/apktool%E5%8F%8D%E7%BC%96%E8%AF%91.png)

##### 安装 dex2jar

1. 下载最新版 dex2jar-2.0.zip 并解压
2. 给 d2j-dex2jar.sh 设置可执行权限（Linux）

~~~shell
sudo chmod a+x d2j-dex2jar.sh
~~~

3. 将 app 后缀改为 zip 格式，解压得到 classes.dex 文件，将 classes. dex 文件复制到 dex2jar-2.0 目录下
4. 执行 `./dex2jar-2.0` ，可能会出现以下错误

 ![dex2jar报错](/home/haospring/Documents/MyGithub/myNote/12_questions&solve/ubuntu20%E5%8F%8D%E7%BC%96%E8%AF%91apk.assets/dex2jar%E6%8A%A5%E9%94%99.png)

使用 vim 、notepad++ 或其他编辑器，将 .dex 的头文件改为 036，重新执行命令，生成 .jar 文件

![notepad++编辑dex文件](/home/haospring/Documents/MyGithub/myNote/12_questions&solve/ubuntu20%E5%8F%8D%E7%BC%96%E8%AF%91apk.assets/notepad++%E7%BC%96%E8%BE%91dex%E6%96%87%E4%BB%B6.png) 

[参考链接](https://www.jianshu.com/p/55bf5f688e9a)

##### 安装jd-gui

1. 下载安装 jd-gui-1.6.6.deb ，Ubuntu20.04 可能会出现安装后无法打开的问题
2. 查看系统log，`/var/log/syslog` 表示系统日志，`/var/log/apport.log` 表示应用 crash 日志

~~~shell
cat /var/log/syslog | grep jd-gui
~~~

3. 发现报错原因为 Exception in thread "main" java.awt.AWTError: Assistive Technology not found
4. 解决办法：执行命令 `sudo vim /etc/java-8-openjdk/accessibility.properties`
5. 将第二步生成的 .jar 文件用 jd-gui 打开，即可看到 java 源码

[参考链接](https://blog.csdn.net/weixin_42361018/article/details/114745151)