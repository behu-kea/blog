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
	      String studentName = student.getName();
    }
}
```



## Inheritance

Inheritance let's programmers create new classes that share functionality with other classes. Now we as developers don't need to recode all the lines again. 

```java
class Mammal {

}
class Elephant extends Mammal {

}
```



## Polymorphism

An object might take on many forms. Polymorphism in OOP occurs when a super class references a sub class object.

If one task is performed in different ways, it is known as polymorphism. 

```java
class Person {
 void walk() {
  System.out.println(“Can Run….”);
 }
}
class Employee extends Person {
 void walk() {
  System.out.println(“Running Fast…”);
 }
  
 public static void main(String arg[]) {
  Person p = new Employee(); //upcasting
  p.walk();
 }
}
```



## Abstraction

In java and programming in general we want to work on a high level of abstraction. You can also say that we are hiding complexity with abstraction. We know how to turn on our television by pressing a button, but all the details of actually starting a television (electricity, wires, gates, processors) is hidden away.

Abstraction can in Java be achieved withan `abstract` class where only method names and return values are specified but not the body!

```java
abstract class Shape {
    public abstract void draw();
}
class Circle extends Shape{
    public void draw() {
        System.out.println("Circle!");
    }
}
public class Test {
    public static void main(String[] args) {
        Shape circle = new Circle();
        circle.draw();
    }
}
```

The same can be achieved with an `interface`. 



## Extra relevant words

### Coupling

If two classes are connected in some way



### Cohesion

Cohesion - How refers about how a class is designed. The more focused a class is, the cohesiveness of that class is more. 

High cohesion

```java
class Name {
  String name;
  public String getName(String name)
  {
    this.name = name;
    return name;
  }
} 
 
class Age {
  int age;
  public int getAge(int age)
  {
    this.age = age;
    return age;
  }
} 
 
class Number {
  int mobileno;
  public int getNumber(int mobileno)
  {
    this.mobileno = mobileno;
    return mobileno;
  }
} 
 
class Display {
  public static void main(String[] args)
  {
    Name n = new Name();
    System.out.println(n.getName("Geeksforgeeks"));
    Age a = new Age();
    System.out.println(a.getAge(10));
    Number no = new Number();
    System.out.println(no.getNumber(1234567891));
  }
}
```



### Association

The relationship between classes. Fx one to one, one to many, many to many etc. 
