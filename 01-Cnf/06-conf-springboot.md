
### SpringBoot conf: ssl cert ###
```
server.port=443
server.ssl.key-store=/usr/local/tomcat85/www.xxx.cn.jks
server.ssl.key-store-password=28f2u95g433
server.ssl.key-store-type=JKS

```

### SpringBoot conf: close start banner ###
```
spring.main.banner-mode=off
```

### SpringBoot conf: use jsp as template ###
```
# spring.thymeleaf.cache=false
# spring.thymeleaf.enabled=false

spring.mvc.view.prefix=/WEB-INF/views/
spring.mvc.view.suffix=.jsp
```
