


<dependency>
	<groupId>hsqldb</groupId>
	<artifactId>hsqldb</artifactId>
	<version>1.8.0.10</version>
	<!-- <scope>compile</scope> -->
</dependency>
<dependency>
	<groupId>com.jolbox</groupId>
	<artifactId>bonecp</artifactId>
	<version>0.8.0.RELEASE</version>
</dependency>

bonecp-config.xml
bonecp-default-config.xml
https://www.cnblogs.com/zhwl/archive/2013/07/23/3208550.html

# ==================================

<?xml version="1.0" encoding="UTF-8"?>
<bonecp-config>
	<default-config>
		<property name="driverClass">org.h2.Driver</property>
		<property name="jdbcUrl">jdbc:h2:./bin/aba/h2db.bo</property>
		<property name="username">tests</property>
		<property name="password">tests</property>
		<property name="partitionCount">3</property>
		<property name="maxConnectionsPerPartition">30</property>
		<property name="minConnectionsPerPartition">6</property>
		<property name="acquireIncrement">3</property>
	</default-config>
	<named-config name="hsql">
		<property name="driverClass">org.hsqldb.jdbcDriver</property>
		<property name="jdbcUrl">jdbc:hsqldb:file:./bin/aba/hsql.bo</property>
		<property name="username">tests</property>
		<property name="password">tests</property>
		<property name="partitionCount">3</property>
		<property name="maxConnectionsPerPartition">30</property>
		<property name="minConnectionsPerPartition">6</property>
		<property name="acquireIncrement">3</property>
	</named-config>
	<named-config name="h2db">
		<property name="driverClass">org.h2.Driver</property>
		<property name="jdbcUrl">jdbc:h2:./bin/aba/h2db.bo</property>
		<property name="username">tests</property>
		<property name="password">tests</property>
		<property name="partitionCount">3</property>
		<property name="maxConnectionsPerPartition">30</property>
		<property name="minConnectionsPerPartition">6</property>
		<property name="partitionCount">3</property>
		<property name="acquireIncrement">3</property>
	</named-config>
</bonecp-config>

# ==================================
# bonecp.properties
driverClass=com.mysql.jdbc.Driver
jdbcUrl=jdbc:mysql://127.0.0.1/yourdb
username=tests
password=tests
maxConnectionsPerPartition=30
minConnectionsPerPartition=10
idleConnectionTestPeriod=60
partitionCount=3
acquireIncrement=5
idleMaxAge=240*
statementCacheSize=100*
releaseHelperThreads=3*

<property name="maxConnectionsPerPartition">30</property>
<property name="minConnectionsPerPartition">10</property>
<property name="partitionCount">3</property>
<property name="acquireIncrement">5</property>
# ==================================

This project is currently licensed under Apache v2, 
though I'm willing to consider other licenses if this doesn't match your needs. 
You may also contact me if you require additional commercial support. 

<bean id="dataSource" class="org.springframework.jdbc.datasource.LazyConnectionDataSourceProxy">
	<property name="targetDataSource">
		<ref local="mainDataSource" />
	</property>
</bean>

<bean id="mainDataSource" class="com.jolbox.bonecp.BoneCPDataSource" destroy-method="close">
	<property name="driverClass" value="com.mysql.jdbc.Driver" />
	<property name="jdbcUrl" value="jdbc:mysql://127.0.0.1/yourdb" />
	<property name="username" value="root" />
	<property name="password" value="abcdefgh" />
	<property name="idleConnectionTestPeriod" value="60" />
	<property name="idleMaxAge" value="240" />
	<property name="maxConnectionsPerPartition" value="60" />
	<property name="minConnectionsPerPartition" value="20" />
	<property name="partitionCount" value="3" />
	<property name="acquireIncrement" value="10" />
	<property name="statementsCacheSize" value="50" />
	<property name="releaseHelperThreads" value="3" />
</bean>

