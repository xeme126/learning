

<dependency>
  <groupId>commons-dbcp</groupId>
  <artifactId>commons-dbcp</artifactId>
  <version>1.4</version>
</dependency>

<dependency>
  <groupId>commons-pool</groupId>
  <artifactId>commons-pool</artifactId>
  <version>1.6</version>
</dependency>

Apache Commons DBCP可以配置为跟踪和恢复这些被弃的数据库连接对象。不仅恢复还可以跟踪那些连接数据库却没有关闭的代码片段。
http://www.tomcatexpert.com/blog/2010/04/01/configuring-jdbc-pool-high-concurrency
http://blog.csdn.net/lovebosom/article/details/54693362


    <Resource name="jdbc/ds_hsql50"
        type="javax.sql.DataSource"
        factory="org.apache.tomcat.jdbc.pool.DataSourceFactory"
        driverClassName="org.hsqldb.jdbcDriver"
        url="jdbc:hsqldb:file:./bin/afa/hsql.db30"
        username="tests"
        password="tests"
        initialSize="10"
        maxActive="30"
        maxIdle="15"
        minIdle="3"
        maxWait="12000"
        suspectTimeout="60"
        removeAbandonedOnBorrow="true"
        removeAbandonedOnMaintenance="true"
        removeAbandonedTimeout="60"
        removeAbandoned="true"
        logAbandoned="true"
        validationQuery="select count(1) as cnt from information_schema.tables"
        testWhileIdle = "true"
        timeBetweenEvictionRunsMillis="30000"
        minEvictableIdleTimeMillis="60000"
        numTestsPerEvictionRun="3"
        testOnBorrow="false" />

    <Resource name="jdbc/ds_h2db50"
        type="javax.sql.DataSource"
        factory="org.apache.tomcat.jdbc.pool.DataSourceFactory"
        driverClassName="org.h2.Driver"
        url="jdbc:h2:./bin/afa/h2db.db20"
        username="tests"
        password="tests"
        initialSize="10"
        maxActive="30"
        maxIdle="15"
        minIdle="3"
        maxWait="12000"
        suspectTimeout="60"
        removeAbandonedOnBorrow="true"
        removeAbandonedOnMaintenance="true"
        removeAbandonedTimeout="60"
        removeAbandoned="true"
        logAbandoned="true"
        validationQuery="select count(1) as cnt from information_schema.tables"
        testWhileIdle = "true"
        timeBetweenEvictionRunsMillis="30000"
        minEvictableIdleTimeMillis="60000"
        numTestsPerEvictionRun="3"
        testOnBorrow="false" />

    <Resource name="jdbc/ds_hsql"
        auth="Container"
        type="javax.sql.DataSource"
        driverClassName="org.hsqldb.jdbcDriver"
        url="jdbc:hsqldb:file:./bin/afa/hsql.db3"
        username="tests"
        password="tests"
        initialSize="3"
        maxActive="90"
          maxIdle="3"
          minIdle="1"
        maxWait="12000"
        removeAbandonedOnBorrow="true"
        removeAbandonedOnMaintenance="true"
        removeAbandonedTimeout="60"
        removeAbandoned="true"
        logAbandoned="true"
        validationQuery="select count(1) as cnt from information_schema.tables"
        testWhileIdle = "true"
        timeBetweenEvictionRunsMillis="30000"
        minEvictableIdleTimeMillis="1800000"
        numTestsPerEvictionRun="3"
        testOnBorrow="false" />

    <Resource name="jdbc/ds_h2db"
        auth="Container"
        type="javax.sql.DataSource"
        driverClassName="org.h2.Driver"
        url="jdbc:h2:./bin/afa/h2db.db2"
        username="tests"
        password="tests"
        initialSize="3"
        maxActive="90"
          maxIdle="3"
          minIdle="1"
        maxWait="12000"
        removeAbandonedOnBorrow="true"
        removeAbandonedOnMaintenance="true"
        removeAbandonedTimeout="60"
        removeAbandoned="true"
        logAbandoned="true"
        validationQuery="select count(1) as cnt from information_schema.tables"
        testWhileIdle = "true"
        timeBetweenEvictionRunsMillis="30000"
        minEvictableIdleTimeMillis="1800000"
        numTestsPerEvictionRun="3"
        testOnBorrow="false" />

