
Apache License, Version 2.0

<druid.version>1.0.11</druid.version>
<version>1.0.9/11/13 1.1.3/4</version>

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

<!-- Druid 数据库源配置 -->
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



在web.xml中配置，添加统计监控filter，访问监控页面：http://192.168.1.12:8081/views/druid

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


  
  
  