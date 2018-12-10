Chapter01 课程学习笔记
======
#### 项目实践
该项目例子下的Chapter01是可以直接运行的源码([去原项目wiki参考](https://github.com/romantiskt/AfterClass/blob/master/Chapter01/README.md))
##### 编译环境
- Mac OS:10.14.2 
- AndroidStudio:3.2.1
- API22模拟器(x86)
- ndk-r16b
- cmake
##### 前期准备
- 为项目配置成ndk16b([下载地址](https://dl.google.com/android/repository/android-ndk-r16b-darwin-x86_64.zip))->如果此demo不配置ndk16b则无法生成日志，原因待查
- structure配置新ndk路径
- 配置defaultConfig,加入如下代码
```
externalNativeBuild {
            cmake {
                cppFlags "-std=c++11"
                arguments "-DANDROID_TOOLCHAIN=gcc"
            }
        }
```
* 编译breakpad

```
因为使用的breakpad工具取决于每个人的编译环境，所以最好下载breakpad源码编译
1：git clone breakpad源码
2： ./configure 
3: make

经过上述步骤，则生成了开发工具minidump_stackwalker 在breakpad/src/precessor目录下
```

##### 运行项目,获取日志
不知是新AndroidStudio原因还是项目配置原因，下载的第三方项目都需要先 build->make project->rebuild project。
项目运行后 点击按钮app采集崩溃日志 在sdcard/crashDump目录下
##### 日志输出 dump文件->log
```
/Users/wangyang/company/breakpad/src/processor/minidump_stackwalk /Users/wangyang/company/Chapter01/c7d1a83c-d7fa-4cd7-dd2eb1af-3ea72455.dmp >crashlog.txt  
```
##### 日志分析

```
/Users/wangyang/sdk/android-ndk-r16b/toolchains/aarch64-linux-android-4.9/prebuilt/darwin-x86_64/bin/aarch64-linux-android-addr2line -f -C -e /Users/wangyang/company/Chapter01/sample/build/intermediates/transforms/mergeJniLibs/debug/0/lib/x86/libcrash-lib.so 0x515
```


#### [Breakpad](https://github.com/google/breakpad)
* Breakpad是什么？应用场景是什么？
* 怎么集成到app中
* 编译