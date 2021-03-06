


# Maven主聚合继承工程中 #
<distributionManagement>
	<repository>
		<id>nexus-releases</id>
		<name>Nexus Releasse Repository</name>
		<url>http://localhost:8081/nexus/content/repositories/releases/</url>
	</repository>
	<snapshotRepository>
		<id>nexus-snapshots</id>
		<name>Nexus Snapshot Repository</name>
		<url>http://127.0.0.1:8081/nexus/content/repositories/snapshots/</url>
	</snapshotRepository>
</distributionManagement>


# 编译插件 3.3出错 #
<plugin>
	<groupId>org.apache.maven.plugins</groupId>
	<artifactId>maven-compiler-plugin</artifactId>
	<version>2.3.2</version>
	<configuration>
		<source>1.6</source>
		<target>1.6</target>
		<encoding>UTF-8</encoding>
	</configuration>
</plugin>  




<New class="com.mchange.v2.c3p0.ComboPooledDataSource">
	<Set name="driverClassName">com.mysql.jdbc.Driver</Set>
	<Set name="url">jdbc:mysql://host/test</Set>
	<Set name="username">tests</Set>
	<Set name="password">tests</Set>
	<Set name="checkoutTimeout">5000</Set>
	<Set name="initialPoolSize">10</Set>
	<Set name="maxIdleTime">30</Set>
	<Set name="maxPoolSize">160</Set>
	<Set name="minPoolSize">10</Set>
	<Set name="maxStatements">200</Set>
	<Set name="maxConnectionAge">0</Set>
	<Set name="acquireIncrement">15</Set>
</New>

# Spring 4.1+相关 #
<dependency>
	<groupId>com.fasterxml.jackson.core</groupId>
	<artifactId>jackson-core</artifactId>
	<version>2.5.1</version>
</dependency>
<dependency>
	<groupId>com.fasterxml.jackson.core</groupId>
	<artifactId>jackson-databind</artifactId>
	<version>2.5.1</version>
</dependency>
<dependency>
	<groupId>com.fasterxml.jackson.core</groupId>
	<artifactId>jackson-annotations</artifactId>
	<version>2.5.1</version>
</dependency>
# Spring上传用 #
<dependency>
	<groupId>commons-logging</groupId>
	<artifactId>commons-logging</artifactId>
	<version>1.1.2</version>
</dependency>
<dependency>
	<groupId>commons-io</groupId>
	<artifactId>commons-io</artifactId>
	<version>2.2</version>
</dependency>
<dependency>
	<groupId>commons-fileupload</groupId>
	<artifactId>commons-fileupload</artifactId>
	<version>1.2</version>
</dependency>
# 发害邮件用 #
<dependency>
	<groupId>javax.activation</groupId>
	<artifactId>activation</artifactId>
	<version>1.1.1</version>
</dependency>
<dependency>
	<groupId>javax.mail</groupId>
	<artifactId>mail</artifactId>
	<version>1.4.7</version>
</dependency>
<dependency>
	<groupId>javax.servlet</groupId>
	<artifactId>servlet-api</artifactId>
	<scope>provided</scope>
</dependency>
<dependency>
	<groupId>junit</groupId>
	<artifactId>junit</artifactId>
	<scope>test</scope>
</dependency>
<dependency>
	<groupId>jstl</groupId>
	<artifactId>jstl</artifactId>
</dependency>
<dependency>
	<groupId>log4j</groupId>
	<artifactId>log4j</artifactId>
</dependency>
<dependency>
	<groupId>org.slf4j</groupId>
	<artifactId>slf4j-log4j12</artifactId>
</dependency>
<dependency>
	<groupId>org.slf4j</groupId>
	<artifactId>slf4j-api</artifactId>
</dependency>
<dependency>
	<groupId>com.yuba.tests</groupId>
	<artifactId>ayuba-base</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<type>jar</type>
</dependency>
</dependencies>
<dependency>
	<groupId>net.sf.ehcache</groupId>
	<artifactId>ehcache</artifactId>
	<version>2.8.5</version>
</dependency>
<dependency>
	<groupId>aspectj</groupId>
	<artifactId>aspectjweaver</artifactId>
</dependency>
<dependency>
	<groupId>org.aspectj</groupId>
	<artifactId>aspectjweaver</artifactId>
</dependency>
<dependency>
	<groupId>cglib</groupId>
	<artifactId>cglib-nodep</artifactId>
</dependency>
<dependency>
	<groupId>aopalliance</groupId>
	<artifactId>aopalliance</artifactId>
</dependency>
<dependency>
	<groupId>log4j</groupId>
	<artifactId>log4j</artifactId>
</dependency>
<dependency>
	<groupId>org.slf4j</groupId>
	<artifactId>slf4j-log4j12</artifactId>
</dependency>
<dependency>
	<groupId>org.slf4j</groupId>
	<artifactId>slf4j-api</artifactId>
</dependency>
<dependency>
	<groupId>com.h2database</groupId>
	<artifactId>h2</artifactId>
