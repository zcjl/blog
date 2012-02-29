---
layout: post
title: Tip：Mac下非正常退出LibreOffice后无法关闭Restore Windows的解决办法
date: 2012-02-29 15:35
comments: true
categories: 
---
Mac Lion下，由于没有正常退出LibreOffice，重启后会出现一个`“Restore Windows”`的提示
![libreoffice](/images/libre-office-restore-windows.png)
但杯具的是，无论你选择`“Don't Restore Windows”`还是`“Restore Windows”`，这个窗口都无法关闭，而且没有正常关闭的文档也恢复不了

Mac Lion提供了一个叫做Resume的Feature，以便用户非正常退出或错误滴`Ctrl+Q`后还能恢复现场。各应用的即时状态，是保存存在`“$HOME/Library/Saved Application State”`目录下的

对应到前面LibreOffice的问题，如果是使用`Ctrl+Q`退出应用，其实是会弹出提示保存文档的。但非正常退出，重启应用就会弹出前面的提示。<br>
解决办法，粗暴点就是
	rm $HOME/Library/Saved Application State/org.libreoffice.script.savedState


参考资料：<br>
<http://osxdaily.com/2011/07/17/delete-specific-application-saved-states-from-mac-os-x-10-7-lion-resume/>