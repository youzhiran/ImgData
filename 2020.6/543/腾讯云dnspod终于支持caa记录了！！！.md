##  前言

在腾讯云或者dnspod购买过域名的同学，在**想要自动化续期泛域名ssl证书的时候肯定遇到过无法设置caa记录的问题，导致自动化续期工具无法续期**。最近，网站的证书又快要到期了，我再次打开了腾讯云发现依旧没有caa记录设置，很是失望，毕竟17年就说要加的功能到现在也没加进去。

无奈，不想每次手动续期的我，继续百度解决方法，柳暗花明又一村，看到一条不起眼的评论说：在dnspod里可以添加caa记录，我赶紧打开dnspod，的确，添加caa记录功能就在那里。

![](https://cdn.jsdelivr.net/gh/youzhiran/ImgData/2020.6\543\1.png)

接下来，本文就将介绍使用宝塔自动化计划任务申请Let's Encrypt泛域名证书。



## 腾讯云与dnspod

DNSPod建立于2006年3月份，2011年8月8日，DNSPod被腾讯收购



## CAA记录是什么？

[scode type="share"]CAA，全称Certificate Authority Authorization，即证书颁发机构授权。它为了改善PKI(Public Key Infrastructure：公钥基础设施)生态系统强度、减少证书意外错误发布的风险，通过DNS机制创建CAA资源记录，从而限定了特定域名颁发的证书和CA(证书颁发机构)之间的联系。从此，再也不能是任意CA都可以为任意域名颁发证书了。[/scode]



## 使用宝塔自动续期泛域名证书

###  申请Let's Encrypt泛域名证书

1.在宝塔网站界面点击所需要添加泛域名证书的网站

![](https://cdn.jsdelivr.net/gh/youzhiran/ImgData/2020.6\543\image-20200918115805066.png)



2.在弹出的界面点击`SSL`——`Let's Encrypt`——`DNS验证(支持通配符)`——勾选`自动组合泛域名`和你的域名

![](https://cdn.jsdelivr.net/gh/youzhiran/ImgData/2020.6\543\image-20200918115955506.png)



3.点击`设置`，按照说明设置`API Token`。

![](https://cdn.jsdelivr.net/gh/youzhiran/ImgData/2020.6\543\image-20200918120302285.png)

具体方法可登陆dnspod，按照下图设置；也可直接访问 https://console.dnspod.cn/account/token 进行设置

![](https://cdn.jsdelivr.net/gh/youzhiran/ImgData/2020.6\543\image-20200918120542474.png)



4.添加完毕以后，回到宝塔面板，点击`申请`即可，稍等片刻提示成功即可。



5.若提示**当前被要求验证CAA记录**，这里我建议等待1小时后再试。

![](https://cdn.jsdelivr.net/gh/youzhiran/ImgData/2020.6\543\image-20200918121936682.png)



### 使用计划任务自动续期证书

1.如果你之前操作没有问题的话，宝塔这里应该已经自己添加了计划任务。

![](https://cdn.jsdelivr.net/gh/youzhiran/ImgData/2020.6\543\image-20200919091553118.png)



2.点击`执行`可以手动执行一次，点击`日志`可以查看运行情况；若之前的操作没有什么问题，证书将在距离到期时间1个月内尝试自动续签。