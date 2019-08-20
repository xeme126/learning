
返回到某一页面
如果是数据，则页面只有${data}
否则是视图

//@MultipartConfig
//@WebServlet(urlPatterns="/*")

@Bean  
public MultipartConfigElement multipartConfigElement() {  
    MultipartConfigFactory factory = new MultipartConfigFactory();  
    factory.setMaxFileSize("10240KB"); //KB,MB
    factory.setMaxRequestSize("102400KB");  
    return factory.createMultipartConfig();  
}  


private String srnd() {
    long num = 0l;
    try {
        SecureRandom sr = SecureRandom.getInstance("SHA1PRNG");
        num = sr.nextLong();
    } catch (Exception e) {
        num = Math.round(Math.random()*100000000);
    }
    return Long.toString(num, 36).substring(1);
}

private Method[] getAllDeclaredMethods(Class c) {

    if (c.equals(javax.servlet.http.HttpServlet.class)) {
        return null;
    }

    Method[] parentMethods = getAllDeclaredMethods(c.getSuperclass());
    Method[] thisMethods = c.getDeclaredMethods();

    if ((parentMethods != null) && (parentMethods.length > 0)) {
        Method[] allMethods =  new Method[parentMethods.length + thisMethods.length];
        System.arraycopy(parentMethods, 0, allMethods, 0,  parentMethods.length);
        System.arraycopy(thisMethods, 0, allMethods, parentMethods.length,  thisMethods.length);
        thisMethods = allMethods;
    }
    return thisMethods;
}




@Configuration  
@SpringBootApplication  

@Bean
public MultipartConfigElement multipartConfigElement() {  
    MultipartConfigFactory factory = new MultipartConfigFactory();  
    //factory.setMaxFileSize("10240KB"); //KB,MB  
    //factory.setMaxRequestSize("102400KB");  
    factory.setMaxFileSize("10MB");
    factory.setMaxRequestSize("100MB");  
    return factory.createMultipartConfig();  
}  

@Bean
public TomcatEmbeddedServletContainerFactory tomcatEmbedded() {

    TomcatEmbeddedServletContainerFactory tomcat = new 
         TomcatEmbeddedServletContainerFactory();

    tomcat.addConnectorCustomizers((TomcatConnectorCustomizer) connector -> {
    
        // connector other settings...

        // configure maxSwallowSize
        if ((connector.getProtocolHandler() instanceof AbstractHttp11Protocol<?>)) {
            // -1 means unlimited, accept bytes
            ((AbstractHttp11Protocol<?>) 
             connector.getProtocolHandler()).setMaxSwallowSize(-1);
        }
        
    });

    return tomcat; 
}



import javax.servlet.MultipartConfigElement;
import javax.sql.DataSource;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration;
import org.springframework.boot.autoconfigure.jdbc.DataSourceBuilder;
import org.springframework.boot.builder.SpringApplicationBuilder;
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.boot.web.servlet.ServletRegistrationBean;
import org.springframework.boot.web.support.SpringBootServletInitializer;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Primary;
import org.springframework.jdbc.core.JdbcTemplate;

import com.nyzy.sample.conf.MyServlet;

import net.sf.log4jdbc.Log4jdbcProxyDataSource;

//@ServletComponentScan(value = "com.nyzy.smaple.ssfh")
//@ServletComponentScan
@SpringBootApplication
@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})
public class AppSpringBoot extends SpringBootServletInitializer {
	private final static Logger LOG = LoggerFactory.getLogger(AppSpringBoot.class);
	public static void main(String[] args) {
		SpringApplication.run(AppSpringBoot.class, args);
	}

	protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
		LOG.info("A00 - SpringBootServletInitializer ~");
		return application.sources(AppSpringBoot.class);
	}
	
	@Bean
	public ServletRegistrationBean myServlet2() {
		//(String location, long maxFileSize, long maxRequestSize, int fileSizeThreshold)
		//MultipartConfigElement multipartConfig = new MultipartConfigElement(location);
		//return new ServletRegistrationBean<MyServlet>(new MyServlet(), "/my/*");
		String location = null;
		ServletRegistrationBean registrationBean = new ServletRegistrationBean();
		registrationBean.setMultipartConfig(new MultipartConfigElement(location));
		registrationBean.setServlet(new MyServlet());
		registrationBean.addUrlMappings("/my/*");
		return registrationBean;
	}

