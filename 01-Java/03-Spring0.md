


<Resource name="jdbc/ds_mysql"
        type="javax.sql.DataSource" 
        factory="org.apache.tomcat.jdbc.pool.DataSourceFactory"
        driverClassName="com.mysql.jdbc.Driver"
        url="jdbc:mysql://localhost:3306/test?useUnicode=true&amp;characterEncoding=UTF-8"
        username="tests"
        password="tests"
        initialSize="10"
        maxActive="100"
        maxIdle="50"
        minIdle="3"
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
        
<bean id="userAccessInterceptor"class="com.yuba.tests.interceptor.UserAccessInterceptor" />

class UserAccessInterceptor extends HandlerInterceptorAdapter {
    @Override
    public boolean preHandle(HttpServletRequest request,HttpServletResponse response, Object handler) throws 

Exception {
        if(handler instanceof ResourceHttpRequestHandler){
            return true;
        }
if(Utils.isNull(UserCookie.getApploginUserId())){
response.sendRedirect(request.getContextPath()+"/login.jsp");
return false;
}
        return true;
    }
}<mvc:interceptors>
	<mvc:interceptor>
		<mvc:mapping path="/*/*" />
		<bean class="com.ziyou.platform.interceptor.SessionTimeoutInterceptor">
			<property name="allowUrls">
				<list>
					<!-- 如果请求中包含以下路径，则不进行拦截 -->
					<value>/login</value>
					<value>/js</value>
					<value>/css</value>
					<value>/image</value>
					<value>/images</value>
				</list>
			</property>
		</bean>
	</mvc:interceptor>
</mvc:interceptors>

<mvc:interceptors>
	<mvc:interceptor>
		<!-- <mvc:mapping path="/**" /> -->
		<mvc:mapping path="/**/*.do" />
		<mvc:mapping path="/**/*.json" />
		<mvc:exclude-mapping path="/**/*.jsp" />
		<mvc:exclude-mapping path="/open/*" />
		<mvc:exclude-mapping path="/webservice/open/*" />
		<bean id="wxInterceptor" class="com.yuba.tests.interceptor.WxInterceptor" />
	</mvc:interceptor>
</mvc:interceptors>

<mvc:interceptors>
	<mvc:interceptor>
		<mvc:mapping path="/*.do" />
		<mvc:mapping path="/*.ajax" />
		<mvc:mapping path="/*.htm" />
		<mvc:mapping path="/*/*.do" />
		<mvc:mapping path="/*/*.ajax" />
		<mvc:mapping path="/*/*.htm" />
		<mvc:exclude-mapping path="/login.htm" />
		<bean class="com.yuba.tests.interceptor.SecurityInterceptor" />
	</mvc:interceptor>
</mvc:interceptors>

<mvc:interceptors>
	<mvc:interceptor>
		<mvc:mapping path="/**" />
		<mvc:mapping path="*.jsp" />
		<mvc:exclude-mapping path="/ropapi*" />
		<mvc:exclude-mapping path="/login" />
		<mvc:exclude-mapping path="/function_list" />
		<bean id="loginInterceptor" class="com.yuba.tests.interceptor.LoginInterceptor" />
	</mvc:interceptor>
</mvc:interceptors>

<mvc:interceptors>
	<mvc:interceptor>
		<mvc:mapping path="/**" />
		<ref bean="userAccessInterceptor" />
	</mvc:interceptor>
</mvc:interceptors>









 
org.apache.tomcat.jdbc.pool.DataSource dataSource = new org.apache.tomcat.jdbc.pool.DataSource();
dataSource.setDriverClassName("com.mysql.jdbc.Driver");
dataSource.setUrl(databaseUrl);
dataSource.setUsername(userName);
dataSource.setPassword(password);

dataSource.setInitialSize(5); // 连接池启动时创建的初始化连接数量（默认值为0）
dataSource.setMaxActive(20); // 连接池中可同时连接的最大的连接数
dataSource.setMaxIdle(12); // 连接池中最大的空闲的连接数，超过的空闲连接将被释放，如果设置为负数表示不限
dataSource.setMinIdle(0); // 连接池中最小的空闲的连接数，低于这个数量会被创建新的连接
dataSource.setMaxWait(60000); // 最大等待时间，当没有可用连接时，连接池等待连接释放的最大时间，超过该时间限制会抛出异常，如果设置-1表示无限等待
dataSource.setRemoveAbandonedTimeout(180); // 超过时间限制，回收没有用(废弃)的连接
dataSource.setRemoveAbandoned(true); // 超过removeAbandonedTimeout时间后，是否进 行没用连接（废弃）的回收
dataSource.setTestOnBorrow(true);
dataSource.setTestOnReturn(true);
dataSource.setTestWhileIdle(true);
dataSource.setValidationQuery("SELECT 1");
dataSource.setTimeBetweenEvictionRunsMillis(1000 * 60 * 30); // 检查无效连接的时间间隔 设为30分钟

