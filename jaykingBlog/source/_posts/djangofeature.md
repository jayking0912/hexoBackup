---
title: django优缺点
date: 2017-04-02 14:15:32
tags: django
categories: web后端
---



Django 大包大揽，用它来快速开发一些 Web 应用是不错的。如果你顺着 [Django](http://www.nowamagic.net/academy/tag/Django) 的设计哲学来，你会觉得 Django 很好用，越用越顺手；相反，你如果不能融入或接受 Django 的设计哲学，你用 Django 一定会很痛苦，趁早放弃的好。所以说在有些人眼里 Django 无异于仙丹， 但对有一些人来说它又是毒药且剧毒。

先说[缺点](http://www.nowamagic.net/academy/tag/%E7%BC%BA%E7%82%B9)：

- 系统紧耦合，如果你觉得 Django 内置的某项功能不是很好，想用喜欢的第三方库来代替是很难的，比如下面将要说的 ORM、Template。要在 Django 里用 SQLAlchemy 或 Mako 几乎是不可能，即使打了一些补丁用上了也会让你觉得非常非常别扭。
- Django 自带的 ORM 远不如 SQLAlchemy 强大，除了在 Django 这一亩三分地，SQLAlchemy 是 Python 世界里事实上的 ORM 标准，其它框架都支持 SQLAlchemy 了，唯独 Django 仍然坚持自己的那一套。Django 的开发人员对 SQLAlchemy 的支持也是有过讨论和尝试的，不过最终还是放弃了，估计是代价太高且跟 Django 其它的模块很难合到一块。
- Template 功能比较弱，不能插入 Python 代码，要写复杂一点的逻辑需要另外用 Python 实现 Tag 或 Filter。
- 让人纠结的 auth 模块，Django 的 auth 跟其它模块结合紧密，功能也挺强的，就是做的有点过了，用户的数据库 schema 都给你定好了，这样问题就来了，比如很多网站要求 email 地址唯一，可 schema 里这个字段的值不是唯一的，纠结是必须的了。
- 核心开发团队似乎比较顽固，除了说第三方库难使用，据说历史上 ORM API 繁琐（后来按 ActiveRecord 风格重写），曾经对 ajax 热潮也不怎么当回事。
- 周边资源不够发达，其实说来说去有些相关，这个是第三方库比较难融合相关的，没有很好的插件体系。虽然官方文档还不错，但是相关书籍很资料相比 rails 等并不多。
- 早前有说没有结合测试框架，最新的 1.5 肯定是有了。不过个人判断又是反应迟钝的一个表现。不过个人也不喜欢测试太重，这点跟作者想法比较一致。

再来看看一些优点：

- 自助管理后台，admin interface 是Django 里比较吸引眼球的一项 contrib，让你几乎不用写一行代码就拥有一个完整的后台管理界面。
- 虽然 Django 自带的 ORM 不如 SQLAlchemy 强大，但也不弱。一般来说可以不怎么使用 SQL 语句，每条记录都是一个对象，而取对象的关联，易如反掌。
- URL design，Django 的 url 模块设计得看似很复杂，都是使用正则表达式，但真正用到的都是很简单的正则，等你用到一定程度的时候，发现这块东西，做的很细致，地址的表达上，你可以随心所欲，那些优美的，简洁的，专业的地址，不管哪种，你都能表现出来。
- Django 的 App 理念很好。App 可插拔，是不可多得的思想。不需要了，可以直接删除，对系统影响不大。
- Django 的错误提示做的足够详细了，我有时喜欢上 Django 的出错页面了，那页面先不说有多详细，但光页面的美观上就是一种享受。有时，Django 的错误提示信息，让你马上就能知道在那个页面哪行代码出错了。