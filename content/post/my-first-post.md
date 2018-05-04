---
title: "0基础搭建Hugo个人blog"
date: 2018-04-27T17:47:23+08:00
draft: false
---

0基础搭建Hugo个人blog
====================
以64位Windows系统为例
---------------------

用hugo搭建个人blog需要GitHub账号，一台能够科学上网的电脑并安装Git，GitHub Desktop和VS Code。
### 准备工作
* 在[GitHub网站](https://github.com)申请账号，后续我们使用GitHub为我们免费提供的网址__xxxx.github.io__为blog地址（**xxxx为你的用户名**）。
* [廖雪峰的安装git教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
不需要看太多文字介绍，我们只需要看安装Git部分即可。以下是Windows版介绍：
 在[Git官网](https://git-scm.com/downloads)下载Windows版，安装时点选**默认选项**即可。安装完成后在开始菜单找到Git并打开Git Bash，在弹出的命令行窗口中输入:
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
* 下载[GitHub Desktop](https://desktop.github.com/)安装程序，**安装过程无选项**，只需要在装好后选择登入GitHub账号即可。
* 下载[VS Code](https://code.visualstudio.com/)安装程序，安装时点选**默认选项**即可。
### 在本地搭建Hugo网站
* 在[hugo下载地址](https://github.com/gohugoio/hugo/releases)找到**hugo_0.40.1_Windows-64bit.zip**文件点击下载，在此过程中可以打开Windows Explorer，找到D盘，创建一个新的文件夹叫做Hugo，打开Hugo文件夹，在里面创建两个新的文件夹分别叫做**bin**和**Sites**。将下载好的zip文件放进bin文件夹中，并解压到当前文件夹。**确保hugo.exe直接放在D:/Hugo/bin中**。
* **设置环境变量**。控制面板→系统→高级系统设置→环境变量→新建（系统变量）：
> 变量名：**PATH** 
> 
> 变量值：**D:\Hugo\bin>set PATH=%PATH%;D:\Hugo\bin**

详解：在开始中找到Cortana（小娜），输入控制面板，打开后找到**系统**。选择系统窗口左侧的**高级系统设置**，点开**环境变量**窗口，找到环境变量下的**新建**按钮，在弹出窗口中输入变量名：**PATH** 变量值：**D:\Hugo\bin>set PATH=%PATH%;D:\Hugo\bin**。一路选择确认键退出所有窗口即可。
* 在开始中找到Cortana（小娜），输入**CMD**打开命令提示符输入`hugo help`并按Enter键。可以看到窗口显示**A Fast and Flexible Static Site Generator built with love by  spf13 and friends in Go.** 这代表hugo已经安装完成了。在窗口继续输入:
```
C:\Program Files> cd D:\Hugo\Sites
C:\Program Files> D:
D:\Hugo\Sites>
``` 
进入sites文件夹中，此时我们需要创建一个新的网站名作为blog的名称。例如`xxxx.github.io`，继续在窗口输入：
```
D:\Hugo\Sites> hugo new site xxxx.github.io
D:\Hugo\Sites>cd xxxx.github.io
D:\Hugo\Sites\xxxx.github.io>dir
``` 
确认是否创建成功，如果出现`Directory of D:\hugo\sites\xxxx.github.io`即表示成功。
* 选择主题。在[hugo主题库](https://themes.gohugo.io/)选择主题，点开你喜欢的图片可以选择DEMO预览效果。以[我选择的主题](https://themes.gohugo.io/retrofulhugo/)为例， 滑到网页中间位置看到**Installation**后有介绍在CMD中如何加载你喜欢的主题。打开**命令提示符**窗口。输入：
``` 
D:\Hugo\Sites\xxxx.github.io>cd Themes 
D:\Hugo\Sites\xxx.com\Themes>git init
D:\Hugo\Sites\xxxx.github.io\Themes>git submodule add https://github.com/5armale/retrofulhugo.git themes/retrofulhugo
``` 
需注意一定要末尾加上**themes/xxxx**（xxxx是你想要主题的名字）。
* 打开`D:\Hugo\Sites\xxxx.github.io\themes\retrofulhugo\exampleSite`找到**config.toml**,右键用**VS Code**打开后复制黏贴全部内容到`D:\Hugo\Sites\xxxx.github.io`的**config.toml**里保存退出。
* 打开命令提示符输入：
``` 
D:\Hugo\Sites\xxxx.github.io>hugo new posts my-first-post.md
D:\Hugo\Sites\xxxx.github.io>hugo server -D
``` 
如果出现`Started building sites ...`则说明hugo服务器已经启动，这时用浏览器打开(http://localhost:1313/)看到你设置好的blog中应有一篇文章名为first post，这说明你的blog已经在本地服务器上搭建成功。
### 在GitHub上托管
从这一步开始，hugo给出了几个不同的将个人网站部署为GitHub项目的方法，我们默认采用将网址格式为https://<USERNAME|ORGANIZATION>.github.io/的网站放上GitHub的做法。
* 打开GitHub Desktop，选择**file-add local repository**，点击**choose**找到`D:\Hugo\Sites\xxxx.github.io`后**add repository**，然后跳回主界面选择**commit**，点击**publish branch**上传。
* 选择**file-clone a repository**，files处选择你刚才上传的xxxx.github.io库，local path处在路径名称最后添加`-hugo`，选择**clone**。
* 点开主界面上的**current repository**
可以看到下方显示了两个库，选择第二个`xxxx.github.io`，然后选择主界面中的**current branch**，点击**New branch**，将新分支命名为hugo，然后选择**publish branch**，上传新分支。
* 点开主界面上的**current repository**，选择第一个`xxxx.github.io`，右键找到**show in explorer**， 删掉里面.git文件之外全部文件，然后回到GitHub Desktop中**commit**再**publish branch**上传。
* 打开命令提示符，输入：
```
D:\Hugo\Sites\xxxx.github.io-hugo>hugo
```
然后Windows Explorer进入`D:\Hugo\Sites\xxxx.github.io-hugo\public`文件夹，将public文件夹中全部文件剪切到`D:\Hugo\Sites\xxxx.github.io`文件夹中，回到GitHub desktop中**commit**再**publish branch**上传。稍等片刻就可以进入xxxx.github.io看到你的blog了。