---
title: Parameter number 1 is not an OUT parameter
categories: 
  - 编程
  - Java
  - Mybatis
  - Debug
date: 2020-09-02 11:57:29
updated: 2021-03-18 02:43:27
abbrlink: c5a0d373
---
<div id='my_toc'><a href="/blog/c5a0d373/#错误提示" class="header_1">错误提示</a>&nbsp;<br><a href="/blog/c5a0d373/#原因" class="header_1">原因</a>&nbsp;<br><a href="/blog/c5a0d373/#解决方案" class="header_1">解决方案</a>&nbsp;<br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
# 错误提示
今天复习的时候,运行以前的测试项目出现了如下错误:
<pre>
DEBUG [main] ==&gt;  Preparing: { <mark>call insert_user( ?, ?, ?, ? )</mark> } 
org.apache.ibatis.exceptions.PersistenceException: 
&#35;&#35;&#35; Error updating database.  Cause: java.sql.SQLException: <mark>Parameter number 1 is not an OUT parameter</mark>
&#35;&#35;&#35; SQL: { call insert_user( ?,         ?, ?, ? ) }
&#35;&#35;&#35; Cause: java.sql.SQLException: Parameter number 1 is not an OUT parameter
	at org.apache.ibatis.exceptions.ExceptionFactory.wrapException(ExceptionFactory.java:30)
	at org.apache.ibatis.session.defaults.DefaultSqlSession.update(DefaultSqlSession.java:200)
	at org.apache.ibatis.session.defaults.DefaultSqlSession.insert(DefaultSqlSession.java:185)
	at org.apache.ibatis.binding.MapperMethod.execute(MapperMethod.java:57)
	at org.apache.ibatis.binding.MapperProxy.invoke(MapperProxy.java:59)
	at com.sun.proxy.$Proxy2.inserUser(Unknown Source)
	at test.InserTest.main(InserTest.java:21)
Caused by: java.sql.SQLException: Parameter number 1 is not an OUT parameter
	at com.mysql.cj.jdbc.exceptions.SQLError.createSQLException(SQLError.java:129)
	at com.mysql.cj.jdbc.exceptions.SQLError.createSQLException(SQLError.java:97)
	at com.mysql.cj.jdbc.exceptions.SQLError.createSQLException(SQLError.java:89)
	at com.mysql.cj.jdbc.exceptions.SQLError.createSQLException(SQLError.java:63)
	at com.mysql.cj.jdbc.CallableStatement.checkIsOutputParam(CallableStatement.java:643)
	at com.mysql.cj.jdbc.CallableStatement.registerOutParameter(CallableStatement.java:1714)
	at com.mysql.cj.jdbc.CallableStatement.registerOutParameter(CallableStatement.java:1722)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.ibatis.logging.jdbc.PreparedStatementLogger.invoke(PreparedStatementLogger.java:78)
	at com.sun.proxy.$Proxy4.registerOutParameter(Unknown Source)
	at org.apache.ibatis.executor.statement.CallableStatementHandler.registerOutputParameters(CallableStatementHandler.java:110)
	at org.apache.ibatis.executor.statement.CallableStatementHandler.parameterize(CallableStatementHandler.java:94)
	at org.apache.ibatis.executor.statement.RoutingStatementHandler.parameterize(RoutingStatementHandler.java:64)
	at org.apache.ibatis.executor.SimpleExecutor.prepareStatement(SimpleExecutor.java:86)
	at org.apache.ibatis.executor.SimpleExecutor.doUpdate(SimpleExecutor.java:49)
	at org.apache.ibatis.executor.BaseExecutor.update(BaseExecutor.java:117)
	at org.apache.ibatis.executor.CachingExecutor.update(CachingExecutor.java:76)
	at org.apache.ibatis.session.defaults.DefaultSqlSession.update(DefaultSqlSession.java:198)
	... 5 more

</pre>

# 原因
这个项目需要调用数据库中的存储过程.由于是测试项目,我当时测试成功之后,就把对应的数据库表格和存储过程删除掉了。
今天测试的时候,我忘了事先在数据库中创建需要调用的存储过程`insert_user`。
# 解决方案
创建需要的数据库表格,创建需要的存储过程`insert_user`。
