

# Deploy springboot project to Tomcat



## Allow Tomcat Manager & Host Manager Access from Remote Host

This means you will be able to go to http://3.15.43.206:8080/manager/html/



Create a new file called `manager.xml` 

```bash
sudo vim /opt/tomcat/conf/Catalina/localhost/manager.xml
```

Now add the following lines to the file:

```xml
<Context privileged="true" antiResourceLocking="false" 
         docBase="{catalina.home}/webapps/manager">
    <Valve className="org.apache.catalina.valves.RemoteAddrValve" allow="^.*$" />
</Context>
```

If you have not used `vim` before then you need to figure out how to do that or you can watch this video on creating a new file in `vim`: https://www.youtube.com/watch?v=FLCCqzwHB5s



Now do the same with this file:

```bash
sudo vim /opt/tomcat/conf/Catalina/localhost/host-manager.xml
```

```xml
<Context privileged="true" antiResourceLocking="false" 
         docBase="${catalina.home}/webapps/host-manager">
    <Valve className="org.apache.catalina.valves.RemoteAddrValve" allow="^.*$" />
</Context>
```



## Adding a user to the tomcat server



```bash
vim /opt/tomcat/conf/tomcat-users.xml
```

Add the following before  the `</tomcat-users>` tag

```xml
<role rolename="manager-gui"/>
<user username="USERNAME" password="PASSWORD" roles="manager-gui"/>
```



### Building the WAR file

In your `pom.xml` file add the following

```xml
<packaging>war</packaging>
```

Also remember to add the java version to your `pom.xml` file. Remember to install the latest version og java on the server: `sudo yum install java`

```xml
<properties>
    <java.version>1.8</java.version>
</properties>
```

Now in IntelliJ when you go to `file -> Project structure -> artifacts` there should two: 

1. `PROJECTNAME:war`
2. `PROJECTNAME:war exploded`

If not you need to add them using the `+`



Now to build the `war` file click `Build -> Build Artifacts -> All Artifacts`

A new folder called `target` will be built, the `war` file to use is the file called `PROJECTNAME-VERSION.war` so fx `social-media-site-1.0.war`

This is the file to upload



## Deploying a webapplication

Go to http://YOUR_IP:8080/manager/html



Where is says `WAR file to deploy` find your war file created above and deploy it. In your `pom.xml` file remember to add this to specify the java version

