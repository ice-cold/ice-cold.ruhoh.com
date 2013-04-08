---
title: CGI/FASTCGI/ISAPI区别
date: '2013-04-08'
description: CGI/FASTCGI/ISAPI区别
categories: web
tags: [CGI, FASTCGI, ISAPI ]
---

###一 CGI原理及其性能###

1) CGI概念

CGI即通用网关接口(Common Gateway Interface)，它是一段程序，运行在服务器上，提供同客户端HTML页面的交互，通俗的讲CGI就象是一座桥，把网页和WEB服务器中的执行程序连接起来，它把HTML接收的指令传递给服务器的执行程序，再把服务器执行程序的结果返还给HTML页。

2）CGI程序语言

事实上，任何一种程序语言，只要能在服务器主机上利用CGI接口来编写应用程序，都可以叫作CGI程序语言。目前最为流行的CGI程序语言有四种：C，Shell,Perl和VisualBasic,其它一些语言也有许多人在用，如TCL,Fortran及AppleScript等。

3）CGI程序的执行

CGI 程序一般是个可执行程序。编译好的CGI程序一般要集中放在一个目录下。具体存放的位置随操作系统的不同而不同。CGI程序的执行一般有两种调用方式：第一种是通过URL直接调用，如：“http://202.114.2.182/cgi-win/cgi.exe”，在浏览器的URL栏里直接写入上述描述就可以调用该程序；另一种方式，也是主要的方式,是通过交互式主页里的FORM栏调用，通常都是用户在填完一张输入信息Form后按确认按钮启动CGI程序。

4）CGI工作的主要流程

CGI工作的主要流程是：1.一个用户请求激活一个CGI应用程序；2.CGI应用程序将交互主页里用户输入信息提取出来；3.将用户输入的信息传给服务器主机应用程序（如数据库查询〕；4.将服务器处理结果通过HTML文件返回给用户；5.CGI进程结束。

5）CGI的性能评价

CGI 的跨平台性能极佳，几乎可以在任何操作系统上实现，如DOS、WINDOWS、UNIX、OS/2、Macintosh等。实现CGI的编程语言也有很多选择。CGI的应用程序一般都是一个独立的可执行程序，和WWW服务器各自占据着不同的进程,而且一般一个CGI程序只能处理一个用户请求。这样，每有一个用户请求，都会激活一个CGI进程，当用户请求数量非常多时，会大量挤占系统的资源如内存，CPU时间等，造成效能低下。


###二 ISAPI原理及其性能###

1）ISAPI概念

ISAPI即Internet Server Application Program Interface，是微软提供的一套面向Internet服务的API接口，它能实现CGI能提供的全部功能，并在此基础上进行了扩展，如提供了过滤器应用程序接口。ISAPI 服务器扩展是可以被 HTTP 服务器加载和调用的 DLL。Internet 服务器扩展也称为 Internet 服务器应用程序 (ISA)，用于增强符合 Internet 服务器 API (ISAPI) 的服务器的功能。ISA 通过浏览器应用程序调用，并且将相似的功能提供给通用网关接口 (CGI) 应用程序。

2）ISAPI程序语言

由于开发ISAPI应用要用到微软的一套API,所以能用来开发ISAPI应用的语言不如CGI那么多。主要有VisualC++4.1以上版本,VisualBasic5.0、BorlandC++5.0也可以。

3）ISAPI原理

ISAPI 的工作原理和CGI大体上是相同的，都是通过交互式主页取得用户输入信息，然后交服务器后台处理。但是二者在实现机制上大相庭径。ISAPI与CGI最大的区别在于：不同于CGI，在ISAPI下建立的应用程序是以动态连接库的形式存在；而CGI的应用程序一般都是可执行程序。

4）ISAPI程序的执行

ISAPI 应用的工作流程与CGI有一些不同。ISAPI应用的DLL不仅可以象CGI程序一样被用户请求激活，还可以被系统预先激活来监视用户输入；对于被用户激活的DLL，在处理完一个用户请求后不会马上消失，而是继续驻留在内存中等待处理别的用户输入，直到过了一段时间后一直没有用户输入。

5）5ISAPI性能评价

一个ISAPI的DLL，可以在被用户请求激活后长驻内存，等待用户的另一个请求，还可以在一个DLL里设置多个用户请求处理函数，此外，ISAPI的DLL应用程序和WWW服务器处于同一个进程中，效率要显著高于CGI。不过ISAPI的平台兼容性较差，目前只能用于微软自己的Windows95和NT操作系统上，服务器平台也仅限于 IIS（InternetInformationServer)和MSpersonalwebserver以及NTworkstation上的 peerwebserver。

6）ISAPI 筛选器是什么？

ISAPI 筛选器是在启用 ISAPI 的 HTTP 服务器上运行的 DLL，用以筛选与服务器之间来回传送的数据。该筛选器注册事件的通知，例如登录或 URL 映射。当发生选定事件时，筛选器被调用，并且您可以监视及更改数据（在数据从服务器传输到客户端或相反的过程中）。可以使用 ISAPI 筛选器提供增强的 HTTP 请求记录（例如，跟踪登录到服务器的用户）、自定义加密、自定义压缩或其他身份验证方法。

