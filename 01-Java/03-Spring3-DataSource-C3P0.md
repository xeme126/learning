


<dependency>
  <groupId>c3p0</groupId>
  <artifactId>c3p0</artifactId>
  <version>0.9.5.2</version>
</dependency>

<dependency>
  <groupId>c3p0</groupId>
  <artifactId>c3p0</artifactId>
  <version>0.9.1.2</version>
</dependency>
<dependency>
  <groupId>com.mchange</groupId>
  <artifactId>mchange-commons-java</artifactId>
  <version>0.2.11</version>
</dependency>


<dependency>
  <groupId>com.mchange</groupId>
  <artifactId>mchange-commons-java</artifactId>
  <version>0.2.12</version>
</dependency>
<dependency>
    <groupId>commons-dbutils</groupId>
    <artifactId>commons-dbutils</artifactId>
    <version>1.6</version>
</dependency>
<dependency>
    <groupId>org.bouncycastle</groupId>
    <artifactId>bcprov-jdk15on</artifactId>
    <version>1.58</version>
</dependency>


ComboPooledDataSource ds=new ComboPooledDataSource();
//2.设置连接参数，url,驱动，用户名，密码，初始化连接数，最大连接数
ds.setJdbcUrl("jdbc:mysql://localhost:3306/jdbc_demo");;
ds.setDriverClass("com.mysql.jdbc.Driver");
ds.setUser("root");
ds.setPassword("root");
ds.setInitialPoolSize(3);
ds.setMaxPoolSize(6);
ds.setMaxIdleTime(3000);



十一月 13, 2017 10:59:34 上午 org.apache.catalina.loader.WebappClassLoaderBase clearReferencesJdbc
严重: The web application [] registered the JDBC driver [org.hsqldb.jdbc.JDBCDriver] but failed to unregister it when the web application was stopped. To prevent a memory leak, the JDBC Driver has been forcibly unregistered.
十一月 13, 2017 10:59:34 上午 org.apache.catalina.loader.WebappClassLoaderBase clearReferencesJdbc
严重: The web application [] registered the JDBC driver [net.sf.log4jdbc.DriverSpy] but failed to unregister it when the web application was stopped. To prevent a memory leak, the JDBC Driver has been forcibly unregistered.
十一月 13, 2017 10:59:34 上午 org.apache.catalina.loader.WebappClassLoaderBase clearReferencesJdbc
严重: The web application [] registered the JDBC driver [org.h2.Driver] but failed to unregister it when the web application was stopped. To prevent a memory leak, the JDBC Driver has been forcibly unregistered.
十一月 13, 2017 10:59:34 上午 org.apache.catalina.loader.WebappClassLoaderBase clearReferencesThreads
严重: The web application [] appears to have started a thread named [Timer-0] but has failed to stop it. This is very likely to create a memory leak.
十一月 13, 2017 10:59:34 上午 org.apache.catalina.loader.WebappClassLoaderBase clearReferencesThreads
严重: The web application [] appears to have started a thread named [com.mchange.v2.async.ThreadPoolAsynchronousRunner$PoolThread-#0] but has failed to stop it. This is very likely to create a memory leak.
十一月 13, 2017 10:59:34 上午 org.apache.catalina.loader.WebappClassLoaderBase clearReferencesThreads
严重: The web application [] appears to have started a thread named [com.mchange.v2.async.ThreadPoolAsynchronousRunner$PoolThread-#1] but has failed to stop it. This is very likely to create a memory leak.
十一月 13, 2017 10:59:34 上午 org.apache.catalina.loader.WebappClassLoaderBase clearReferencesThreads
严重: The web application [] appears to have started a thread named [com.mchange.v2.async.ThreadPoolAsynchronousRunner$PoolThread-#2] but has failed to stop it. This is very likely to create a memory leak.
十一月 13, 2017 10:59:34 上午 org.apache.catalina.loader.WebappClassLoaderBase clearReferencesThreads
严重: The web application [] appears to have started a thread named [HSQLDB Timer @119d341] but has failed to stop it. This is very likely to create a memory leak.

