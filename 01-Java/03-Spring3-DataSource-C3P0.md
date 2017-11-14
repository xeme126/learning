


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


<Resource name="jdbc/ds_h2db"
       auth="Container"
       type="com.mchange.v2.c3p0.ComboPooledDataSource"
       factory="org.apache.naming.factory.BeanFactory"
       driverClass="org.h2.Driver"
       jdbcUrl="jdbc:h2:data02/h2bz05"
       user="tests"
       password="tests"
       initialPoolSize="3"
       maxPoolSize="60"
       minPoolSize="3"
       acquireIncrement="3"
       maxStatements="300"
       checkoutTimeout="3000"
       propertyCycle="1"
       maxConnectionAge="10"
       numHelperThreads="10"
       maxIdleTime="2"
       maxIdleTimeExcessConnections="1"
       idleConnectionTestPeriod="5"
       unreturnedConnectionTimeout="15"
       maxStatementsPerConnection="5"
       maxAdministrativeTaskTime="3"
       preferredTestQuery="select 1"
       acquireRetryDelay="1000"
       acquireRetryAttempts="60" />

