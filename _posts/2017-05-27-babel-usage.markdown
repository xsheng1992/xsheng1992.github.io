---
layout: post
title:  "babel及webpack的安装使用"
date:   2017-05-31 14:39:21
categories: babel webpack
---
这篇文章讲讲babel和webpack的使用方法。

## Babel

首先，如果现在使用es6编写代码，浏览器可能还不支持某些功能，因此需要转换成es5，而这个转换的工具就是babel。

#### .babelrc

要在你的项目中使用Babel，首先需要配置.babelrc文件，而接下去的这些工具模块的使用，都依赖这个文件。

.babelrc文件的基本格式如下：

{% highlight javascript %}
{
  "presets": [],
  "plugins": []
}
{% endhighlight %}

presets字段里面设定的是转码规则，plugins字段里设定的是插件，目前官方提供的转码规则有以下几种：

* es2015
* stage-0
* stage-1
* stage-2
* stage-3
* react

你也可以使用latest来获取最新的转码规则

{% highlight basic %}
//es2015和最新的转码规则
$ npm install --save-dev babel-preset-es2015
$ npm install --save-dev babel-preset-latest

//不同阶段语法提案的转码规则
$ npm install --save-dev babel-preset-stage-0
$ npm install --save-dev babel-preset-stage-1
$ npm install --save-dev babel-preset-stage-2
$ npm install --save-dev babel-preset-stage-3

//react转码规则
$ npm install --save-dev babel-preset-react
{% endhighlight %}

然后将安装好的转码规则加入.babelrc文件中：

{% highlight javascript %}
{
  "presets": [
    "latest",
    "stage-3",
    //...
  ],
  "plugins": []
}
{% endhighlight %}

#### babel-cli

babel-cli用于命令行转码，你可以安装在全局：

{% highlight basic %}
$ npm install --global babel-cli
{% endhighlight %}

然后对文件转码：

{% highlight basic %}
# 转码结果输出到标准输出
$ babel example.js

# 转码结果写入一个文件
# --out-file 或 -o 参数指定输出文件
$ babel example.js --out-file compiled.js
# 或者
$ babel example.js -o compiled.js

# 整个目录转码
# --out-dir 或 -d 参数指定输出目录
$ babel src --out-dir lib
# 或者
$ babel src -d lib

# -s 参数生成source map文件
$ babel src -d lib -s
{% endhighlight %}

上面是在全局下安装的babel-cli，但是我们平常用的时候不可能每个项目的配置都一样，所以，还可以将babel-cli安装在项目之中。

{% highlight basic %}
$ npm install --save-dev babel-cli
{% endhighlight %}

然后再在package.json中的script下添加一句：

{% highlight javascript %}
{
  // ...
  "devDependencies": {
    "babel-cli": "^6.24.1"
  },
  "scripts": {
    "build": "babel src -d lib"
  },
}
{% endhighlight %}

然后要生成项目时运行 `npm run build` 就会把src文件夹中的文件转换成es5，然后输出到lib文件夹中了。

## 一个问题  
  
如果使用es6的模块化写法的时候，如：

{% highlight javascript %}
import delay from './app.js'
{% endhighlight %}

这时侯上面的语句会被转化成：

{% highlight javascript %}
var _app = require('./app.js');
{% endhighlight %}

然而运行之后这句语句会报错，这是因为babel把‘ES6 模块化语法’转化为了‘CommonJS 模块化语法’，然而浏览器端默认也无法识别 CommonJs 规范，所以会报错。所以这时候就需要额外的模块打包工具，这样就可以在浏览器端运行了。我这里使用的模块化工具是webpack。

## webpack

#### 安装

当然首先是安装，同样可以选择全局安装或安装在项目中：

{% highlight command %}
# 全局安装
$ npm install webpack -g 

# 安装在项目中
$ npm install --save-dev webpack
{% endhighlight %}

#### 配置文件 webpack.config.js

安装完后我们就要写配置文件webpack.config.js了。

一个常见的配置文件如下所示：

{% highlight javascript %}
//一个常见的Webpack配置文件
var webpack = require('webpack');
var path = require('path');

module.exports = {
  entry: "./src/index.js",
  output: {
    path: path.resolve(__dirname, './dist'),
    publicPath: '/dist/',
    filename: "bundle.js"
  },

  module: {
    loaders: [
      {
        test: /\.json$/,
        loader: "json"
      },
      {
        test: /\.js$/,
        exclude: /node_modules/,
        loader: 'babel'
      },
      {
        test: /\.(png|jpg|gif|svg)$/,
        loader: 'file-loader',
        options: {
          name: '[name].[ext]?[hash]'
        }
      }
    ]
  },

  plugins: []
}
{% endhighlight %}

entry是入口文件的路径，output中的path是打包后的文件存放的地方，filename是打包后的文件的名字。

Loader可以理解为是模块和资源的转换器，它本身是一个函数，接受源文件作为参数，返回转换的结果。这样，我们就可以通过require来加载任何类型的模块或文件，比如js、json、css、图片等。

要使用loader必须安装各自的loader工具，如我们用babel转换js文件，就要安装babel-loader，转换图片需要file-loader。

{% highlight command %}
$ npm install --save-dev babel-loader
$ npm install --save-dev file-loader
{% endhighlight %}

还可以使用插件，只要安装对应插件就行了，在plugins里写入。

要运行webpack（开发环境或最终打包，开发环境需要额外安装webpack-dev-server），需要在package.json里将添加webpack的dev和build命令：

{% highlight javascript %}
{
  //...
  "description": "babel runtime environment",
  "scripts": {
    "dev": "webpack-dev-server --hot --inline",
    "build": "webpack --progress"
  },
}
{% endhighlight %}

要运行npm run dev 还要在webpack.config.js中添加devserver：

{% highlight javascript %}
{
  //...
  devServer: {
    historyApiFallback: true,
    inline: true
  },
}
{% endhighlight %}

差不多就这样了。