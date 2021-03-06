
Apache License, Version 2.0

<dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>druid</artifactId>
        <version>${druid.version}</version>
</dependency>
 
<dependency>
  <groupId>com.alibaba</groupId>
  <artifactId>fastjson</artifactId>
  <version>1.1.39</version>
</dependency>

<druid.version>1.0.11</druid.version>
<version>1.0.9/11/13 1.1.3/4</version>

# ============================

url = jdbc:mysql://localhost:3306/yourdb
driverClassName=com.mysql.jdbc.Driver
username = tests
password = tests
filters = stat
maxActive = 30
initialSize = 2
maxWait = 60000
minIdle = 10
maxIdle = 15
timeBetweenEvictionRunsMillis = 60000
minEvictableIdleTimeMillis = 300000
validationQuery = SELECT 1
testWhileIdle = true
testOnBorrow = false
testOnReturn = false
maxOpenPreparedStatements = 20
removeAbandonedTimeout = 1800
removeAbandoned = true
logAbandoned = true

# ============================
jdbc.driverClassName=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/yourdb?useUnicode=true&characterEncoding=UTF-8&autoReconnect=true&failOverReadOnly=false
jdbc.username=tests
jdbc.password=tests
jdbc.maxActive=20
jdbc.initialSize=2
jdbc.maxWait=60000
jdbc.minIdle=2
jdbc.poolPreparedStatements=true
jdbc.maxOpenPreparedStatements=20
jdbc.testWhileIdle=true
jdbc.testOnBorrow=false
jdbc.testOnReturn=false

# ============================
driverClassName=com.mysql.jdbc.Driver
url=jdbc:mysql://127.0.0.1:3306/test?characterEncoding=utf-8
username=tests
password=tests
filters=stat
initialSize=2
maxActive=300
maxWait=60000
timeBetweenEvictionRunsMillis=60000
minEvictableIdleTimeMillis=300000
validationQuery=SELECT 1
testWhileIdle=true
testOnBorrow=false
testOnReturn=false
poolPreparedStatements=false
maxPoolPreparedStatementPerConnectionSize=200

# ============================
@@@ &statementInterceptors=com.right.framework.utils.ShowSqlStatementInterceptor

<Resource 
    name="jdbc/ds_oracle"
    factory="com.alibaba.druid.pool.DruidDataSourceFactory"
    auth="Container"
    type="javax.sql.DataSource"
    driverClassName="oracle.jdbc.OracleDriver"
    url="jdbc:oracle:thin:@192.168.1.10:1521:yourdb"
    username="tests"
    password="tests"
    maxActive="50"
    maxWait="10000"
    removeabandoned="true"
    removeabandonedtimeout="60"
    logabandoned="false"
    filters="stat"/>

<Resource 
    name="jdbc/ds_mysql"
    factory="com.alibaba.druid.pool.DruidDataSourceFactory"
    auth="Container"
    type="javax.sql.DataSource"
    driverClassName="com.mysql.jdbc.Driver"
    url="jdbc:mysql://192.168.1.10:3306/yourdb?useUnicode=true&amp;characterEncoding=utf-8"
    username="tests"
    password="tests"
    maxActive="50"
    maxWait="10000"
    removeabandoned="true"
    removeabandonedtimeout="60"
    logabandoned="false"
    filters="stat"/>

<Resource 
    name="jdbc/ds_sqlms"
    auth="Container"
    factory="com.alibaba.druid.pool.DruidDataSourceFactory" 
    type="javax.sql.DataSource"
    driverClass="com.microsoft.sqlserver.jdbc.SQLServerDriver"
    url="jdbc:sqlserver://192.168.1.11:1433;DatabaseName=yourdb"
    username="sa" 
    password="tests"
    maxActive="50"
    maxWait="10000"
    removeabandoned="true"
    removeabandonedtimeout="60"
    logabandoned="false"
    filters="stat"/>

# 在web.xml引用JDNI数据源 #
    
