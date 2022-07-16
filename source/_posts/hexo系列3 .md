---
title: post
date: 2022-07-16 13:58:56
tags: hexo-博客备份
categories： hexo
---

# hexo 运行流程梳理

```java
hexo clean  #删除缓冲文件(db.json)和(public中的)已生成的静态文件
hexo g      #读取配置文件，根据主题配置，将md解析成HTML，将source里的文件转换到public文件夹
hexo s 		#将静态文件部署到本地，预览
hexo d 		#清理.deploy_git文件夹，将public复制到.deploy_git,发布到github
```

![流程图](../../../Study/Typora/pic/Hexo flowing pic.jpg)

# blog备份

之前不太重视，然后换个电脑之后发现以前写的博客全都没了，原以为可以再通过git克隆到本地的，细究才发现，下回来的也只有静态文件，md和一些配置全都无了:sob: ,因此hexo 只支持push上传，无法下载源代码，**备份非常重要**

![image-20220716151711107](../../../Study/Typora/pic/image-20220716151711107.png)

以下是备份方式：

1. 