BasicDataSource提供了close()方法关闭数据源，所以必须设定destroy-method=”close”属性，
 以便Spring容器关闭时，数据源能够正常关闭。除以上必须的数据源属性外，还有一些常用的属性： 
    defaultAutoCommit：设置从数据源中返回的连接是否采用自动提交机制，默认值为 true； 
    defaultReadOnly：设置数据源是否仅能执行只读操作， 默认值为 false； 
    maxActive：最大连接数据库连接数，设置为0时，表示没有限制； 
    maxIdle：最大等待连接中的数量，设置为0时，表示没有限制； 
    maxWait：最大等待秒数，单位为毫秒， 超过时间会报出错误信息； 
    validationQuery：用于验证连接是否成功的查询SQL语句，SQL语句必须至少要返回一行数据， 如你可以简单地设置为：select 1
    removeAbandoned：是否自我中断，默认是 false ； 
    removeAbandonedTimeout：几秒后数据连接会自动断开，在removeAbandoned为true，提供该值； 
    logAbandoned：是否记录中断事件， 默认为 false； 
    
要增加连接池中被弃的连接重新可用，打开配置文件，为Resource标签配置以下参数：
removeAbandonedOnBorrow=true
removeAbandonedOnMaintenance=true
removeAbandonedTimeout=60
logAbandoned="true"

默认情况下removeAbandonedOnBorrow和removeAbandonedOnMaintenance都是为false。
注意：removeAbandonedOnMaintenance只有在timeBetweenEvictionRunsMillis设置为正数的情况下才有效。
removeAbandonedTimeout属性是设置数据库连接被释最多空闲时间多少秒之后设置为空闲。默认移除废弃连接的时间为300秒。



<Resource name="jdbc/ds_h2db"
        auth="Container"
        type="javax.sql.DataSource"
        driverClassName="org.h2.Driver"
        url="jdbc:h2:./bin/aza/h2db.db02"
        username="tests"
        password="tests"
        initialSize="3"
        maxActive="90"
          maxIdle="3"
          minIdle="1"
        maxWait="12000"
        removeAbandonedOnBorrow="true"
        removeAbandonedOnMaintenance="true"
        removeAbandonedTimeout="60"
        removeAbandoned="true"
        logAbandoned="true"
        validationQuery="select count(1) as cnt from information_schema.tables"
        testWhileIdle = "true"
        timeBetweenEvictionRunsMillis="30000"
        minEvictableIdleTimeMillis="1800000"
        numTestsPerEvictionRun="3"
        testOnBorrow="false" />

<Resource name="jdbc/xds_h2db"
        auth="Container"
        factory="org.apache.tomcat.jdbc.pool.DataSourceFactory"
        type="javax.sql.DataSource"
        driverClassName="org.h2.Driver"
        url="jdbc:h2:./bin/aza/h2db.db03"
        username="tests"
        password="tests"
        maxActive="150"
        maxIdle="3"
        maxWait="15000"
        removeAbandoned="true"
        removeAbandonedTimeout="60"
        validationQuery="select 1" 
        logAbandoned="true"
        testOnBorrow="true" />

<Resource name="jdbc/TestDB"
    type="javax.sql.DataSource"
    factory="org.apache.tomcat.jdbc.pool.DataSourceFactory"
    driverClassName="com.mysql.jdbc.Driver"
    url="jdbc:mysql://localhost:3306/mysql"
    username="mysql_user"
    password="mypassword123"
    initialSize="10"
    maxActive="30"
    maxIdle="15"
    minIdle="3"
    suspectTimeout="60"
    timeBetweenEvictionRunsMillis="30000"
    minEvictableIdleTimeMillis="60000" />

