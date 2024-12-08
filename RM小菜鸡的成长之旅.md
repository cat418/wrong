# RM小菜鸡的成长之旅

## 关于.gitnore

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



![image-20241208101222218](/home/xzq/.config/Typora/typora-user-images/image-20241208101222218.png)

![image-20241208100603516](/home/xzq/.config/Typora/typora-user-images/image-20241208100603516.png)

## 关于Docker

#Docker是一个开源的容器化平台，通过创建容器打包依赖项，确保代码能在任何开发环境中一致的运行。

除了Docker还有Podman等容器化平台，有兴趣可查看下表

![image-20241208100254159](/home/xzq/.config/Typora/typora-user-images/image-20241208100254159.png)

## 关于Dckerfile

## 关于内存和存储空间的区别

![image-20241208102344293](/home/xzq/.config/Typora/typora-user-images/image-20241208102344293.png)

## 关于生命周期问题

刚入队时，学长总提醒我们代码编写要考虑到生命周期的问题，所以生命周期到底是什么呢？ 🤔

#代码的生命周期是从代码创建到最终退役的完整过程。

![image-20241208103203544](/home/xzq/.config/Typora/typora-user-images/image-20241208103203544.png)