- 查看当前连接设备：

  - 查看当前连接设备：

  ~~~shell
  adb devices
  ~~~

  - 如果发现多个设备：

  ~~~shell
  # adb -s 设备号 其他指令
  adb -s emulator-5554 install -t app-debug.apk
  ~~~

- 查看顶部 activity

  ~~~shell
  adb shell dumpsys activity | grep "MainActivity"
  ~~~

  ![adb dumpasys](adb.assets/adb%20dumpasys.png)

- 查看日志

  ~~~shell
  adb logcat >> a.txt
  ~~~

- 安装apk文件

  ~~~shell
  adb install xxx.apk
  ~~~

  - 此安装方式，如果已经存在，无法安装，使用**覆盖安装：**

  ~~~shell
  adb install -r xxx.apk
  ~~~

  - AS 直接 RUN 出来的apk，无法直接安装，使用**-t**

  ~~~shell
  adb install -t xxx.apk
  ~~~

- 查看手机端安装的所有包名

  ~~~shell
  adb shell pm list packages
  adb shell pm list packages | grep com.thunder*
  ~~~

- 启动 Activity

  ~~~shell
  # adb shell am start 包名/完整 Activity 路径
  adb shell am start com.thundersoft.myapplicationkotlin/.MainActivity
  ~~~

- 卸载安装的 app

  ~~~shell
  adb uninstall com.thundersoft.myapplication
  # 保留数据卸载
  adb uninstall -k com.thundersoft.myapplication
  ~~~

- 向设备 push 文件

  ~~~shell
  # adb push 文件名 设备路径
  adb push helloworld.txt /sdcard/Documents/
  ~~~

- 从设备中拉取数据

  ~~~shell
  # adb pull 设备中的文件 本地路径
  adb pull /sdcard/Documents/helloworld.txt ~/Documents
  ~~~

- 设备录屏

  ~~~shell
  # adb shell screenrecord 设备路径
  adb shell screenrecord /sdcard/Movies/demo.mp4
  adb reboot
  ~~~

- 屏幕截图

  ~~~shell
  adb shell screencap /sdcard/Pictures/demo.png
  adb reboot
  ~~~



[参考链接：ADB常用命令及其用法大全](https://blog.csdn.net/qq_39969226/article/details/87897863)























