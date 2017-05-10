---
layout: post
title:  "vuex文档中对象展开运算符无法使用问题"
date:   2017-05-10 09:51:14
categories: vue vuex
---
在vuex文档state一节中，mapState可以通过对象展开运算符(...)将state映射到计算属性中，但是实际尝试过之后发现会报错，以下代码：

{% highlight ruby %}
computed: {
	localcomputed(){},
	...mapState({
		//...
	})
}
{% endhighlight %}

报错的原因是...mapState，其实是babel预置的转换器无法转换这个对象展开运算符的原因，所以只要下载转换器插件就行了。

首先，npm安装插件：

{% highlight ruby %}
npm install babel-plugin-transform-object-rest-spread
{% endhighlight %}

然后在babel的配置文件.babelrc中应用插件：

{% highlight ruby %}
{
  "presets": [
    ["latest", {
      "es2015": { "modules": false }
    }]
  ],
  "plugins": ["transform-object-rest-spread"]
}
{% endhighlight %}

这样就可以了，不过要记住重启webpack。

参考来源：[https://blog.daraw.cn/2016/09/22/vuex2-problems-with-mapgetter/?utm_source=tuicool&utm_medium=referral][1]

[1]: https://blog.daraw.cn/2016/09/22/vuex2-problems-with-mapgetter/?utm_source=tuicool&utm_medium=referral

