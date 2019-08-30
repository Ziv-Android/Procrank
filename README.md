## 前言
源码使用的是Android7.0下的`WORKING_DIRECTORY/system/extras`文件, 若直接使用原目录, 编译`procrank`时会提示
```
undefined reference to `strlcpy'
```
在本项目中我已经添加进来`bionic/libc/upstream-openbsd/lib/libc/string/strlcpy.c`


## 编译
1. 下载并进入目录
```
git clone https://github.com/Ziv-Android/Procrank.git
cd Procrank
```
2. 执行make编译
```
mkdir build
cd build
cmake ..
make
```

若执行`make`失败,可以先删除我已经编译好的文件
```
rm -rf build
```
重新执行第2步即可

## 安装
将`procrank`和`procmem`文件push到手机的`/system/xbin`目录下,`libpagemap.a`文件到`/system/lib`目录下
```
adb push procrank /system/xbin
adb push procmem /system/xbin
adb push libpagemap.a /system/lib
```
添加权限
```
chmod 777 /system/xbin/procrank
chmod 777 /system/xbin/procmem
chmod 777 /system/lib/libpagemap.a
```
如遇到权限问题需要重新挂载system的话执行以下命令
```
mount -o remount,rw /system
```
