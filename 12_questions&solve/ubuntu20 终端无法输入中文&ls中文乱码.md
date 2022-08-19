### ubuntu20.04 终端无法输入中文，以及ls命令出现中文乱码问题解决方案

#### 1. 安装中文支持包

~~~shell
sudo apt-get install language-pack-zh-hans
~~~

#### 2. 修改 *~/.bashrc* 文件

~~~shell
vim ~/.bashrc

# 将下面两行加入到文件末尾
export LC_ALL="zh_CN.UTF-8"
export LANG="zh_CN.UTF-8"
~~~

#### 3. 刷新文件

~~~shell
# 保存并退出后
source ~/.bashrc
~~~



