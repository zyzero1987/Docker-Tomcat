# Docker-Tomcat
After you have a docker tomcat image pull and run as a container, then you will find several things  
1. Under webapps folder, there has no any folder even for the **ROOT** folder
2. If you want to use the tomcat ajp port to connect to a apache server, then the ajp connector tag does not get uncommented
```
<!-- <Connector protocol="AJP/1.3" address="::1" port="8009" redirectPort="8443" /> -->
```
3. For using ajp, you need to add a secret property into that Connector
```
<Connector port="8009" redirectPort="8443" protocol="AJP/1.3" secret="you-secret" secretRequired="true" tomcatAuthentication="false" allowedRequestAttributesPattern=".*" packetSize="65534" address="0.0.0.0"/>
```
4. **::1** in the ajp connector is for ip6, ip4 that you need to define that value as **0.0.0.0**
