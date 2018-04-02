

Vibur DBCP - concurrent and dynamic JDBC connection pool
Apache-2.0 license

<dependency>
  <groupId>org.vibur</groupId>
  <artifactId>vibur-dbcp</artifactId>
  <version>20.0</version>
</dependency>


Log4j Configuration SnippetAnchor link for: vibur log4j configuration
<logger name="org.vibur.dbcp" additivity="false">
    <level value="debug"/>
    <appender-ref ref="console"/>
</logger>



	public DataSource createDataSourceWithStatementsCache() {
		ViburDBCPDataSource ds = new ViburDBCPDataSource();

		ds.setJdbcUrl("jdbc:hsqldb:mem:sakila;shutdown=false");
		ds.setUsername("sa");
		ds.setPassword("");

		ds.setPoolInitialSize(10);
		ds.setPoolMaxSize(100);

		ds.setConnectionIdleLimitInSeconds(30);
		ds.setTestConnectionQuery("isValid");

		ds.setLogQueryExecutionLongerThanMs(500);
		ds.setLogStackTraceForLongQueryExecution(true);

		ds.setStatementCacheMaxSize(200);

		ds.start();
		return ds;
	}


<bean id="dataSource" class="org.vibur.dbcp.ViburDBCPDataSource" init-method="start" destroy-method="terminate">
   <property name="jdbcUrl" value="jdbc:hsqldb:mem:sakila;shutdown=false"/>
   <property name="username" value="sa"/>
   <property name="password" value=""/> 
   <property name="poolInitialSize">10</property>
   <property name="poolMaxSize">100</property> 
   <property name="connectionIdleLimitInSeconds">30</property>
   <property name="testConnectionQuery">isValid</property> 
   <property name="logQueryExecutionLongerThanMs" value="500"/>
   <property name="logStackTraceForLongQueryExecution" value="true"/> 
   <property name="statementCacheMaxSize" value="200"/>
</bean>



