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

To create a test write the `@Test` annotation before a `void`function. This test comes from Junit. To test if two things are equal call the `assertEquals`. First argument is the expected value, second argument is the actual value. To run the test, right click the file and select run. 



## Mocking

Unit tests are testing single classes. But what if that class depends on other classes? Which more often than not is the case. Then we use mocking. Here we mock or create objects of a class with values we decide. It is also called a test-double. So its not an object that has values from the real world but values that we as developers have decided. This makes our tests a lot more consistent. 



@DataJpaTest sætter h2databasen op og bruger den



### H2 database

H2 is a memory database that means that it only lives in memory. Everytime springboot is closed the database will be closed aswell. Therefores it is mostly used for testing. 

This is how you install the database 👇

```xml
<dependency>
  <groupId>com.h2database</groupId>
  <artifactId>h2</artifactId>
  <scope>runtime</scope>
</dependency>
```



If you have the h2 database installed and have the `@DataJpaTest` annotation then springboot will use the h2 database. 

```java
@DataJpaTest
public class RepositoryTest {
    @Autowired
    MovieCategoryRepository movieCategoryRepository;

    @Test
    @Sql("/create-movie-category.sql")
    public void testCount(){
        long result = movieCategoryRepository.count();
        assertEquals(2,result);
    }

    @Test
    @Sql("/create-movie-category.sql")
    public void testMovieCategoryName(){
        MovieCategory movieCategory = movieCategoryRepository.findById(1l).get();
        assertEquals("Horror",movieCategory.getName());
    }
}
```

So here we are mocking the `MovieCategoryRepository`. We are mocking it by before we run our test running some sql `@Sql("/create-movie-category.sql")`.  This sql inserts two movie categories (mocking some data). Then basiscally when using the repository with fx `movieCategoryRepository.count()` the count will use the h2 database with the two movie categories inserted through the `create-movie-category.sql`



**create-movie-category.sql**

```sql
DELETE FROM movie_category where id > 0;
INSERT INTO movie_category (id, name) VALUES (1, 'Horror');
INSERT INTO movie_category (id, name) VALUES (2, 'Comedy');
```





## Questions

- How does h2 relate to testing and mocking? 
- How do i mock some data in fx testing some repository function?
- Is there a smart way to run the tests?







