# RM小菜鸡的成长之旅

## 关于.gitignore

\#.gitignore是一个文本文件,用于告诉Git忽略某些文件或目录，使其不会被提交到版本库中 排除不需要版本控制的文件 如:系统临时文件，IDE文件，环境配置文件，依赖缓存文件,密钥文件等。

作用:减小代码库体积，保护隐私信息

==常见的规则:==

``` c++
example.log 	//忽略example.log文件
node/  			//忽略特定目录
*.log 			//忽略所有拓展名的文件
tmp/*   		//匹配tmp目录下所有文件和文件夹    
.env   			//忽略本地环境文件
logs/*
!logs/work      //忽略logs目录下的所有文件,但会保留logs/work
```

## 关于镜像

#在Docker中，镜像是一个包含了应用程序及其依赖环境的只读模版。镜像用来创建容器，容器是镜像的运行实例。

**镜像是轻量级的打包单元**：它包含了操作系统、依赖环境、配置文件、应用程序代码等。

**镜像是静态的**：它是只读的，无法直接修改。

容器是基于镜像实例化出来的，可以理解为“镜像的运行环境”。

镜像本身并不占用内存，只占用磁盘存储空间。[内存和存储空间的区别](#内存和存储空间的区别)



![镜像和容器的区别](https://github.com/cat418/wrong/blob/main/%E5%B0%8F%E8%8F%9C%E9%B8%A1picture/5.png)

![不同的镜像类型](https://github.com/cat418/wrong/blob/main/%E5%B0%8F%E8%8F%9C%E9%B8%A1picture/3.png)

## 关于Docker

#Docker是一个开源的容器化平台，通过创建容器打包依赖项，确保代码能在任何开发环境中一致的运行。

除了Docker还有Podman等容器化平台，有兴趣可查看下表

![image-20241208100254159](https://github.com/cat418/wrong/blob/main/%E5%B0%8F%E8%8F%9C%E9%B8%A1picture/2.png)

## 关于Dckerfile



## 关于内存和存储空间的区别

![区别](https://github.com/cat418/wrong/blob/main/%E5%B0%8F%E8%8F%9C%E9%B8%A1picture/1.png)

## 关于生命周期问题

刚入队时，学长总提醒我们代码编写要考虑到生命周期的问题，所以生命周期到底是什么呢？ 🤔

#代码的生命周期是从代码创建到最终退役的完整过程。

![作用](https://github.com/cat418/wrong/blob/main/%E5%B0%8F%E8%8F%9C%E9%B8%A1picture/4.png)

## 关于ROS

[学习网站](https://docs.ros.org/en/jazzy/Installation.html)

#在 ROS（Robot Operating System）中，`package.xml` 是描述软件包（package）元数据的配置文件。每个 ROS 软件包都有一个 `package.xml` 文件，用于定义该软件包的基本信息、依赖关系和其他元数据。

`package.xml` 是 ROS 软件包的重要组成部分，CMake 和 ROS 工具在编译和运行时都会参考这个文件。

#**定义软件包信息**：
包括软件包的名称、版本、描述、维护者信息等。

**声明依赖关系**：
明确该软件包依赖于哪些其他 ROS 软件包或系统库。

**提供工具支持**：
用于 `rosdep` 工具进行依赖管理，自动安装依赖。

**方便软件包的发现**：
其他用户或 ROS 工具可以通过 `package.xml` 确定一个软件包的功能或依赖信息。

## 关于linux指令

``` c++
ls -a //列出所有文件，包括隐藏文件
```

## 关于 #include <eigen3/Eigen/Core>

Eigen是一个有效支持线性代数，矩阵和矢量运算，数值分析及其相关的算法的C ++开源库.

### 矩阵和向量的定义

``` c++
#include <eigen3/Eigen/Core>
#include <iostream>

int main() {
    // 定义一个固定大小的 3x3 矩阵
    Eigen::Matrix3d mat; // 相当于 Eigen::Matrix<double, 3, 3>
    mat << 1, 2, 3,
           4, 5, 6,
           7, 8, 9;

    // 输出矩阵
    std::cout << "Matrix:\n" << mat << std::endl;
    return 0;
}
```

#### 1.动态大小矩阵

``` c++
#include <eigen3/Eigen/Core>
#include <iostream>

int main() {
    // 动态大小矩阵
    Eigen::MatrixXd mat(2, 3); // 2 行 3 列
    mat << 1, 2, 3,
           4, 5, 6;

    std::cout << "Dynamic Matrix:\n" << mat << std::endl;
    return 0;
}
```

#### 2.向量定义

``` c++
#include <eigen3/Eigen/Core>
#include <iostream>

int main() {
    // 静态大小向量
    Eigen::Vector3d vec(1, 2, 3); // 3 维向量

    // 动态大小向量
    Eigen::VectorXd dynamic_vec(4);
    dynamic_vec << 1, 2, 3, 4;

    std::cout << "Static Vector:\n" << vec << std::endl;
    std::cout << "Dynamic Vector:\n" << dynamic_vec << std::endl;
    return 0;
}
```

想详细了解请参考这个文档：

[Eigen库的学习](https://blog.csdn.net/m0_63111108/article/details/124949608)



## 关于相机的畸变系数矩阵

#可以用Mat或者vector<double>表示.

但是后者更加灵活，如下对比：

``` c++
cv::Mat distCoeffs = (cv::Mat_<double>(1, 5) << k1, k2, p1, p2, k3);
std::vector<double> distCoeffs = {k1, k2, p1, p2, k3};
```

二者的相互转换：

``` c++
std::vector<double> distVec;
distCoeffs.copyTo(distVec); // distCoeffs 是 cv::Mat 类型
cv::Mat distCoeffs(distVec); // distVec 是 std::vector<double> 类型
```



## 关于相机句柄

#指代一个用于访问和控制相机硬件的对象。通过编程接口与相机设备进行交互的方式。，它可以代表一个打开的相机设备，程序可以通过该句柄来获取相机的数据流、配置设置、获取图像或视频帧。这个句柄通常是一个整数值或对象，程序通过它进行相机的初始化、设置（如分辨率、曝光时间等），以及数据捕捉。如opencv中的VideoCapture返回的对象可以视为相机句柄。

## 关于一些不懂得词

### 1.echo

打印文本或变量的值

### 2.shell

在操作系统中，**Shell** 是用户与操作系统内核之间的接口，主要用来解释用户的命令，并与内核进行交互。它既是一种命令解释器，又是一个强大的脚本编程语言环境。

### 3.欧拉角

1.俯仰角(pitch):绕物体的横向轴（y轴）旋转的角度。

2.偏航角(Yaw):绕物体的垂直轴(z轴)旋转的角度。

3.滚转角(Roll):绕物体的纵向轴(x轴)旋转的角度。

缺点："万向锁"当俯仰角接近+-90度时，旋转轴的自由度减少，导致欧拉角无法唯一描述旋转.

### 4.四元数

