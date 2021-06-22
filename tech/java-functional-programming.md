# Java functional programming

Java supports functional programming where we can work with fx lists in a new easier way. It's called the declarative where we with the code tell it what we want, not how do do it!



Let's look at some different functional techniques



## Function

A `Function` is a standalone method or you can just call it a function that takes one argument. 



Here is the same thing done as both a `Function` and a method

```java
public static void main(String[] args) {
  	Function<Integer, String> integerToStringFunction = integer -> {
    		return integer + "asd";
  	};
    String stringFromFunction = integerToStringFunction.apply(23);
    System.out.println(stringFromFunction); // "23asd"

    String stringFromMethod = integerToStringMethod(23);
    System.out.println(stringFromMethod); // "23asd"
}

static String integerToStringMethod(Integer number) {
    return number + "asd";
}
```

When you define the `Function` you need to tell it what should be the argument type and the return type`<ArgumentType, ReturnType>`. Then you write the argument name followed by `->` then you write the function body. When there only is one line, you can even omit the curly brackets:

```java
Function<Integer, String> integerToStringFunction = integer -> integer + "asd";
```



## BiFunction

Nearly the same as the function. But the BiFunction can takes two arguments! 

```java
BiFunction<Integer, Integer, Integer>sum = (number1, number2) -> number1 + number2;
System.out.println(sum.apply(2,8)); // 10
```



## Consumer

An operation that takes one argument but returns nothing.

```java
Consumer<String> emojifyString = stringToEmojify -> System.out.println(stringToEmojify + "🎉");
emojifyString.accept("asd"); // "asd🎉"
```



## BiConsumer

An operation that takes two arguments but returns nothing. More general with bi it means it takes two arguments

```java
BiConsumer<String, String> emojifyStringBi = (stringToLog, emoji) -> System.out.println(stringToLog + emoji);
emojifyStringBi.accept("test string", "☀️"); // "test string☀️"
```



## Predicate

A `Predicate` method is a statement about something that is either `true` or `false`. Here is an example:

```java
Predicate<Integer> isStudentOldPredicate = studentAge -> studentAge > 55;
System.out.println(isStudentOldPredicate.test(67)); // true
System.out.println(isStudentOldPredicate.test(23)); // false

System.out.println(isStudentOldMethod.test(67)); // true
System.out.println(isStudentOldMethod.test(23)); // false

// This is the same as the Predicate
// This does not run, you need to move the method outside of the main method!
public static boolean isStudentOldMethod(Integer studentAge) {
  return studentAge > 55;
}
```

The `Predicate` can take a lambda expression which is what we see with the `studentAge -> studentAge > 45`. The `Predicate` takes an integer and returns `true` or `false` if that `studentAge` is larger than 45. 

We run/test the predicate by calling `.test` on the predicate. Indicating that we test if something is `true` or `false`.

There are also `BiPredicate`!



## Supplier

A `supplier` represents a supplier of results. 

```java
Supplier<String> getDBConnectionSupplier = () -> "jdbc:mysql://localhost:8080/users";

System.out.println(getDBConnection());
System.out.println(getDBConnectionSupplier.get());

public static String getDBConnection() {
    return "jdbc:mysql://localhost:8080/users";
}
```



## Java streams

Now we take all the things that we have learned about functional programming and put it all together!

Java streams make it easier to work with lists. 

You take a `List` and call `.stream()` on the `List`. Now dependent on what you want to do you can either `filter`, `sort`, `map`, `foreach` and lots of other methods too.



### Implementing streams

```java
List<Student> students = new ArrayList();
students.add(new Student("benjamin", 23));
students.add(new Student("Maria", 78));
students.add(new Student("Katinka", 45));
students.add(new Student("gugugu", 1));
students.add(new Student("bugugu", 1));

List<Student> oldStudents = students
        .stream()
        .filter(student -> student.getAge() > 45)
        .collect(Collectors.toList());
oldStudents.forEach(System.out::println);

List<Student> test = students.stream()
        .filter(student -> student.getFirstName().charAt(0) == 'b')
        .collect(Collectors.toList());
test.forEach(System.out::println);

List<Student> sortedStudents = students.stream().sorted(Comparator.comparing(Student::getAge)).collect(Collectors.toList());
sortedStudents.forEach(System.out::println);
```



#### Filter

The filter will filter a list. Fx filtering the lost os only Student's that are older than 45 is in the list:

```java
List<Student> students = new ArrayList();
students.add(new Student("benjamin", 23));
students.add(new Student("Maria", 78));
students.add(new Student("Katinka", 45));
students.add(new Student("gugugu", 1));
students.add(new Student("bugugu", 1));

Predicate<Student> ageFilterPredicate = student -> student.getAge() > 45;
	List<Student> oldStudentsLong = students
		.stream()
    .filter(ageFilterPredicate)
    .collect(Collectors.toList());

// Can be shortened
List<Student> oldStudents = students
  .stream()
	.filter(ageFilterPredicate = student -> student.getAge() > 45)
  .collect(Collectors.toList());
```

- First we call `.stream()` on the `List`. This will return a `Stream` object. This object we can call a bunch of methods on. Fx `map`, `filter`, `sort`, etc.
- Now we call `.filter`. This method takes a `Predicate`. The `Predicate` takes a `Student` object and returns `true` or `false` if that `Student`object is larger that 45. The `filter` method takes the `ageFilterPredicate` and applies this for each element in the `student` `List`. The `Predicates` that return `true` are kept in the `List` the rest are discarded. 
  In human friendly words: We go through each `Student` in `students`. If they are older than 45 that are kept for the new `oldStudents` `List` otherwise they are discarded
- `.collect(Collectors.toList())` - here we collect the results and convert them from a stream back into a `List`.



#### Map

In mapping we are changing/transforming the individual elements in the array. Fx in this example we are changing the array from a list of students to a list of strings (that is the students first names). The `map` method takes a `Function` that we have been working with above.

```java
List<String> studentFirstnames = students
        .stream()
        .map(student -> student.getFirstName())
        .collect(Collectors.toList());
studentFirstnames.forEach(System.out::println);
```

- `.map(student -> student.getFirstName())` - This looks like a `Predicate` like we saw in `filter` but it is acutally a `Function` map. it does not return a `boolean` but can return anything. See it as a method that takes a parameter `Student` then return `student.getFirstName()` .



#### Sort

The principle for sorting is the same. But the `sorted` method takes another argument

```java
List<Student> sortedStudents = students
  	.stream()
  	.sorted(Comparator.comparing(Student::getAge))
  	.collect(Collectors.toList());
sortedStudents.forEach(System.out::println);
```



