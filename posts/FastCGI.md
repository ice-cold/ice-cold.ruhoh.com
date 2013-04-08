---
title: FastCGI 不完全高级指南
date: '2013-04-08'
description: FastCGI 不完全高级指南
categories: web
tags: [FastCGI, Apache Module, IIS ISAPI ]
---

###一、FastCGI是什么？###

　　FastCGI是语言无关的、可伸缩架构的CGI开放扩展，其主要行为是将CGI解释器进程保持在内存中并因此获得较高的性能。众所周知，CGI解释器的反复加载是CGI性能低下的主要原因，如果CGI解释器保持在内存中并接受FastCGI进程管理器调度，则可以提供良好的性能、伸缩性、Fail-Over特性等等。
    
   FastCGI的官方站点在：http://www.fastcgi.com

　　FastCGI的工作原理是：

　　1、Web Server 启动时载入FastCGI进程管理器（IIS ISAPI或Apache Module）;

　　2、FastCGI进程管理器自身初始化，启动多个CGI解释器进程 (在任务管理器中可见多个php-cgi.exe)并等待来自Web Server的连接;

　　3、当客户端请求到达Web Server时，FastCGI进程管理器选择并连接到一个CGI解释器。Web server将CGI环境变量和标准输入发送到FastCGI子进程php-cgi.exe。

　　4、FastCGI子进程完成处理后将标准输出和错误信息从同一连接返回Web Server。当FastCGI子进程关闭连接时，请求便告处理完成。FastCGI子进程接着等待并处理来自FastCGI进程管理器（运行在 WebServer中）的下一个连接。 在正常的CGI模式中，php-cgi.exe在此便退出了。

　　在上述情况中，你可以想象 CGI通常有多慢。每一个Web请求PHP都必须重新解析php.ini、重新载入全部dll扩展并重初始化全部数据结构。使用FastCGI，所有这些都只在进程启动时发生一次。一个额外的好处是，持续数据库连接(Persistent database connection)可以工作。

###二、为什么要使用FastCGI，而不是多线程CGI解释器？###

　　这可能出于多方面的考虑，例如：

　　1、你无论如何也不能在windows平台上稳定的使用多线程CGI解释器，无论是IIS ISAPI方式还是APACHE Module方式，它们总是运行一段时间就崩溃了。奇怪么？但是确实存在这样的情况！

　　当然，也有很多时候你能够稳定的使用多线程CGI解释器，但是，你有可能发现网页有时候会出现错误，无论如何也找不到原因，而换用FastCGI方式时这种错误的概率会大大的降低。我也不清楚这是为什么，我想独立地址空间的CGI解释器可能终究比共享地址空间的形式来得稳定一点点。

　　2、性能！性能？可能么，难道FastCGI比多线程CGI解释器更快？但有时候确实是这样，只有测试一下你的网站，才能最后下结论。原因嘛，我觉得很难讲，但有资料说在Zend WinEnabler的时代，Zend原来也是建议在Windows平台下使用FastCGI而不是IIS ISAPI或Apache Module，不过现在Zend已经不做这个产品了。

###三、不使用FastCGI的理由###

　　1、多进程比多线程消耗更多的服务器内存，php-cgi.exe解释器每进程消耗7至25兆内存，将这个数字乘以50或100试试。

　　2、性能。确实有时候多线程CGI解释器更快，呵呵，而且有时候，它也很稳定。

　　3、CGI？听起来就很土，呵呵

###四、IIS FastCGI配置方法###

　　1、首先确定你已正确安装了PHP 4.3.x及更新的版本。早期版本的PHP并未默认加入FastCGI支持，如果你想在早期版本中工作，需要重新编译它。我们假设PHP安装在c:\php，支持FastFCGI的可执行文件名是php-cgi.exe。

　　　　注意：建议在Php.ini中关闭cgi.force_redirect，启用fastcgi.impersonate，启用cgi.rfc2616_header

　　2、下载http://www.caraveo.com/fastcgi/fastcgi-0.6.zip  并将其中的isapi_fcgi.dll解压缩到c:\php目录下（不是必须在此目录，这里只是叙述方便）。

　　3、使用regedit.exe建立如下注册表项：

　　HKEY_LOCAL_MACHINE:Software\FASTCGI\.php　（必需）

　　4、在此项下建立如下键值：

　　字符串类型：AppPath，值为c:\php\php-cgi.exe　（必需）

　　字符串类型：BindPath，值为php-fcgi　　　　　 （必需）

　　以下是可选配置键值：

　　DWORD类型：StartServers，启动时默认启动的解释器个数，默认值5

　　DWORD类型：MaxServers，最大解释器个数，默认25

　　DWORD类型：IncrementServers，当解释器不够用时增量个数，默认2

　　DWORD类型：Timeout，增量解释器（超出StartServers数目的）存活时间，默认600（秒）

　　DWORD类型：ThreadPoolSize，线程池大小，仅IIS下有效，默认10

　　DWORD类型：Impersonate，仅IIS有效，如果为1，使用IIS安全标志，为0则关闭此特性。不要关闭它除非你不担心安全问题。默认1

　　DWORD类型：MaxPostData，Post数据预读Byte限制，默认0

　　DWORD类型：BypassAuth，仅IIS有效，如果为1并且isapi_fcgi.dll被配置为IIS Filter，同时IIS被配置为使用BASIC Authentication，这将强制所有认证请求使用IIS匿名用户。这一选项的目的是允许脚本实现自己的安全机制。默认0

