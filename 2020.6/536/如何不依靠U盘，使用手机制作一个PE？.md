# 如何不依靠U盘，使用手机制作一个PE？

## 前言

作为朋友圈里的（伪）搞机大佬，会利用PE装机绝对可以把小白唬住；生活在信息时代的我们，我们却不一定时常带着U盘，但手机绝对不可能落下，如果可以仅靠手机制作一个PE，岂不是妙哉！

![](https://cdn.jsdelivr.net/gh/youzhiran/ImgData/2020.6/536/2.jpg)

本文就将介绍利用 DriveDroid 在手机里创建一个虚拟U盘并使用微pe进行装机。

[scode type="yellow"]阅读本文需要您会进入BIOS设置启动项，且DriveDroid 需要root权限，请确认您知道这是什么，并具有在电脑/手机无法启动时，恢复正常的能力[/scode]



## 初次设置

### 下载

前往谷歌play商店下载 DriveDroid ，不方便访问谷歌的同学，也可关注微信公众号**技术宅小哥哥**，回复536，即可获取 DriveDroid 0.10.50版。

### 获取 root 权限

打开 DriveDroid ，首先迎接我们的是设置向导，第一步是授予root权限，按要求授予即可。成功获取root，即会提示 **Root acquired**（已获取root权限）。

![](https://cdn.jsdelivr.net/gh/youzhiran/ImgData/2020.6/536/111.png)



###  设置镜像储存路径

这一步可以选择镜像文件的储存路径，默认的路径是download，这里可能需要点击 **允许访问‘下载内容’** ，不同手机显示的界面不同，以自己显示的界面为准。当然也可以设置一个专用目录，便于区分，这里设置错误也没关系，后期可以在设置中修改。

![](https://cdn.jsdelivr.net/gh/youzhiran/ImgData/2020.6/536/222.png)



### 检测 USB 系统

当向导进行到**Plug-in USB cable**这一步时，你需要使用数据线将手机与电脑连接起来，当 DriveDroid 中的 usb 图标没有被划去，显示为图片中形状时即为连接成功，便可以点击 next 进行下一步。

不同设备调用的 usb 连接机制不同，Drivedroid 支持多种连接方式，我们在 **USB System** 这一步中选择一个可以用的即可。

Drivedroid 使用即大容量存储模式加载镜像，使你的安卓设备以USB或者CD-ROM方式显示出来，在**USB Mass Storage** 步骤下，可以确认手机是否可以正常加载镜像。

该步骤两个选项为：

- 安卓设备在系统中正常显示

- 没有设备正在显示

如果电脑没有显示，可能是此USB系统方式不兼容你的手机，我们可以点击 **CHOOSE A DIFFERENT USB SYSTEM** 选择其他USB系统进行测试。

![](https://cdn.jsdelivr.net/gh/youzhiran/ImgData/2020.6/536/1595213409663.png)



### Boot 启动测试

翻译：重启电脑，在BIOS（固件）里设置你的安卓设备作为启动设备。

- 使用 Drivedroid 成功启动
- 启动选项中未显示这个安卓设备
- 启动到了原系统，而不是 Drivedroid
- 不知道该怎么办

<img src="https://cdn.jsdelivr.net/gh/youzhiran/ImgData/2020.6/536/image-20200720112434989.png" alt="" style="zoom: 30%;" />

重启电脑后显示 **DriveDroid booted succesfully!** ，即如下界面即为成功。

![](https://cdn.jsdelivr.net/gh/youzhiran/ImgData/2020.6/536/image-20200720093643649.png)



## 制作空白镜像

完成向导，进入 DriveDroid ，点击`右下角的加号`——`Create blank image...`——设置文件名和大小——选择刚刚创建的`空白镜像`——`Writable USB on Mass Storage 1`

[scode type="blue"]镜像大小按需设置即可；

第3张图中3个选项分别为：只读储存、读写储存、CD-ROM[/scode]

![](https://cdn.jsdelivr.net/gh/youzhiran/ImgData/2020.6\536\0.png)



此时，我们的电脑中即会出现一个U盘图标，可能Windows会提示格式化，如果直接格式化就可以当作一个U盘使用。我们接下来制作pe时会自动格式化，这里就不作格式化了。

![](https://cdn.jsdelivr.net/gh/youzhiran/ImgData/2020.6/536/image-20200720120805762.png)



## 安装微PE到空白镜像

这一步的操作和正常使用U盘安装微pe一致，前往微pe官网 http://www.wepe.com.cn/download.html 下载安装即可

1.选择右下角的安装微pe到U盘

![image-20200720122204989](https://cdn.jsdelivr.net/gh/youzhiran/ImgData/2020.6/536/image-20200720122204989.png)



2.确认**选择的U盘是我们之前制作的空白镜像**，文件系统推荐NTFS，点击`立即安装进U盘`即可

![](https://cdn.jsdelivr.net/gh/youzhiran/ImgData/2020.6/536/image-20200720123412285.png)



3.不要触碰数据线，易断开连接，等待安装完毕，提示完成即可

若长时间无反应，请确认数据线连接正常

![](https://cdn.jsdelivr.net/gh/youzhiran/ImgData/2020.6/536/image-20200720122946443.png)



4.成功进入微pe，若提示加载失败可能由于制作过程中数据线松动，请重新制作

![](https://cdn.jsdelivr.net/gh/youzhiran/ImgData/2020.6/536/image-20200720131017358.png)