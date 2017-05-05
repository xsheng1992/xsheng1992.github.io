---
layout: post
title:  "vue-router改变路由时获取路由路径"
date:   2017-05-05 11:45:52
categories: vue vue-router
---
之前写仿qq的页面时遇到过一个问题：导航条在鼠标移上去时变颜色，其他时候相应的栏目变颜色：

![导航条][img1]

[img1]: http://olr7t6rk5.bkt.clouddn.com/2017/05/vue-router-get-path/20170505101523.png

鼠标移上去时绑定mouseenter,mouseleave事件就行了，但是让相应栏目背景变颜色就需要获取到当前的路由地址了。

#### 先说created和mounted

creatd是vue 1.0 的钩子函数，只要是在组件被创建后进行的操作。而在2.0中，created钩子函数被替换为mounted了。

#### 获取路由地址

刚开始我以为要获取页面的路由地址，只要设定一个变量，然后获取当前地址就行了，然后我也这么做了，但是结果获取到的永远是根路由 `'/'`。

我是用window.location.pathname来获取地址的，但是我用的vue-router使用的是hash模式，加在地址后面的是hash，所以获取到的一直都是 `'/'`（其实这里通过获取hash也行）。不过，就算在mounted钩子函数中获取也不行，因为只会获取一次，所以需要监听。

#### 监听路由地址变动

vue中，路由对象会注入每一个组件，通过访问`$route`就能获取到路由信息，所以只用在watch中监听`$route`，监听到变动后再执行一个数据处理的函数就行了。

路径可以通过`this.$route.path`来获取，所以代码如下：

{% highlight ruby %}
methods: {
  fetchdata(str) {
    //do something
  }
},
watch: {
  '$route'(to, from) {
    this.fetchdata(this.$route.path)
  }
}
{% endhighlight %}

然后通过判断子项目指向的路由地址是否是当前路由地址来使导航条项目的背景变色了。


