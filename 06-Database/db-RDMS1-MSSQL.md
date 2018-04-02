

create table tba (uid integer identity(1,1) PRIMARY KEY, 
users varchar(50) unique, passw varchar(50), memos varchar(50), state tinyint )

create table tbb (uid integer identity(1,1) PRIMARY KEY, 
users varchar(50) unique, passw varchar(50), memos varchar(50), state tinyint );

# Tomcat数据源须有以下两行中任一行 jdts不支持factory模式 因driver不同而有异  #
type="javax.sql.DataSource"
# －－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－
factory="org.apache.tomcat.jdbc.pool.DataSourceFactory"
# －－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－－

<Resource name="jdbc/ds_sqlms"
        auth="Container"
        type="javax.sql.DataSource"
        driverClassName="net.sourceforge.jtds.jdbc.Driver"
        url="jdbc:jtds:sqlserver://localhost:1433;DatabaseName=abab;"
        username="tests"
        password="tests"
        initialSize="3"
        maxActive="30"
        maxIdle="3"
        minIdle="1"
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

        
<Resource name="jdbc/ds_sqlserver"
        auth="Container"
        type="javax.sql.DataSource"
        driverClassName="net.sourceforge.jtds.jdbc.Driver" 
        url="jdbc:jtds:sqlserver://localhost:1433;DatabaseName=abab;"
        username="tests"
        password="tests"
        initialSize="3"
        maxActive="30"
        maxIdle="3"
        minIdle="1"
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

<Resource name="jdbc/ds_sqlserver"
        auth="Container"
        type="javax.sql.DataSource"
        driverClassName="net.sourceforge.jtds.jdbc.Driver"
        url="jdbc:jtds:sqlserver://localhost:1433;DatabaseName=abab;"
        username="tests"
        password="tests"
        initialSize="3"
        maxActive="30"
        maxIdle="3"
        minIdle="1"
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
        