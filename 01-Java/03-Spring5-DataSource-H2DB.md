
create table if not exists sysUser (uid integer primary key auto_increment, users varchar(50) 
unique, passw varchar(50), memos varchar(50), state tinyint) 

insert into sysUser (users, passw, memos, state) values ('liujy-1-279517533506026','zhang-1-279517533506026','tests-1-279517533506026',1) ;
insert into sysUser (users, passw, memos, state) values ('liujy-2-279517534419495','zhang-2-279517534419495','tests-2-279517534419495',1) ;
insert into sysUser (users, passw, memos, state) values ('liujy-3-279517534541160','zhang-3-279517534541160','tests-3-279517534541160',1) ;
insert into sysUser (users, passw, memos, state) values ('liujy-4-279517534652116','zhang-4-279517534652116','tests-4-279517534652116',1) ;
insert into sysUser (users, passw, memos, state) values ('liujy-5-279517534759976','zhang-5-279517534759976','tests-5-279517534759976',1) ;
insert into sysUser (users, passw, memos, state) values ('liujy-6-279517534873457','zhang-6-279517534873457','tests-6-279517534873457',1) ;
insert into sysUser (users, passw, memos, state) values ('liujy-7-279517534983432','zhang-7-279517534983432','tests-7-279517534983432',1) ;
insert into sysUser (users, passw, memos, state) values ('liujy-8-279517535091044','zhang-8-279517535091044','tests-8-279517535091044',1) ;
insert into sysUser (users, passw, memos, state) values ('liujy-9-279517535200093','zhang-9-279517535200093','tests-9-279517535200093',1) ;

select uid as userId, users as userName, passw as userPass, memos as Remark 
from sysUser where users like 'liujy%' limit 5 

update sysUser set passw='liujy' where uid = 11 


select * from sysUser order by 1 desc limit 15 offset 35
select * from sysUser order by 1 desc limit 15 offset 30
select * from sysUser order by 1 desc limit 5 offset 3
select * from sysUser order by 1 desc

select table_name as tbn, 1 as cnt from information_schema.tables where table_schema='PUBLIC'

select 'sysUser' as rows, count(1) as cnt from sysUser 
union all 
select table_name as tbn, 1 as cnt from information_schema.tables where table_schema='PUBLIC'


h2db : select 1

h2db & hsql

select * from information_schema.views
select * from information_schema.tables
select count(1) as cnt from information_schema.tables
select count(1) as cnt from information_schema.views

select * from information_schema.tables
select * from information_schema.views
select count(1) as cnt from information_schema.tables
select count(1) as cnt from information_schema.views


http://blog.csdn.net/guicaizhou/article/details/51859500

//org.h2.jdbcx.JdbcDataSourceFactory
//org.h2.jdbcx.JdbcConnectionPool
//org.h2.jdbcx.JdbcDataSource
//H2 	H2 	org.h2.jdbcx.JdbcDataSource
//HSQLDB 	HSQLDB 	org.hsqldb.jdbc.JDBCDataSource
//		ds.getPooledConnection();
//		dataSource.url=jdbc:h2:./bin/afa/h2db.db2
//		dataSource.user=tests
//		dataSource.password=tests

org.h2.jdbcx.JdbcDataSource ds = new org.h2.jdbcx.JdbcDataSource();
ds.setURL("jdbc:h2:./bin/afa/h2db.db2");
ds.setUser("tests");
ds.setPassword("tests");

Context ctx;
try {
ctx = new InitialContext();
ctx.bind("jdbc/ds_h2db", ds);
} catch (NamingException e) { 
e.printStackTrace();
}


连接内嵌模式的数据库
"jdbc:h2:file:D:/test"  连接自定目录下的指定数据库
"jdbc:h2:~/test" 连接默认目录下的指定数据库
连接内存模式的数据库
jdbc:h2:mem:test
连接server模式的数据库
jdbc:h2:tcp://localhost/~/test
ssl连接数据库
jdbc:h2:ssl://localhost/~/test
连接压缩文件内的数据库
jdbc:h2:zip:D:/test.zip!/test 


