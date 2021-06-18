# Java streams

Java streams make it easier to work with lists. 

You take a `List` and call `.stream()` on the `List`. Now dependent on what you want to do you can either filter, sort, map, foreach and some other things too. 



## Implementing streams

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



### Filter

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
- Now we call `.filter`. This method takes a `Predicate`. A `Predicate` method is a statement about something that is either `true` or `false`. The `Predicate` can take a lambda expression which is what we see with the `student -> student.getAge() > 45`. This takes a `Student` object and returns `true` or `false` if that `Student`object is larger that 45. The `filter` method takes the `ageFilterPredicate` and applies this for each element in the `student` `List`. The `Predicates` that return `true` are kept in the `List` the rest are discarded. 
  In human friendly words: We go through each `Student` in `students`. If they are older than 45 that are kept for the new `oldStudents` `List` otherwise they are discarded
- `.collect(Collectors.toList())` - here we collect the results and convert them from a stream back into a `List`.



### Map

In mapping we are changing/transforming the individual elements in the array. Fx in this example we are changing the array from a list of students to a list of strings (that is the students first names)

```java
List<String> studentFirstnames = students
        .stream()
        .map(student -> student.getFirstName())
        .collect(Collectors.toList());
studentFirstnames.forEach(System.out::println);
```

- `.map(student -> student.getFirstName())` - This looks like a `Predicate` like we saw in `filter` but it is acutally a function map. it does not return a `boolean` but can return anything. See it as a method that takes a parameter `Student` then return `student.getFirstName()` .



### Sort

The principle for sorting is the same. But the `sorted` method takes another argument

```java
List<Student> sortedStudents = students
  	.stream()
  	.sorted(Comparator.comparing(Student::getAge))
  	.collect(Collectors.toList());
sortedStudents.forEach(System.out::println);
```



