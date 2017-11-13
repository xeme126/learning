


create table if not exists sysUser (uid integer primary key identity, users varchar(50), passw 
varchar(50), memos varchar(50), state tinyint )

insert into sysUser (users, passw, memos, state) values ('liujy-1-279939611878728','zhang-1-279939611878728','tests-1-279939611878728',1) 
1: insert into sysUser (users, passw, memos, state) values ('liujy-2-279939613201857','zhang-2-279939613201857','tests-2-279939613201857',1) 
2: insert into sysUser (users, passw, memos, state) values ('liujy-3-279939613340048','zhang-3-279939613340048','tests-3-279939613340048',1) 
3: insert into sysUser (users, passw, memos, state) values ('liujy-4-279939613465235','zhang-4-279939613465235','tests-4-279939613465235',1) 
4: insert into sysUser (users, passw, memos, state) values ('liujy-5-279939613589746','zhang-5-279939613589746','tests-5-279939613589746',1) 
5: insert into sysUser (users, passw, memos, state) values ('liujy-6-279939613716034','zhang-6-279939613716034','tests-6-279939613716034',1) 
6: insert into sysUser (users, passw, memos, state) values ('liujy-7-279939613839841','zhang-7-279939613839841','tests-7-279939613839841',1) 
7: insert into sysUser (users, passw, memos, state) values ('liujy-8-279939613963419','zhang-8-279939613963419','tests-8-279939613963419',1) 
8: insert into sysUser (users, passw, memos, state) values ('liujy-9-279939614088456','zhang-9-279939614088456','tests-9-279939614088456',1) 

select uid as userId, users as userName, passw as userPass, memos as Remark 
from sysUser where users like 'liujy%' limit 5 

update sysUser set passw='liujy' where uid = 11 



select * from sysUser order by 1 desc limit 15 offset 35
select * from sysUser order by 1 desc limit 15 offset 30
select * from sysUser order by 1 desc limit 5 offset 3
select * from sysUser order by 1 desc

select table_name as tbn, 1 as cnt from information_schema.tables where table_schema='PUBLIC'

SELECT 'sysUser' AS ROWS, COUNT(1) AS CNT from SYSUSER UNION ALL SELECT TABLE_NAME AS TBN, 1 AS CNT FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_SCHEMA='PUBLIC'

h2db & hsql

select * from information_schema.views
select * from information_schema.tables
select count(1) as cnt from information_schema.tables
select count(1) as cnt from information_schema.views

select * from information_schema.tables
select * from information_schema.views
select count(1) as cnt from information_schema.tables
select count(1) as cnt from information_schema.views

