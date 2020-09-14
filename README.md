# Docker-Tomcat (Windows Version)
After you have a docker tomcat image pull and run as a container, then you will find several things  
1. Under webapps folder, there has no any folder even for the **ROOT** folder
![Alt text](img/5.JPG?raw=true)

2. If you want to use the tomcat ajp port to connect to a apache server, then the ajp connector tag does not get uncommented
```
<!-- <Connector protocol="AJP/1.3" address="::1" port="8009" redirectPort="8443" /> -->
```
3. For using ajp, you need to add a secret property into that Connector
```
<Connector port="8009" redirectPort="8443" protocol="AJP/1.3" secret="you-secret" secretRequired="true" tomcatAuthentication="false" allowedRequestAttributesPattern=".*" packetSize="65534" address="0.0.0.0"/>
```
4. **::1** in the ajp connector is for ip6, ip4 that you need to define that value as **0.0.0.0**

## Create Tomcat Docker Container Process
1. Pull tomcat image from docker hub
```
docker pull tomcat:8.5-jdk11-openjdk
```
![Alt text](img/1.JPG?raw=true)
2. Create container
```
docker run -dit -p 8085:8080 --name tomcat-init tomcat:8.5-jdk11-openjdk
```
![Alt text](img/2.JPG?raw=true)
![Alt text](img/3.JPG?raw=true)  
3. Using exec command to get into tomcat container
```
winpty docker exec -it tomcat-init //bin//bash
```
![Alt text](img/4.JPG?raw=true)  
4. Because of this is the new tomcat container so in the webapps folder where it's empty  
![Alt text](img/5.JPG?raw=true)  
![Alt text](img/6.JPG?raw=true)  
5. Copty the a ROOT folder with a index.html into the container tomcat webapps  
```
docker cp ROOT tomcat-init:/usr/local/tomcat/webapps
```
![Alt text](img/7.JPG?raw=true)  ![Alt text](img/8.JPG?raw=true)

