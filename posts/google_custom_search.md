---
title: Google自定义搜索打造站内搜索引擎
date: '2013-02-21'
description: 如何打造站内搜索
categories: 搜索
tags: [google, 自定义搜索, sitemap generator ]
---

在网站中都必不可少的有“站内搜索”功能，这一功能，能非常方便的帮助他人在我们的网站上找到需要的文章和相关内容。而频繁的“站内搜索”，需要调用我们的数据库资源，增加服务器负担。今天，把这个“负担”转嫁给Google，利用谷歌Google强大的自定义搜索引擎功能为我们的网站服务。

##Google自定义搜索账号申请##

1、首先您需要登陆Google自定义搜索的账号申请页面：http://www.google.com.hk/cse/
，并点击右上角的“注册”按钮，进行注册。如果你有谷歌账号，直接登陆即可。

2、填写必要的账户注册信息，并同意接受Google服务条款和隐私权政策后，创建您的账户。

3、登陆Google自定义搜索，选择新建搜索引擎。
<p>
  <img src="{{urls.media}}/new_search_engines.jpg">
</p>

4、进入设置您的搜索引擎页面，请按以下步骤进行操作。

①描述您的搜索引擎：给您的站内搜索添加名称，和描述，语言请选择为中文简体。

②定义您的搜索引擎：这里我们输入要进行全站搜索的网站。（提醒注意→要搜索的网站填写格式为：www.***.com/*）

③选择版本：当然选择“标准版：免费，但需要在结果页上展示广告。”

④勾选“我已阅读并同意接受服务条款”，并点击下一步。
<p>
  <img src="{{urls.media}}/search_engines_basic.jpg">
</p>

5、选择或自定义样式。
<p>
  <img src="{{urls.media}}/search_engines_look.jpg">
</p>
##Google sitemap generator##

设置的自定义搜索，并不是马上就可以搜索了，还必须生成网站的sitemap。
https://www.google.com/webmasters/tools/