//	@Bean
//	public ServletRegistrationBean<MyServlet> myServlet() {
//		return new ServletRegistrationBean<MyServlet>(new MyServlet(), "/my/*");
//	}
//
//	@Bean
//	public ServletRegistrationBean<MyServlet> myServlet2() {
//		String location = null;
//		//MultipartConfigElement multipartConfig = new MultipartConfigElement(location);
//		//return new ServletRegistrationBean<MyServlet>(new MyServlet(), "/my/*");
//		ServletRegistrationBean<MyServlet> registrationBean = new ServletRegistrationBean<MyServlet>();
//		registrationBean.setMultipartConfig(new MultipartConfigElement(location));
//		registrationBean.setServlet(new MyServlet());
//		registrationBean.addUrlMappings("/my/*");
//		return registrationBean;
//	}
	
	@Bean(name = "dataSource1")
	@Qualifier(value = "dataSource1")
	@ConfigurationProperties(prefix = "spring.datasource")
	public DataSource createDataSource() {
		LOG.info("010 --> createDataSource");
		return DataSourceBuilder.create().build();
	}

	@Primary
	@Bean(name="dataSource")
	@Qualifier(value = "dataSource")
	public Log4jdbcProxyDataSource createProxyDataSource(@Qualifier("dataSource1") DataSource dataSource) {
		LOG.info("020 --> createProxyDataSource");
		return new Log4jdbcProxyDataSource(dataSource);
	}

	@Primary
	@Bean(name = "jdbcTemplate")
	@Qualifier(value = "jdbcTemplate")
	public JdbcTemplate jdbcTemplate(@Qualifier("dataSource") DataSource dataSource) {
		LOG.info("030 --> jdbcTemplate");
		return new JdbcTemplate(dataSource);
	}

	@Bean(name = "dataSource1a")
	@Qualifier(value = "dataSource1a")
	@ConfigurationProperties(prefix = "spring.datasource")
	public DataSource createDataSource1() {
		LOG.info("010 --> createDataSource1");
		return DataSourceBuilder.create().build();
	}

	@Bean(name="dataSource1a1")
	@Qualifier(value = "dataSource1a1")
	public Log4jdbcProxyDataSource createProxyDataSource1(@Qualifier("dataSource1a") DataSource dataSource) {
		LOG.info("020 --> createProxyDataSource1");
		return new Log4jdbcProxyDataSource(dataSource);
	}

	@Bean(name = "jdbcTemplate1")
	@Qualifier(value = "jdbcTemplate1")
	public JdbcTemplate jdbcTemplate1(@Qualifier("dataSource1a1") DataSource dataSource) {
		LOG.info("030 --> jdbcTemplate1 ");
		return new JdbcTemplate(dataSource);
	}
	
	@Bean(name = "dataSource3a1")
	@Qualifier(value = "dataSource3a1")
	@ConfigurationProperties(prefix = "spring.datasource.ds3")
	public DataSource createDataSource3() {
		LOG.info("010 --> createDataSource3");
		return DataSourceBuilder.create().build();
	}

	@Bean(name="dataSource3a")
	@Qualifier(value = "dataSource3a")
	public Log4jdbcProxyDataSource createProxyDataSource3(@Qualifier("dataSource3a1") DataSource dataSource) {
		LOG.info("020 --> createProxyDataSource3");
		return new Log4jdbcProxyDataSource(dataSource);
	}

	@Bean(name = "jdbcTemplate3")
	@Qualifier(value = "jdbcTemplate3")
	public JdbcTemplate jdbcTemplate3(@Qualifier("dataSource3a") DataSource dataSource) {
		LOG.info("030 --> jdbcTemplate3 ");
		return new JdbcTemplate(dataSource);
	}
	
}
