
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <version>1.4.196</version>
</dependency>


H2数据库支持如下3种连接模式：
内嵌模式（通过JDBC进行本地连接，应用和数据库在同一个JVM中）
服务器模式（通过JDBC或ODBC或TCP/IP进行远程连接）
混合模式（同时支持本地和远程连接）

import org.h2.jdbcx.JdbcDataSource;
import javax.naming.Context;
import javax.naming.InitialContext;
JdbcDataSource ds = new JdbcDataSource();
ds.setURL("jdbc:h2:?/test");
ds.setUser("sa");
ds.setPassword("sa");
Context ctx = new InitialContext();
ctx.bind("jdbc/dsName", ds);

import java.sql.Connection;
import javax.sql.DataSource;
import javax.naming.Context;
import javax.naming.InitialContext;
Context ctx = new InitialContext();
DataSource ds = (DataSource) ctx.lookup("jdbc/dsName");
Connection conn = ds.getConnection();

<bean id="h2Server" class="org.h2.tools.Server" factory-method="createTcpServer"
	init-method="start" destroy-method="stop">
	<constructor-arg value="-tcp,-tcpAllowOthers,-tcpPort,8043" />
</bean>

<context-param>
	<param-name>db.tcpServer</param-name>
	<param-value>-tcpAllowOthers</param-value>
</context-param>

<listener>
	<listener-class>org.h2.server.web.DbStarter</listener-class>
</listener>

<context-param>
	<param-name>db.url</param-name>
	<param-value>jdbc:h2:r:/h2db/awbprint/x4z5gjb3</param-value>
</context-param>
<context-param>
	<param-name>db.user</param-name>
	<param-value>sa</param-value>
</context-param>
<context-param>
	<param-name>db.password</param-name>
	<param-value>sa</param-value>
</context-param>
<context-param>
	<param-name>db.tcpServer</param-name>
	<param-value>-tcpAllowOthers</param-value>
</context-param>


H2, the Java SQL database. The main features of H2 are:
    Very fast, open source, JDBC API
    Embedded and server modes; in-memory databases
    Browser based Console application
    Small footprint: around 1.5 MB jar file size

Version 1.4.195 (2017-04-23), Last Stable
Version 1.4.196 (2017-06-10)

Database Files Encryption
The database files can be encrypted. Three encryption algorithms are supported:
    "AES"  - also known as Rijndael, only AES-128 is implemented.
    "FOG"  - pseudo-encryption only useful for hiding data from a text editor.
    "XTEA" - the 32 round version.

Class.forName("org.h2.Driver");
String url = "jdbc:h2:~/test;CIPHER=AES";
String user = "sa";
String pwds = "filepwd userpwd";
conn = DriverManager.getConnection(url, user, pwds);

java -cp h2*.jar org.h2.tools.ChangeFileEncryption -dir ~ -db test -cipher AES -encrypt filepwd

### Opening a Database Only if it Already Exists
String url = "jdbc:h2:/data/sample;IFEXISTS=TRUE";
### Don't Close a Database when the VM Exits
String url = "jdbc:h2:~/test;DB_CLOSE_ON_EXIT=FALSE";
### Execute SQL on Connection
String url = "jdbc:h2:mem:test;INIT=runscript from '~/create.sql'\\;runscript from '~/init.sql'";

Database URLs
Embedded
jdbc:h2:~/test 'test' in the user home directory
jdbc:h2:/data/test 'test' in the directory /data
jdbc:h2:test in the current(!) working directory

In-Memory
jdbc:h2:mem:test multiple connections in one process
jdbc:h2:mem: unnamed private; one connection

Server Mode
jdbc:h2:tcp://localhost/~/test user home dir
jdbc:h2:tcp://localhost//data/test absolute dir
Server start:java -cp *.jar org.h2.tools.Server

Settings
jdbc:h2:..;MODE=MySQL compatibility (or HSQLDB,...)
jdbc:h2:..;TRACE_LEVEL_FILE=3 log to *.trace.db

Topic URL Format and Examples
Embedded (local) connection
jdbc:h2:file:][<path>]<databaseName>
jdbc:h2:~/test
jdbc:h2:file:/data/sample
jdbc:h2:file:C:/data/sample (Windows only)

In-memory (private)   jdbc:h2:mem:
In-memory (named)   jdbc:h2:mem:<databaseName>
jdbc:h2:mem:test_mem

