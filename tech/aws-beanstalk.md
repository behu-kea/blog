# Deploy Spring boot to AWS Beanstalk



AWS Beanstalk is an easier way to deploy web application and run web applicaitons. The developer does not need to manage databases, servers, upgrading packages etc. It's all done by Beanstalk



## Creating your first instance

Go to https://us-east-2.console.aws.amazon.com/elasticbeanstalk/home?region=us-east-2#/gettingStarted

Choose `Web server envirenment`

The platform should be  `Java`. As the application code upload a jar file👇



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



## Adding the right port

Now if you go to the application you will probably see a 502 bad gateway, that is because beanstalk is listening on port 5000, but spring boot is running the application on 8080. 



To change that you can do one of these two things:

1. Add `server.port=5000` in your `application.properties` file. Remember to put the `application.properties` in the `/src/main/resources` folder
2. In the Configuration (in the left side of the site, maybe click the hamburger menu to open it). Click `Edit` at the Software category. In the Environment properties add `server.port` as Name and `5000` as Value

