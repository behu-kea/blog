# Spring rest

Spring boot has some built in functinoality for creating a rest controller



## Installing Spring rest

Sprint Rest is a part of the spring web dependency

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```



## Rest controller

Annotate a controller with the `@RestController` annotation. Tells spring boot that we will do some request mapping. It's like the `@controller` but different because the `@Controller` annotation looks for a view, but in the `RestController` we will be returning some data



Just like we have done in the `@Controller` class we can define a `GetMapping`. In the `@Controller` we would return a string with the name of the view or we would add `@ResponseBody`. But in the `@RestController` we only need to return the type that we are working with. Then Spring boot will take care of converting the model to JSON

```java
@RestController
public class StudentController {
    @GetMapping("/student")
    public Student getStudent(@RequestParam(value = "name") String name) {
        Student student = new Student(new Long(1), name, "asd", "2", 23);

        return student;
    }
}
```

