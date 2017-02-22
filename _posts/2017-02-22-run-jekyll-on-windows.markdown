---
layout: post
title:  "在Windows平台上安装Jekyll运行环境"
date:   2017-02-22 14:07:46
categories: jekyll run
---
<h1 id="step0">前言</h1>

由于这段时间在研究利用github搭建自己的博客，所以利用到了Jekyll。虽然官方并不建议在Windows上搭建Jekyll环境，不过我目前基本上使用的是Windows平台，所以了解了下在Windows下搭建Jekyll运行环境的过程。  

本文内容来自<http://jekyll-windows.juthilo.com>.  

过程可分为以下5步：  

[1.  安装Ruby](#step1)  
[2.  安装Jekyll](#step2)  
[3.  代码高亮](#step3)  
[4.  开启监听](#step4)  
[5.  运行](#step5)  

-------------------------------

<h1 id="step1">1. 安装Ruby</h1>

我们得安装Ruby和Ruby Devkit。

### 安装Ruby

你可以点击下面链接，根据你自己的系统来获取32位或64位的Ruby安装包。

<a href="http://rubyinstaller.org/downloads" target="_blank">点击获取Ruby安装包</a>

下载完成后执行安装程序，当进行到下图的步骤时，一定要记住**勾上“Add Ruby executables to your PATH”**。

![Ruby安装界面][img1]

[img1]: http://olr7t6rk5.bkt.clouddn.com/2017/02/run-jekyll-on-windows/20170222094218.png

### 安装Ruby DevKit

还是在刚才的页面，点击下载符合你系统要求的Ruby DevKit安装包。

<a href="http://rubyinstaller.org/downloads" target="_blank">点击获取Ruby DevKit安装包</a>

下载下来的安装包是一个压缩文件，点击运行会让你输入解压路径，路径可以自己随便选，我将它解压到了`C:\RubyDevKit\`。

之后打开命令行（按win+R打开“运行”，输入cmd，点击确定），进入解压的文件夹  

{% highlight ruby %}
cd C:\RubyDevKit
{% endhighlight %}

运行下面命令（上一行执行完后执行下一条）

{% highlight ruby %}
ruby dk.rb init

ruby dk.rb install
{% endhighlight %}

这样Ruby就算安装完成了。

-------------------------------

<h1 id="step2">2. 安装Jekyll</h1>

在命令行中运行下面代码

{% highlight ruby %}
gem install jekyll
{% endhighlight %}

-------------------------------

<h1 id="step3">3. 代码高亮</h1>

### 安装Rouge

首先安装Rouge，在命令行中输入：

{% highlight ruby %}
gem install rouge
{% endhighlight %}

然后，在你的`_config.yml`中，将你的代码高亮设置为rouge

{% highlight ruby %}
highlighter: rouge
{% endhighlight %}

完成！

### 使用Pygments

如果你想用Pygments来使代码高亮，你必须安装Python和pip。

### 安装Python

注意请安装Python2的版本，不要安装Python3的版本，点击下面链接可以获取Python安装包：

<a href="https://www.python.org/downloads" target="_blank">点击获取Python安装包</a>

之后安装，**注意勾选“Add python.exe to Path.”**

![Python安装界面][img2]

[img2]: http://olr7t6rk5.bkt.clouddn.com/2017/02/run-jekyll-on-windows/20170222105648.png

### 安装pip

pip对Pythone来说相当于Ruby的gem，点击下面链接，在页面中找到`get-pip.py`，点击并下载

<a href="https://pip.pypa.io/en/latest/installing" target="_blank">点击获取pip</a>

在终端中进入`get-pip.py`文件所在的文件夹（如`C:\pip`，或其他你所保存的文件夹），并执行：

{% highlight ruby %}
cd C:\pip

python get-pip.py
{% endhighlight %}

（我在下载完`get-pip.py`文件后它自己自动执行了，那么上面这步就可以省略了。）

在终端中继续输入：

{% highlight ruby %}
python -m pip install Pygments
{% endhighlight %}

如果要使用Pygments来使你的代码高亮，需要在你的`_config.yml`中，将你的代码高亮设置为pygments

{% highlight ruby %}
highlighter: pygments
{% endhighlight %}

-------------------------------

<h1 id="step4">4. 开启监听</h1>

jekyll有个内置的自动重生成功能，它会实时监测你的源码文件夹，如果有文件进行了改动，它就会自动重新build，从Jekyll v2.4.0开始，执行`jekyll serve`命令时默认关闭这个功能，你可以手动执行`jekyll serve --watch`来开启。

### 安装wdm Gem

在终端输入：

{% highlight ruby %}
gem install wdm
{% endhighlight %}

-------------------------------

<h1 id="step5">5. 运行</h1>

为确保jekyll可以正确读取utf-8编码的网站，你需要将jekyll的编码模式设置为utf-8。可以在`_config.yml`中设置：

{% highlight ruby %}
encoding: utf-8
{% endhighlight %}

或者，你可以将终端的编码改成utf-8，但是这需要你在每次打开新的终端时都设置一次。设置方法：

{% highlight ruby %}
chcp 65001
{% endhighlight %}

现在，你可以运行jekyll了，利用终端进入你网站的目录，运行`jekyll serve`。在你的Windows上，你可以运行以下命令了：

{% highlight ruby %}
jekyll build
jekyll build --watch
jekyll build --w
jekyll serve
jekyll serve --watch
jekyll serve --w
{% endhighlight %}

要查看更多Jekyll信息，可以访问官方网站：

[Jekyll中文文档][1]

[1]: http://jekyll.com.cn/