<bean id="mainDataSource" class="com.jolbox.bonecp.BoneCPDataSource" destroy-method="close">
   <property name="driverClass" value="com.mysql.jdbc.Driver" />
   <property name="jdbcUrl" value="jdbc:mysql://127.0.0.1/yourdb" />
   <property name="username" value="root"/>
   <property name="password" value="abcdefgh"/>
   <property name="idleConnectionTestPeriod" value="60"/>
   <property name="idleMaxAge" value="240"/>
   <property name="maxConnectionsPerPartition" value="30"/>
   <property name="minConnectionsPerPartition" value="10"/>
   <property name="partitionCount" value="3"/>
   <property name="acquireIncrement" value="5"/>
   <property name="statementsCacheSize" value="100"/>
   <property name="releaseHelperThreads" value="3"/>
</bean>

# =============================== 
@Component
public class Foo { 
@Autowired
DataSource ds; 
public void testBoneCP() throws SQLException {
    Connection connection = ds.getConnection();
    System.out.println(connection); // do something with the connection here..
 } 
}

Class.forName("org.hsqldb.jdbcDriver");    // load the DB driver
BoneCPConfig config = new BoneCPConfig();  // create a new configuration object
config.setJdbcUrl("jdbc:hsqldb:mem:test"); // set the JDBC url
config.setUsername("sa"); // set the username
config.setPassword("");   // set the password
config.setXXXX(...);    // (other config options here)

BoneCP connectionPool = new BoneCP(config);   // setup the connection pool

Connection conn = connectionPool.getConnection();  // fetch a connection
// ...  do something with the connection here ...

conn.close();
connectionPool.shutdown();

# ===============================

Class.forName("org.hsqldb.jdbcDriver");   // load the DB driver
BoneCPDataSource ds = new BoneCPDataSource();  // create a new datasource object
ds.setJdbcUrl("jdbc:hsqldb:mem:test");    // set the JDBC url
ds.setUsername("sa");  // set the username
ds.setPassword("");    // set the password
ds.setXXXX(...);       // (other config options here)

Connection conn = ds.getConnection();
//...  do something with the connection here ...

conn.close(); // close the connection
ds.close();   // close the datasource pool

# ===============================


try {
  Class.forName("org.hsqldb.jdbcDriver");
} catch (Exception e) {
  e.printStackTrace();
}

try {
  // setup the connection pool
  BoneCPConfig config = new BoneCPConfig();
  config.setJdbcUrl("jdbc:hsqldb:mem:test"); 
  config.setUsername("sa");
  config.setPassword("");
  config.setMinConnectionsPerPartition(5);
  config.setMaxConnectionsPerPartition(10);
  config.setPartitionCount(1);
  connectionPool = new BoneCP(config);
  connection = connectionPool.getConnection();
  if (connection != null) {
    System.out.println("Connection successful!");
    Statement stmt = connection.createStatement();
    ResultSet rs = stmt.executeQuery("SELECT 1 FROM INFORMATION_SCHEMA.SYSTEM_USERS"); 
    while (rs.next()) {
      System.out.println(rs.getString(1)); 
    }
  }
  connectionPool.shutdown();
} catch (SQLException e) {
  e.printStackTrace();
} finally {
  if (connection != null) {
    try {
      connection.close();
    } catch (SQLException e) {
      e.printStackTrace();
    }
  }
}



<bean id="dataSource"
	class="org.springframework.jdbc.datasource.LazyConnectionDataSourceProxy">
	<property name="targetDataSource">
		<ref local="mainDataSource" />
	</property>
</bean>

<bean id="mainDataSource" class="com.jolbox.bonecp.BoneCPDataSource" destroy-method="close">
	<property name="driverClass" value="com.mysql.jdbc.Driver" />
	<property name="jdbcUrl" value="jdbc:mysql://127.0.0.1/yourdb" />
	<property name="username" value="root" />
	<property name="password" value="abcdefgh" />
	<property name="idleConnectionTestPeriod" value="60" />
	<property name="idleMaxAge" value="240" />
	<property name="maxConnectionsPerPartition" value="60" />
	<property name="minConnectionsPerPartition" value="20" />
	<property name="partitionCount" value="3" />
	<property name="acquireIncrement" value="10" />
	<property name="statementsCacheSize" value="50" />
	<property name="releaseHelperThreads" value="3" />