</dependency>
<dependency>
	<groupId>org.hsqldb</groupId>
	<artifactId>hsqldb</artifactId>
</dependency>
<dependency>
	<groupId>com.alibaba</groupId>
	<artifactId>fastjson</artifactId>
</dependency>
<dependency>
	<groupId>com.fasterxml.jackson.core</groupId>
	<artifactId>jackson-core</artifactId>
</dependency>
<dependency>
	<groupId>com.fasterxml.jackson.core</groupId>
	<artifactId>jackson-annotations</artifactId>
</dependency>
<dependency>
	<groupId>com.fasterxml.jackson.core</groupId>
	<artifactId>jackson-databind</artifactId>
</dependency>
<dependency>
	<groupId>com.github.pagehelper</groupId>
	<artifactId>pagehelper</artifactId>
</dependency>
<dependency>
	<groupId>com.github.jsqlparser</groupId>
	<artifactId>jsqlparser</artifactId>
</dependency>
<dependency>
	<groupId>com.alibaba</groupId>
	<artifactId>druid</artifactId>
</dependency>
<dependency>
	<groupId>mysql</groupId>
	<artifactId>mysql-connector-java</artifactId>
</dependency>
<dependency>
	<groupId>org.mybatis</groupId>
	<artifactId>mybatis</artifactId>
</dependency>
<dependency>
	<groupId>org.mybatis</groupId>
	<artifactId>mybatis-spring</artifactId>
</dependency>
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-aop</artifactId>
</dependency>
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-aspects</artifactId>
</dependency>
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-beans</artifactId>
</dependency>
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-core</artifactId>
</dependency>
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-context</artifactId>
</dependency>
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-context-support</artifactId>
</dependency>
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-jdbc</artifactId>
</dependency>
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-tx</artifactId>
</dependency>
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-orm</artifactId>
</dependency>
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-oxm</artifactId>
</dependency>
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-web</artifactId>
</dependency>
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-webmvc</artifactId>
</dependency>
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-instrument</artifactId>
</dependency>
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-test</artifactId>
</dependency>
<dependency>
	<groupId>org.apache.shiro</groupId>
	<artifactId>shiro-core</artifactId>
</dependency>
<dependency>
	<groupId>org.apache.shiro</groupId>
	<artifactId>shiro-ehcache</artifactId>
</dependency>
<dependency>
	<groupId>org.apache.shiro</groupId>
	<artifactId>shiro-spring</artifactId>
</dependency>
<dependency>
	<groupId>org.apache.shiro</groupId>
	<artifactId>shiro-quartz</artifactId>
</dependency>
</dependencies>

<resource-ref>
	<description>struts datasource</description>
	<res-ref-name>jdbc/struts</res-ref-name>
	<res-type>javax.sql.DataSource</res-type>
	<res-auth>Container</res-auth>
</resource-ref>
<resource-ref>
	<description>DB Connection</description>
	<res-ref-name>jdbc/DSTest</res-ref-name>
	<res-type>javax.sql.DataSource</res-type>
	<res-auth>Container</res-auth>
</resource-ref>
<dependency>
	<groupId>org.postgresql</groupId>
	<artifactId>postgresql</artifactId>
	<version>9.4-1200-jdbc4</version>
</dependency>
<dependency>
	<groupId>org.firebirdsql.jdbc</groupId>
	<artifactId>jaybird</artifactId>
	<version>2.1.6</version>
</dependency>
<dependency>
	<groupId>org.apache.httpcomponents</groupId>
	<artifactId>httpclient</artifactId>
	<version>4.3.3</version>
</dependency>
<dependency>
	<groupId>org.apache.httpcomponents</groupId>
	<artifactId>httpcomponents-client</artifactId>
	<version>4.3.3</version>
</dependency>
<dependency>
	<groupId>org.apache.httpcomponents</groupId>
	<artifactId>httpcore</artifactId>
	<version>4.3.2</version>
</dependency>
<dependency>
	<groupId>org.apache.httpcomponents</groupId>
	<artifactId>httpmime</artifactId>
	<version>4.3.3</version>
</dependency>
<dependency>
	<groupId>org.apache.httpcomponents</groupId>
	<artifactId>httpcore-nio</artifactId>
	<version>4.3.2</version>
</dependency>
<dependency>
	<groupId>org.apache.httpcomponents</groupId>
	<artifactId>httpclient-android</artifactId>
	<version>4.3.3</version>
</dependency>
<dependency>
	<groupId>org.apache.tapestry</groupId>
	<artifactId>tapestry-core</artifactId>
	<version>${tapestry.version}</version>
</dependency>
<dependency>
	<groupId>org.apache.tapestry</groupId>
	<artifactId>tapestry-json</artifactId>
	<version>${tapestry.version}</version>
</dependency>
<dependency>
	<groupId>org.apache.tapestry</groupId>
	<artifactId>tapestry-spring</artifactId>
	<version>${tapestry.version}</version>
</dependency>
<dependency>
	<groupId>org.apache.tapestry</groupId>
	<artifactId>tapestry-hibernate-core</artifactId>
	<version>${tapestry.version}</version>
