## 前言

日常使用typecho过程中，有时会遇到更换图片链接，替换文本等操作，本文将以为jsdelivr链接添加@master文本为例子，简单学习记录sql操作。

想要系统学习SQL教程也可访问廖老师的官方教程：https://www.liaoxuefeng.com/wiki/1177760294764384



## 备份

操作数据库前请先备份数据库，防止误删重要数据，删库跑路的事情可千万不能发生在我们身上。一般想宝塔这些面板、PhpMyAdmin都会提供数据库备份功能，按要求操作即可。

![](https://cdn.jsdelivr.net/gh/youzhiran/ImgData@master/2021.1/549/1.jpg)



## 搜索并选择

这里我用的数据库管理程序是PhpMyAdmin，打开typecho对应的数据库，打开`typecho_contents`表，可以看到我们写的文章正是在`text`列中，而我们此次操作的目的就是在`youzhiran/ImgData/`后添加`@master`。![](https://cdn.jsdelivr.net/gh/youzhiran/ImgData@master/2021.1/549/image-20210303103520322.png)



数据库操作基本就是cdru，也就是增删改查。我们首先使用`SELECT`语句，查询出需要的数据：

```SQL
SELECT text
FROM `typecho_contents` 
WHERE type='post' AND text LIKE '%https://cdn.jsdelivr.net/gh/youzhiran/ImgData/%'
```

第一行语句选择了`text`列，第二行语句选择了`typecho_contents`表，第三行语句选择了`type`列中为`post`并且`text`列包含`https://cdn.jsdelivr.net/gh/youzhiran/ImgData/`的数据行。

![](https://cdn.jsdelivr.net/gh/youzhiran/ImgData@master/2021.1/549/image-20210304132547030.png)

这里PhpMyAdmin帮我们自动添加了`LIMIT 25`的语句，进行了分页，可以看到每页结果为25行。



## 替换链接

对之前的`SELECT`语句进行修改，改为`UPDATE`语句进行修改：

```SQL
UPDATE typecho_contents 
SET text = REPLACE(text,'https://cdn.jsdelivr.net/gh/youzhiran/ImgData/','https://cdn.jsdelivr.net/gh/youzhiran/ImgData@master/')
WHERE type='post' AND text LIKE '%https://cdn.jsdelivr.net/gh/youzhiran/ImgData%'
```

第一行语句选择了`typecho_contents`表；第二行语句选择了选择了`text`列并对本文进行替换，具体规则为`update 表名 set 字段 = replace(字段, '要修改的内容' , '修改后的内容')`；第三行语句选择了`type`列中为`post`并且`text`列包含`https://cdn.jsdelivr.net/gh/youzhiran/ImgData/`的数据行。



我们可以先点击`模拟查询`，检测sql语句是否正确，这里显示影响了67行，与之前查询出的行数一致。

![](https://cdn.jsdelivr.net/gh/youzhiran/ImgData@master/2021.1/549/image-20210304133051670.png)



点击`执行`正式修改数据：

![](https://cdn.jsdelivr.net/gh/youzhiran/ImgData@master/2021.1/549/image-20210304133257432.png)



返回网站，刷新页面，可以看到图片链接确实被修改了。至此，修改链接文本工作结束。

![](https://cdn.jsdelivr.net/gh/youzhiran/ImgData@master/2021.1/549/image-20210304133421152.png)



## 总结

```SQL
UPDATE <表名>
SET <列名> = REPLACE(<列名>,'<要被替换的文本>','<新的文本>')
WHERE <一些限制条件>
```

