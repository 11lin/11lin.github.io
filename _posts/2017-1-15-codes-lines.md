---
layout: post
title:  "搞定所有代码文件数量以及行数的统计"
categories: blog
date: 2017/01/15 17:41:08
---
使用几个命令就可以搞定了

{% highlight bash linenos %}
#文件数统计
find . -name "*.md"|wc -l
#代码行数统计,如果wc是汉化过的，请把"total"替换"总用量"
#方法1
find . -name "*.md"|xargs wc -l|grep "total"|awk '{print $1}'
#方法2
find . -name "*.md"|xargs cat|wc -l
#去除空行
find . -name "*.md"|xargs cat|grep -v ^$|wc -l
{% endhighlight %}
