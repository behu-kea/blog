# Java fundamental loop concepts

There are 4 fundamental Java concpets



## Encapsulation

Encapsulation also called data hiding is about hiding the fields of a class so another class cannot access the fields directly.

Here is an example of something that is **not** using encapsulation 

**Student.java**

```java
public class Student {
    public String name;
}
```



**Main.java**

```java
public class Main {
    public static void main(String[] args) {
 				Student student = new Student();
      	// Not using encapsulation!
      	student.name = "per";
    }
}
```





**Student.java**

```java
public class Student {
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

}
```



**Main.java**

```java
public class Main {
    public static void main(String[] args) {
 				Student student = new Student();
      	// Using encapsulation!
      	student.setName("per");
    }
}
```









## Inheritance



## Polymorphism



## Abstraction



