---
layout: post
title:  "webpack引入velocity时遇到的小问题"
date:   2017-04-18 15:57:00
categories: webpack 插件
---

今天在看vue官方提供的webpack-simple的demo，按照网上的一篇文章想要自己稍微修改下这个demo。实际操作时需要引入velocity来实现一些动画效果，然而利用npm安装了velocity后运行时却一直报错：

{% highlight ruby %}
  Uncaught Error: Cannot find module "fs":
{% endhighlight %}

开始时一直以为是引用的方式错误，于是一直在找webpack引入插件的方法，如：

##### 直接引入

{% highlight ruby %}
  import Velocity from 'velocity'
{% endhighlight %}

这是我最先使用的引用方式，然而并没有用。

##### ProvidePlugin

{% highlight ruby %}
plugins: [
  new webpack.ProvidePlugin({
    velocity: "velocity"
  }),
]
{% endhighlight %}

这是在webpack.config.js文件中添加插件，然而还是没有用处。

##### externals引用

{% highlight ruby %}
externals:{
  'jquery':'window.jQuery'
}
{% endhighlight %}

这也是在webpack.config.js文件中添加插件，结果不用多说还是错的。

正当我对这个世界产生怀疑时，我点开了velocity的官网进入了它的GitHub页面，然后看到了

{% highlight ruby %}
  npm install velocity-animate
{% endhighlight %}

是的，用npm安装时这个插件的名字不是velocity，而是velocity-animate。


velocity-animate

velocity-animate

velocity-animate

我网上查了下，Velocity是一个基于Java的模板引擎...

后来我直接用上面的‘直接引入’方法就成功引入了

{% highlight ruby %}
  import Velocity from 'velocity-animate'

  //或者使用require
  require('velocity-animate')
{% endhighlight %}

至此，还是要多多学习知识啊。