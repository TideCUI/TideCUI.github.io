---
title: post
date: 2022-07-16 13:58:56
tags: hexo-博客备份
categories: hexo
---

# hexo 运行流程梳理

```java
hexo clean  #删除缓冲文件(db.json)和(public中的)已生成的静态文件
hexo g      #读取配置文件，根据主题配置，将md解析成HTML，将source里的文件转换到public文件夹
hexo s 		#将静态文件部署到本地，预览
hexo d 		#清理.deploy_git文件夹，将public复制到.deploy_git,发布到github
```

![流程图](../../../Study/Typora/pic/Hexo flowing pic.jpg)

# 备份原理

在github上再创建一个branch用于存放本地的源代码，取名为Blog,区别于之前创建的master分支，我们通过hexo操作三连将本地源代码部署到了master分支，通过git操作三连绕开hexo，将源代码直接push到远程仓库blog分支，实现备份

# blog备份

之前不太重视，然后换个电脑之后发现以前写的博客全都没了，原以为可以再通过git克隆到本地的，细究才发现，下回来的也只有静态文件，md和一些配置全都无了:sob: ,因此hexo 只支持push上传，无法下载源代码，**备份非常重要**

![image-20220716151711107](../../../Study/Typora/pic/image-20220716151711107.png)

# 备份过程：

1. 在`blog/source/`根目录下创建一个`README.md` 文件，方便github上阅览

   为防止被`hexo g` 渲染成html格式，需要加一个跳过渲染的指令，打开根目录下的`_config.yml` ,添加指令

   ```C
   skip_render: - ‘README.md’
   ```

   如下

   ![image-20220716161721306](../../../Study/Typora/pic/image-20220716161721306.png)

2. 修改根目录下的`.gitignore`，.gitignore的原内容：

   ![image-20220716171312582](../../../Study/Typora/pic/image-20220716171312582.png)

   在后面增加

   ```C
   #ignored useless themes
   /themes/landscape/
   ```

   用来忽略原先的主题文件

   3. 创建blog分支

      ```c
      git add .
      git commit -m "init the blog"
      git branch blog
      git checkout blog
      git push origin blog
      ```

   4. github 上把blog分支设为默认分支，这样我们以后可以直接下载源代码

![image-20220716155635023](../../../Study/Typora/pic/image-20220716155635023.png)

# 写博客及备份指令

```c
#Writing
# 同步到master分支
hexo clean
hexo generate
hexo deploy

# 手动同步到blog分支上
git add. 
git commit -m "提交信息"
git push origin blog #如果设置了blog为默认分支，可以直接git push
```
