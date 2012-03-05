---
layout: post
title: "【转】分享平时工作中那些给力的shell命令"
date: 2012-03-05 11:43
comments: true
categories: shell operation
---
Copied from <http://yunhaozou.org/perl-shell/162.html>，经过适当的排版编辑

###1. 显示消耗内存/CPU最多的10个进程
	ps aux | sort -nk +4 | tail
	ps aux | sort -nk +3 | tail

###2. 查看Apache的并发请求数及其TCP连接状态
	netstat -n | awk ‘/^tcp/ {++S[$NF]} END {for(a in S) print a, S[a]}’
<!--more-->

###3. 找出自己最常用的10条命令及使用次数（或求访问最多的ip数）
	sed -e ‘s/| /\n/g’ ~/.bash_history |cut -d ‘ ‘ -f 1 | sort | uniq -c | sort -nr | head

###4. 日志中第10个字段表示连接时间，求平均连接时间
	cat access_log |grep “connect cbp” |awk ‘BEGIN{sum=0;count=0;}{sum+=$10;count++;}END{printf(“sum=%d,count=%d,avg=%f\n”,sum,count,sum/count)}’

###5. lsof命令
	lsof abc.txt 显示开启文件abc.txt的进程
	lsof -i :22 知道22端口现在运行什么程序
	lsof -c abc 显示abc进程现在打开的文件
	lsof -p 12  看进程号为12的进程打开了哪些文件

###6. 杀掉一个程序的所有进程
	pkill -9 httpd
	killall -9 httpd
*注意尽量不用`-9`，数据库服务器上更不能轻易用`kill`，否则造成重要数据丢失后果将不堪设想。*

###7. rsync命令（要求只同步某天的压缩文件，而且远程目录保持与本地目录一致）
	/usr/bin/rsync -azvR –password-file=/etc/rsync.secrets `find . -name “*$yesterday.gz”  -type f ` storage@192.168.2.23::logbackup/13.21/

###8. 把目录下*.sh文件改名为*.SH
	find .  -name “*.sh” | sed  ’s/\(.*\)\.sh/mv \0 \1.SH/’ |sh
	find .  -name “*.sh” | sed  ’s/\(.*\)\.sh/mv & \1.SH/’|sh  （跟上面那个效果一样）

###9. ssh执行远程的程序，并在本地显示
	ssh -n -l zouyunhao 192.168.2.14 “ls -al /home/zouyunhao”

###10. 直接用命令行修改密码
	echo “zouyunhaoPassword” |passwd –stdin zouyunhao

###11. 将 ssh keys 复制到 user@remoteServer 以启用无密码 SSH 登录。
	ssh-keygen
	ssh-copy-id -i ~/.ssh/id_rsa.pub user@remoteServer

###12. 以http方式共享当前文件夹的文件
	python -m SimpleHTTPServer
在浏览器访问`http://IP:8000/`即可下载当前目录的文件。

###13. shell段注释
	:<<’echo hello,world!’

###14. 查看服务器序列号
	dmidecode |grep “Serial Number”
*查看机器其他硬件信息也可用这个命令*

###15. 查看网卡是否有网线物理连接
	/sbin/mii-tool

###16. 查看linux系统或者mysql错误码表示的意思，如查看13错误码表示的意思：
	perror  13

###17. 关于cpu个数
查看逻辑cpu个数：
	cat /proc/cpuinfo | grep “processor” | wc -l
查看物理cpu个数：
	cat /proc/cpuinfo | grep “physical id” | sort | uniq | wc -l
查看每个物理cpu的核数cores：
	cat /proc/cpuinfo | grep “cpu cores”
*如果所有物理cpu的cores个数加起来小于逻辑cpu的个数，则该cpu使用了超线程技术。*<br>
查看每个物理cpu中逻辑cpu的个数：
	cat /proc/cpuinfo | grep “siblings”

###18. 从格式不规范的日志中截取字符串
	perl  -ne  ’print “$1\n” if  /servletPath=(\S+)/g’  test.log


*（不断更新中……）*

本文出自[孤风颠影|网站运维](http://yunhaozou.org/) 网址:<http://yunhaozou.org/perl-shell/162.html>. 转载请保留.