</bean>
<bean id="mainDataSource" class="com.jolbox.bonecp.BoneCPDataSource" destroy-method="close">
	<property name="driverClass" value="com.mysql.jdbc.Driver" />
	<property name="jdbcUrl" value="jdbc:mysql://127.0.0.1/yourdb" />
	<property name="username" value="root" />
	<property name="password" value="abcdefgh" />
	<property name="idleConnectionTestPeriod" value="60" />
	<property name="idleMaxAge" value="240" />
	<property name="maxConnectionsPerPartition" value="30" />
	<property name="minConnectionsPerPartition" value="10" />
	<property name="partitionCount" value="3" />
	<property name="acquireIncrement" value="5" />
	<property name="statementCacheSize" value="100" />
	<property name="releaseHelperThreads" value="3" />
</bean>
<bean id="sessionFactory" class="org.springframework.orm.hibernate.LocalSessionFactoryBean"	autowire="autodetect">
	<property name="hibernateProperties">
		<props>
			<prop key="hibernate.connection.provider_class">com.jolbox.bonecp.provider.BoneCPConnectionProvider
			</prop>
			<prop key="hibernate.connection.driver_class">com.mysql.jdbc.Driver</prop>
			<prop key="hibernate.connection.url">jdbc:mysql://127.0.0.1/yourdb</prop>
			<prop key="hibernate.connection.username">root</prop>
			<prop key="hibernate.connection.password">abcdefgh</prop>
			<prop key="bonecp.idleMaxAge">240</prop>
			<prop key="bonecp.idleConnectionTestPeriod">60</prop>
			<prop key="bonecp.partitionCount">3</prop>
			<prop key="bonecp.acquireIncrement">10</prop>
			<prop key="bonecp.maxConnectionsPerPartition">60</prop>
			<prop key="bonecp.minConnectionsPerPartition">20</prop>
			<prop key="bonecp.preparedStatementCacheSize">50</prop>
			<prop key="bonecp.statementsCachedPerConnection">30</prop>
			<prop key="bonecp.releaseHelperThreads">3</prop>
		</props>
	</property>
</bean>

# ==============================================
jdbc.driverClass=oracle.jdbc.driver.OracleDriver  
jdbc.jdbcUrl=jdbc:oracle:thin:@192.168.30.4:1521:test  
jdbc.username=tests  
jdbc.password=tests

