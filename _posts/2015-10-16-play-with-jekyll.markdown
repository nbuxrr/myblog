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

##一、安装jekyll依赖环境
安装ruby->配置天朝的gem源->使用gem安装jekyll

###安装ruby
{% highlight ruby %}
$ sudo apt-get install ruby ruby-dev
$ ruby -v
{% endhighlight %}
安装的ruby需要时1.9.xx及以上吧，不然貌似就要悲剧了。

###配置gem源
将gem的国外源换成天朝某宝的源
{% highlight ruby %}
$ gem sources --add https://ruby.taobao.org/ --remove https://rubygems.org/
$ gem sources -l
{% endhighlight %}
查看源列表，只保留某宝的原就可以了。

###安装jekyll
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

到此应该可以cd到你期望的目录下使用jekyll new xxxx创建一个xxxx的demo博客项目，然后cd到xxxx在jekyll server，到你的浏览器里打开**127.0.0.1:4000**就可以看到一个Welcome to Jekyll!的页面了

##二、写第一篇博客
找一个自己喜欢的jekyll主题模板(index.html、_includes、_layouts、pages....)->配置自己博客网站的私人信息(_config.yml)->写一篇自己的blog(_post)->测试检查(jekyll server)

选择了一个什么样的主题决定了需要添加什么样的信息到_config.yml中，也决定了在博文markdown文件中应该添加哪些信息。
总而言之，读一遍主题模板的代码就大概清楚目录中所有文件的关系了，囧。

示例目录结构如下:
{% highlight ruby %}
.
├── CNAME
├── _config.yml
├── _includes
│   ├── disqus.html
│   ├── footer.html
│   ├── googleanalytics.html
│   ├── header.html
│   ├── header_title.html
│   └── navside.html
├── _layouts
│   ├── base.html
│   ├── base_title.html
│   ├── book.html
│   ├── page.html
│   ├── page_title.html
│   └── post.html
├── _posts
│   ├── 2015-10-12-welcome-to-jekyll.markdown
│   └── 2015-10-16-play-with-jekyll.markdown
├── _site
│   ├── 2015
│   ├── CNAME
│   ├── index.html
│   ├── pages
│   ├── public
│   └── sitemap.txt
├── index.html
├── pages
│   ├── about.html
│   ├── archive.html
│   └── atom.xml
├── public
│   ├── css
│   ├── fonts
│   ├── img
│   └── js
└── sitemap.txt
{% endhighlight %}

##三、托管到github
安装git管理工具->注册github账号如果你还没有的话->创建仓库(repository)->将jekyll项目模板提交到github->访问blog主页。
完全就是github的使用技巧和小白也会的访问网页，略。

PS几个重点:

1、提交jekyll博客项目到github上时可以选择提交至目标仓库的gh-pages分支，也可以选择提交至master主分支(需要仓库命名为“username.github.io”的格式)。

举个🌰，我的git用户名是nbuxrr，那么我的jekyll blog文件可以提交到一个我喜欢的仓库名如myblog，再将上边jekyll blog项目的文件提交到这个仓库的gh-page分支，然后在浏览器上访问https://nbuxrr.github.io/myblog地址来打开我的blog。
或者我也可以选择创建一个名叫nbuxrr.github.io的仓库，然后将目录提交到这个仓库的master主分支，然后在浏览器访问
https://nbuxrr.github.io打开blog就可以了。

2、想要通过访问自定义的域名来访问托管在github上的blog，需要: 自己购买一个域名(例如birdxu.com)->设置域名解析记录（注册一个DNSPod账号，登录DNSPod后，在域名管理中添加购买的域名，然后建立一条主机记录为@、记录类型为A、记录值为192.30.252.153的记录，如果不是从DNSPod购买的域名，还需要在域名购买商的网站上添加将域名解析交给DNSPod的配置，详细见DNSPod的服务帮助，因为DNSPod的DNS添加解析记录服务是免费的所以就选它了）->在jekyll目录项新建一个CNAME的文本文件，内容只填购买的域名（birdxu.com），然后提交github如上目录结构位置。然后就可以直接通过自定义的域名来访问blog了。
如果不想把自己购买的域名就这样用掉，也可以再在DNSPod的域名管理下添加一条例如主机记录为blog、记录类型为CNAME、记录值为nbuxrr.github.io.的记录，再将github上的CNAME改为blog.bird.com就可以用blog.birdxu.com作为blog的地址了。
[GitHub Help](https://help.github.com/categories/github-pages-basics/)

3、如果主题中包含了disqus的评论模块，则需要在disqus上注册一个账号，再配置一个”Add Disqus to your site“，将blog的地址配置到这个add配置里，将add配置里配置的shortname配置到_config.yml的disqus的shortname中。








