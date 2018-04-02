

<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <version>1.4.196</version>
</dependency>

<dependency>
  <groupId>hsqldb</groupId>
  <artifactId>hsqldb</artifactId>
  <version>1.8.0.10</version>
</dependency>

<dependency>
  <groupId>org.firebirdsql.jdbc</groupId>
  <artifactId>jaybird</artifactId>
  <version>2.1.6</version>
</dependency>

https://www.zybuluo.com/liyuj/note/230739
https://www.zybuluo.com/liyuj/note/230739

			 
https://bitbucket.org/xerial/sqlite-jdbc
https://bitbucket.org/xerial/sqlite-jdbc/downloads download SQLite3 jdbc
-------------------------------------
### sqlite3 ###
-------------------------------------
select * from sqlite_master ;

create table if not exists tba
(kid integer primary key autoincrement, kws varchar(50), vals varchar(50));

drop table if exists tb0 ;
create table if not exists tb0
(kid integer primary key autoincrement, kws varchar(50), vals varchar(50));
insert into tb0 (kws, vals) values ('tests1', 'tests1'), ('tests2', 'tests2'); 

drop table if exists tb3 ;
create table if not exists tb3
(kid integer primary key autoincrement, kws varchar(50), vals varchar(50));
insert into tb3 (kws, vals) values ('tests1', 'tests1'), ('tests2', 'tests2'); 
select * from tb3;

drop index uniq_tb0;
create unique index uniq_tb0 on tb0 (kws);

create cluster index idx_tba on tba (vals desc) ;

-------------------------------------
### h2db ###
-------------------------------------
select * from information_schema.views
select * from information_schema.tables
select * from information_schema.columns

create table if not exists tb0
(kid integer primary key auto_increment, kws varchar(50), vals varchar(50));

alter table tb0 add CONSTRAINT uniq_tba UNIQUE (kws);
insert into tb0 (kws, vals) values ('tests1', 'tests1'), ('tests2', 'tests2'); 
create index idx_tb0 on tb0 (vals desc);
insert into tb0 (kws, vals) values ('tests11', 'tests1'), ('tests22', 'tests2'); 

drop table if exists tb3;
create table if not exists tb3
(kid integer primary key auto_increment, kws varchar(50), vals varchar(50));


-------------------------------------
### hsqldb ###
-------------------------------------
select * from information_schema.views
select * from information_schema.tables
select * from information_schema.columns
create table if not exists tba
(kid integer primary key identity, kws varchar(50), vals varchar(50));
create table if not exists tb0
(kid integer primary key identity, kws varchar(50), vals varchar(50));
insert into tba (kws, vals) values ('tests1', 'tests1'), ('tests2', 'tests2');
create table if not exists tb1
(kid integer primary key identity, kws varchar(50) unique, vals varchar(50));
insert into tb1 (kws, vals) values ('tests1', 'tests1'), ('tests2', 'tests2');
create table if not exists tb2
(kid integer primary key identity, kws varchar(50) unique, vals varchar(50)); 
insert into tb2 (kws, vals) values ('tests1', 'tests1'), ('tests2', 'tests2');

alter table tba add CONSTRAINT uniq_tba UNIQUE (kws);
insert into tba (kws, vals) values ('tests1', 'tests1'), ('tests2', 'tests2'); 
create index idx_tba on tba (vals desc)

create table if not exists myUser 
(userId integer primary key identity, users varchar(50), passw varchar(50), 
birth integer, email varchar(50), mobile varchar(50), phone varchar(50));
insert into myUser (users, passw, birth, email, mobile, phone)
values ('liujy', 'ljy321', '19920101', 'tests@fa.com', 'aaa', 'bbb');


drop table if exists tb3;
create table if not exists tb3
(kid integer primary key identity, kws varchar(50), vals varchar(50));
-------------------------------------


###SQLite3自增字段### 
create table if not exists ttb01 (kid integer primary key autoincrement , kws varchar(50) unique, kvs varchar(50)); 
update myUser set users=users||"-"||passw where users = ? ;

###H2DB自增字段### 
create table tba userid bigint auto_increment primary key, users varchar(32), passw varchar(32)); 
select last_insert_rowid(); 
###HSQLDB自增字段### 
create table tba (kid INTEGER NOT NULL PRIMARY KEY IDENTITY, kws varchar(30), kvs varchar(30) ); 
create table tbb (kid BIGINT NOT NULL PRIMARY KEY IDENTITY, kws varchar(30), kvs varchar(30) ); 
###HSQLDB自增字段### 
create table tba (kid INTEGER NOT NULL PRIMARY KEY IDENTITY, kws varchar(30), kvs varchar(30) ); 
create table tbb (kid BIGINT NOT NULL PRIMARY KEY IDENTITY, kws varchar(30), kvs varchar(30) ); 

###SQL2000自增字段### 
create table tba (userid integer identity(1,1) PRIMARY KEY, users varchar(32), passw varchar(32)); 
###SQLite3自增字段### 
create table if not exists tba (kid integer primary key autoincrement , kws varchar(50), kvs varchar(50)); 
###MySQL5自增字段### 
create table tba (userid bigint auto_increment primary key, users varchar(32), passw varchar(32)) 
ENGINE=InnoDB DEFAULT CHARSET=utf8 ; 
ENGINE=MyISAM DEFAULT CHARSET=utf8 
### MYSQL5 自增字段 ### 
create table if not exists tba (userid integer auto_increment primary key, users varchar(32), passw varchar(32)) 
ENGINE=InnoDB DEFAULT CHARSET=utf8 ; 

h2,mysql支持 select last_insert_id(); 
### MYSQL5导入数据 ### 
load data local infile 'E:\\dns\\rite\\20141217-rdns.txt' into table dns fields terminated by ','; 