# ==============================================
bonecp.minConnectionsPerPartition=1  
#Sets the maximum number of connections that will be contained in every partition.   
#Setting this to 5 with 3 partitions means you will have 15 unique   
#connections to the database. Note that the connection pool will not create all   
#these connections in one go but rather start off with minConnectionsPerPartition and gradually   
#increase connections as required.  
bonecp.maxConnectionsPerPartition=5  
#Sets the acquireIncrement property.  When the available connections are about to run   
#out, BoneCP will dynamically create new ones in batches. This property controls how   
#many new connections to create in one go (up to a maximum of   
#maxConnectionsPerPartition). Note: This is a per partition setting.  
bonecp.acquireIncrement=1  
#Sets number of partitions to use.  In order to reduce lock contention   
#and thus improve performance, each incoming connection request picks off a connection from   
#a pool that has thread-affinity, i.e. pool[threadId % partition_count]. The higher this number,   
#the better your performance will be for the case when you have plenty   
#of short-lived threads. Beyond a certain threshold, maintenance of these pools will start   
#to have a negative effect on performance (and only for the case when   
#connections on a partition start running out).  Default: 1, minimum: 1, recommended:   
#2-4 (but very app specific)  
bonecp.partitionCount=1  
#Sets the idleConnectionTestPeriod.  This sets the time (in minutes), for a connection   
#to remain idle before sending a test query to the DB. This is   
#useful to prevent a DB from timing out connections on its end. Do   
#not use aggressive values here!   Default: 240 min, set to 0   
#to disable  
bonecp.idleConnectionTestPeriodInMinutes=240  
#Sets the idleConnectionTestPeriod.  This sets the time (in seconds), for a connection   
#to remain idle before sending a test query to the DB. This is   
#useful to prevent a DB from timing out connections on its end. Do   
#not use aggressive values here!   Default: 240 min, set to 0   
#to disable  
bonecp.idleConnectionTestPeriodInSeconds=14400  
#Sets Idle max age (in min).  The time (in minutes), for a   
#connection to remain unused before it is closed off. Do not use aggressive   
#values here!  Default: 60 minutes, set to 0 to disable.  
bonecp.idleMaxAgeInMinutes=60  
#Sets Idle max age (in seconds).  The time (in seconds), for a   
#connection to remain unused before it is closed off. Do not use aggressive   
#values here!  Default: 60 minutes, set to 0 to disable.  
bonecp.idleMaxAgeInSeconds=3600  
#Sets statementsCacheSize setting.  The number of statements to cache.  
bonecp.statementsCacheSize=0  
#Sets number of helper threads to create that will handle releasing a connection.   
#When this value is set to zero, the application thread is blocked   
#until the pool is able to perform all the necessary cleanup to recycle   
#the connection and make it available for another thread.  When a non-zero   
#value is set, the pool will create threads that will take care of   
#recycling a connection when it is closed (the application dumps the connection into   
#a temporary queue to be processed asychronously to the application via the release   
#helper threads).  Useful when your application is doing lots of work on   
#each connection (i.e. perform an SQL query, do lots of non-DB stuff and   
#perform another query), otherwise will probably slow things down.   
bonecp.releaseHelperThreads=3  
#Instruct the pool to create a helper thread to watch over connection acquires   
#that are never released (or released twice). This is for debugging purposes only   
#and will create a new thread for each call to getConnection(). Enabling this   
#option will have a big negative impact on pool performance.  
bonecp.closeConnectionWatch=false  
#If enabled, log SQL statements being executed.  
bonecp.logStatementsEnabled=false  
#Sets the number of ms to wait before attempting to obtain a connection   
#again after a failure.  
bonecp.acquireRetryDelayInMs=7000  
#Set to true to force the connection pool to obtain the initial connections   
#lazily.  
bonecp.lazyInit=false  
#Set to true to enable recording of all transaction activity and replay the   
#transaction automatically in case of a connection failure.  
bonecp.transactionRecoveryEnabled=false  
#After attempting to acquire a connection and failing, try to connect these many   
#times before giving up. Default 5.  
bonecp.acquireRetryAttempts=5  
#Set to true to disable JMX.  
bonecp.disableJMX=false  
#Queries taking longer than this limit to execute are logged.  
bonecp.queryExecuteTimeLimitInMs=0  
#Sets the Pool Watch thread threshold.  The pool watch thread attempts to   
#maintain a number of connections always available (between minConnections and maxConnections). This value   
#sets the percentage value to maintain. For example, setting it to 20 means   
#that if the following condition holds: Free Connections / MaxConnections < poolAvailabilityThreshold    
#new connections will be created. In other words, it tries to keep at   
#least 20% of the pool full of connections. Setting the value to zero   
#will make the pool create new connections when it needs them but it   
#also means your application may have to wait for new connections to be   
#obtained at times.  Default: 20.  
bonecp.poolAvailabilityThreshold=20  
#If set to true, the pool will not monitor connections for proper closure.   
#Enable this option if you only ever obtain your connections via a mechanism   
#that is guaranteed to release the connection back to the pool (eg Spring's   
#jdbcTemplate, some kind of transaction manager, etc).  
bonecp.disableConnectionTracking=false  
#Sets the maximum time (in milliseconds) to wait before a call to getConnection   
#is timed out.  Setting this to zero is similar to setting it   
#to Long.MAX_VALUE  Default: 0 ( = wait forever )  
bonecp.connectionTimeoutInMs=0  
#Sets the no of ms to wait when close connection watch threads are   
#enabled. 0 = wait forever.  
bonecp.closeConnectionWatchTimeoutInMs=0  
#Sets number of statement helper threads to create that will handle releasing a   
#statement.  When this value is set to zero, the application thread is   
#blocked until the pool and JDBC driver are able to close off the   
#statement.  When a non-zero value is set, the pool will create threads   
#that will take care of closing off the statement asychronously to the application   
#via the release helper threads).  Useful when your application is opening up   
#lots of statements otherwise will probably slow things down.  
bonecp.statementReleaseHelperThreads=0  
#Sets the maxConnectionAge in seconds. Any connections older than this setting will be   
#closed off whether it is idle or not. Connections currently in use will   
#not be affected until they are returned to the pool.  
bonecp.maxConnectionAgeInSeconds=0  
#If set to true, keep track of some more statistics for exposure via   
#JMX. Will slow down the pool operation.  
bonecp.statisticsEnabled=false  
#If set to true, no attempts at passing in a username/password will be   
#attempted when trying to obtain a raw (driver) connection. Useful for cases when   
#you already have another mechanism on authentication eg NTLM.  
bonecp.externalAuth=false  