<resource-ref>
    <description>Oracle DB Connection</description>
    <res-ref-name>jdbc/ds_oracle</res-ref-name>
    <res-type>javax.sql.DataSource</res-type>
    <res-auth>Container</res-auth>
</resource-ref>

<resource-ref>
    <description>MySQL DB Connection</description>
    <res-ref-name>jdbc/ds_mysql</res-ref-name>
    <res-type>javax.sql.DataSource</res-type>
    <res-auth>Container</res-auth>
</resource-ref>

<resource-ref>
    <description>SQLServer DB Connection</description>
    <res-ref-name>jdbc/ds_sqlms</res-ref-name>
    <res-type>javax.sql.DataSource</res-type>
    <res-auth>Container</res-auth>
</resource-ref>

# =======================================
<servlet>
	<servlet-name>DruidStatView</servlet-name>
	<servlet-class>com.alibaba.druid.support.http.StatViewServlet
	</servlet-class>
	<init-param>
		<param-name>resetEnable</param-name>
		<param-value>true</param-value>
	</init-param>
	<init-param>
		<param-name>loginUsername</param-name>
		<param-value>admin</param-value>
	</init-param>
	<init-param>
		<param-name>loginPassword</param-name>
		<param-value>admin</param-value>
	</init-param>
</servlet>
<servlet-mapping>
	<servlet-name>DruidStatView</servlet-name>
	<url-pattern>/druid/*</url-pattern>
</servlet-mapping>

# =======================================

<bean id="dataSource" class="org.springframework.jndi.JndiObjectFactoryBean">
	<property name="jndiName">
		<value>java:comp/env/jdbc/ds_h2db</value>
	</property>
</bean>

<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource"
	destroy-method="close">
	<property name="driverClassName" value="${jdbc.driver}" />
	<property name="url" value="${jdbc.url}" />
	<property name="username" value="${jdbc.username}" />
	<property name="password" value="${jdbc.password}" />
	<property name="defaultAutoCommit" value="false" />
	<property name="initialSize" value="2" />
	<property name="maxActive" value="10" />
	<property name="maxWait" value="60000" />
</bean>

<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource"
	init-method="init" destroy-method="close">
	<property name="url" value="${jdbc.url}" />
	<property name="username" value="${jdbc.username}" />
	<property name="password" value="${jdbc.password}" />
	<property name="initialSize" value="${jdbc.initialPoolSize}" />
	<property name="minIdle" value="${jdbc.minPoolSize}" />
	<property name="maxActive" value="${jdbc.maxPoolSize}" />
	<property name="validationQuery" value="${jdbc.validationQuery}" />
	<property name="maxWait" value="60000" />
	<property name="timeBetweenEvictionRunsMillis" value="60000" />
	<property name="minEvictableIdleTimeMillis" value="300000" />
	<property name="testWhileIdle" value="true" />
	<property name="testOnBorrow" value="false" />
	<property name="testOnReturn" value="false" />
	<property name="poolPreparedStatements" value="true" />
	<property name="maxPoolPreparedStatementPerConnectionSize"
		value="20" />
	<property name="filters" value="stat,log4j,wall" />
</bean>

<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource"
	init-method="init" destroy-method="close">
	<property name="url" value="${jdbc_url}" />
	<property name="username" value="${jdbc_user}" />
	<property name="password" value="${jdbc_password}" />
	<property name="filters" value="stat" />
	<property name="maxActive" value="20" />
	<property name="initialSize" value="1" />
	<property name="maxWait" value="60000" />
	<property name="minIdle" value="1" />
	<property name="timeBetweenEvictionRunsMillis" value="60000" />
	<property name="minEvictableIdleTimeMillis" value="300000" />
	<property name="validationQuery" value="SELECT 'x'" />
	<property name="testWhileIdle" value="true" />
	<property name="testOnBorrow" value="false" />
	<property name="testOnReturn" value="false" />
	<property name="poolPreparedStatements" value="true" />
	<property name="maxPoolPreparedStatementPerConnectionSize" value="50" />
</bean>

<bean id="mainDataSource" class="com.alibaba.druid.pool.DruidDataSource"
	init-method="init" destroy-method="close">
	<!-- 基本属性 url、user、password -->
	<property name="url" value="${main.db.jdbcUrl}" />
	<property name="username" value="${main.db.username}" />
	<property name="password" value="${main.db.password}" />
	<!-- 配置初始化大小、最小、最大 -->
	<property name="initialSize" value="${main.db.initialSize}" />
	<property name="minIdle" value="${main.db.minIdle}" />
	<property name="maxActive" value="${main.db.maxActive}" />
	<!-- 配置获取连接等待超时的时间 -->
	<property name="maxWait" value="${main.db.maxWait}" />
	<!-- 配置间隔多久才进行一次检测，检测需要关闭的空闲连接，单位是毫秒 -->
	<property name="timeBetweenEvictionRunsMillis" value="50" />
	<!-- 配置一个连接在池中最小生存的时间，单位是毫秒 -->
	<property name="minEvictableIdleTimeMillis" value="300000" />
	<property name="validationQuery" value="select 1" />
	<property name="testWhileIdle" value="true" />
	<property name="testOnBorrow" value="true" />
	<property name="testOnReturn" value="true" />
	<!-- 超过时间限制是否回收 -->
	<property name="removeAbandoned" value="true" />
	<!-- 超时时间；单位为秒。180秒=3分钟 -->
	<property name="removeAbandonedTimeout" value="500000000" />
	<!-- 关闭abanded连接时输出错误日志 -->
	<property name="logAbandoned" value="true" />
	<!-- 打开PSCache，并且指定每个连接上PSCache的大小 -->
	<!--property name="poolPreparedStatements" value="true"/> <property name="maxPoolPreparedStatementPerConnectionSize" 
		value="20"/ -->
	<!-- 配置监控统计拦截的filters。状态统计：stat，日常记录：slf4j -->
	<property name="filters" value="stat,slf4j" />
</bean>

<bean id="dataSource" class="org.vibur.dbcp.ViburDBCPDataSource"
	init-method="start" destroy-method="terminate">
	<property name="jdbcUrl" value="jdbc:hsqldb:mem:sakila;shutdown=false" />
	<property name="username" value="sa" />
	<property name="password" value="" />
	<property name="poolInitialSize">10</property>
	<property name="poolMaxSize">100</property>
	<property name="connectionIdleLimitInSeconds">30</property>
	<property name="testConnectionQuery">isValid</property>
	<property name="logQueryExecutionLongerThanMs" value="500" />
	<property name="logStackTraceForLongQueryExecution" value="true" />
	<property name="statementCacheMaxSize" value="200" />
</bean>


# 在web.xml中配置，添加统计监控filter，访问监控页面：http://192.168.1.12:8081/views/druid

# ==================================
<filter>
  <filter-name>DruidWebStatFilter</filter-name>
  <filter-class>com.alibaba.druid.support.http.WebStatFilter</filter-class>
  <init-param>
  <param-name>exclusions</param-name>
  <param-value>*.js,*.gif,*.jpg,*.png,*.css,*.ico,/druid/*</param-value>
  </init-param>
</filter>
<filter-mapping>
    <filter-name>DruidWebStatFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
<servlet>
    <servlet-name>DruidStatView</servlet-name>
    <servlet-class>com.alibaba.druid.support.http.StatViewServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>DruidStatView</servlet-name>
    <url-pattern>/druid/*</url-pattern>
</servlet-mapping>


<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource" init-method="init" destroy-method="close"> 
      <!-- 基本属性 url、user、password -->
      <property name="url" value="${jdbc_url}" />
      <property name="username" value="${jdbc_user}" />
      <property name="password" value="${jdbc_password}" />
      <!-- 配置初始化大小、最小、最大 -->
      <property name="initialSize" value="1" />
      <property name="minIdle" value="1" /> 
      <property name="maxActive" value="20" />
      <!-- 配置获取连接等待超时的时间 -->
      <property name="maxWait" value="60000" />
      <!-- 配置间隔多久才进行一次检测，检测需要关闭的空闲连接，单位是毫秒 -->
      <property name="timeBetweenEvictionRunsMillis" value="60000" />
      <!-- 配置一个连接在池中最小生存的时间，单位是毫秒 -->
      <property name="minEvictableIdleTimeMillis" value="300000" />
      <property name="validationQuery" value="SELECT 1 " />
      <property name="testWhileIdle" value="true" />
      <property name="testOnBorrow" value="false" />
      <property name="testOnReturn" value="false" />
      <!-- 打开PSCache，并且指定每个连接上PSCache的大小 -->
      <property name="poolPreparedStatements" value="true" />
      <property name="maxPoolPreparedStatementPerConnectionSize" value="30" />
      <!-- 配置监控统计拦截的filters -->
      <property name="filters" value="stat" /> 
  </bean>
  
<!-- 只需要修改initialSize、minIdle、maxActive。
如果用Oracle，则把poolPreparedStatements配置为true，mysql可以配置为false。
分库分表较多的数据库，建议配置为false。-->


<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource" init-method="init" destroy-method="close">
   <property name="driverClassName" value="${jdbc.driverClassName}" />
   <property name="url" value="${jdbc.url}" />
   <property name="username" value="${jdbc.username}" />
   <property name="password" value="${jdbc.password}" />
   <property name="filters" value="stat" />
   连接池的最大数据库连接数。设为0表示无限制。一般把maxActive设置成可能的并发量就行了
   <property name="maxActive" value="1000" />
   初始化大小
   <property name="initialSize" value="10" />
   最大等待毫秒数, 单位为 ms, 如果超过此时间将接到异常,设为-1表示无限制
   <property name="maxWait" value="60000" />
   最大等待(空闲)连接中的数量,设 0 为没有限制
   <property name="maxIdle" value="100" />
   最小等待(空闲)连接中的数量
   <property name="minIdle" value="10" />
   在空闲连接回收器线程运行期间休眠的时间值,以毫秒为单位. 如果设置为非正数,则不运行空闲连接回收器线程
   <property name="timeBetweenEvictionRunsMillis" value="60000" />
   连接池中保持空闲而不被空闲连接回收器线程 ，回收的最小时间值，单位毫秒
   <property name="minEvictableIdleTimeMillis" value="300000" />
   SQL查询,用来验证从连接池取出的连接,在将连接返回给调用者之前.如果指定, 则查询必须是一个SQL SELECT并且必须返回至少一行记录
   <property name="validationQuery" value="SELECT 'x'" />
   指明连接是否被空闲连接回收器(如果有)进行检验.如果检测失败, 则连接将被从池中去除.
   注意: 设置为true后如果要生效,validationQuery参数必须设置为非空字符串
   <property name="testWhileIdle" value="true" />
   指明是否在从池中取出连接前进行检验,如果检验失败 则从池中去除连接并尝试取出另一个. 注意: 设置为true后如果要生效,validationQuery参数必须设置为非空字符串
   <property name="testOnBorrow" value="false" />
   指明是否在归还到池中前进行检验
   <property name="testOnReturn" value="false" />
   开启池的prepared statement 池功能
   <property name="poolPreparedStatements" value="true" />
   <property name="maxPoolPreparedStatementPerConnectionSize" value="50" />
</bean>

<servlet>
	<servlet-name>DruidStatView</servlet-name>
	<servlet-class>com.alibaba.druid.support.http.StatViewServlet</servlet-class>
</servlet>
<servlet-mapping>
	<servlet-name>DruidStatView</servlet-name>
	<url-pattern>/druid/*</url-pattern>
<servlet-mapping>
  
  
  