# Spring boot testing



## Testing

Very shortly testing is about writing tests that ensures that the code you have written works and runs as expected. 



### Testing in Springboot

Under the `src` folder there should be a folder called `test`. Under this folder you should put your tests.



```java
@SpringBootTest
public class CinemaTest {
    @Test
    void testSomething() {
        int variableToTest = 1;
        assertEquals(1, variableToTest);
    }
}
```

 To create a test class in Spring boot write the `@SpringBootTest` annotation to tell spring boot that it is a test class you have created. 

To create a test write the `@Test` annotation before a `void`function. To test if two things are equal call the `assertEquals`. First argument is the expected value, second argument is the actual value. To run the test, right click the file and select run. 



## Mocking

Unit tests are testing single classes. But what if that class depends on other classes? Which more often than not is the case. Then we use mocking. Here we mock or create objects of a class with values we decide. It is also called a test-double. So its not an object that has values from the real world but values that we as developers have decided. This makes our tests a lot more consistent. 







## Questions

- How does h2 relate to testing and mocking? And how practically can i set it up?
- How do i mock some data in fx testing some repository function?
- Is there a smart way to run the tests?