public class SessionTimeoutInterceptor  implements HandlerInterceptor{  
    public String[] allowUrls;//还没发现可以直接配置不拦截的资源，所以在代码里面来排除  
    public void setAllowUrls(String[] allowUrls) {  
        this.allowUrls = allowUrls;  
    }  
    @Override  
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response,  
            Object arg2) throws Exception {  
        String requestUrl = request.getRequestURI().replace(request.getContextPath(), "");    
        System.out.println(requestUrl);  
        if(null != allowUrls && allowUrls.length>=1)  
            for(String url : allowUrls) {    
                if(requestUrl.contains(url)) {    
                    return true;    
                }    
            }  
        User user = (User) request.getSession().getAttribute("user");  
        if(user != null) {    
            return true;  //返回true，则这个方面调用后会接着调用postHandle(),  afterCompletion()  
        }else{  
            // 未登录  跳转到登录页面  
            throw new SessionTimeoutException();//返回到配置文件中定义的路径  
        }  
    }  
    @Override  
    public void afterCompletion(HttpServletRequest arg0,  
            HttpServletResponse arg1, Object arg2, Exception arg3)  
            throws Exception {  
    }  
    @Override  
    public void postHandle(HttpServletRequest arg0, HttpServletResponse arg1,  
            Object arg2, ModelAndView arg3) throws Exception {  
    }  
}  

另外，你要在controller中设置session的超时时间  
request.getSession().setMaxInactiveInterval(20);//20秒  
request.getSession().setAttribute("user", user);  

<mvc:interceptors>  
<mvc:interceptor>  
<mvc:mapping path="/organmgt/**" />
<!-- 如果不配置或/*,将拦截所有的Controller --> 
<bean class="com.woaika.loan.front.common.filter.OrgMgtInterceptor" />
</mvc:interceptor>  
</mvc:interceptors> 
   
public class CostTimeInteceptor extends HandlerInterceptorAdapter {
private static final Logger log = LoggerFactory.getLogger(CostTimeInteceptor.class);
@Override
public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws 

Exception {
long startTime = System.currentTimeMillis();
request.setAttribute("startTime", startTime);
return true;
}
@Override
public void postHandle(HttpServletRequest request, HttpServletResponse response, 
     Object handler, ModelAndView modelAndView) throws Exception {
long startTime = (Long) request.getAttribute("startTime");
long endTime = System.currentTimeMillis();
long executeTime = endTime - startTime;
if (log.isInfoEnabled()) log.info("[" + request.getRequestURI() + "] executeTime : " + executeTime + "ms");
}
}
<mvc:interceptors>    
       <mvc:interceptor>    
           <!--设置拦截的路径  mvc:mapping指定到哪个action ,  用mappingURL匹配方法-->    
           <mvc:mapping path="/dynamic/dynamic.do" />    
           <bean class="com.weshare.common.web.LoginInterceptorController">   
                <property name="mappingURL" value="^.*checklogin$" />  
           </bean>    
       </mvc:interceptor>    
   </mvc:interceptors>    
public class LoginInterceptorController extends HandlerInterceptorAdapter {    
    public LoginInterceptorController() {  
    }  
    
    private String mappingURL;// 利用正则映射到需要拦截的路径  
    public void setMappingURL(String mappingURL) {  
        this.mappingURL = mappingURL;  
    }  
  
    public boolean preHandle(HttpServletRequest request,  
            HttpServletResponse response, Object handler) throws Exception {  
        /* 在aC-context.xml中匹配的 /dynamic/dynamic.do, 在这里匹配action 拦截对应的方法 
        String url = request.getRequestURL().toString();  /dynamic/dynamic.do 
        request.getParameter("action");   addDynamic 
        */  
        String url = request.getParameter("action");  
        if (mappingURL == null || url.matches(mappingURL)) {  
            System.out.println("匹配成功、"); 
            return true;  
        }  
        System.out.println("preHandle()");  
        return true;  
    }  
    public void postHandle(HttpServletRequest request,  
            HttpServletResponse response, Object handler,  
            ModelAndView modelAndView) throws Exception {  
        System.out.println("postHandle()");  
    }  
    public void afterCompletion(HttpServletRequest request,  
            HttpServletResponse response, Object handler, Exception ex)  
            throws Exception {  
        System.out.println("afterCompletion()");  
    }  
}  





<Resource type="javax.sql.DataSource"
    name="jdbc/TestDB"
    factory="org.apache.tomcat.jdbc.pool.DataSourceFactory"
    driverClassName="com.mysql.jdbc.Driver"
    url="jdbc:mysql://localhost:3306/mysql"
    username="mysql_user"
    password="mypassword123" />

