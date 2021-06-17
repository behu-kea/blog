# Spring data JPA

JPA stands for Java persistence API

Hipernate is the most popular implementation of JPA. It takes a Java class that is mapped to our database using an ORM. 

Spring Data JPA is an abstraction on top of Hibernate and JPA which makes it easy to work with application that talks to the database. We can work with sql through just working with the objects. 

Basiscally Data JPA works by the developer working with Java objects, these objects are mapped to a database and therefore fx creating a new object will make an `INSERT INTO` sql query inserting that object. Now we can significantly reduce the number of sql queries we are writing



## Installing Data JPA

Add this to your maven file

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

 Your `application.properties` file should look like this. Adding the correct database url and username and password!

```java
spring.datasource.url=jdbc:mysql://localhost:3306/jpa-data
spring.datasource.username=
spring.datasource.password=
spring.jpa.hibernate.ddl-auto=create-drop
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
spring.jpa.properties.hibernate.format_sql=true
```

The other configurations are not relevant for now. 



## Mapping a `Class` to a `table`

Create a new class and then add an annotation called `@Entity(name = "TABLE_NAME")` (using the `javax.persistence.Entity`)

This will make the class into a table in your database. 

You have to remember to tell JPA which field is the primary key. We do this with the `@id` annotation 

````java
import javax.persistence.Entity;
import javax.persistence.Id;

@Entity(name = "Student")
public class Student {
    @Id
    private Long id;
    private String firstName;
    private String lastName;
    private String email;
  	....
````

When we run the query now, we can see the output from Hibernate:

```
Hibernate: 
    
    create table student (
       id int8 not null,
        age int4,
        email varchar(255),
        first_name varchar(255),
        last_name varchar(255),
        primary key (id)
    )
```

This is because we have this setting in the application.properties:

```
spring.jpa.show-sql=true
```



## Controlling column information

Sometime we want to add information to a column like the name of the column, the type, if it can be `NULL` etc. We do this with the `@Column` annotation



````java
@Entity(name = "Student")
public class Student {
    @Id
    private Long id;
  	@Column (
      	// the specific column name
        name="first_name",
      	// cannot be NULL
        nullable = false,
      	// the type
        columnDefinition = "TEXT"
    )
    private String firstName;
````

The `@Column` annotation takes some different arguments, like the name of the column, `nullable` etc



## Repositories

The repository is the layer that actually performs the sql queries to fx get a `Student` or delete a `Student`. 

It works by making a new `interface` that extends `JpaRepository` that has methods for getting, creating, deleting etc. 



To get the functionality provided in the CRUD create a new `interface` that extends `extends JpaRepository`. This extension need two types! Firstly the type of the class that will be interacted with, in this example `Student` the second argument is the type of the id!

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface StudentRepository extends JpaRepository<Student, Long> {

}
```



Now you can use the methods as follows:

```java
@Controller
public class StudentController {
    @Autowired
    StudentRepository studentRepository;

    @GetMapping("/")
    @ResponseBody
    public String getIndex() {
        Student benjamin = new Student(new Long(1), "asd", "asd", "asd", 2);
        studentRepository.save(benjamin);
        return "";
    }
}
```

