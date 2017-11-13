


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



<bean id="dataSource" class="org.springframework.jndi.JndiObjectFactoryBean">
	<property name="jndiName" value="java.evn:jdbc/ds_mysql" />
</bean>

<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
	<property name="driverClassName" value="${jdbc.driver}" />
	<property name="url" value="${jdbc.url}" />
	<property name="username" value="${jdbc.username}" />
	<property name="password" value="${jdbc.password}" />
	<property name="defaultAutoCommit" value="false" />
	<property name="initialSize" value="2" />
	<property name="maxActive" value="10" />
	<property name="maxWait" value="60000" />
</bean>
    
    

<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource">
    <property name="driverClassName" value="${jdbc.driver}" />
    <property name="url" value="${jdbc.url}" />
    <property name="username" value="${jdbc.username}" />
    <property name="password" value="${jdbc.password}" /> 
    <property name="maxActive" value="${dbcp.maxActive}" />
    <property name="maxIdle" value="${dbcp.maxIdle}" />
    <property name="defaultAutoCommit" value="false" /> 
    <property name="timeBetweenEvictionRunsMillis" value="360000" />
    <property name="minEvictableIdleTimeMillis" value="360000" />
</bean>

<bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource" destroy-method="close">
    <property name="driverClass" value="${jdbc.driverClass}"/>
    <property name="jdbcUrl" value="${jdbc.url}"/>
    <property name="user" value="${jdbc.username}"/>
    <property name="password" value="${jdbc.password}"/>
    <property name="initialPoolSize" value="1"/>
    <property name="minPoolSize" value="1"/>
    <property name="maxPoolSize" value="300"/>
    <property name="maxIdleTime" value="60"/>
    <property name="acquireIncrement" value="5"/>
    <property name="idleConnectionTestPeriod" value="60"/>
</bean>

<bean name="dataSource" class="com.alibaba.druid.pool.DruidDataSource" init-method="init" 

destroy-method="close">
    <property name="url" value="${jdbc.url}" />
    <property name="username" value="${jdbc.username}" />
    <property name="password" value="${jdbc.password}" />
    <property name="initialSize" value="5" /> 
    <property name="maxActive" value="60" /> 
    <property name="maxIdle" value="20" /> 
    <property name="minIdle" value="0" /> 
    <property name="maxWait" value="60000" /> 
    <property name="validationQuery" value="${jdbc.validationQuery}" />
    <property name="testOnBorrow" value="false" />
    <property name="testOnReturn" value="false" />
    <property name="testWhileIdle" value="true" />
    <property name="timeBetweenEvictionRunsMillis" value="60000" /> 
    <property name="minEvictableIdleTimeMillis" value="25200000" /> 
    <property name="removeAbandoned" value="true" /> 
    <property name="removeAbandonedTimeout" value="1800" /> 
    <property name="logAbandoned" value="true" /> 
    <!-- 
    <property name="poolPreparedStatements" value="true" />
    <property name="maxPoolPreparedStatementPerConnectionSize" value="300" />
    <property name="filters" value="stat" /> -->
    <property name="filters" value="mergeStat" />
</bean>

<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource"  destroy-method="close">
    <property name="driverClassName" value="${jdbc.driver}" />
    <property name="url" value="${jdbc.url}" />
    <property name="username" value="${jdbc.user}" />
    <property name="password" value="${jdbc.password}" />
    <property name="maxIdle" value="60" />
    <property name="maxActive" value="100" />
    <property name="timeBetweenEvictionRunsMillis" value="3600000" />
    <property name="minEvictableIdleTimeMillis" value="3600000" />
</bean>

<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
    <property name="driverClassName" value="com.mysql.jdbc.Driver" />
    <property name="url" value="jdbc:mysql://localhost:3306/test?useUnicode=true&amp;characterEncoding=utf8" />
    <property name="username" value="tests" />
    <property name="password" value="tests" />
    <property name="initialSize" value="3" />
    <property name="maxIdle" value="2" />
    <property name="maxActive" value="30" />
    <property name="maxWait" value="10000" />
</bean>

<bean id="txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
    <property name="dataSource" ref="dataSource" />
</bean>

<tx:annotation-driven transaction-manager="txManager" />

<bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
    <property name="dataSource" ref="dataSource" />
</bean>
  
    