<Resource type="javax.sql.DataSource"
    name="jdbc/TestDB"
    factory="org.apache.tomcat.jdbc.pool.DataSourceFactory"
    driverClassName="com.mysql.jdbc.Driver"
    url="jdbc:mysql://localhost:3306/mysql"
    username="mysql_user"
    password="mypassword123" />

<bean id="dataSource" class="com.spring.dynamic_datasource.DynamicDataSource">
	<property name="targetDataSources">
		<map key-type="java.lang.String">
			<entry value-ref="datasource_test" key="datasource_test"></entry>
			<entry value-ref="datasource_learn_system" key="datasource_learn_system"></entry>
		</map>
	</property>
	<property name="defaultTargetDataSource" ref="datasource_learn_system"></property>
</bean>
 
<bean id="datasource_test" class="org.apache.commons.dbcp.BasicDataSource">
	<property name="driverClassName" value="com.mysql.jdbc.Driver" />
	<property name="url" value="jdbc:mysql://localhost:3306/test" />
	<property name="username" value="tests" />
	<property name="password" value="tests" />
</bean>

<bean id="datasource_learn_system" class="org.apache.commons.dbcp.BasicDataSource">
	<property name="driverClassName" value="com.mysql.jdbc.Driver" /> 
	<property name="url" value="jdbc:mysql://localhost:3306/learn_system" /> 
	<property name="username" value="tests" />
	<property name="password" value="tests" />
</bean> 

<code>
import org.springframework.jdbc.datasource.lookup.AbstractRoutingDataSource;
public class DynamicDataSource extends AbstractRoutingDataSource {
	public static final String DATASOURCE_TEST = "datasource_test";
	public static final String DATASOURCE_LEARN_SYSTEM = "datasource_learn_system";
	public static final ThreadLocal<String> contextHolder = new ThreadLocal<String>();
	public static void setCustomerType(String customerType) {
		contextHolder.set(customerType);
	}

	public static String getCustomerType() {
		return contextHolder.get();
	}

	public static void clearCustomerType() {
		contextHolder.remove();
	}

	@Override
	protected Object determineCurrentLookupKey() {
		return getCustomerType();
	}
}

 @Override  
public boolean saveUploadPicture(Picture_of_user picture_of_user) {  
    boolean flag = false;  
    sql = "insert into picture_of_user(id,picture_name,picture_size,upload_date,picture_type,username) " +  
            "values(?,?,?,?,?,?);";  
    //切换数据源 datasource_test  
    //这段代码相当于，把String类型的参数 datasource_test 放在了保存到了本地线程的当前线程中，也就是当前正在执行的线程。  
    DynamicDataSource.setCustomerType(DynamicDataSource.DATASOURCE_LEARN_SYSTEM);  
    int i = this.getJdbcTemplate().update(sql, new Object[]{  
            null,  
            picture_of_user.getPicture_name(),  
            picture_of_user.getPicture_size(),  
            picture_of_user.getUpload_date(),  
            picture_of_user.getPicture_type(),  
            picture_of_user.getUsername()  
    });  
    //如果插入操作执行成功，则flag=true；否则flag=flase  
    if(i > 0){  
        //测试输出  
        System.out.println("i = " + i);  
        flag = true;  
    }  
    else{  
        //测试输出  
        System.out.println("i = " + i);  
        flag = false;  
    }  
    return flag;  
}  
</code>


<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
	<property name="driverClassName" value="com.microsoft.sqlserver.jdbc.SQLServerDriver" />
	<property name="url" value="jdbc:sqlserver://localhost:1433;DatabaseName=spring" />
	<property name="username" value="sa" />
	<property name="password" value="tests" />
</bean>

<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
	<property name="driverClassName" value="${jdbc.driverClassName}" />
	<property name="url" value="${jdbc.url}" />
	<property name="username" value="${jdbc.username}" />
	<property name="password" value="${jdbc.password}" />
</bean>

<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
	<property name="driverClassName" value="${jdbc.driverClassName}" />
	<property name="url" value="${jdbc.url}" />
	<property name="username" value="${jdbc.username}" />
	<property name="password" value="${jdbc.password}" />
</bean>

<bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
	<property name="driverClassName" value="${test.jdbc.driverClassName}" />
	<property name="url" value="${test.jdbc.url}" />
	<property name="username" value="${test.jdbc.username}" />
	<property name="password" value="${test.jdbc.password}" />
</bean>

<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource"
	destroy-method="close">
	<property name="driverClassName" value="com.mysql.jdbc.Driver" />
	<property name="url" value="jdbc:mysql://localhost:3309/sampledb" />
	<property name="username" value="root" />
	<property name="password" value="1234" />