# ============================================== 
bean id="propertyConfigurer" class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">
	<property name="locations">
		<list>
			<value>classpath:cn/com/config/dataSource/bonecp.properties</value>
		</list>
	</property>
</bean>

<bean id="dataSource" class="org.springframework.jdbc.datasource.LazyConnectionDataSourceProxy">
	<property name="targetDataSource">
		<ref local="boneCPDataSource" />
	</property>
</bean>

<bean id="boneCPDataSource" class="com.jolbox.bonecp.BoneCPDataSource" destroy-method="close">
	<!-- BoneCP type -->
	<property name="driverClass" value="${jdbc.driverClass}" />
	<property name="jdbcUrl" value="${jdbc.jdbcUrl}" />
	<property name="username" value="${jdbc.username}" />
	<property name="password" value="${jdbc.password}" />
	<property name="minConnectionsPerPartition" value="${bonecp.minConnectionsPerPartition}" />
	<property name="maxConnectionsPerPartition" value="${bonecp.maxConnectionsPerPartition}" />
	<property name="partitionCount" value="${bonecp.partitionCount}" />
	<property name="acquireIncrement" value="${bonecp.acquireIncrement}" />
	<property name="statementsCacheSize" value="${bonecp.statementsCacheSize}" />
	<property name="releaseHelperThreads" value="${bonecp.releaseHelperThreads}" />
</bean>  


BoneCP主要配置参数
1.jdbcUrl
设置数据库URL
2.username
设置数据库用户名
3.password
设置数据库密码
4.partitionCount
设置分区个数。这个参数默认为1，建议3-4（根据特定应用程序而定）。
为了减少锁竞争和改善性能，从当前线程分区(thread-affinity)中获取一个connection，
也就是这个样子：partitions[Thread.currentThread().getId() % partitionCount]。当拥有充足的短期(short-lived)的线程时候，这个参数设置越大，性能越好。当超过一定的阀值时，连接池的维护工作就可能对性能造成一定的负面影响（仅当分区上的connection使用耗尽时）。
5.maxConnectionsPerPartition
设置每个分区含有connection最大个数。这个参数默认为2。如果小于2，BoneCP将设置为50。
比如：partitionCount设置为3，maxConnectionPerPartition设置为5，你就会拥有总共15个connection。
注意：BoneCP不会将这些connection一起创建出来，而是说在需要更多connection的时候从minConnectionsPerPartition参数开始逐步地增长connection数量。
6.minConnectionsPerPartition
设置每个分区含有connection最大小个数。这个参数默认为0。
7.acquireIncrement
设置分区中的connection增长数量。这个参数默认为1。
当每个分区中的connection大约快用完时，BoneCP动态批量创建connection，
这个属性控制一起创建多少个connection（不会大于maxConnectionsPerPartition）。
注意：这个配置属于每个分区的设置。
8.poolAvailabilityThreshold
设置连接池阀值。这个参数默认为20。如果小于0或是大于100，BoneCP将设置为20。
连接池观察线程(PoolWatchThread)试图为每个分区维护一定数量的可用connection。
这 个数量趋于maxConnectionPerPartition和minConnectionPerPartition之间。这个参数是以百分比的形式来 计算的。例如：设置为20，下面的条件如果成立：Free Connections / MaxConnections < poolAvailabilityThreshold；就会创建出新的connection。
换句话来说连接池为每个分区至少维持20%数量的可用connection。
设置为0时，每当需要connection的时候，连接池就要重新创建新connection，这个时候可能导致应用程序可能会为了获得新connection而小等一会。
9.connectionTimeout
设置获取connection超时的时间。这个参数默认为Long.MAX_VALUE;单位：毫秒。
在调用getConnection获取connection时，获取时间超过了这个参数，就视为超时并报异常。

