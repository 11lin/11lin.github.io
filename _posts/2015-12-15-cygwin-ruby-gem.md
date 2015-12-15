---
layout: post
title:  "cygwin gem 报utf8错误处理!"
categories: blog
date: 2015/12/15 15:21:11
---

> - ruby 2.0.0p598 (2014-11-13) [x86_64-cygwin]
> - gem 2.4.1

	$ gem update
	Updating installed gems
	ERROR:  While executing gem ... (ArgumentError)
	    invalid byte sequence in UTF-8


**处理方法** LANG=C.BINARY gem update

[参考cygwin](https://cygwin.com/ml/cygwin/2014-09/msg00098.html)