</bean>



    
<bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver"/>

<bean id="messageSource" class="org.springframework.context.support.ReloadableResourceBundleMessageSource">
  <property name="basenames">
      <list>
          <value>classpath:/conf/message/i18n_en_US</value>
          <value>classpath:/conf/message/i18n_zh_CN</value>
          <value>classpath:/conf/message/i18n_zh_TW</value>
      </list>
  </property>
  <property name="cacheSeconds" value="5"/>
  <property name="defaultEncoding" value="utf-8"/>
</bean>

<bean id="exceptionResolver" class="com.xyt.staff.mvc.resolver.GsmExceptionResolver">
    <property name="exceptionMappings">
        <props>
          <prop key="java.lang.exception">/error/500.jsp</prop>
        </props>
    </property>
</bean>



<mvc:interceptors>
  <bean id="localeChangeInterceptor" class="org.springframework.web.servlet.i18n.LocaleChangeInterceptor" />
  <mvc:interceptor>
    <!-- 系统拦截器 -->
    <mvc:mapping path="/**" />
    <bean class="com.xyt.staff.mvc.interceptor.ControllerInterceptor">
      <!-- 当传统非AJAX请求时返回页面地址  无登录或会话过期-->
      <property name="noSession" value="/"/>
      <!-- 当传统非AJAX请求时返回页面地址  无权限-->
      <property name="noPermission" value="/"/>
      <!-- 拦截例外-->
      <property name="notCheckURISet">
        <list>
            <value>/front/</value>
            <value>/data/</value>
            <value>/fs/</value>
            <value>/pcOcr/</value>
            <value>/error/</value>
            <value>/upload/</value>
        </list>
      </property>
    </bean>
  </mvc:interceptor>
</mvc:interceptors>






<tx:annotation-driven transaction-manager="transactionManager" proxy-target-class="true" />

<bean id="messageSource" class="org.springframework.context.support.ReloadableResourceBundleMessageSource">
    <property name="basename" value="/WEB-INF/conf/messages" />
    <property name="cacheSeconds" value="3000" />
</bean>

<mvc:annotation-driven />
<mvc:annotation-driven />
<mvc:resources location="/static/" mapping="/static/**" />

<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix" value="/WEB-INF/view" />
    <property name="suffix" value=".jsp" />
</bean>

<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix" value="/WEB-INF/view"></property>
    <property name="suffix" value=".jsp"></property>
</bean>

<bean id="viewResolver" class="org.springframework.web.servlet.view.freemarker.FreeMarkerViewResolver">
    <property name="prefix" value="/WEB-INF/view" />
    <property name="suffix" value=".html" />
    <property name="cache" value="true" />
    <property name="exposeSpringMacroHelpers" value="true" />
    <property name="exposeRequestAttributes" value="true" />
    <property name="exposeSessionAttributes" value="true" />
    <property name="requestContextAttribute" value="rc" />
    <property name="contentType" value="text/html;charset=UTF-8" />
    <property name="order" value="0" />
</bean>


<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
    xmlns:task="http://www.springframework.org/schema/task"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans-3.2.xsd
           http://www.springframework.org/schema/task
           http://www.springframework.org/schema/task/spring-task-3.2.xsd
           http://www.springframework.org/schema/context
           http://www.springframework.org/schema/context/spring-context-3.2.xsd">
           
    <task:executor id="executor" pool-size="5" />  
    <task:scheduler id="scheduler" pool-size="10" />
    <task:annotation-driven executor="executor" scheduler="scheduler" />
    
</beans>

<!-- 
    <aop:aspectj-autoproxy proxy-target-class="true" />
    <bean id="executor" class="org.springframework.scheduling.concurrent.ThreadPoolTaskExecutor">
        <property name="corePoolSize" value="5" />
        <property name="maxPoolSize" value="50" />
        <property name="queueCapacity" value="500" />
    </bean>
 -->
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
    xmlns:task="http://www.springframework.org/schema/task"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans-3.2.xsd
           http://www.springframework.org/schema/task
           http://www.springframework.org/schema/task/spring-task-3.2.xsd
           http://www.springframework.org/schema/context
           http://www.springframework.org/schema/context/spring-context-3.2.xsd">
           
    <task:executor id="executor" pool-size="5" />  
    <task:scheduler id="scheduler" pool-size="10" />
    <task:annotation-driven executor="executor" scheduler="scheduler" />
    
</beans>

<!-- 
    <aop:aspectj-autoproxy proxy-target-class="true" />
    <bean id="executor" class="org.springframework.scheduling.concurrent.ThreadPoolTaskExecutor">
        <property name="corePoolSize" value="5" />
        <property name="maxPoolSize" value="50" />
        <property name="queueCapacity" value="500" />
    </bean>
 -->
 