<Resource name="jdbc/TestDB1"
    auth="Container"
    factory="org.apache.tomcat.jdbc.pool.DataSourceFactory"
    dataSourceJNDI="DerbyXA1" 
    type="javax.sql.XADataSource"
    testWhileIdle="true"
    testOnBorrow="true"
    testOnReturn="false"
    validationQuery="SELECT 1"
    validationInterval="30000"
    timeBetweenEvictionRunsMillis="5000"
    maxActive="100"
    minIdle="10"
    maxIdle="20"
    maxWait="10000"
    initialSize="10"
    removeAbandonedTimeout="60"
    removeAbandoned="true"
    logAbandoned="true"
    minEvictableIdleTimeMillis="30000"
    jmxEnabled="true"
    jdbcInterceptors="ConnectionState;StatementFinalizer;SlowQueryReportJmx(threshold=10000)"
    abandonWhenPercentageFull="75"/>

<Resource name="jdbc/ds_mysql"
    type="javax.sql.DataSource"
    factory="org.apache.tomcat.jdbc.pool.DataSourceFactory"
    driverClassName="com.mysql.jdbc.Driver"
    url="jdbc:mysql://localhost:3306/mysql"
    username="tests"
    password="tests"
    initialSize="10"
    maxActive="100"
    maxIdle="50"
    minIdle="3"
    removeAbandonedOnBorrow="true"
    removeAbandonedOnMaintenance="true"
    removeAbandonedTimeout="60"
    removeAbandoned="true"
    logAbandoned="true"
    validationQuery="select 1"
    testWhileIdle = "true"
    timeBetweenEvictionRunsMillis="30000"
    minEvictableIdleTimeMillis="1800000"
    numTestsPerEvictionRun="3"
    testOnBorrow="false" />


<Resourcename="jdbc/MyXA1" 
    factory="org.apache.tomcat.jdbc.naming.GenericNamingResourcesFactory"
    type="oracle.jdbc.xa.client.OracleXADataSource"
    url="jdbc:oracle:thin:@168.1.50.20:1522:orcl"
    username="scott"
    password="scott" />

<Resource name="jdbc/TestDB"
    dataSourceJNDI="MyXA1"
    factory="org.apache.tomcat.jdbc.pool.DataSourceFactory"
    type="javax.sql.XADataSource"
    username="scott"
    password="scott"/>

 
 <!-- Tomcat JDBC连接池配置示例，自动检查连接的可用性，dbcp定时检测连接，dbcp自动重连的配置
	   JNDI数据源的name，查找时用：java:comp/env/jdbc/TestDB -->

<Resource
    name="jdbc/TestDB"
    type="javax.sql.DataSource"
    factory="org.apache.tomcat.dbcp.dbcp.BasicDataSourceFactory"
    driverClassName="com.mysql.jdbc.Driver"
    url="jdbc:mysql://localhost:3306/testcharacterEncoding=UTF-8&amp;autoReconnectForPools=true&amp;rewriteBatchedStatements=true&amp;useCursorFetch=true&amp;defaultFetchSize=20" 数据库URL地址
    username="xxx" 访问数据库用户名
    password="xxx" 访问数据库的密码
    maxWait="3000" 从池中取连接的最大等待时间，单位ms.
    initialSize="10"  初始化连接
    maxIdle="60"   最大空闲连接
    minIdle="10"   最小空闲连接
    maxActive="80" 最大活动连接
    validationQuery = "SELECT 1"  验证使用的SQL语句
    testWhileIdle = "true"   指明连接是否被空闲连接回收器(如果有)进行检验.如果检测失败,则连接将被从池中去除.
    testOnBorrow = "false"   借出连接时不要测试，否则很影响性能
    timeBetweenEvictionRunsMillis = "30000" 每30秒运行一次空闲连接回收器
    minEvictableIdleTimeMillis = "1800000"  池中的连接空闲30分钟后被回收
    numTestsPerEvictionRun="10" 在每次空闲连接回收器线程(如果有)运行时检查的连接数量
    removeAbandoned="true"		连接泄漏回收参数，当可用连接数少于3个时才执行
    removeAbandonedTimeout="180" />  连接泄漏回收参数，180秒，泄露的连接可以被删除的超时值

