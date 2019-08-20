
# tomcat datasource #

## tomcat85 datasource ##
```
<Resource name="jdbc/ds_h2db"
    auth="Container"
    type="javax.sql.DataSource"
    driverClassName="org.h2.Driver"
    url="jdbc:h2:./bin/h2db.db3"
    username="tests"
    password="tests"
    maxIdle="3"
    maxTotal="9"
    maxWaitMillis="6000"
    removeAbandonedOnBorrow="true"
    removeAbandonedTimeout="60"
    validationQuery="select 1"
    testOnBorrow="true"
    logAbandoned="true" />

<Resource name="jdbc/ds_hsql"
    auth="Container"
    type="javax.sql.DataSource"
    driverClassName="org.hsqldb.jdbcDriver"
    url="jdbc:hsqldb:file:~/hsql.db1"
    username="tests"
    password="tests"
    maxIdle="3"
    maxTotal="9"
    maxWaitMillis="6000"
    validationQuery="select count(1) as cnt from information_schema.views"
    removeAbandonedOnBorrow="true"
    removeAbandonedTimeout="60"
    testOnBorrow="true"
    logAbandoned="true" />
    
<Resource name="jdbc/ds_pgsql"
    auth="Container"
    type="javax.sql.DataSource"
    driverClassName="org.postgresql.Driver"
    url="jdbc:postgresql://192.168.0.137:33069/tests"
    username="tests"
    password="tests123"
    maxIdle="3"
    maxTotal="9"
    maxWaitMillis="6000"
    removeAbandonedOnBorrow="true"
    removeAbandonedTimeout="60"
    validationQuery="select 1"
    testOnBorrow="true"
    logAbandoned="true" />

<Resource name="jdbc/ds_mysql"
    auth="Container"
    type="javax.sql.DataSource"
    driverClassName="com.mysql.jdbc.Driver"
    url="jdbc:mysql://192.168.0.137:3306/mdb_test?useUnicode=true&amp;characterEncoding=UTF-8"
    username="tests"
    password="tests"
    maxIdle="3"
    maxTotal="9"
    maxWaitMillis="6000"
    removeAbandonedOnBorrow="true"
    removeAbandonedTimeout="60"
    validationQuery="select 1"
    testOnBorrow="true"
    logAbandoned="true" />
    
    
    <Resource name="jdbc/ds_hsql"
        auth="Container"
        type="javax.sql.DataSource"
        driverClassName="org.hsqldb.jdbcDriver"
        url="jdbc:hsqldb:file:~/hsql.db1"
        username="tests"
        password="tests"
        maxIdle="3"
        maxTotal="9"
        maxWaitMillis="6000"
        validationQuery="select count(1) as cnt from information_schema.views"
        removeAbandonedOnBorrow="true"
        removeAbandonedTimeout="60"
        testOnBorrow="true"
        logAbandoned="true" />

    <Resource name="jdbc/ds_mysql"
        auth="Container"
        type="javax.sql.DataSource"
        driverClassName="com.mysql.jdbc.Driver"
        url="jdbc:mysql://localhost:3306/mdb_test?useUnicode=true&amp;characterEncoding=UTF-8"
        username="tests"
        password="tests"
        maxIdle="3"
        maxTotal="9"
        maxWaitMillis="6000"
        removeAbandonedOnBorrow="true"
        removeAbandonedTimeout="60"
        validationQuery="select 1"
        testOnBorrow="true"
        logAbandoned="true" />

    <Resource name="jdbc/ds_h2db"
        auth="Container"
        type="javax.sql.DataSource"
        driverClassName="org.h2.Driver"
        url="jdbc:h2:./bin/h2db.db3"
        username="tests"
        password="tests"
        maxIdle="3"
        maxTotal="9"
        maxWaitMillis="6000"
        removeAbandonedOnBorrow="true"
        removeAbandonedTimeout="60"
        validationQuery="select 1"
        testOnBorrow="true"
        logAbandoned="true" />

    <Resource name="jdbc/ds_pgsql"
        auth="Container"
        type="javax.sql.DataSource"
        driverClassName="org.postgresql.Driver"
        url="jdbc:postgresql://192.168.0.137:33069/tests"
        username="tests"
        password="tests123"
        maxIdle="3"
        maxTotal="9"
        maxWaitMillis="6000"
        removeAbandonedOnBorrow="true"
        removeAbandonedTimeout="60"
        validationQuery="select 1"
        testOnBorrow="true"
        logAbandoned="true" />

    <Resource name="jdbc/ds_mssql"
        auth="Container"
        type="javax.sql.DataSource"
        driverClassName="net.sourceforge.jtds.jdbc.Driver"
        url="jdbc:jtds:sqlserver://192.168.0.100:9433/xcyfd20180704"
        username="sa"
        password="123456"
        maxIdle="3"
        maxTotal="9"
        maxWaitMillis="6000"
        removeAbandonedOnBorrow="true"
        removeAbandonedTimeout="60"
        validationQuery="select 1"
        testOnBorrow="true"
        logAbandoned="true" />

    <Resource name="jdbc/ds_hsql"
        auth="Container"
        type="javax.sql.DataSource"
        driverClassName="org.hsqldb.jdbcDriver"
        url="jdbc:hsqldb:file:./dat/v2.hsql.db3"
        username="tests"
        password="tests"
        maxIdle="3"
        maxTotal="9"
        maxWaitMillis="6000"
        validationQuery="select count(1) as cnt from information_schema.views"
        removeAbandonedOnBorrow="true"
        removeAbandonedTimeout="60"
        testOnBorrow="true"
        logAbandoned="true" />
```

## tomcat8 tomcat-users.xml ##
```
<role rolename="manager"/>
<role rolename="probeuser"/>
<role rolename="poweruser"/>
<user username="probe" password="probe" roles="manager,poweruser,probeuser"/>
```

## tomcat80 datasource ##


## tomcat70 datasource ##