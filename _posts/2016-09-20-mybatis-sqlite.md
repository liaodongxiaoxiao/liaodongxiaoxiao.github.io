---
layout: post
title:  Mybatis 和 Sqlite 配置使用
categories: [java]
tags:	[java,sqlite,mybatis]
---
<p> 在Android项目开发过程中，用到默认 base 数据。其中一种做法是，把这些数据存到 `base.db`  sqlite数据库文件中，将base.db文件放置到assets目录下。在首次启动应用时，将base.db 拷贝到SDcard或/data/data/xxx/databases目录下使用。
</p>

>靠手动处理会很麻烦，因此可用通过使用java代码来构造。这时Mybatis和Sqlite是
>一个不错的选择。

#### 准备
*	工具
	-	SqlitStudio 
	-	eclipse
* 	 jar 包

|jar lib                   |作用                    |
|:------------             |:-------------          |
|sqlite-jdbc-3.8.11.2.jar  | jdbc 连接 sqlite 数据库|
|mybatis-3.0.6.jar         | orm 持久化             |
|log4j-1.2.15.jar          | 控制台打印执行SQL语句  |

#### 步骤
1. 通过使用SqliteStudio创建需求的数据结构的db文件，并将db文件拷贝到src路径下
2. 创建mybatis db配置文件
*src/db.properties*

```java
jdbc.driverClassName=org.sqlite.JDBC
jdbc.name=user.db
jdbc.url=jdbc:sqlite:src/user_test.db 
#指定db所在的路径 jdbc.url=jdbc:sqlite:E:/user_test.db
jdbc.username=
jdbc.password=
```
3.	配置Mybatis
```html
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
	<!-- 引用db.properties配置文件 -->
	<properties resource="db.properties" />
	<!-- development : 开发模式 work : 工作模式 -->
	<environments default="development">
		<environment id="development">
			<transactionManager type="JDBC" />
			<!-- 配置数据库连接信息 -->
			<dataSource type="POOLED">
				<!-- value属性值引用db.properties配置文件中配置的值 -->
				<property name="driver" value="${jdbc.driverClassName}"/>
				<property name="url" value="${jdbc.url}"/>
				<property name="username" value="${jdbc.username}"/>
				<property name="password" value="${jdbc.password}"/>
			</dataSource>
		</environment>
	</environments>
	<mappers>
 		<!--指定mapper对应的xml -->   
    		<mapper resource="com/ldxx/ms/orm/User.xml" />  
	</mappers>
</configuration>
```
4.	配置log4j文件，参考demo
5.	编写DBUtils工具类，加载Mybatis配置，提供SqlSession对象
```java
public class DBUtils {
	private static SqlSession sqlSession = null;

	static {
		try {
			// 加载配置文件
			Reader reader = Resources.getResourceAsReader("mybatis.xml");
			SqlSessionFactory sqlMapper = new SqlSessionFactoryBuilder().build(reader);
			//设置为true 自动提交事务
			sqlSession = sqlMapper.openSession(true);
			reader.close();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}

	private DBUtils() {
	}

	public static SqlSession getSqlSession() {
		return sqlSession;
	}
}
```
6. 在创建Dao对象时，传入SqlSession对象

更多详情请参考，[完整代码-github](https://github.com/liaodongxiaoxiao/MybatisSqlite)

[sqlite-jdbc](https://github.com/xerial/sqlite-jdbc)