　　BINARY类型：CustomVars，附加环境变量值，新行分隔，Null结束

　　5、如果是IIS6，添加一个Web服务扩展指向c:\php\isapi_fcgi.dll，并允许。应用程序池中的“最大工作进程数”请保持为1。

　　6、添加应用程序扩展映射关系：

         1). 在Internet信息服务管理器中，选择网站或应用程序的根目录。

         2). 打开目录属性页（右键选择“属性”），再选择“主目录”。

         3). 点击“配置”按钮，选择“映射”Tab页。

         4). 点击“添加...”，在“可执行文件”设为: c:\php\isapi_fcgi.dll，扩展名设为.php，一定要选择“确认文件是否存在”，
         然后“确定”保存设置。

         5). 再同样添加对.php3或.phtml扩展名的支持（可选）。

         6). 保存设定并重新启动IIS。

　　7、测试一下，同时请求多个Web页面，然后察看任务管理器中的进程，页面完成后php-cgi.exe进程持续运行并不退出。

###五、Apache配置方法###

　　1、首先确定你已正确安装了PHP 4.3.x及更新的版本。早期版本的PHP并未默认加入FastCGI支持，如果你想在早期版本中工作，需要重新编译它。我们假设PHP安装在c:\php，支持FastFCGI的可执行文件名是php-cgi.exe。

　　　　注意：建议在Php.ini中打开cgi.force_redirect，关闭fastcgi.impersonate，关闭cgi.rfc2616_headers。

　　2、下载http://www.fastcgi.com/dist/mod_fastcgi-2.4.2-AP20.dll ，放到Apache 2.x的Modules目录中。

　　3、确定Apache 2.x在CGI方式下可以正常运行PHP。httpd.conf中存在如下几行：

　　　　ScriptAlias /php/ "c:/php/"

　　　　Action application/x-httpd-php "/php/php-cgi.exe"

　　　　SetEnv PHPRC "C:/php"

　　　　AddType application/x-httpd-php .php

　　4、在httpd.conf中添加:

　　　　LoadModule fastcgi_module modules/mod_fastcgi-2.4.2-AP20.dll

　　　　# 说明：此处的 -processes 3 表示启动三个 php-cgi.exe 进程，

　　　　# 关于 FastCgiServer 的详细参数请参考 FastCGI 文档。

　　　　FastCgiServer "c:/php/php-cgi.exe" -processes 3

　　5、重新启动Apache，测试同上。

###六、高级配置###

　　设想这样一种场景，你的服务器上同时跑Apache 2和IIS 6，两个Web服务器都跑php应用。那么，有如下三种可能：

　　A、php使用iis isapi和apache module安装，均为多线程方式运行。这个和FastCGI没有关系。

　　B、其中一个服务器使用FastCGI方式，另一个使用多线程方式。这个能运行正常。

　　C、两个均使用FastCGI方式，这个往往不正常。一般表现为：

　　　　两个服务器各自启动一些php-cgi.exe进程，然后服务器之一不解释php页面，或者隔一会儿就派生新的php-cgi.exe进程（可怕呀）。

　　为什么呢？我想大概是因为上面使用的两个东西（iis isapi和apache module）的作者大概并没有想过要和对方同时使用吧，呵呵。想了想，Apache 2和IIS 6如果可以共用一批php-cgi.exe解释器就好了，既不浪费内存，估计也不会有调度问题了。

　　经过研究和测试证明，这个想法是可行的。但是，由于Shane Caraveo并未在ISAPI DLL中提供使用外置FastCGI服务的功能，因此在此场景中只能是由IIS负责启动和管理php-cgi.exe，然后配置Apache去使用这些受 IIS管理的php-cgi.exe进程。

　　配置方法：

　　1、按上述四中的方法配置IIS FastCGI。

　　2、基本按上述五中的方法配置Apache FastCGI，五.4改为在httpd.conf中添加:

　　　　LoadModule fastcgi_module modules/mod_fastcgi-2.4.2-AP20.dll

　　　　# 使用外部FastCGI服务器，请参考 FastCGI 文档。

　　　　FastCgiExternalServer "c:/php/php-cgi.exe" -socket "php-fcgi"

　　注意：-socket参数后的值必须与HKEY_LOCAL_MACHINE:Software\FASTCGI\.php中BindPath的值一致，这样两个FastCGI进程管理器才会使用同一个命名管道连接php-cgi.exe。

　　注意：此配置中php-cgi.exe进程只受IIS中的FastCGI进程管理器管理， Apache的繁忙请求并不会使IIS中的FastCGI调度更多的php-cgi.exe进程。因此，在IIS中配置FastCGI时应当使 StartServers值足够大，以避免php解释器数量不足。同样带来的问题是，如果IIS关闭了，那么Apache就会找不到Php解释器了，这个要留心。

　　由此带来的一个问题是：此时的php.ini中cgi.force_redirect、fastcgi.impersonate、cgi.rfc2616_headers应该怎么设定呢？这个留给大家去思考吧……呵呵

　　另外一个可能遇到的问题是，IIS非常空闲，一段时间后由IIS启动的php-cgi.exe退出了，则apache就解释不了 Php了，怎么办呢？这时可以访问一下iis网站，php-cgi.exe就又起来了，晕哦。一个建议是使用IIS 6的进程池管理，在应用程序池中关掉“空闲超时”，并且，在“应用程序池标识”中将运行账号设定为与Apache服务启动账号一致。
