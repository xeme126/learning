
https://db-engines.com/en/ranking
https://db-engines.com/en/ranking

SQL和NoSQL数据库只是用不同的方式来完成相同的事情。
我们可能会先选择其中之一然后更换到另一个上，但是在选择之前制定一个计划将会节约许多的时间和金钱。

适合使用SQL开发的项目：
    可以预先定义逻辑相关的离散数据的需求
    数据一致性是必要的
    具有良好的开发者经验和技术支持的标准的成熟技术

适合使用NoSQL开发的项目：

    不相关，不确定和逐步发展的数据需求
    更简单或者更宽松的能够快速开始编程的项目
    速度和可扩展性至关重要的
			 
各种驱动的连接方法：
1. MySQL(http://www.mysql.com) mysql-connector-java-2.0.14-bin.jar ;
  Class.forName( "org.gjt.mm.mysql.Driver" );
  cn = DriverManager.getConnection( "jdbc:mysql://MyDbComputerNameOrIP:3306/myDatabaseName", sUsr, sPwd ); 
2. PostgreSQL(http://www.de.postgresql.org) pgjdbc2.jar ;
  Class.forName( "org.postgresql.Driver" ); 
  cn = DriverManager.getConnection( "jdbc:postgresql://MyDbComputerNameOrIP/myDatabaseName", sUsr, sPwd ); 
3. Oracle(http://www.oracle.com/ip/deploy/database/oracle9i/) classes12.zip ;
  Class.forName( "oracle.jdbc.driver.OracleDriver" ); 
  cn = DriverManager.getConnection( "jdbc:oracle:thin:MyDbComputerNameOrIP:1521:ORCL", sUsr, sPwd ); 
4. Sybase(http://jtds.sourceforge.net) jconn2.jar ;
  Class.forName( "com.sybase.jdbc2.jdbc.SybDriver" ); 
  cn = DriverManager.getConnection( "jdbc:sybase:Tds:MyDbComputerNameOrIP:2638", sUsr, sPwd ); 
  //(Default-Username/Password: "dba"/"sql") 
5. Microsoft SQLServer(http://jtds.sourceforge.net) ;
  Class.forName( "net.sourceforge.jtds.jdbc.Driver" ); 
  cn = DriverManager.getConnection( "jdbc:jtds:sqlserver://MyDbComputerNameOrIP:1433/master", sUsr, sPwd ); 
6. Microsoft SQLServer(http://www.microsoft.com) ;
  Class.forName( "com.microsoft.jdbc.sqlserver.SQLServerDriver" ); 
  cn = DriverManager.getConnection( "jdbc:microsoft:sqlserver://MyDbComputerNameOrIP:1433;databaseName=master", 

sUsr, sPwd ); 
7. ODBC 
  Class.forName( "sun.jdbc.odbc.JdbcOdbcDriver" ); 
  Connection cn = DriverManager.getConnection( "jdbc:dbc:" + sDsn, sUsr, sPwd ); 
8.DB2 Class.forName("com.ibm.db2.jdbc.net.DB2Driver"); 
  String url="jdbc:db2://192.9.200.108:6789/SAMPLE" 
  cn = DriverManager.getConnection( url, sUsr, sPwd ); 
9.access由于access并不是作为一项服务运行，所以url的方法对他不适用。access可以通过odbc，也可以通过服务器映射路径的形式 找到.mdb文件


各种数据库使用JDBC连接的方式，可以作为一个手册使用。 
1、Oracle8/8i/9i数据库（thin模式） 
Class.forName("oracle.jdbc.driver.OracleDriver").newInstance(); 
String url="jdbc:oracle:thin:@localhost:1521:orcl"; //orcl为数据库的SID 
String user="test"; 
String password="test"; 
Connection conn= DriverManager.getConnection(url,user,password);
2、DB2数据库 
Class.forName("com.ibm.db2.jdbc.app.DB2Driver ").newInstance(); 
String url="jdbc:db2://localhost:5000/sample"; //sample为你的数据库名 
String user="admin"; 
String password=""; 
Connection conn= DriverManager.getConnection(url,user,password);
3、Sql Server7.0/2000数据库 
Class.forName("com.microsoft.jdbc.sqlserver.SQLServerDriver").newInstance(); 
String url="jdbc:microsoft:sqlserver://localhost:1433;DatabaseName=mydb"; 
//mydb为数据库 
String user="sa"; 
String password=""; 
Connection conn= DriverManager.getConnection(url,user,password);
4、Sybase数据库 
Class.forName("com.sybase.jdbc.SybDriver").newInstance(); 
String url =" jdbc:sybase:Tds:localhost:5007/myDB";//myDB为你的数据库名 
Properties sysProps = System.getProperties(); 
SysProps.put("user","userid"); 
SysProps.put("password","user_password"); 
Connection conn= DriverManager.getConnection(url, SysProps);
5、Informix数据库 
Class.forName("com.informix.jdbc.IfxDriver").newInstance(); 
String url = "jdbc:informix-sqli://123.45.67.89:1533/myDB:INFORMIXSERVER=myserver; 
user=testuser;password=testpassword"; //myDB为数据库名 
Connection conn= DriverManager.getConnection(url);
6、MySQL数据库 
Class.forName("org.gjt.mm.mysql.Driver").newInstance(); 
String url ="jdbc:mysql://localhost/myDB?user=soft&password=soft1234&useUnicode=true&characterEncoding=8859_1" 
//myDB为数据库名 
Connection conn= DriverManager.getConnection(url);
7、PostgreSQL数据库 
Class.forName("org.postgresql.Driver").newInstance(); 
String url ="jdbc:postgresql://localhost/myDB" //myDB为数据库名 
String user="myuser"; 
String password="mypassword"; 
Connection conn= DriverManager.getConnection(url,user,password);
8、access数据库直连用ODBC的
Class.forName("sun.jdbc.odbc.JdbcOdbcDriver") ;
String url="jdbc:odbc:Driver={MicroSoft Access Driver 

(*.mdb)};DBQ="+application.getRealPath("/Data/ReportDemo.mdb");
Connection conn = DriverManager.getConnection(url,"","");
Statement stmtNew=conn.createStatement() ;
 