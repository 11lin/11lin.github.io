---
layout: post
title:  "cygwin git-difftool设置成Beyond Compare工具"
categories: blog
date: 2015/12/14 18:14:40
---
Beyond Compare常用的版本也就3、4了。

git for windows版本,bc官网已经给出解决办法了

打开Git Bash 输入下面命令，路径根据自己的设置

	git config --global diff.tool=bc3
	git config --global difftool.bc3.cmd "\"D:/Beyond Compare 4/bcomp.exe\" \$LOCAL \$REMOTE"
	git config --global mergetool.bc3.cmd "\"D:/Beyond Compare 4/bcomp.exe\" \$LOCAL \$REMOTE \$BASE \$MERGED"

>**注意:** Beyond Compare4 diff.tool也要设置成bc3，不然会报错

设置完成之后看起来像这样

	[user]
	    name = chips
	    email = jcfss@126.com
	[diff]
	    tool = bc3
	[difftool "bc3"]
	    cmd = \"D:/Beyond Compare 4/bcomp.exe\" $LOCAL $REMOTE
	[difftool]
	    prompt = false
	[merge]
	    tool = bc3
	[mergetool "bc3"]
	    cmd = \"D:/Beyond Compare 4/bcomp.exe\" $LOCAL $REMOTE $BASE $MERGED
	    trustExitCode = true
	[core]
	    autocrlf = true

git diff太不友善了，Beyond Compare的优势这里就不再阐述了。

由于cgywin里git跟git for windows 不是同一版本，所以还需要在cygwin设置下bc

使用上面的方法完全不行的。
git difftool对比能打开bc，只显示了当前源文件。
没有显示上一个版本的文件。

上网查了查，居然网上没有资料。

我想是不是路径没有识别出来。写了shell名字叫git-diff.sh放在D:/Beyond Compare 4/目录下:
{% highlight shell linenos %}
#!/bin/sh
for var in $@; do
	echo $var
done
"D:/Beyond Compare 4/bcomp.exe" `cygpath -w $1` $2 #/readonly
{% endhighlight %}
比较简单就是两个参数而已，主要的问题是：

cygwin git生成的路径在bc识别不了，需要cygwin转化成windows路径。

	git config --global diff.tool=bc3
	git config --global difftool.bc3.path "D:/Beyond Compare 4/git-diff.sh"
	git config --global mergetool.bc3.path "D:/Beyond Compare 4/git-merge.sh"




[Beyond Compare版本控制设置](http://www.scootersoftware.com/support.php?zz=kb_vcs#gitwindows)

<!-- [欢迎界面]({% post_url 2015-12-10-welcome-to-first %}) -->