<Resource name="jdbc/TestDB"
    auth="Container"
    factory="org.apache.tomcat.jdbc.pool.DataSourceFactory"
    type="javax.sql.DataSource"
    username="scott"
    password="scott"
    driverClassName="oracle.jdbc.driver.OracleDriver"
    url="jdbc:oracle:thin:@168.1.51.21:1522:orcl"
    />

<Resource name="jdbc/testDB"       //指定的jndi名称，会用于spring数据源bean的配置和ResourceLink的配置
    type="javax.sql.DataSource"   //数据源类型，使用标准的javax.sql.DataSource
    driverClassName="com.mysql.jdbc.Driver"    //JDBC驱动器
    url="jdbc:mysql://localhost:3306/test" //数据库URL地址
    username="test"   //数据库用户名
    password="test"   //数据库密码
    maxIdle="40"      //最大的空闲连接数
    maxWait="4000"    //当池的数据库连接已经被占用的时候，最大等待时间
    maxActive="40"    //连接池当中最大的数据库连接
    removeAbandoned="true"
    removeAbandonedTimeout="180"
    logAbandoned="true" //被丢弃的数据库连接是否做记录，以便跟踪
    factory="org.apache.tomcat.dbcp.dbcp.BasicDataSourceFactory" />

<Resource name="jdbc/testDB"  //指定的jndi名称，会用于spring数据源bean的配置和ResourceLink的配置
    type="javax.sql.DataSource"   //数据源类型，使用标准的javax.sql.DataSource
    factory="org.apache.tomcat.dbcp.dbcp.BasicDataSourceFactory"
    driverClassName="com.mysql.jdbc.Driver"    //JDBC驱动器
    url="jdbc:mysql://localhost:3306/test"     //数据库URL地址
    username="test"   //数据库用户名
    password="test"   //数据库密码
    maxIdle="40"      //最大的空闲连接数
    maxWait="4000"    //当池的数据库连接已经被占用的时候，最大等待时间
    maxActive="40"    //连接池当中最大的数据库连接
    removeAbandoned="true"
    removeAbandonedTimeout="180"
    logAbandoned="true" />  //被丢弃的数据库连接是否做记录，以便跟踪
    
initialSize=10 设置连接池建立时连接的数目
     当连接池定义在GlobalNamingResources中，连接池在Tomcat启动时创键
     当连接池定义在Context中，连接池在第一次查找JNDI时创建
maxActive=100 连接数据库的最大连接数。这个属性用来限制连接池中能够打开连接的数量，可以方便数据库做连接容量规划。
minIdle=10  连接池中存在的最小连接数目。连接池中连接数目可以变很少，如果使用了maxAge属性，有些空闲的连接会被关闭因为离它最近一次连接的时间过去太久了。 但是，我们看到的打开的连接不会少于minIdle。
maxIdle属性有一点麻烦。它的不同的行为取决于是否使用了pool sweeper。pool sweeper是一个可以在连接池正在使用的时候测试空闲连接和重置连接池大小的后台线程。还负责检测连接泄露。

<Resource type="javax.sql.DataSource"
    name="jdbc/TestDB"
    factory="org.apache.tomcat.jdbc.pool.DataSourceFactory"
    driverClassName="com.mysql.jdbc.Driver"
    url="jdbc:mysql://localhost:3306/mysql"
    username="mysql_user"
    password="mypassword123"
    maxActive="100"
    timeBetweenEvictionRunsMillis="30000"
    removeAbandoned="true"
    removeAbandonedTimeout="60"
    logAbandoned="true"  />

