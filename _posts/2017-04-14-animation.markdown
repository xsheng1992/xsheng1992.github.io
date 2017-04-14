---
layout: post
title:  "两个网页动画的动画库"
date:   2017-04-14 09:14:00
categories: 插件 css动画效果
---
#### 两个网页动画的动画库
最近在学习vue.js，里面的过渡效果可以使用第三方的动画库能达到更好的效果，在示例中介绍了两个动画库：Animate.css和Velocity.js。

##### Animate.css

Animate.css是一个css动画库，要应用效果只要加动画的类名就行了。可以点击链接查看主页：
<a href="https://daneden.github.io/animate.css/" target="_blank">Animate.css</a>

##### Velocity.js

Velocity.js是一个js的动画库，它拥有JQuery的animate的所有功能，并且有许多新的功能，比如颜色动画、转换动画(transforms)、循环、 缓动、SVG 动画、和 滚动动画 等特色功能。Velocity和$.animate()有形同的api，但是它也可以不依赖JQuery。

Velocity.js 可以在不引入 jQuery 的情况下单独使用。如果 你需要大部分动画效果能兼容 IE8，就必须引入 jQuery 1×。 它也可以和 Zepto 一起使用，写法和 jQuery 一样：

{% highlight ruby %}
// 无 jQuery 或 Zepto 时，Velocity()方法挂载在 window 对象上 (window.velocity)
// ( 第一个参数为原生js的dom选择器 )
Velocity(document.getElementById("dummy"), {
    opacity: 0.5
}, {
    duration: 1000
});

// 使用 jQuery 或 Zepto 时
$("#dummy").velocity({
    opacity: 0.5
}, {
    duration: 1000
});
{% endhighlight %}

关于Velocity.js更多的详细信息可以去看 <a href="http://www.mrfront.com/docs/velocity.js/" target="_blank">Velocity.js中文手册</a>