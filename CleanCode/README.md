# Clean Code Notes
* The ratio of reading code to writing is well over 10:1

## Naming
* Class name should be a noun and method name should be a verb.
* A good name should provide following
    * Why it exists?
    * What it does?
    * How it is used?

    Bad name: int d; //elapsed time in days
    Good name: Ex: int elapsedTimeInDays

* Use intention revealing names
* Avoid disinformation Ex: accountList
* Make meaningful distinctions. Ex: a1, a2, etc is bad. Also, getActiveAccout, getActiveAccountInfo is bad as well.
* Renaming is really really easy with modern IDEs. Always change it, when you see the need.
* User pronounceable, searchable names.

## Functions - Verbs
* First rule of functions is that they should be small. 
* Second rule should be smaller than that.
* Functions should do one thing and they should do it well. They should do it only.

## Function Arguments
The ideal number of arguments for a function is zero, next comes one, followed closely by two. Three should be avoided where possible. More than 3 requires very special justification and shouldn’t be used.
* Arguments make it hard to comprehend the functionality.
* More arguments make testing very hard with various combinations.
* If a function is going to transform its input argument, the transformation should appear as the return value.
* In general output arguments should be avoided. If your function must change the state of something, have it change the state of its own object. Ex: this or report.appendFooter()
* Separate command from query. Functions either should do something or answer something.
* From a function, prefer throwing exceptions, instead of returning error codes. It makes calling code to handle the logic easily.
* Error handling is one thing. So, function that handles errors should do nothing else.
* DRY

## Comments
* Explain yourself in code, instead of comments
```
// Check to see if the employee is eligible for full benefits if ((employee.flags & HOURLY_FLAG) && 
(employee.age > 65)) 

To

if (employee.isEligibleForFullBenefits()) 
 ```
* A well-chosen name for a small function that does one thing is usually better than a comment header. 

# Formatting
* Most classes should be 200 lines or less.
* Each line 120 characters or less.
* Instance variables should be at the top.
* Vertical ordering for the methods.

# Objects and Data Structures
* Procedural code makes it hard to add new data structures because all the functions must change.  Ex: Adding a new shape. 
* OO code makes it hard to add new functions(classes) because all the classes must change. Ex: Adding a new method like calculate perimeter.
* Objects expose behavior and hide data.

# Error Handling
* Avoid checked exceptions. The cost outweighs the benefits and many languages doesn’t have them, such as C#, C++, Python, Ruby etc.
* Don’t return null. Instead always return empty collections and avoid null checks.
* Returning null from methods is bad. Passing null into methods is worse.
* Use assert for invalid null arguments.

# Boundaries
* Don’t pass Maps around your system. Try to keep it inside a class, or close family of classes where it is used. Avoid returning it, accepting it in public APIs.
```
Ex: public class Sensors {
private Map sensor = new Hashmap();
public Sensor getById(String id) {
return (Sensor) sensors.get(id);
}
}
```
* It is better to write learning tests for third party libraries
* Code at the boundaries need clear separation and tests that define expectation.

# Unit Tests
* Test code is as important as production code. It requires thought, design and care. 

# Classes
* Standard java convention for class organization is to have public static constants, followed by private static variables, followed by private instance variables, followed by public functions, then private utilities.
* First rule of classes is that they should be small. Second rule of classes is that they should be smaller than that.
* A class shouldn’t have too many responsibilities. SRP
* We want our systems to be composed of many small classes, not a few large ones.

# Systems

# Emergence
* Four rules for simple design: 
    * Runs all the tests
    * contains no duplication 
    * Expresses the intent of the programmer
    * Minimize the number of classes and methods.
* Eliminate even a small duplication.

# Concurrency
* Keep your concurrency related code separate from other code.
* Use copies of data to avoid interference.
* Make your threaded code pluggable, to make it easy to test.

# Successive Refinement
* Programmers who satisfy themselves with merely working code are behaving unprofessionally.

# Junit internals

# Quotes
* Boy Scout Rule. We’ve checked the code in a bit cleaner than when we checked it out. 