三、BoneCP线程配置参数
1.releaseHelperThreads
设置connection助手线程个数。这个参数默认为3。如果小于0，BoneCP将设置为3。
设置为0时，应用程序线程被阻塞，直到连接池执行必要地清除和回收connection，并使connection在其它线程可用。
设置大于0时，连接池在每个分区中创建助手线程处理回收关闭后的connection（应用程序会通过助手线程异步地将这个connection放置到一个临时队列中进行处理)。
对于应用程序在每个connection上处理大量工作时非常有用。可能会降低运行速度，不过在高并发的应用中会提高性能。
2.statementReleaseHelperThreads
设置statement助手线程个数。这个参数默认为3。如果小于0，BoneCP将设置为3。
设置为0时，应用程序线程被阻塞，直到连接池或JDBC驱动程序关闭statement。
设置大于0时，连接池会在每个分区中创建助理线程，异步地帮助应用程序关闭statement当应用程序打开了大量的statement是非常有用的。可能会降低运行速度，不过在高并发的应用中会提高性能。
3.maxConnectionAge
设置connection的存活时间。这个参数默认为0，单位：毫秒。设置为0该功能失效。
通过ConnectionMaxAgeThread观察每个分区中的connection，不管connection是否空闲，如果这个connection距离创建的时间大于这个参数就会被清除。当前正在使用的connection不受影响，直到返回到连接池再做处理。
4.idleMaxAge
设置connection的空闲存活时间。这个参数默认为60，单位：分钟。设置为0该功能失效。
通过ConnectionTesterThread观察每个分区中的connection，如果这个connection距离最后使用的时间大于这个参数就会被清除。
注意：这个参数仅和idleConnectionTestPeriod搭配使用，而且不要在这里设置任何挑衅的参数！
5.idleConnectionTestPeriod
设置测试connection的间隔时间。这个参数默认为240，单位：分钟。设置为0该功能失效。
通过ConnectionTesterThread观察每个分区中的connection， 如果这个connection距离最后使用的时间大于这个参数并且距离上一次测试的时间大于这个参数就会向数据库发送一条测试语句，如果执行失败则将这个connection清除。
注意：这个值仅和idleMaxAge搭配使用，而且不要在这里设置任何挑衅的参数！

三、BoneCP可选配置参数
1.acquireRetryAttempts
设置重新获取连接的次数。这个参数默认为5。
获取某个connection失败之后会多次尝试重新连接，如果在这几次还是失败则放弃。
2.acquireRetryDelay
设置重新获取连接的次数间隔时间。这个参数默认为7000，单位：毫秒。如果小于等于0，BoneCP将设置为1000。
获取connection失败之后再次尝试获取connection的间隔时间。
3.lazyInit
设置连接池初始化功能。这个参数默认为false。
设置为true，连接池将会初始化为空，直到获取第一个connection。
4.statementsCacheSize
设置statement缓存个数。这个参数默认为0。
5.disableJMX
设置是否关闭JMX功能。这个参数默认为false。
6.poolName
设置连接池名字。用于当作JMX和助手线程名字的后缀。

