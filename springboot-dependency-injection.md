# Spring boot dependency injection



As a developer we should not focus on class initiation. We will hand over the 



To tell the springboot application that a class should at some time be instansiated use `@Component` before the class keyword. This will make the class object into a bean. And beans are objects that live in a spring container in the JVM. 



 It will make the Class object available in a spring container. So the objects in the spring container will get injected when needed. 



`@Autowired` look for a object of the type you are looking for. 

```
@Autowired
Laptop laptop;
```

This will look for the `Laptop` in the spring container.



```
spring.datasource.url=jdbc:mysql://localhost:3306/wishlist
spring.datasource.password=Za3hTu8pstcpSmZ
spring.datasource.user=root
```