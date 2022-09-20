```linux
adb shell ps #查看进程
adb shell ps | findstr com.app.test  #查看特定apk进程，com.为包名
adb shell ps -x [PID]  #查看特定进程状态
adb shell kill [PID]  #杀死特定进程
adb shell top | grep [package_name]  #实时监听程序进程状态
```