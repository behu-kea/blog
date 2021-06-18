# Spring Repository native Query

Sometimes we want to write native sql queries. With native we mean completely normal sql statements. We can do that in the Repository that has been extends `JpaRepository`



## Writing native queries

We can write native queries using the `@Query` annotation. Then we give a value which will be the native sql query itself. We add `nativeQuery = true` aswell

```java
@Query(value="select * from student", nativeQuery = true)
List<Student> getAllStudentsNow();
```

Now we need to specify the name and the return type of the method. 

We can then in another file fx here in `StudentController` do this

```java
List<Student> allStudents = studentRepository.getAllStudentsNow();
```



## Adding parameter to the method

We can even pass in a parameter to out method

```java
Query(value="select age from student where email= :email", nativeQuery = true)
List<Integer> getAgesForEmail(String email);
```

Here we are calling the method

```java
List<Integer> agesForEmail = studentRepository.getAgesForEmail("test");
```