四、BoneCP调试配置参数
1.closeConnectionWatch
设置是开启connection关闭情况监视器功能。这个参数默认为false。
每当调用getConnection()时，都会创建CloseThreadMonitor，监视connection有没有关闭或是关闭了两次。警告：这个参数对连接池性能有很大的负面影响，慎用！仅在调试阶段使用！
2.closeConnectionWatchTimeout
设置关闭connection监视器（CloseThreadMonitor）持续多长时间。这个参数默认为0；单位：毫秒。仅当closeConnectionWatch参数设置为可用时，设置这个参数才会起作用。
设置为0时，永远不关闭。
3.logStatementsEnabled
设置是否开启记录SQL语句功能。这个参数默认是false。
将执行的SQL记录到日志里面（包括参数值）。
4.queryExecuteTimeLimit
设置执行SQL的超时时间。这个参数默认为0；单位：毫秒。
当查询语句执行的时间超过这个参数，执行的情况就会被记录到日志中。
设置为0时，该功能失效。
5.disableConnectionTracking
设置是否关闭connection跟踪功能。这个参数默认为false。
设置为true，连接池则不会监控connection是否严格的关闭；设置为false，则启用跟踪功能（仅追踪通过Spring或一些事务管理等机制确保正确释放connection并放回到连接池中）。
6.transactionRecoveryEnabled
设置事务回放功能。这个参数默认为false。
设置为true时，MemorizeTransactionProxy可以记录所有在connection上操作的情况，当connetion操作失败的时候会自动回放先前的操作，如果在回放期间还是失败，则抛出异常。注意：这个功能会使连接池微弱地降低运行速度。




// setup the connection pool
BoneCPConfig config = new BoneCPConfig();
config.setJdbcUrl("jdbc:mysql://localhost:3306/demo"); // jdbc url specific to your database, eg jdbc:mysql://127.0.0.1/yourdb
config.setUsername("root"); 
config.setPassword("root");
//设置每60秒检查数据库中的空闲连接数
config.setIdleConnectionTestPeriod(60);
//设置连接空闲时间
config.setIdleMaxAge(240);
//设置每个分区中的最大连接数 30
config.setMaxConnectionsPerPartition(30);
//设置每个分区中的最小连接数 10
config.setMinConnectionsPerPartition(10);
//当连接池中的连接耗尽的时候 BoneCP一次同时获取的连接数
config.setAcquireIncrement(5);
//连接释放处理
config.setReleaseHelperThreads(3);
//设置分区  分区数为3
config.setPartitionCount(3);
//设置配置参数
connectionPool = new BoneCP(config); // setup the connection pool

connection = connectionPool.getConnection(); // fetch a connection

if (connection != null){
    System.out.println("Connection successful!");
    Statement stmt = connection.createStatement();
    ResultSet rs = stmt.executeQuery(" select * from person "); // do something with the connection.
    while(rs.next()){
        System.out.println(rs.getString(1)); // should print out "1"'
        System.out.println(rs.getString(2)); // should print out "1"'
    }
}
connectionPool.shutdown(); // shutdown connection pool.




BoneCPDataSource dataSource=new BoneCPDataSource();
dataSource.setUsername("root");
dataSource.setPassword("root");
dataSource.setJdbcUrl("jdbc:mysql://localhost:3306/demo");
dataSource.setMaxConnectionsPerPartition(10);
dataSource.setMinConnectionsPerPartition(5);
dataSource.setIdleConnectionTestPeriod(60);
dataSource.setIdleMaxAge(240);
dataSource.setAcquireIncrement(5);
dataSource.setReleaseHelperThreads(3);
try {
    connection=dataSource.getConnection();
    if (connection != null){
        System.out.println("Connection successful!");
        Statement stmt = connection.createStatement();
        ResultSet rs = stmt.executeQuery(" select * from person "); // do something with the connection.
        while(rs.next()){
            System.out.println(rs.getString(1)); // should print out "1"'
            System.out.println(rs.getString(2)); // should print out "1"'
        }
    }
} catch (SQLException e) {
    e.printStackTrace();
}

