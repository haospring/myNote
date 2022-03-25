### Ubuntu20.04 无法在设置区域与语言选项设置中文的解决办法

1. 在 `/etc/locale.gen`这个配置文件中查看是否支持中文

~~~shell
vim /etc/locale.gen
~~~

 ![image-20220323102608820](ubuntu20%20%E6%97%A0%E6%B3%95%E5%9C%A8%E8%AE%BE%E7%BD%AE%E4%B8%AD%E8%AE%BE%E7%BD%AE%E4%B8%AD%E6%96%87.assets/image-20220323102608820-16480023723821.png)

2. 出现上图红框中的内容表示支持中文，但是`/etc/locale.gen`是一个只读文件，无法修改，有如下两种方法

   2.1 方法一：将该文件修改为可写文件

   ~~~shell
   sudo chmod a+w /etc/locale.gen
   ~~~

   2.2 方法二：直接切换到 `root`用户

   ~~~shell
   su root
   ~~~

3. 重新执行第一步，按`i`进入编辑模式，取消 `zh_CN.UTF-8 UTF-8`的注释，修改后如下图所示

 ![image-20220323103255353](ubuntu20%20%E6%97%A0%E6%B3%95%E5%9C%A8%E8%AE%BE%E7%BD%AE%E4%B8%AD%E8%AE%BE%E7%BD%AE%E4%B8%AD%E6%96%87.assets/image-20220323103255353.png)

4. 退出并保存文件

   4.1 按 ESC 退出编辑模式

   4.2 输入 `wq`保存修改并退出

5. 将`/etc/locale.gen` 的读写权限恢复

~~~shell
chmod 644 /etc/locale.gen
~~~