Server mode (remote connections) using TCP/IP
jdbc:h2:tcp://<server>[:<port>]/[<path>]<databaseName>
jdbc:h2:tcp://localhost/~/test
jdbc:h2:tcp://dbserv:8084/~/sample
jdbc:h2:tcp://localhost/mem:test

Server mode (remote connections) using TLS
jdbc:h2:ssl://<server>[:<port>]/<databaseName>
jdbc:h2:ssl://localhost:8085/~/sample;

Using encrypted files   jdbc:h2:<url>;CIPHER=AES
jdbc:h2:ssl://localhost/~/test;CIPHER=AES
jdbc:h2:file:~/secure;CIPHER=AES

File locking methods  jdbc:h2:<url>;FILE_LOCK={FILE|SOCKET|NO}
jdbc:h2:file:~/private;CIPHER=AES;FILE_LOCK=SOCKET
Only open if it already exists  jdbc:h2:<url>;IFEXISTS=TRUE
jdbc:h2:file:~/sample;IFEXISTS=TRUE

Don't close the database when the VM exits
jdbc:h2:<url>;DB_CLOSE_ON_EXIT=FALSE
Execute SQL on connection
jdbc:h2:<url>;INIT=RUNSCRIPT FROM '~/create.sql'
jdbc:h2:file:~/sample;INIT=RUNSCRIPT FROM '~/create.sql'\;RUNSCRIPT FROM '~/populate.sql'

User name and/or password
jdbc:h2:<url>;USER=<username>][;PASSWORD=<value>]
jdbc:h2:file:~/sample;USER=sa;PASSWORD=123

Debug trace settings
jdbc:h2:<url>;TRACE_LEVEL_FILE=<level 0..3>
jdbc:h2:file:~/sample;TRACE_LEVEL_FILE=3

Ignore unknown settings
jdbc:h2:<url>;IGNORE_UNKNOWN_SETTINGS=TRUE

Custom file access mode
jdbc:h2:<url>;ACCESS_MODE_DATA=rws

Database in a zip file
jdbc:h2:zip:<zipFileName>!/<databaseName>
jdbc:h2:zip:~/db.zip!/test

Compatibility mode
jdbc:h2:<url>;MODE=<databaseType>
jdbc:h2:~/test;MODE=MYSQL

Auto-reconnect
jdbc:h2:<url>;AUTO_RECONNECT=TRUE
jdbc:h2:tcp://localhost/~/test;AUTO_RECONNECT=TRUE

Automatic mixed mode
jdbc:h2:<url>;AUTO_SERVER=TRUE
jdbc:h2:~/test;AUTO_SERVER=TRUE

Page size
jdbc:h2:<url>;PAGE_SIZE=512

Changing other settings
jdbc:h2:<url>;<setting>=<value>[;<setting>=<value>...]
jdbc:h2:file:~/sample;TRACE_LEVEL_SYSTEM_OUT=3


### Using the JDBC API

Class.forName("org.h2.Driver");
Connection conn = DriverManager.
    getConnection("jdbc:h2:~/test");
conn.close();

### Connection Pool
import org.h2.jdbcx.JdbcConnectionPool;
JdbcConnectionPool cp = JdbcConnectionPool.
    create("jdbc:h2:~/test", "sa", "sa");
Connection conn = cp.getConnection();
conn.close(); cp.dispose();

### TopLink and Glassfish
Datasource class: org.h2.jdbcx.JdbcDataSource
oracle.toplink.essentials.platform.
database.H2Platform


### Using h2database in Web Applications
#(1) Embedded Mode
#(2) Server Mode

### Using a Servlet Listener to Start and Stop a Database
<listener>
    <listener-class>org.h2.server.web.DbStarter</listener-class>
</listener>

### DbStarter can also start the TCP server, use the parameter db.tcpServer in the file web.xml.
<context-param>
    <param-name>db.url</param-name>
    <param-value>jdbc:h2:~/test</param-value>
</context-param>
<context-param>
    <param-name>db.user</param-name>
    <param-value>sa</param-value>
</context-param>
<context-param>
    <param-name>db.password</param-name>
    <param-value>sa</param-value>
</context-param>
<context-param>
    <param-name>db.tcpServer</param-name>
    <param-value>-tcpAllowOthers</param-value>
</context-param>
By default this tool opens an embedded connection using the database URL jdbc:h2:~/test, user name sa, and password sa
Connection conn = getServletContext().getAttribute("connection");


