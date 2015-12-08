---
layout: post
title:  "Markdown 语法测试!"
date:   2015-12-08 19:53:06
categories: 代码
---

<!--使用VS Code编辑MarkDown实在是太爽了-->
<!--暂时先理解为Markdown由如-、*、#等格式控制字符和文章内容字符组成-->
<!--格式控制字符和文章内容字符之间保留个空格比较纯正和正确-->
# Level1			<!--空格似乎非必须但规范-->
## Level2
### Level3
#### Level4
+ 一条			  <!-- +或-或*加空格开头，即可变为无序列表，空格就是必须的了 -->
	这一条是测试
- 一条
	这一条是测试
* 又一条
	这一条又是测试

##### Level5
###### Level6


# 一级标题
## 二级标题
### 三级标题

1. xxxx				<!-- 数字加.加空格开头，即可变为有序列表 -->
	xxxxxxxxxxx
	xxxxxxxxxxx
3. xxxx
	xxxxxxxxxxx
2. xxxx
	xxxxxxxxxxx
0. xxxx				
0. xxxx
0. xxxx

#### 四级标题
##### 五级标题
###### 六级标题

> 这是一行引用		<!-- >加空格开头，表示为引用-->
> > 这是一行嵌套引用2		<!-- >加空格开头，表示为引用-->
> 这是一行引用3		<!-- >加空格开头，表示为引用-->

[这是一个链接](http://www.baidu.com)

# 插入图片测一测
![put a picture](/public/img/testpic.jpg)
![put another picture](http://ww2.sinaimg.cn/large/6aee7dbbgw1efffa67voyj20ix0ctq3n.jpg)


**这里是粗体**

*这里是斜体*


`
int main()
{
	printf("this is a test\n");
	return 0;
} 
`


> ## 这是一个标题。
> 
> 1.   这是第一行列表项。
> 2.   这是第二行列表项。
> 
> 给出一些例子代码：
>
>     return shell_exec("echo $input | $markdown_script");






