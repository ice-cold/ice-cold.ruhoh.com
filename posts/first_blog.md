---
title: First blog
date: '2013-02-19'
description: 如何使用ruhoh，Github搭建个人博客
categories: How to
tags: [ruhoh, Markdown, git, github, windows ]
---

## 开始博客 ##

**第一篇就记录一下[如何使用ruhoh，Github搭建个人博客](http://ice-cold.ruhoh.com/how-to/first-blog/)**


首先介绍一下如何基于开源的ruhoh搭建一个人博客，以及为什么选择[Ruhoh静态博客](http://ruhoh.com/)。

如果你是一名开源爱好者，一定不会错过[github.com](http://github.com)，如果你还没有开源项目怎么办？那就不妨从学习使用入手，用它来搭建一个个人博客或许是个不错的开始。


## 为什么是Ruhoh+github+markdown ##

提起博客系统你最先想到的可能会是Wordpress，但用静态网站生成系统来做个人的博客还是非常值得尝试的，并且可以结合强大的版本控制系统，纯文本，方便备份，离线也可以编辑和预览，还有markdown的易读性，但前提是你要有一颗折腾的起的心:-)

说起Ruhoh就不得不提一下Jekll，Jekyll的作者（也是GitHub的共同创始人）Tom Preston-Werner曾写过一篇博文 [Blogging like a hacker ](http://tom.preston-werner.com/2008/11/17/blogging-like-a-hacker.html)（中文翻译《 [像黑客一样写博客](http://kyle.xlau.org/posts/blogging-like-a-hacker.html) 》 by Kylexlau）。而Ruhoh和[Jekyll-Bootstrap](http://jekyllbootstrap.com/)是同一位作者。他是这么介绍Ruhoh的：

*ruhoh is an exercise in [sharing](http://sivers.org/sharing).*

*ruhoh is inspired by Jekyll and designed based on everything I learned from creating [jekyllbootstrap.com](jekyllbootstrap.com).*

*ruhoh is the next iteration of what I think static, technical blogging can be.*

Ruhoh安装部署非常容易，在这之前你也可以先看看[Jekyll](http://jekyllrb.com/)（发音/'dʒiːk əl/，"杰克尔"）之类的博客生成系统的工作方式。

## 安装Ruhoh ##

**1. 安装配置github for windows**

GitHub 使用 git 分布式版本控制系统，而 git 最初是 Linus Torvalds 为帮助 Linux 开发而创造的，它针对的是 Linux 平台，因此 git 和 Windows 从来不是最好的朋友。幸好 GitHub 发布了 [GitHub for Windows](https://github.com/blog/1127-github-for-windows)，为 Windows 平台开发者提供了一个易于使用的 Git 图形客户端。

GitHub for Windows 是一个 Metro 风格应用程序，集成了自包含版本的 Git，bash 命令行 shell，PowerShell 的 posh-git 扩展。GitHub 为 Windows 用户提供了一个基本的图形前端去处理大部分常用版本控制任务，可以创建版本库，向本地版本库递交补丁，在本地和远程版本库之间同步。微软也通过 CodePlex 向开发者提供 git 版本控制系统，而 GitHub 现在创造了一个更具有吸引力的 Windows 版本。

对于windows用户来说也可以安装[msysgit](http://msysgit.github.com/)，这也是一个托管在github上的站点。

对于新手来说，在github上搭建Ruhoh基本上是follow-and-do。

1.在githhub上注册[免费帐号](https://github.com/signup/free)。

2.[host you blog](http://ruhoh.com/docs/1/publish/)，发布你的博客站点。
	
	创建你博客的 github 仓库
	Add webhook(发布你的博客站点)

**2. ruhoh本地安装**

ruhoh 是一个 ruby 的套件，因此可通过 gem 來安装。在 Windows 平台下安装 Ruby 有几个选择。第一个选择是仅安装编译好的二进制文件。第二个选择是直接执行“一步安装”程序，假如您不知道如何安装 Ruby,[RubyInstaller](http://rubyinstaller.org/)将是您最好的选择。（这种安装方式除 Ruby 之外，捆绑一些额外的资源库。）你还需要先安装[ RubyInstaller DevKit](http://wiki.github.com/oneclick/rubyinstaller/development-kit)。

ruhoh gem依赖于：

    rack - for web-server integration
    directory_watcher - for watching files for updates in realtime.
    mustache - for templating.
    redcarpet - for Markdown parsing.
    nokogiri - for HTML handling and RSS support.

打开Git Shell(安装GitHub for windows时带的)，进去之后可以看到是windows powershell，但支持git等命令，我们可以查看当前安装过的ruby和gem的版本(这里假设安装到C:\Dev下)，并执行：

	$gem install ruhoh 


安装后可以输入以下命令确认是否安装成功。

	$ruhoh help

本地运行Ruhoh:

	$git clone git://github.com/ruhoh/blog.git USERNAME.ruhoh.com

	$cd USERNAME.ruhoh.com

	$rackup -p 9292

打开浏览器访问http://localhost:9292/ 就能看到默认页面。

或者将你的rep推送到github:

	$git clone git://github.com/ruhoh/blog.git USERNAME.ruhoh.com

	$cd USERNAME.ruhoh.com

	$git remote set-url origin git@github.com:USERNAME/USERNAME.ruhoh.com.git

	$git push origin master

Your blog is now available at: http://USERNAME.ruhoh.com。

接下来创建第一篇博文：

	$ruhoh post first_blog

	#将步骤放在first_blog.me中

	$git add posts/first_blog.me        

	$git commit 

	$git push origin master




**Reference**

1. [Git基础](http://www.open-open.com/lib/view/open1328069733264.html)

2. [Git的深入理解与GitHub托管服务的使用](http://www.cnblogs.com/cocowool/archive/2012/02/17/2356125.html)

3. [如何确认Devkit是否安装成功](http://blog.yuaz.net/page/5)

4. [Ruhoh 札记](http://dourok.info/2012/08/20/something-about-ruhoh/)

5. [Jekyll入门](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)

5. [Octopress 笔记](http://netwjx.github.com/blog/2012/03/18/octopress-note/)

6. [如何高效利用GitHub](http://www.yangzhiping.com/tech/github.html)

7. [Github Pages](https://help.github.com/categories/20/articles)