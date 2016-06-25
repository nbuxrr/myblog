---
layout: post
title:  "Apache2 CGI 配置"
categories: 代码
tags: CGI
keywords: CGI
description: apache2 CGI 配置
---

##一、安装及配置apache服务器

{% highlight bash %}
sudo apt-get install apache2
{% endhighlight %}

##二、配置增加CGI功能模块
打开配置文件httpd.conf或者apach2.conf或者叫其他什么名字，(我的为/etc/apache2/apache2.conf，测试系统为ubuntu 16.04)。
增加如下配置：

{% highlight html %}
<Directory "/var/www/html/cgi-bin/">
	Options Indexes FollowSymLinks MultiViews +ExecCGI
	AllowOverride None
	Order allow,deny
	allow from all
</Directory>

LoadModule cgi_module /usr/lib/apache2/modules/mod_cgi.so 	
AddHandler cgi-script .cgi .pl .py .sh 	
{% endhighlight %}

第一段标签应该主要定义一个部署目录，允许mod_cgi.so模块执行该目录下的cgi程序（+ExecCGI）,及其他一些属性配置，不知道就baidu吧。
<br />第二句是将mod_cgi.so加载入apache2，使支持cgi（如果默认已有该配置则不需要加）。
<br />最后一句是配置允许的CGI程序或者脚本的类型，例如本处是使CGI支持perl、python、shell脚本。

##三、配置目录
因为CGI程序可以调用系统的的更多资源，所以CGI会涉及到安全问题，所以需要将CGI放在一个特定的目录下执行，可以指定一个虚拟的目录。

打开配置文件：
{% highlight bash %}
sudo vi /etc/apache2/sites-enabled/000-default
{% endhighlight %}

修改(若没有就增加)其中两句为：
{% highlight bash %}
DocumentRoot /var/www/html
ScriptAlias /cgi-bin/ /var/www/html/cgi-bin/
{% endhighlight %}

第一句 指定html文件的目录。
<br />第二句 将虚拟目录/cgi-bin/映射到/var/www/html/cgi-bin/，该目录中的文件均被认作是cgi程序，所以就不应将html文件放置在此目录下。
所指定的或被映射的目录需要真是存在。


##四、重启apache2配置生效
{% highlight html %}
sudo /etc/init.d/apache2 restart
{% endhighlight %}

##五、测试
例如如果浏览器中访问 http://localhost/cgi-bin/hi.py 就可以执行cgi-bin下的hi.py

{% highlight python %}
#!/usr/bin/python
# -*- coding: UTF-8 -*-
####/var/www/html/cgi-bin/hi.py

print "Content-type:text/html"
print ""                               # 空行，告诉服务器结束头部
print '<html>'
print '<head>'
print '<meta charset="utf-8">'
print '<title>Hi CGI - CGI 程序</title>'
print '</head>'
print '<body>'
print '<h2>我是CGI程序</h2>'
print '</body>'
print '</html>'
{% endhighlight %}

ps: /var/www/html/cgi-bin/hi.py下的文件都应权限设置为755，否则可能无法被cgi执行