7）ISAPI 服务器扩展和筛选器之间的区别是什么？

服务器扩展：在 URL 中引用时运行。被显式调用，例如用 http://myserver/myprog.dll?。被用户第一次调用时根据请求加载。

筛选器：为服务器处理的每个 URL 调用。如果发生已注册事件，自动为任何发送到服务器的 URL 运行。服务因其注册表项而启动时加载。     
     
服务器扩展和筛选器都：* 共享服务的处理空间。* 必须是线程安全的。* 一经加载便保留在内存中（直到服务停止或者内存被其他进程所需要）。


###三 ISAPI与CGI有哪些相同和不同之处？###

ISAPI 服务器扩展为使用 Internet 服务器的通用网关接口 (CGI) 应用程序提供了另一种选择。与 CGI 应用程序不同，ISAPI 在 HTTP 服务器所在的同一地址空间运行，并且可以访问可由 HTTP 服务器使用的所有资源。ISA 的系统开销比 CGI 应用程序低，因为它们不要求创建其他进程，也不执行需要越过进程边界的通信，而这种通信非常耗时。如果内存被其他进程所需要，扩展和筛选器 DLL 都可能被卸载。

Internet客户端通过HTTP服务器调用ISAPI的方法与调用CGI应用程序的方法一样。例如，客户端可以这样调用一个 CGI 应用程序：http://sample、example.exe?Param1&Param2  ，它可以这样调用一个执行相同功能的 ISAPI：http://sample/example.dll?Param1&Param2  。ISAPI 允许在一个DLL中有多个命令，这些命令作为DLL中CHttpServer 对象的成员函数来实现。CGI要求每个任务有一个单独的名称和一个到单独的可执行文件的URL映射。每个新的CGI请求启动一个新进程，而每个不同的请求包含在各自的可执行文件中，这些文件根据每个请求加载和卸载，因此系统开销高于ISA。

ISAPI 筛选器没有等效的 CGI 筛选器。筛选器提供预处理和后处理在客户端和服务器之间发送的所有数据的能力。

**FastCGI**

   1. FastCGI 像是一个常驻 (long-live) 型的 CGI，它可以一直执行着，只要激活后，不会每次都要花费时间去 fork 一次 (这是 CGI 最为人诟病的 fork-and-execute 模式)。

　 2. FastCGI 可在任何平台上使用，Netscape Enterprise 及 IIS 都有 FastCGI 的模块可供使用，阿帕契 (Apache，以及利用 Apache 衍生出做的服务器) 上也有 mod_fastcgi 可用。

　 3. FastCGI 支持 C/C++，Ruby, Perl，Tcl，Java，Python 等程序语言。

　 4. FastCGI 的应用程序亦兼容于 CGI。即 FastCGI 的应用程序也可以当成 CGI 来执行。

　 5. 现有的 CGI 程序要改写成 FastCGI 非常简单，最少可能只需要多加入三行程序代码。

　 6. FastCGI 的侦错方式与 CGI 大同小异，只要带入程序所需的环境变量及参数，即可在命令列模式执行或侦错。

　 7. FastCGI 应用程序的写作方式与 CGI 类似，除了几项原则要特别注意外，FastCGI 的写作方式跟 CGI 几乎一样，与学习 Web Server API 比较起来， FastCGI 简单多了。

　 8. FastCGI 支授分布式运算 (distributed computing)，即 FastCGI 程序可以在网站服务器以外的主机上执行并且接受来自其它网站服务器来的请求。

PHP的FastCGI使你的所有php应用软件通过mod_fastci运行，而不是mod_phpsusexec。FastCGI应用速度很快 是因为他们持久稳定。不必对每一个请求都启动和初始化。这使得应用程序的开发成为可能，否则在CGI范例是不切实际的（例如一个大型的脚本，或者一个需要 连接单个或多个数据库的应用）。

**好处**

PHP脚本运行速度更快(3到30倍)。PHP解释程序被载入内存而不用每次需要时从存储器读取，极大的提升了依靠脚本运行的站点的性能。

需要使用更少的系统资源。由于服务器不用每次需要时都载入PHP解释程序，你可以将站点的传输速度提升很高而不必增加cpu负担。

不需要对现有的代码作任何改变。现有的一切都适用于PHP的FastCGI

**潜在问题**

对所有的子目录（/home/USERNAME/public_html/php.ini）你只有一个可用的php.ini文件。 这是优化网站代码所必需的。如果你需要多个php.ini文件以适应不同的脚本需要，你可以在任何子目录禁用PHP的快速CGI，而其余的地方则继续有 效。如果你需要这样做请联系support。

你对PHP环境做的任何升级（如php.ini文件的改变）都有几分钟的延迟。这是因为为了更快的速度 你的php.ini文件已经被载入内存，而不是每次需要时再从存储器重新读取。
