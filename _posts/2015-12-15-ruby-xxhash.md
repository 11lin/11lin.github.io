---
layout: post
title:  "xxhash介绍"
categories: blog
date: 2015/12/15 16:15:57
---

> - ruby 2.0.0p598 (2014-11-13) [x86_64-cygwin]
> - gem 2.4.1
> - [xxhash  0.3.0 for ruby](https://rubygems.org/gems/xxhash)

最近有时间研究了下cocos2dx 3.x的版本，里面有两个文件引起了我的好奇。(xxhash.h、xxhash.c)

发现xxhash是一个类似于计算md5的库,快md5十几倍

Name|Speed|Q.Score|Author
-------|-------|--------|--------
xxHash|5.4 GB/s|10
MumurHash 3a|2.7 GB/s|10|Austin Appleby
SpookyHash|2.0 GB/s|10|Bob Jenkins
SBox|1.4 GB/s|9| Bret Mulvey
Lookup3|1.2 GB/s|9|Bob Jenkins
CityHash64|1.05 GB/s|10|Pike & Alakuijala
FNV|0.55 GB/s|5|Fowler, Noll, Vo
CRC32|0.43 GB/s|9
MD5-32|0.33 GB/s|10|Ronald L. Rivest
SHA1-32|0.28 GB/s|10


####xxhash 32位跟64位计算区别

Name|Speed on 64 bits|Speed on 32 bits
------|-------------------|------------------
XXH64|13.8 GB/s|1.9 GB/s       
XXH32|6.8 GB/s|6.0 GB/s

用来计算更新文件hash值
xxhash安装出错

	$ gem install xxhash
	ERROR:  Could not find a valid gem 'xxhash' (>= 0) in any repository

直接使用[下载](https://rubygems.org/gems/xxhash)到本地**gem install -l xx.gem**

Usage
====
{% highlight ruby linenos %}
require 'xxhash'
require 'stringio'

text = "test"
seed = 12345
XXhash.xxh32(text, seed) # => 3834992036
#You can use it with IO objects too:
XXhash.xxh32_stream(StringIO.new('test'), 123) # => 2758658570
XXhash.xxh32(File.read("path"), 123)
XXhash.xxh32_stream(File.open("path"), 123)
{% endhighlight %}
	
cygwin gem 错误
==========

	$gem sources --add https://ruby.toabao.org
	https://ruby.toabao.org not a uri

处理方法,直接修改 ~/.gemrc :sources

	---
	:backtrace: false
	:bulk_threshold: 1000
	:sources:
	- https://ruby.taobao.org/
	:update_sources: true
	:verbose: true

[github xxhash of ruby](https://github.com/nashby/xxhash)