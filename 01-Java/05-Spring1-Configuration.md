 
 ### segment.1 ###
 ``` 
@Configuration
public class WebMvcVDConf implements WebMvcConfigurer {

    @Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/files/**").addResourceLocations("file:./doc/");
        registry.addResourceHandler("/files/uploads/certs/**").addResourceLocations("file:./doc/files/uploads/certs/");
        registry.addResourceHandler("/MP_verify_Ul1ylxEQtzMnAYxQ.txt").addResourceLocations("file:./doc/dat/");
    }
    
    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                .allowedOrigins("*")
                .allowCredentials(true)
                .allowedMethods("GET", "POST", "DELETE", "PUT", "OPTIONS")
                .maxAge(3600);

        registry.addMapping("/wx/**")
		        .allowedOrigins("*")
		        .allowCredentials(true)
		        .allowedMethods("GET", "POST", "DELETE", "PUT", "OPTIONS")
		        .maxAge(3600);        
    }
} 
 ```
 