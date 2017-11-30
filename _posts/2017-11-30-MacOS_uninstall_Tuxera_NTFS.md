---
layout: post
title:  MacOS 下完全卸载Tuxera NTFS
categories: [MacOS]
tags:	[MacOS]
---
>  Mac OS 默认是不支持NTFS格式的移动硬盘或U盘。*Tuxera NTFS* 这款应用就是为了解决这一问题，但是它是一款收费软件，可以免费体验15天。体验后想卸载，若只通过在 *Application* 目录删除它的话，是不能完全卸载，所以每次插入NTFS格式的移动硬盘或U盘都会弹出如下提示



<div style="width:100%" align="center">
	<img src="{{ site.BASE_PATH}}/img/mac_uninstall_tuxera_ntfs.png" alt="提示试用已过期" style="width: 400px;"/>
	<p>图0-1 提示试用已过期</p>
</div>

### 完全卸载方法如下

#### Terminal 下执行如下命令
{% highlight java %}
sudo rm -rf /Applications/Tuxera\ Disk\ Manager.app
sudo rm -rf /Library/Application\ Support/Tuxera\ NTFS
sudo rm -rf /Library/Filesystems/fusefs_txantfs.fs
{% endhighlight %}
> 此过程中需要输入密码

##### 参考链接：
[Completely uninstall and remove Tuxera NTFS on MacOs (resets trial version)](https://gist.github.com/miguelmota/3f380d75963ca16bd8cc64a10d0d2163#file-remove_tuxera-sh)

### the end
