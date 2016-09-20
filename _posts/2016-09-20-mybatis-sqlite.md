---
layout: post
title:  Mybatis 和 Sqlite 配置使用
categories: [java]
tags:	[java,sqlite,mybatis]
---
<p> 在Android项目开发过程中，用到默认 base 数据。其中一种做法是，把这些数据存到 base.db sqlite0.
数据库文件中，将base.db文件放置到assets目录下。在首次启动应用时，将base.db 拷贝到SDcard或/data/data/xxx/databases目录下使用。
</p>
<p>
	往往有的时候这写数据靠手动处理会很麻烦，因此可用通过使用java代码来构造。这时Mybatis和Sqlite是一个不错的选择。
</p>

#### 准备
*	工具
	-	SqlitStudio
	-	eclipse
* 	 jar lib

jar lib                  |作用
------------             | -------------
sqlite-jdbc-3.8.11.2.jar | jdbc 连接 sqlite 数据库
mybatis-3.0.6.jar        | orm 持久化
log4j-1.2.15.jar         | 控制台打印执行SQL语句

# 未完待续。。。
[sqlite-jdbc](https://github.com/xerial/sqlite-jdbc)

完整代码地址 [:cyclone:](https://github.com/liaodongxiaoxiao/MybatisSqlite)