<Resource name="jdbc/TestDB" auth="Container"
    type="javax.sql.DataSource"
    description="Oracle Datasource"
    url="jdbc:oracle:thin:@//localhost:1521/orcl"
    driverClassName="oracle.jdbc.driver.OracleDriver"
    username="default_user"
    password="password"
    maxActive="100"
    validationQuery="select 1 from dual"
    validationInterval="30000"
    testOnBorrow="true"
    initSQL="ALTER SESSION SET NLS_DATE_FORMAT = 'YYYY MM DD HH24:MI:SS'"/>

<Resource type="javax.sql.DataSource"
    name="jdbc/TestDB"
    factory="org.apache.tomcat.jdbc.pool.DataSourceFactory"
    driverClassName="com.mysql.jdbc.Driver"
    url="jdbc:mysql://localhost:3306/mysql"
    username="mysql_user"
    password="mypassword123"
    maxActive="100"
    timeBetweenEvictionRunsMillis="30000"
    removeAbandoned="true"
    removeAbandonedTimeout="60"
    logAbandoned="true"
    abandonWhenPercentageFull="50"  />

<Resource name="jdbc/ds_hsql"
    auth="Container"
    type="javax.sql.DataSource"
    driverClassName="org.hsqldb.jdbcDriver"
    url="jdbc:hsqldb:file:abc/db2"
    username="tests"
    password="tests"
    initialSize="10"
    maxActive="100"
    maxIdle="50"
    minIdle="3"
    maxWait="12000"
    removeAbandonedOnBorrow="true"
    removeAbandonedOnMaintenance="true"
    removeAbandonedTimeout="60"
    removeAbandoned="true"
    logAbandoned="true"
    validationQuery="select 1"
    testWhileIdle = "true"
    timeBetweenEvictionRunsMillis="30000"
    minEvictableIdleTimeMillis="1800000"
    numTestsPerEvictionRun="3"
    testOnBorrow="false" />

<Resource factory="org.apache.tomcat.jdbc.naming.GenericNamingResourcesFactory"
    name="jdbc/DerbyXA1"
    type="org.apache.derby.jdbc.ClientXADataSource"
    databaseName="sample1"
    createDatabase="create"
    serverName="localhost"
    portNumber="1527"
    user="sample1"
    password="password"/>

                
//@.配置连接池参数，初始化连接数，最大连接数/连接字符串，驱动，用户名，密码
BasicDataSource dataSource=new BasicDataSource();
dataSource.setUrl("jdbc:mysql://localhost:3306/jdbc_demo");
dataSource.setDriverClassName("com.mysql.jdbc.Driver");
dataSource.setUsername("root");
dataSource.setPassword("root");
dataSource.setInitialSize(3);
dataSource.setMaxActive(6);
dataSource.setMaxIdle(3000);

//数据库连接池
BasicDataSource ds = new BasicDataSource(); 
ds.setUrl("jdbc:mysql:loadbalance://192.168.0.109:3306,192.168.0.110:3306/test_db");
ds.setDriverClassName("com.mysql.jdbc.ReplicationDriver");
ds.setUsername("tests");
ds.setPassword("tests");
ds.setInitialSize(3); 
ds.setMaxActive(10);
ds.setMinIdle(3);
ds.setMaxIdle(5);
ds.setMaxWait(3000);
ds.setRemoveAbandoned(true);
ds.setRemoveAbandonedTimeout(2000);

# 使用ReplicationDriver而不是driver
jdbc.driverClassName=com.mysql.jdbc.ReplicationDriver 
## 使用的是jdbc:mysql:replication://
jdbc.url=jdbc:mysql:replication://master:3306,slave1:3306,slave2:3306/test2?characterEncoding=utf8 
jdbc.username=root
jdbc.password=123456

