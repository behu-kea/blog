# Spring boot dependency injection



Dependency injection means that the spriing container injects objects into other objects. This moves the responsibility of managing components onto the container. 



## Inversion of control

Inversion of control IoC transfers control of objects of portions of a program to a framework. 



## Dependency injection

Dependency injection is a was to implement IoC where the control being inverted is connecting and instantiating obejcts. 

From this where we need to instantiate

```java
public class Store {
    private Item item;
 
    public Store() {
        item = new ItemImpl1();    
    }
}
```

To this where we dont

```java
public class Store {
    private Item item;
    public Store(Item item) {
        this.item = item;
    }
}
```



## Spring IoC container

In Spring there is an IoC container interface called `ApplicationContext`. It manages instantiating, configuring and assembling objects known as beans. We can create a new container by writing 

```java
ApplicationContext context
  = new ClassPathXmlApplicationContext("applicationContext.xml");
```

In order to assemble beans, the container uses configuration metadata,  which can be in the form of XML configuration or annotations.



## More general

As a developer we should not focus on class initiation. We will hand over the responsibility of that to a framework. In Spring that is the Spring container. Its also good for abstraction fx

```
class Laptob {
	private SamsungHarddrive harddrive = new SamsungHarddrive();
}
```

We don't really care about what harddrive, so the spring container should give us the instance of the SamsungHarddrive. Also we can make our program less tight coupled by saying we want a Harddrive and the spring container will give us an instance when we need it. 

```
class Laptob {
	private Harddrive harddrive;
}
```



To tell the springboot application that a class should at some time be instansiated use `@Component` before the class keyword. This will make the class object into a bean. And beans are objects that live in a spring container in the JVM. 

```
@component
class SamsungHarddrive implements Harddrive{
	...
	...
}
```

Now we can rewrite the `laptop` class as follows:

```
class Laptob {
	@Autowired
	private Harddrive harddrive;
}
```



`@Component`  will make the Class object available in a spring container. So the objects in the spring container will get injected when needed. 



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