# Deploy Spring boot to AWS Beanstalk



AWS Beanstalk is an easier way to deploy web application and run web applicaitons. The developer does not need to manage databases, servers, upgrading packages etc. It's all done by Beanstalk



## Creating your first instance

Go to https://us-east-2.console.aws.amazon.com/elasticbeanstalk/home?region=us-east-2#/gettingStarted

Choose `Web server envirenment`

The platform should be  `Java`. As the application code upload a jar file👇

You can also choose Tomcat, but then you need to upload a WAR file. 



## Creating a jar file

So in the `pom.xml` file, add the following 

````xml
<packaging>jar</packaging>
````

Remember to rebuild your maven file now!

Now run this command to build the `jar` file: 

```bash
 ./mvnw package -DskipTests
```

The file will be added to the `target` folder as `APPLICATION_NAME-APPLICATION_VERSION.jar` fx `demo-1.jar` 

If this does not work follow this guide to create a `jar` file: https://www.jetbrains.com/help/idea/compiling-applications.html#package_into_jar



## Adding the right port

If you are running this using `Java` the you need to do this port thing

Now if you go to the application you will probably see a 502 bad gateway, that is because beanstalk is listening on port 5000, but spring boot is running the application on 8080. 



To change that you can do one of these two things:

1. Add `server.port=5000` in your `application.properties` file. Remember to put the `application.properties` in the `/src/main/resources` folder
2. In the Configuration (in the left side of the site, maybe click the hamburger menu to open it). Click `Edit` at the Software category. In the Environment properties add `server.port` as Name and `5000` as Value



## See the logs

You can see the logs in the left side by clicking on Logs. In the top click `Request logs` the select `Last 100 lines` and `Download`



## Something went wrong

- Add a `ServletInitializer.java` in the folder that has the main java file. In my example the folder is called `src/main/java/com/example/demo`

Remember to change the `package`

```java
package com.example.demo;

import org.springframework.boot.builder.SpringApplicationBuilder;
import org.springframework.boot.web.servlet.support.SpringBootServletInitializer;

public class ServletInitializer extends SpringBootServletInitializer {

    @Override
    protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
        return application.sources(DemoApplication.class);
    }

}
```



## Seeing logs from the Spring boot application

If you use Tomcat as the platform then the logs you will se is from Tomcat **not** from the Spring boot application!

To see the logs from the Spring boot application create a new Beanstalk application and as the `Platform branch` select `Tomcat 8.5 with Java 8 running on 64bit Amazon Linux`



![Screenshot 2021-04-22 at 10.01.00](../assets/beanstalk-tomcat.png)



Now if you log something from your Spring boot application you will be able to see them in the logs:

![Beanstalk logs](../assets/beanstalk-logs.png)



![Beanstalk logs Spring boot](../assets/beanstalk-logs-spring-boot.png)



The log is coming from here:

![Spring boot log](../assets/spring-boot-log.png)



So if you get a 500 error message you need to go to the Beanstalk logs and find out what the problem is!