DataSource ds = new DataSource();  
ds.setDataSource(myOtherDataSource);  
Connection con = ds.getConnection();  
if (con instanceof XAConnection) {  
        XAConnection xacon = (XAConnection)con;  
        transactionManager.enlistResource(xacon.getXAResource());  
}  
Statement st = con.createStatement();  
ResultSet rs = st.executeQuery(SELECT 1);  
    
默认配置的DBCP连接池，是不对池中的连接做测试的，有时连接已断开了，但DBCP连接池不知道，还以为连接是好的呢。
应用从池中取出这样的连接访问数据库一定会报错。这也是好多人不喜欢DBCP的原因。
问题例一：
MySQL8小时问题，Mysql服务器默认连接的“wait_timeout”是8小时，也就是说一个connection空闲超过8个小时，Mysql将自动断开该 connection。
但是DBCP连接池并不知道连接已经断开了，如果程序正巧使用到这个已经断开的连接，程序就会报错误。
问题例二：
以前还使用Sybase数据库，由于某种原因，数据库死了后重启、或断网后恢复。
等了约10分钟后，DBCP连接池中的连接还都是不能使用的（断开的），访问数据应用一直报错，最后只能重启Tomcat问题才解决 。
解决方案：
方案1、定时对连接做测试，测试失败就关闭连接。
方案2、控制连接的空闲时间达到N分钟，就关闭连接，（然后可再新建连接）。
以上两个方案使用任意一个就可以解决以述两类问题。如果只使用方案2，建议 N <= 5分钟。连接断开后最多5分钟后可恢复。
也可混合使用两个方案，建议 N = 30分钟。
下面就是DBCP连接池，同时使用了以上两个方案的配置配置
validationQuery = "SELECT 1"  验证连接是否可用，使用的SQL语句
testWhileIdle = "true"      指明连接是否被空闲连接回收器(如果有)进行检验.如果检测失败,则连接将被从池中去除.
testOnBorrow = "false"   借出连接时不要测试，否则很影响性能
timeBetweenEvictionRunsMillis = "30000"  每30秒运行一次空闲连接回收器
minEvictableIdleTimeMillis = "1800000"  池中的连接空闲30分钟后被回收,默认值就是30分钟。
numTestsPerEvictionRun="3" 在每次空闲连接回收器线程(如果有)运行时检查的连接数量，默认值就是3.
解释： 
配置timeBetweenEvictionRunsMillis = "30000"后，每30秒运行一次空闲连接回收器（独立线程）。并每次检查3个连接，如果连接空闲时间超过30分钟就销毁。销毁连接后，连接数量就少了，如果小于minIdle数量，就新建连接，维护数量不少于minIdle，过行了新老更替。 
testWhileIdle = "true" 表示每30秒，取出3条连接，使用validationQuery = "SELECT 1" 中的SQL进行测试，测试不成功就销毁连接。销毁连接后，连接数量就少了，如果小于minIdle数量，就新建连接。
testOnBorrow = "false" 一定要配置，因为它的默认值是true。false表示每次从连接池中取出连接时，不需要执行validationQuery = "SELECT 1" 中的SQL进行测试。若配置为true,对性能有非常大的影响，性能会下降7-10倍。所在一定要配置为false.
每30秒，取出numTestsPerEvictionRun条连接（本例是3，也是默认值），发出"SELECT 1" SQL语句进行测试，测试过的连接不算是“被使用”了，还算是空闲的。连接空闲30分钟后会被销毁。

    <property name="removeAbandonedTimeout">60</property>
    <property name="removeAbandonedOnMaintenance">true</property>
    <property name="removeAbandonedOnBorrow">true</property>
    <property name="removeAbandoned">true</property>
    <property name="logAbandoned">true</property>
    <property name="testWhileIdle">true</property>
    <property name="testOnBorrow">false</property>
    <property name="validationQuery">select 1</property>
    <property name="numTestsPerEvictionRun">3</property>
    <property name="timeBetweenEvictionRunsMillis">30000</property>
    <property name="minEvictableIdleTimeMillis">1800000</property>    
    