### Using the H2 Console Servlet
<servlet>
    <servlet-name>H2Console</servlet-name>
    <servlet-class>org.h2.server.web.WebServlet</servlet-class>
    <!--
    <init-param>
        <param-name>webAllowOthers</param-name>
        <param-value></param-value>
    </init-param>
    <init-param>
        <param-name>trace</param-name>
        <param-value></param-value>
    </init-param>
    -->
    <load-on-startup>1</load-on-startup>
</servlet>
<servlet-mapping>
    <servlet-name>H2Console</servlet-name>
    <url-pattern>/console/*</url-pattern>
</servlet-mapping>



### using the functions CSVREAD and CSVWRITE, or it can be used outside the database as a standalone tool.
SELECT * FROM CSVREAD('test.csv');
CREATE TABLE TEST AS SELECT * FROM CSVREAD('test.csv');
CREATE TABLE TEST(ID INT PRIMARY KEY, NAME VARCHAR(255))
    AS SELECT * FROM CSVREAD('test.csv');

CREATE TABLE TEST(ID INT, NAME VARCHAR);
INSERT INTO TEST VALUES(1, 'Hello'), (2, 'World');
CALL CSVWRITE('test.csv', 'SELECT * FROM TEST');


### Backup using the Script Tool
java org.h2.tools.Script -url jdbc:h2:~/test -user sa -script test.zip -options compression zip
### Restore from a Script
java org.h2.tools.RunScript -url jdbc:h2:~/test -user sa -script test.zip -options compression zip
### Online Backup
BACKUP TO 'backup.zip'

###
### Use the following configuration to start and stop the H2 TCP server using the Spring Framework:
<bean id = "org.h2.tools.Server"
            class="org.h2.tools.Server"
            factory-method="createTcpServer"
            init-method="start"
            destroy-method="stop">
    <constructor-arg value="-tcp,-tcpAllowOthers,-tcpPort,8043" />
</bean>



import java.sql.*;
import org.h2.jdbcx.JdbcConnectionPool;
public class Test {
    public static void main(String[] args) throws Exception {
        JdbcConnectionPool cp = JdbcConnectionPool.create(
            "jdbc:h2:~/test", "sa", "sa");
        for (int i = 0; i < args.length; i++) {
            Connection conn = cp.getConnection();
            conn.createStatement().execute(args[i]);
            conn.close();
        }
        cp.dispose();
    }
}

import java.sql.*;
import org.h2.tools.Csv;
import org.h2.tools.SimpleResultSet;
public class TestCsv {
    public static void main(String[] args) throws Exception {
        SimpleResultSet rs = new SimpleResultSet();
        rs.addColumn("NAME", Types.VARCHAR, 255, 0);
        rs.addColumn("EMAIL", Types.VARCHAR, 255, 0);
        rs.addRow("Bob Meier", "bob.meier@abcde.abc");
        rs.addRow("John Jones", "john.jones@abcde.abc");
        new Csv().write("data/test.csv", rs, null);
    }
}
import java.sql.*;
import org.h2.tools.Csv;
public class TestCsv {
    public static void main(String[] args) throws Exception {
        ResultSet rs = new Csv().read("data/test.csv", null, null);
        ResultSetMetaData meta = rs.getMetaData();
        while (rs.next()) {
            for (int i = 0; i < meta.getColumnCount(); i++) {
                System.out.println(
                    meta.getColumnLabel(i + 1) + ": " +
                    rs.getString(i + 1));
            }
            System.out.println();
        }
        rs.close();
    }


https://code.google.com/p/h2sharp/wiki/BuildingH2Sharp


Using H2 in Microsoft .NET
The database can be used from Microsoft .NET even without using Java, by using IKVM.NET. You can access a H2 database on .NET using the JDBC API, or using the ADO.NET interface.
Using the ADO.NET API on .NET

An implementation of the ADO.NET interface is available in the open source project H2Sharp.
Using the JDBC API on .NET
    Install the .NET Framework from Microsoft. Mono has not yet been tested.
    Install IKVM.NET.
    Copy the h2*.jar file to ikvm/bin
    Run the H2 Console using: ikvm -jar h2*.jar
    Convert the H2 Console to an .exe file using: ikvmc -target:winexe h2*.jar. You may ignore the warnings.
    Create a .dll file using (change the version accordingly): ikvmc.exe -target:library -version:1.0.69.0 h2*.jar
If you want your C# application use H2, you need to add the h2.dll and the IKVM.OpenJDK.ClassLibrary.dll to your C# solution. Here some sample code:


