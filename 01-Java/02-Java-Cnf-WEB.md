



<listener>
  <listener-class>com.yuba.core.listeners.StartupListener</listener-class>
</listener>

<servlet>
  <servlet-name>H2Console</servlet-name>
  <servlet-class>org.h2.server.web.WebServlet</servlet-class>
  <init-param>
    <param-name>webAllowOthers</param-name>
    <param-value></param-value>
  </init-param>
  <init-param>
    <param-name>trace</param-name>
    <param-value></param-value>
  </init-param>
  <load-on-startup>1</load-on-startup>
</servlet>
<servlet-mapping>
  <servlet-name>H2Console</servlet-name>
  <url-pattern>/console/*</url-pattern>
</servlet-mapping>

<servlet>
  <description>startup</description>
  <servlet-name>startup</servlet-name>
  <servlet-class>com.yuba.core.main.StartupServlet</servlet-class>
  <load-on-startup>2</load-on-startup>
</servlet>

<servlet>
  <servlet-name>YumaUploadServlet</servlet-name>
  <servlet-class>com.yuba.util.file.YumaUploadServlet</servlet-class>
</servlet>
<servlet-mapping>
  <servlet-name>YumaUploadServlet</servlet-name>
  <url-pattern>/upload.do</url-pattern>
</servlet-mapping>

<welcome-file-list>
  <welcome-file>index.jsp</welcome-file>
  <welcome-file>index.html</welcome-file>
</welcome-file-list>