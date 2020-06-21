### Why Lambdas ?
* Enables functional programming in Java
* Makes code concise and readable
* Easier-to-use APIs and libraries
* Enables support for parallel processing

### Limitations with OOP
* Everything is an object
* All code blocks are associated with classes and objects

Lamdas are functions, which exist in isolation, they do not belong to a class. Those can be considered as values and passed around.
```
String name = "foo";
double pi = 3.14;
aBlockOfCode = {
}

Ex:
aBlockOfCode = public void perform() {
  System.out.println("Perform Behavior");
}
```
In the above example, we have some extra code, which is not really needed in the context of isolated functions(lambdas). That information could be either inferred or redundant.
* The <code> public </code> access specifier makes sense in the context of a class. But not in lamdas as whoever has access to that variable could invoke it.
* Similarly Return type could be inferred.
* Method name is redundant as we could invoke the behavior with variable name.
* If the method implementation is one line, then we don't need curly braces. So after removing all those it becomes
```
aBlockOfCode = () -> System.out.println("Perform Behavior");
```
Some additional lambda Examples
```
greetingFuntion = () -> System.out.println("Greeting");

doubleNumberFunction = (int a) -> a*2;

addFunction = (int a, int b) -> a + b;

safeDivideFunction = (int a, int b) -> {
  if(b==0)
    retun 0;
  return a / b;
}

stringLengthFunction = (String s) -> s.length();
stringLengthFunction = s -> s.length(); //Shortest lambda. Here type of s is inferred from the method type.


```
#### Lambda as Interface Type
* Lamdas leverage Interfaces for type. Type interface should have only one abstract method and its signature should be same as lambda, so that it could be used for compile time checking.
* Lambdas are not exactly annonymous inner classes, but similar.
* This provides backward compatibility so that we could reuse all existing libraries and anonymous inner classes.

### Functional Interface
* Interface which has only one abstract method.
* We could optionally add <code>@FunctionalInterface</code> annotation to functional interfaces, so that we don't accidentally add additional methods and break existing lambdas.
* <code>java.util.function</code> package contains set of common functional interfaces to cater most needs.

### Closures in Lambda Expressions
* Variables declared outside lambda could be accessed inside lambda. But they are considered final. If we try to override the value, compiler will give an error.
* Unlike anonymous inner classes, lambdas doesn't have <code>this</code> reference. In case of lambdas <code>this</code> points to the class who is holding the lambda.


### Method References
* Alternative syntax to lambda, if there are no arguments or equal number of arguments as passthrough.
```
printPeople(people, p -> true, System.out::println);
```

### forEach iteration
* Java8 introduced a new internal iteration method. Example with lamdba/method reference.
```
people.foreach(System.out::println);
```### Lambda Expressions
Lambda's make writing and reading anonymous classes easier. They are very popular in Scala.
```java
private static final FileFilter FOLDER_FILTER = new FileFilter() {
    @Override
    public boolean accept(final File pathname) {
        return pathname.isDirectory();
    }
};

private static final FileFilter filterLamda = (File pathname) -> pathname.isDirectory();
```
Ex: Comparator, Runnable

#### FAQ's

* What is the type of the lambda expression? A functional interface(only one abstract method).
* Can a lambda be put in a variable? Yes. Can be taken as method param. Can be returned by a method.
* Is a lambda expression an object? JVM doesn't create a new regular object, so the over head is low. 

#### Method References
:: Syntax
```java
 Ex: boolean isLegalName = list.stream().anyMatch(user::isLegalName); 
 ```
Unlike anonymous inner classes, there is no object creation overhead on the JVM (Ex: new)

### Functional Interface
Functional interfaces are also called Single Abstract Method Interfaces (SAM Interfaces). They permit exactly one abstract method.
```java
@FunctionalInterface
public interface MyFirstFunctionalInterface
{
    public void firstWork();
}
```
### Stream API
Stream API in Java8 is a new concept and major change. It provides a mechanism for processing data such as filtering, transforming, etc. Stream is a typed interface. It is not a collection.
```java
public interface Stream<T> extends BaseStream<T, Stream<T>> {
}
```
* It can process large amounts of data efficiently. i.e. parallel, pipelined.
* Stream is an object which can define operations.
* An object that does not hold any data unlike collections.
* An object that should not change the data it processes. Not enforced.
* An object optimized from the algorithm point of view.
* Stream does not hold any data. The call to the filter method is lazy. All the methods of stream that return another stream are lazy.
```java
Ex: public Employee getUserById(Integer uid) {
    return (Employee) new ArrayList<Employee>().stream()
        .filter(user -> user.getId().equals(uid)).findFirst().get();
}
```

#### Mapping Operation



### Date & Time API 
java.time package

* Date class is mutable. So it is obsolete now.
* Instant class object is immutable. Ex: Instant.now() // Precision in nano seconds
* LocalDate is used when the precision level is at date level.
* For using date functionality with zone information, there are 3 new classes. "OffsetDate, OffsetTime, OffsetDateTime".
```java
Ex: ZonedDateTime zonedDateTime = ZonedDateTime.now(ZoneId.of("Europe/Paris"));
```
### Default Methods 
Java8 supports having static and default method implementations in the interface.
```java
public interface Iterable<E> {
   default void forEach(Consumer<E> consumer) {
       for (E e : this) {
          consumer.accept(e);
       }
    }
}
```
### Avoid evil NPEs with "Optional"
```java
public class Address {
    private final String addressLine;  // never null
    private final String city;         // never null
    private final String postcode;     // optional, thus may be null
    // constructor ensures non-null fields really are non-null
    // optional field can just be stored directly, as null means optional
    public Address(String addressLine, String city, String postcode) {
      this.addressLine = Preconditions.chckNotNull(addressLine);
      this.city = Preconditions.chckNotNull(city);
      this.postcode = postcode;
    }
    // normal getters
    public String getAddressLine() { return addressLine; }
    public String getCity() { return city; }
    // special getter for optional field
    public Optional<String> getPostcode() {
      return Optional.ofNullable(postcode);
    }
    // return optional instead of null for business logic methods that may not find a result
    public static Optional<Address> findAddress(String userInput) {
      return ... // find the address, returning Optional.empty() if not found
    }
  }
```

### Perm Gen Space : 
### Concurrent Accumulators :
```java
List<String> memNamesInUppercase = memberNames.stream().sorted()
                            .map(String::toUpperCase)
                            .collect(Collectors.toList()); 
```

### Nashorn Javascript Engine : 
```java
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;
public class NashornJs {
	public static void main(String[] args) throws Exception {
		ScriptEngineManager scriptEngineManager = new ScriptEngineManager();
		ScriptEngine scriptEngine = scriptEngineManager
				.getEngineByName("nashorn");
		try {
			scriptEngine.eval("print('Nashorn Hello World!');");
		} catch (final ScriptException se) {
			se.printStackTrace();
		}
	}
}
```

