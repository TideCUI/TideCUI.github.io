---
title: win11系统下用hexo搭建个人Blog
date: 2022-07-13 00:47:54
tags: hexo配置部署
categories: hexo
---


# 配置环境

本博客搭建于`win11`系统下

<!--more-->

# 准备工作

## node.js 下载

* 下载地址: <https://nodejs.org/en/>

* 安装步骤: 正常安装即可，最后几步有类似全家桶软件如`vscode,python`等，确保取消勾选

  > 我使用的是`node.js v18.5.0`版本

## git 下载

* 下载地址: <https://git-scm.com/download/win>

* 安装步骤: 正常操作，无坑

  > 我使用的是`git 2.37.1`版本

## github 账号创建

* 网站网址: <https://github.com/>
* 注意: 牢记邮箱，密码和**用户名**，尤其是username， 这个涉及到后面个人博客网址，最好可识别度高，方便，像我由原来的`Tide-C`替换成`TideCUI`这个社交统一用户名了，不然我老是搞混

# 搭建Hexo框架

## 提醒

* 听说用win自带的cmd命令行会出现某些不知名问题，所以我推荐用<u>git bash</u>

* 在本地新建一个为以后写博客而预留的文件夹，最好打开路径方便，新建后打开此空文件夹(全是空白)，右键点击 `git bash here`开始进入命令行程序
* 提前验证一下**node.js**和其中**npm**模块是否正常，分别键入`node -v`和`npm -v`，效果图如下:![image-20220714010827653](D:\Study\Typora\pic\image-20220714010827653.png)

## Hexo 简介

Hexo是一个简单、快速、强大的基于Github Pages 的博客发布工具，支持Markdown格式，有众多优秀插件和主题，后续我会对自己的博客进行优化，敬请期待。

## Hexo 原理

由于github  pages存放的都是静态文件，博客存放的不只是文章内容，还有文章列表、分类、标签、翻页等动态内容，假如每次写完一篇文章都要手动更新博文目录和相关链接信息，相信谁都会疯掉，所以hexo所做的就是将这些md文件都放在本地，每次写完文章后调用写好的命令来批量完成相关页面的生成，然后再将有改动的页面提交到github。

## 命令行安装cnpm

键入`npm install -g cnpm --registry=https://registry.npm.taobao.org`，后键入`cnpm -v`验证是否成功，效果图如下：

![image-20220714011903129](D:\Study\Typora\pic\image-20220714011903129.png)

【注释】使用阿里系（淘宝）镜像源会比较快

## 命令行安装hexo

键入`cnpm install -g hexo-cli`，再键入`hexo -v`验证安装是否成功，效果图如下：![image-20220714012851669](D:\Study\Typora\pic\image-20220714012851669.png)

后键入`pwd`(即print working directory),必须确认一下当前位置，否则必**报错**

![image-20220714013410967](D:\Study\Typora\pic\image-20220714013410967.png)

最后键入`hexo init `初始化hexo

![image-20220714013533625](D:\Study\Typora\pic\image-20220714013533625.png)

## 运行测试

键入`hexo s #开启本地预览服务`,看箭头所指，打开浏览器，输入下划线网址`https://localhost:4000/`![image-20220714014736676](D:\Study\Typora\pic\image-20220714014736676.png)

即可看到我们搭建成功的效果，这是hexo 初始化为我们自动生成的第一篇博客

![image-20220714014942564](D:\Study\Typora\pic\image-20220714014942564.png)

# 部署至github

## 创建github仓库（repository）

github给每个人均提供有且仅有一个的个人**ID.github.io** 的仓库名称，图中我就不能再命名一个相同的了，这就确保我们之后的个人博客网址具有唯一性 ![image-20220714015944361](D:\Study\Typora\pic\image-20220714015944361.png)

## SSH免密登录配置

为了拥有GitHub权限，我们需要在本地与其服务器之间建立连接，我没在本地下载github软件，用账号密码登录不太安全，而选择使用SSH免密登录。

键入`cd ~/.ssh` 【注】检查本机已有的ssh文件，如果提示 

> **no such file or directory**,则说明你是第一次使用git

键入`ssh-keygen -t rsa -C "自己的邮箱地址"` 然后连续3次**回车**，最终会生成一个文件在用户目录下，打开用户目录，找到`.ssh\id_rsa.pub`文件，记事本打开并复制里面的内容，打开你的github主页，进入个人设置 -> SSH and GPG keys -> New SSH key：![image-20220714174215930](D:\Study\Typora\pic\image-20220714174215930.png)

将复制内容粘贴至key即可。

> 这部分很关键，我第一次部署的时候一直卡在这里，就是没有使用SSH将本地端口连接到服务器上，具体报错情况为 ***fatal: Could not read from remote repository.  Please make sure you have the correct access rights***，引以为戒。

### 配置测试

键入`ssh -T "自己邮箱地址"` ，如果提示`Are you sure you want to continue connecting(yes/no)` 

键入`yes` ， 然后你会看到

> Hi,XXX! You’ve successfully authenticated,but github does not provide shell access.

看到这个信息说明SSH配置成功。 

最后为便于管理github,我们也将git管理软件进行登录

键入`git config --global user.email "自己邮箱地址"`

​		`git config --global user.name "github用户名" `  完成绑定

## 将第一篇博客部署至github

下面我们将第一篇 **Hello World**博客上传至github,分为两步：

1. 修改源目录下的`_config.yml`文件![image-20220714184102376](D:\Study\Typora\pic\image-20220714184102376.png)点开它，用sublime text 对其部分内容进行编写，找到如下部分![image-20220714184231141](D:\Study\Typora\pic\image-20220714184231141.png)

   编写完成后如下![image-20220714184651155](D:\Study\Typora\pic\image-20220714184651155.png)
   红线部分内容为自己初创的github仓库SSH地址，寻找方法为在github上点开自己的repository,点击SSH，再点右边复制图标即可，![image-20220714185131036](D:\Study\Typora\pic\image-20220714185131036.png)

2.键入`cnpm install hexo-deployer-git --save`,【注】这步是安装hexo的某个插件

否则会报错如下：

```yaml
Deployer not found: github 或者 Deployer not found: git
```

3.键入`hexo g`

4.最后一步键入`hexo d` 上传文件至github，大功告成！![image-20220714190932760](D:\Study\Typora\pic\image-20220714190932760.png)

# Hexo 博客写作流程

## hexo 常用命令

```c#
hexo new "postName" #新建文章
hexo new page "pageName" #新建页面
hexo generate #生成静态页面至public目录
hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
hexo deploy #部署到GitHub
hexo help  # 查看帮助
hexo version  #查看Hexo的版本
```

缩写

```c#
hexo n == hexo new
hexo g == hexo generate
hexo s == hexo server
hexo d == hexo deploy
```

组合

```c#
hexo s -g #生成并本地预览
hexo d -g #生成并上传
```

## 流程

1. 找到专门写作blog的文件夹，键入`hexo new "Blog_Title"` 
2. 在==source/_post/==路径下找到刚才创建的md文件，用markdown写作工具打开开始写博客
3. 完事后键入`hexo g`
4. 最后键入`hexo d`完成上传

这样==XXX.github.io==就成为我们的专属博客网站了