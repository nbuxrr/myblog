---
layout: post
title:  "搭建个人jekyll博客"
categories: 代码
tags: jekyll
keywords: jekyll github pages
description:
---

缘于一次偶尔的逛知乎，看到有人讨论使用github搭建个人博客的问题...最后的重点是jekyll+github搭建博客的好处很多：模板自由、页面干净、没有广告、托管免费、无限流量...
搜罗网上各种搭建jekyll的教程，不出意外的遇到了一些些坑，主要有些牛人们也比较懒，懒惰的菜鸟就比较受伤了。囧。

搭建步骤如下：
安装ruby->配置天朝的gem源->使用gem安装jekyll

##一、安装jekyll依赖环境
###安装ruby
{% highlight ruby %}
$ sudo apt-get install ruby ruby-dev
$ ruby -v
{% endhighlight %}
安装的ruby需要时1.9.xx及以上吧，不然貌似就要悲剧了。

###[配置gem源](https://ruby.taobao.org)
将gem的国外源换成天朝某宝的源
{% highlight ruby %}
$ gem sources --add https://ruby.taobao.org/ --remove https://rubygems.org/
$ gem sources -l
{% endhighlight %}
查看源列表，只保留某宝的原就可以了。

###[安装jekyll](http://jekyllrb.com/docs/installation/)
{% highlight ruby %}
$ gem install jekyll -V
{% endhighlight %}
加-V只是将后台运行信息打印出来，心里感受好一点，强迫症患者。

按照搜罗到教程以为jekyll搭建好了，到目前为止都很顺利，满心欢喜的cd自己的目录下去jekyll new xxxx创建自己的jekylldemo项目，结果报了没有nodejs支持等之类的错误信息，好像安装个nodejs就可以了的样子。
网上搜罗了一下，果然[“ubuntu下需要自己安装nodejs, 等一些其他的包(如果没安装下面的包，运行jekyll server等会遇到ExecJS::RuntimeUnavailable 错误)”](http://www.th7.cn/system/lin/201406/58865.shtml)
{% highlight ruby %}
$ sudo apt-get install python-software-properties
$ sudo add-apt-repository ppa:chris-lea/node.js
$ sudo apt-get update
$ sudo apt-get install nodejs
{% endhighlight %}

走过的弯路如下：
{% highlight ruby %}
$ gem install rails -V
$ gem install bundle -V
$ gem install bundler -V
$ gem install rdoc -V
$ gem install rdiscount -V
$ curl -shttps://rvm.beginrescueend.com/install/rvm
{% endhighlight %}

[Test](http://jekyllrb.com/docs/quickstart/)
到此应该可以cd到你期望的目录下使用jekyll new xxxx创建一个xxxx的demo博客项目，然后cd到xxxx在jekyll server，到你的浏览器里打开**127.0.0.1:4000**就可以看到一个Welcome to Jekyll!的页面了
