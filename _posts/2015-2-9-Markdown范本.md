---
layout: post
title: "《Nagios系统监控实践》简评+笔记"
date: 2014-03-26 13:42
comments: true
categories: Nagios
---

<!-- more -->


文章的内容排版分类比较清晰(不过有个别的比如nrpe, check\_mk等在多个章节中都提到):

* 第一章讲了一些运维监控的基本思想。


这本书是一本入门Nagios的好书，虽然讲得不是很深，但是全局性把握到了，可以很直观全面的学习Nagios。


---

快速扫完这本书，也学到了一些东西，在网上简单了解了下这些东西，还未做尝试(所以可能有误)，先简单记录下：

### 开发脚本模板(P72) ###

第五章第一节，提到了 **开发脚本模板**，

模板:

	define host {
		name         base_host
		....
		register     0
	}



这个可以保存为名叫 hosts.skel 的框架模板

定义中的NAME, DOMAIN 这些都是一些变量，可以被替代的值。

这样就可以通过一份主机列表和一个小脚本来快速填充配置。比如主机列表:

	host1.mydomain.com
	host2.mydomain.com
	host3.mydomain.com
	...

小脚本:

	#!/bin/bash
	while read i
	do
		NAME='echo ${i} | cut -d. -f1'
		DOMAIN='echo ${i} | cut -d. -f2-'
		sed -e "s/NAME/$NAME/" -e "s/DOMAIN/$DOMAIN/" hosts.skel >> hosts.cfg
	done

### 第七章 Nagios的一些扩展(P129) ###

介绍了一些Nagios的优化和调整经验。

配合[NSCA](http://exchange.nagios.org/directory/Addons/Passive-Checks/NSCA--2D-Nagios-Service-Check-Acceptor/details)


这一块的内容还需要进一步的了解学习。**TODO**

### NRPE(P105) ###

[NRPE](http://exchange.nagios.org/directory/Addons/Monitoring-Agents/NRPE--2D-Nagios-Remote-Plugin-Executor/details)(Nagios Remote Plugin Executor) 官方介绍和原理图:

> NRPE allows you to remotely execute Nagios plugins on other Linux/Unix machines. This allows you to monitor remote machine metrics (disk usage, CPU load, etc.). NRPE can also communicate with some of the Windows agent addons, so you can execute scripts and check metrics on remote Windows machines as well.

![Nagios NRPE 原理图](http://tankywoo-wb.b0.upaiyun.com/nagios_nrpe.png)

NRPE是一个轻量级的C/S系统，通过它Nagios服务器可以执行存放在被监控主机上的远端插件。

监控端运行一个 `check_nrpe` 程序，远端主机运行一个 `NRPE Daemon`。

监控端 `check_nrpe` 本地配置要监控的服务，通过SSL方式连接到远端的 `NRPE Daemon`，然后 NRPE Daemon 会执行相应的检测，将检查结果返回给`check_nrpe`。

这种方式也可以降低监控端主机的运行压力。

### Check MK(P114) ###

![Check MK 原理图](http://tankywoo-wb.b0.upaiyun.com/nagios_check_mk.png)



### NagiosQL(P77) ###

[NagiosQL](http://www.nagiosql.org/) 

* [InfoQ - 作者访谈与书评：“Nagios企业监控实践（原书第2版）”](http://www.infoq.com/cn/articles/building-nagios-monitoring-infrastructure-review)
