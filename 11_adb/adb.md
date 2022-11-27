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

- 查看 activity

  - 查看当前运行的所有 activity

  ~~~shell
  adb shell dumpsys activity
  ~~~

  - 查看当前可见的 activity，包括任务栈信息等

  ~~~shell
  adb shell dumpsys activity activities
  ~~~

  - 查看最近运行的 activity

  ~~~shell
  adb shell dumpsys activity recents
  ~~~

  ![adb dumpasys](adb.assets/adb%20dumpasys.png)

- 日志

  - 导出日志到本地

  ~~~shell
  adb logcat >> a.txt
  ~~~

  - 终端查看日志

  ~~~shell
  adb logcat | grep haospring
  ~~~

- 安装 APK

  - 非系统 APP 安装

  ~~~shell
  adb install xxx.apk
  ~~~

  - 系统 APP 安装

  ~~~shell
  adb push fileName path
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

  - 查看应用包名

  ~~~shell
  adb shell pm list packages
  adb shell pm list packages | grep com.haospring*
  ~~~

  - 查看应用所在路径

  ~~~shell
  adb shell pm list packages -f
  ~~~

- 启动 Activity

  - 启动 Activity

  ~~~shell
  # adb shell am start 包名/完整Activity路径
  adb shell am start -n com.haospring.test_messenger/.activity.MainActivity
  ~~~

  - 启动 Activity 并且携带一个Intent（key：haospring，value：hcs）

  ~~~shell
  # -e 表示添加额外Key-Value信息
  adb shell am start -n com.haospring.test_messenger/.activity.MainActivity -e haospring hcs
  ~~~

  - 通过隐式 Intent 启动一个 Activity

  ~~~shell
  # -a 表示action,-c 表示category,-d 表示data_uri,
  adb shell am start -a "com.haospring.testtaskaffinity.SecondActivity"
  ~~~

  - 关闭 Activity

  ~~~shell
  adb shell am force-stop com.haospring.test_messenger/.activity.MainActivity
  ~~~

- 启动 Service

  - 启动 Service

  ~~~shell
  adb shell am startservice -n com.haospring.test_messenger/.service.MessengerService
  ~~~

  - 关闭 Service

  ~~~shell
  adb shell am stopservice com.haospring.test_messenger/.service.MessengerService
  ~~~

- 发送广播

  - 发送广播

  ~~~shell
  adb shell am broadcast -a "com.haospring.mybroadcast"
  ~~~

  - 发送携带参数的广播（Intent）

  ~~~shell
  adb shell am broadcast -a "com.haospring.mybroadcast" -e haospring hcs
  ~~~

- 卸载安装的 app

  ~~~shell
  adb uninstall com.thundersoft.myapplication
  # 保留数据卸载
  adb uninstall -k com.thundersoft.myapplication
  adb shell cmd package uninstall -k com.hcs.testconfigchanges
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

- 查看当前正在运行的进程列表

  ~~~shell
  adb shell ps
  adb shell ps | grep com.haospring
  ~~~

- adb shell dumpsys 命令使用

  - 查看 dumpsys 能提供查询信息的服务

  ~~~shell
  adb shell service list
  ~~~

  - 查看 cpu 使用情况

  ~~~shell
  adb shell dumpsys cpuinfo
  ~~~

  - 查看 cpu 实时运行情况

  ~~~shell
  adb shell top
  ~~~

  - 查看内存使用情况

  ~~~shell
  adb shell dumpsys meminfo
  ~~~
  
- 切换黑白模式

  - 切换白天模式

  ~~~shell
  adb shell cmd uimode night no
  ~~~

  - 切换黑夜模式

  ~~~shell
  adb shell cmd uimode night yes
  ~~~

  

[参考链接：ADB常用命令及其用法大全](https://blog.csdn.net/qq_39969226/article/details/87897863)























