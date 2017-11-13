
Apache License 2.0

HikariCP号称是现在性能最好的JDBC连接池组件,Spring现在也集成了HikariCP,具体的性能到底如何,没有仔细的测试过，不过从它现在的发展来看，其可能确实如它宣传的那样其性能高过目前所有的连接池组件。 https://github.com/brettwooldridge/HikariCP

In order to get the best performance out of MySQL, these are some of our recommended settings. 
https://github.com/brettwooldridge/HikariCP/wiki/MySQL-Configuration
A typical MySQL configuration for HikariCP might look something like this:

jdbcUrl=jdbc:mysql://localhost:3306/bizdb
user=tests
password=tests
dataSource.cachePrepStmts=true
dataSource.prepStmtCacheSize=250
dataSource.prepStmtCacheSqlLimit=2048
dataSource.useServerPrepStmts=true
dataSource.useLocalSessionState=true
dataSource.useLocalTransactionState=true
dataSource.rewriteBatchedStatements=true
dataSource.cacheResultSetMetadata=true
dataSource.cacheServerConfiguration=true
dataSource.elideSetAutoCommits=true
dataSource.maintainTimeStats=false




	    <dependency>
	        <groupId>com.zaxxer</groupId>
	        <artifactId>HikariCP-java6</artifactId>
	        <version>2.3.13</version>
	    </dependency>
		<dependency>
	        <groupId>com.zaxxer</groupId>
	        <artifactId>HikariCP-java7</artifactId>
	        <version>2.4.13</version>
	    </dependency>
	    <dependency>
	        <groupId>com.zaxxer</groupId>
	        <artifactId>HikariCP</artifactId>
	        <version>2.7.3</version>
	    </dependency>

Requirements 
⇒ Java 8+ (Java 6/7 artifacts are in maintenance mode)
⇒ slf4j library

Java 8 maven artifact:

    <dependency>
        <groupId>com.zaxxer</groupId>
        <artifactId>HikariCP</artifactId>
        <version>2.7.3</version>
    </dependency>

Java 9 Early Access maven artifact:

    <dependency>
        <groupId>com.zaxxer</groupId>
        <artifactId>HikariCP-java9ea</artifactId>
        <version>2.6.1</version>
    </dependency>

Java 7 maven artifact (maintenance mode):

    <dependency>
        <groupId>com.zaxxer</groupId>
        <artifactId>HikariCP-java7</artifactId>
        <version>2.4.13</version>
    </dependency>

Java 6 maven artifact (maintenance mode):

    <dependency>
        <groupId>com.zaxxer</groupId>
        <artifactId>HikariCP-java6</artifactId>
        <version>2.3.13</version>
    </dependency>


 
import java.sql.Connection;
import java.sql.SQLException;
import com.zaxxer.hikari.HikariConfig;
import com.zaxxer.hikari.HikariDataSource;

public class DataSource {
	private HikariDataSource ds; 
	public void init(int minimum, int Maximum) {
		// 连接池配置
		HikariConfig config = new HikariConfig();
		config.setDriverClassName("com.mysql.jdbc.Driver");
		config.setJdbcUrl("jdbc:mysql://127.0.0.1:3306/test?user=root&password=123456&useUnicode=true&characterEncoding=utf8");
		config.addDataSourceProperty("cachePrepStmts", true);
		config.addDataSourceProperty("prepStmtCacheSize", 500); //128
		config.addDataSourceProperty("prepStmtCacheSqlLimit", 2048); //256
		config.setConnectionTestQuery("SELECT 1");
		config.setAutoCommit(true);
		// 池中最小空闲链接数量
		config.setMinimumIdle(minimum);
		// 池中最大链接数量
		config.setMaximumPoolSize(Maximum);
		ds = new HikariDataSource(config);
	}
 
	public void shutdown() {
		ds.shutdown();
	}
 
	public Connection getConnection() {
		try {
			return ds.getConnection();
		} catch (SQLException e) {
			e.printStackTrace();
			ds.resumePool();
			return null;
		}
	}

	public static void main(String[] args) throws SQLException {
		DataSource ds = new DataSource();
		ds.init(10, 50);
		Connection conn = ds.getConnection();
		// ......
		// 最后关闭链接
		conn.close();
	}
}

Initialization

You can use the HikariConfig class like so1:

HikariConfig config = new HikariConfig();
config.setJdbcUrl("jdbc:mysql://localhost:3306/simpsons");
config.setUsername("bart");
config.setPassword("51mp50n");
config.addDataSourceProperty("cachePrepStmts", "true");
config.addDataSourceProperty("prepStmtCacheSize", "250");
config.addDataSourceProperty("prepStmtCacheSqlLimit", "2048");

HikariDataSource ds = new HikariDataSource(config);

 1 MySQL-specific example, DO NOT COPY VERBATIM.

or directly instantiate a HikariDataSource like so:

HikariDataSource ds = new HikariDataSource();
ds.setJdbcUrl("jdbc:mysql://localhost:3306/simpsons");
ds.setUsername("bart");
ds.setPassword("51mp50n");
...

or property file based:

// Examines both filesystem and classpath for .properties file
HikariConfig config = new HikariConfig("/some/path/hikari.properties");
HikariDataSource ds = new HikariDataSource(config);

Example property file:

dataSourceClassName=org.postgresql.ds.PGSimpleDataSource
dataSource.user=test
dataSource.password=test
dataSource.databaseName=mydb
dataSource.portNumber=5432
dataSource.serverName=localhost

or java.util.Properties based:

Properties props = new Properties();
props.setProperty("dataSourceClassName", "org.postgresql.ds.PGSimpleDataSource");
props.setProperty("dataSource.user", "test");
props.setProperty("dataSource.password", "test");
props.setProperty("dataSource.databaseName", "mydb");
props.put("dataSource.logWriter", new PrintWriter(System.out));

HikariConfig config = new HikariConfig(props);
HikariDataSource ds = new HikariDataSource(config);

There is also a System property available, hikaricp.configurationFile, that can be used to specify the location of a properties file. If you intend to use this option, construct a HikariConfig or HikariDataSource instance using the default constructor and the properties file will be loaded.