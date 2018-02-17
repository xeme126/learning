
https://ignite.apache.org/
https://www.zybuluo.com/liyuj/note/230739
https://github.com/ptupitsyn/ignite-multi-platform-demo

		<ignite.version>2.1.0</ignite.version>
		<ignite.version>1.9.0</ignite.version>
		<dependency>
			<groupId>org.apache.ignite</groupId>
			<artifactId>ignite-web</artifactId>
			<version>${ignite.version}</version>
		</dependency>
		<dependency>
			<groupId>org.apache.ignite</groupId>
			<artifactId>ignite-core</artifactId>
			<version>${ignite.version}</version>
		</dependency>
		<dependency>
			<groupId>org.apache.ignite</groupId>
			<artifactId>ignite-spring</artifactId>
			<version>${ignite.version}</version>
		</dependency> 
		<dependency>
			<groupId>org.apache.ignite</groupId>
			<artifactId>ignite-indexing</artifactId>
			<version>${ignite.version}</version>
		</dependency>

<bean class="org.springframework.jdbc.datasource.DriverManagerDataSource" id="dataSource">
    <property name="driverClassName" value="com.mysql.jdbc.Driver"></property>
    <property name="url" value="jdbc:mysql://localhost:3306/mydbname"></property>
    <property name="username" value="tests"></property>
    <property name="password" value="tests"></property>
</bean>

<bean class="org.apache.ignite.configuration.IgniteConfiguration" id="ignite.cfg">
    <property name="cacheConfiguration">
        <list>
            <bean class="org.apache.ignite.configuration.CacheConfiguration">
                <property name="name" value="personCache"></property>
                <property name="readThrough" value="true"></property>
                <property name="writeThrough" value="true"></property>
                <property name="cacheStoreFactory">
                    <bean class="javax.cache.configuration.FactoryBuilder" factory-method="factoryOf">
                        <constructor-arg value="myexamples.store.PersonStore"></constructor-arg>
                    </bean>
                </property>
                <property name="queryEntities">
                    <list>
                        <bean class="org.apache.ignite.cache.QueryEntity">
                            <property name="keyType" value="java.lang.Long"></property>
                            <property name="valueType" value="ignite.myexamples.model.Person"></property>
                            <property name="fields">
                                <map>
                                    <entry key="id" value="java.lang.Long"></entry>
                                    <entry key="name" value="java.lang.String"></entry>
                                    <entry key="orgId" value="java.lang.Long"></entry>
                                    <entry key="salary" value="java.lang.Integer"></entry>
                                </map>
                            </property>
                        </bean>
                    </list>
                </property>
            </bean>
        </list>
    </property>
    <property name="peerClassLoadingEnabled" value="true"></property>
</bean>