</dependency>
<dependency>
	<groupId>org.apache.tapestry</groupId>
	<artifactId>tapestry-ioc</artifactId>
	<version>${tapestry.version}</version>
</dependency>
<dependency>
	<groupId>org.apache.tapestry</groupId>
	<artifactId>tapestry-upload</artifactId>
	<version>${tapestry.version}</version>
</dependency>
<dependency>
	<groupId>org.apache.commons</groupId>
	<artifactId>commons-dbcp2</artifactId>
	<version>${commons-dbcp2.version}</version>
</dependency>
<dependency>
	<groupId>org.apache.commons</groupId>
	<artifactId>commons-pool2</artifactId>
	<version>${commons-pool2.version}</version>
</dependency>
<dependency>
	<groupId>org.apache.commons</groupId>
	<artifactId>commons-io</artifactId>
	<version>1.3.2</version>
</dependency>
<dependency>
	<groupId>org.apache.commons</groupId>
	<artifactId>commons-lang3</artifactId>
	<version>${commons-lang3.version}</version>
</dependency>
<dependency>
	<groupId>commons-codec</groupId>
	<artifactId>commons-codec</artifactId>
	<version>1.6</version>
</dependency>
<dependency>
	<groupId>org.apache.commons</groupId>
	<artifactId>commons-proxy</artifactId>
	<version>1.0</version>
</dependency>
<dependency>
	<groupId>org.apache.commons</groupId>
	<artifactId>commons-jexl</artifactId>
	<version>2.1.1</version>
</dependency>
<dependency>
	<groupId>org.apache.commons</groupId>
	<artifactId>commons-exec</artifactId>
	<version>1.2</version>
</dependency>
<dependency>
	<groupId>org.apache.commons</groupId>
	<artifactId>commons-compress</artifactId>
	<version>1.8</version>
</dependency>
<dependency>
	<groupId>org.apache.commons</groupId>
	<artifactId>commons-daemon</artifactId>
	<version>1.0.9</version>
</dependency>
<dependency>
	<groupId>org.apache.commons</groupId>
	<artifactId>commons-email</artifactId>
	<version>1.3.2</version>
</dependency>
<dependency>
	<groupId>org.apache.commons</groupId>
	<artifactId>commons-math</artifactId>
	<version>2.2</version>
</dependency>
<dependency>
	<groupId>org.apache.commons</groupId>
	<artifactId>commons-collections4</artifactId>
	<version>4.0</version>
</dependency>
<dependency>
	<groupId>org.kuali.commons</groupId>
	<artifactId>commons-beanutils</artifactId>
	<version>1.8.3-kuali-4</version>
</dependency>
<dependency>
	<groupId>commons-dbutils</groupId>
	<artifactId>commons-dbutils</artifactId>
	<version>1.5</version>
</dependency>
<dependency>
	<groupId>com.googlecode.xmemcached</groupId>
	<artifactId>xmemcached</artifactId>
	<version>1.4.3</version>
</dependency>
<dependency>
	<groupId>opensymphony</groupId>
	<artifactId>oscache</artifactId>
	<version>2.4.1</version>
</dependency>
<dependency>
	<groupId>commons-codec</groupId>
	<artifactId>commons-codec</artifactId>
	<version>1.9</version>
</dependency>
<dependency>
	<groupId>commons-io</groupId>
	<artifactId>commons-io</artifactId>
	<version>1.4</version>
</dependency>
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
<dependency>
	<groupId>commons-logging</groupId>
	<artifactId>commons-logging</artifactId>
	<version>1.2</version>
</dependency>
<dependency>
	<groupId>org.apache.commons</groupId>
	<artifactId>commons-email</artifactId>
	<version>1.3</version>
</dependency>
<dependency>
	<groupId>org.apache.commons</groupId>
	<artifactId>commons-email</artifactId>
	<version>1.3</version>
</dependency>
<dependency>
	<groupId>org.apache.commons</groupId>
	<artifactId>commons-proxy</artifactId>
	<version>1.0</version>
</dependency>



### call dll ### 
		
<dependency>
	<groupId>net.sf.jacob-project</groupId>
	<artifactId>jacob</artifactId>
	<version>1.14.3</version>
</dependency>
<dependency>
	<groupId>org.aspectj</groupId>
	<artifactId>aspectjweaver</artifactId>
	<version>1.8.5</version>
</dependency>
<dependency>
	<groupId>aopalliance</groupId>
	<artifactId>aopalliance</artifactId>
	<version>1.0</version>
</dependency>		

### Shiro相关 ###
<dependency>
    <groupId>org.apache.shiro</groupId>
    <artifactId>shiro-core</artifactId>
    <version>1.1.0</version>
</dependency>
<dependency>
    <groupId>org.apache.shiro</groupId>
    <artifactId>shiro-web</artifactId>
    <version>1.1.0</version>
</dependency>
<dependency>
    <groupId>org.apache.shiro</groupId>
    <artifactId>shiro-spring</artifactId>
    <version>1.1.0</version>
</dependency>

