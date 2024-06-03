---
title:  Hexo+Github搭建博客
categories: 
- 博客搭建
description:  零基础小白搭建使用Github Pages托管的hexo
cover: https://s2.loli.net/2024/04/29/kzFnAC7tamuhL4e.png
tags:
- blog
- hexo
---


## 一、环境搭建

### 1、安装Node.js

​		安装对应系统和版本的node.js：https://nodejs.cn/download/

​		如果有node版本切换的需求建设使用nvm进行安装。

### 2、安装git

​		安装对应系统版本的git：https://git-scm.com/download/win

​		使用默认配置进行git安装，安装完成后使用`git --vision`检验是否安装成功，显示git版本号就表示安装成功。

### 3、注册Github

​		注册Github（可能需要魔法上网）：https://github.com/

### 4、安装Hexo

​		新建一个文件夹，用来存放自己的博客文件。



​		在该目录下右键打开`PowerShell`，在面版里输入下面的命令全局安装Hexo，安装完成后，输入`hexo -v`来检验是否安装成功。

```node
	$ npm install -g hexo-cli
```

​		输入`hexo init`对文件夹进行初始化，然后输入`npm i`安装必要组件。



​		完成网站配置后，`hexo g`生成静态网页，然后输入`hexo s`运行本地服务器，在浏览器中打开命令行提示的地址[localhost:4000/](http://localhost:4000/)，就能够看到初始化的博客界面了。

​		

​		按`ctrl+c`关闭本地服务器。



## 二、连接Github

### 1、创建Github Page项目

​		点击主页有侧菜单栏的“New respository”按键，创建新的项目。

<img src="https://s2.loli.net/2024/04/26/zrmkZihs8Pju1CE.jpg" style="zoom: 80%;" />

​		输入自己的项目名字，`<username>.github.io`（后面一定要加`.github.io`后缀），README初始化也要勾上。

<img src="https://s2.loli.net/2024/04/26/7DqFPAdeVpoXW8t.jpg" style="zoom: 50%;" />

​		点击Create repository按钮完成项目的创建。在创建完成的项目界面点击settings：

<img src="https://s2.loli.net/2024/04/26/nCJ7O2wFkZgbVx1.jpg" style="zoom:50%;" />

​		

### 2、设置hexo主题

​		hexo设置了丰富美观的免费主题，在主题库里选择一个自己喜欢的主题：https://hexo.io/themes/

​		我以自己使用的“butterfly”主题为例：

在你的 Hexo 根目录里，在控制台输入命令：

```git
git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
```

修改 Hexo 根目錄下的 _config.yml，把主題改為 butterfly:

```yml
theme: butterfly
```

如果你沒有 pug 以及 stylus 的渲染器，请下載安裝：

```npm
npm install hexo-renderer-pug hexo-renderer-stylus --save
```

依次输入命令行，进行本地预览：

```
hexo clean
```

```
hexo g
```

```
hexo s
```

### 3、上传到github

#### （1）获取id_rsa.pub

​	进入文件夹C:\Users\用户名\\.ssh:

​	会有需要的两个文件：id_rsa（私钥）  id_rsa_pub（公钥）

![](https://s2.loli.net/2024/04/28/o4zOnykjdZUqcf3.jpg)

如果不能打开这个文件夹，则需要重写生成密钥：

```
ssh-keygen -t rsa -C "配置git时的邮箱"
```

-t 指定密钥类型，默认是 rsa ，可以省略。
-C 设置注释文字，比如邮箱。
-f 指定密钥文件存储文件名。

后面的步骤直接按回车。

复制文件“id_rsa.pub”这个文件的所有内容。

#### （2）添加公钥到github

点击右上角头像，点击下拉列表的“setting”，打开设置界面

点击“SSH and GPG keys”，再点击“New SSH key”:

<img src="https://s2.loli.net/2024/04/28/8acgfkAZbyXlJp3.jpg" style="zoom: 50%;" />

在Title里填入备注，用来标注这个”ssh key“是哪个设备的，再把“id_rsa.pub”文件里的内容复制到“key”区域，再点击“Add SSH key”。

<img src="https://s2.loli.net/2024/04/28/Uf3Xh5goParT2md.jpg" style="zoom:67%;" />

在“git bash here”控制面板中输入：

```git
ssh -T git@github.com
```

出现下面的提示表示添加成功：

![](https://s2.loli.net/2024/04/28/w4zJreAZl2YHFfu.jpg)

#### （3）配置config文件

打开博客根目录下的`_config.yml`文件，这是博客的配置文件，在这里你可以修改与博客相关的各种信息。

修改最后一行的配置：

```yml
deploy:
  type: git
  repository: https://github.xxx.github.io
  branch: master
```

repository修改为你自己的github项目地址。

#### （4）发布文章

在博客根目录下右键打开git bash，安装一个扩展：

```npm
npm i hexo-deployer-git
```

然后新建一篇文章,输入:

```npm
hexo new post "article title"
```

在博客根目录下`source/_posts`目录下多了一个文件夹和一个`.md`文件，这就是你的文章文件。

依次输入下面命令发布文章：

```npm
//生成静态网页
hexo g
//本地预览
hexo s
//上传到github，插件冲突使用 hexo deploy
hexo d
```

