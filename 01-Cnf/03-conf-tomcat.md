
### tomcat8.5 maxSwallowSize ###
- maxSwallowSize="209715203"
```    
<Connector port="80" protocol="HTTP/1.1"
	connectionTimeout="20000"
	maxSwallowSize="209715200"
    redirectPort="8443" />

```

### tomcat8.5 ssl cert conf ###
```
	<Connector port="443" protocol="org.apache.coyote.http11.Http11NioProtocol"
		maxThreads="150" minSpareThreads="30" maxSpareThreads="200"
		acceptCount="200" SSLEnabled="true" defaultSSLHostConfigName="www.powspot.cn">
		<SSLHostConfig hostName="www.powspot.cn">
			<Certificate certificateKeystoreFile="/usr/local/java/www.aaa.cn.jks"
				certificateKeystorePassword="28f2u95g433" type="RSA" />
		</SSLHostConfig>
	</Connector>
```