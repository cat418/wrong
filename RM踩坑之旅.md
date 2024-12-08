# -----RM踩坑之旅------------

## 1.类模板函数的声明和定义问题



``` c++
cmake_minimum_required(VERSION 3.17)

project(test)

file(GLOB_RECURSE SRC basic/src/*.cpp class_test/src/*.cpp high_precision/src/*.cpp stl/src/*.cpp)

add_executable(${PROJECT_NAME} main.cpp ${SRC})

target_include_directories(${PROJECT_NAME} PUBLIC basic/include )

target_include_directories(${PROJECT_NAME} PUBLIC class_test/include)

target_include_directories(${PROJECT_NAME} PUBLIC high_precision/include)
include_directories(${PROJECT_NAME} PUBLIC stl/include)
```



``` c++
zq@xzq:~/project/cpp_test/build$ make
[ 16%] Building CXX object CMakeFiles/test.dir/main.cpp.o
[ 33%] Building CXX object CMakeFiles/test.dir/basic/src/basic.cpp.o
[ 50%] Building CXX object CMakeFiles/test.dir/class_test/src/class_test.cpp.o
[ 66%] Building CXX object CMakeFiles/test.dir/high_precision/src/high_precision.cpp.o
[ 83%] Building CXX object CMakeFiles/test.dir/stl/src/stl.cpp.o
[100%] Linking CXX executable test
/usr/bin/ld: CMakeFiles/test.dir/main.cpp.o: in function `main':
main.cpp:(.text+0x4f): undefined reference to `Vector<int>::Vector()'
/usr/bin/ld: main.cpp:(.text+0x60): undefined reference to `Vector<int>::pushBack(int)'
/usr/bin/ld: main.cpp:(.text+0x71): undefined reference to `Vector<int>::pushBack(int)'
/usr/bin/ld: main.cpp:(.text+0x82): undefined reference to `Vector<int>::pushBack(int)'
/usr/bin/ld: main.cpp:(.text+0xb9): undefined reference to `Vector<int>::popBack()'
/usr/bin/ld: main.cpp:(.text+0xfa): undefined reference to `Vector<int>::insert(int, int)'
/usr/bin/ld: main.cpp:(.text+0x14d): undefined reference to `Vector<int>::front()'
/usr/bin/ld: main.cpp:(.text+0x191): undefined reference to `Vector<int>::back()'
/usr/bin/ld: main.cpp:(.text+0x1b9): undefined reference to `Vector<int>::clear()'
/usr/bin/ld: main.cpp:(.text+0x1c5): undefined reference to `Vector<int>::empty()'
/usr/bin/ld: main.cpp:(.text+0x205): undefined reference to `Vector<int>::pushBack(int)'
/usr/bin/ld: main.cpp:(.text+0x216): undefined reference to `Vector<int>::pushBack(int)'
/usr/bin/ld: main.cpp:(.text+0x23e): undefined reference to `Vector<int>::size()'
/usr/bin/ld: main.cpp:(.text+0x266): undefined reference to `Vector<int>::begin()'
/usr/bin/ld: main.cpp:(.text+0x277): undefined reference to `Vector<int>::end()'
collect2: error: ld returned 1 exit status
make[2]: *** [CMakeFiles/test.dir/build.make:161：test] 错误 1
make[1]: *** [CMakeFiles/Makefile2:83：CMakeFiles/test.dir/all] 错误 2
make: *** [Makefile:91：all] 错误 2
```

**为什么cmakelists.txt没有问题，但是链接不到函数的声明**

*类模板函数需要在头文件中声明和定义*

==一般把头文件后缀写为.hpp==

## 2.类成员的静态函数的初始化

**在类内**

``` c++
iniline static int a=0;
```

**在类外(==注意加上作用域==)**

``` c++
int Person::a=0;
```

## 3.2024.12.6 关于clash

泡芙云报错

![img](https://github.com/cat418/wrong/blob/main/RM%E8%B8%A9%E5%9D%91picture/1.png)

解决方法:

如果有Repair的选项，直接点然后重启.

如果没有:

![image-20241206201113109](https://github.com/cat418/wrong/blob/main/RM%E8%B8%A9%E5%9D%91picture/2.png)

如果还有问题可以看这个文档

[ 关于clash报错 ](https://blog.csdn.net/qq_62650410/article/details/132133333)

## 4.视频播放报错[ WARN:0] global ./modules/videoio/src/cap_gstreamer.cpp (1100) open OpenCV | GStreamer warning: Cannot query video position: status=0, value=-1, duration=-1

在获取fps的代码后加上

``` c++
 if (fps <= 0) {
        fps = 30;  // 设置默认的帧率
        }
```

视频即可正常播放

==如果显示核心转储应该就是代码的问题和视频没关系==

导致报错原因

**1.视频文件损坏 **

**2.GStream插件问题** 

``` c++gst-inspect-1.0
gst-inspect-1.0 //检查插件是否缺失
```

**3.视频格式本身不支持查询 **



## 5.关于核心转储

### 1.数组越界

``` c++
    cv::Mat img[3];
    cv::split( frame, img);
    cv::Mat r_b = img[3] - img[0]; //应该是img[2]-img[0] Mat img[3]中的3是元素的个数 最后一行的3是下标
```







