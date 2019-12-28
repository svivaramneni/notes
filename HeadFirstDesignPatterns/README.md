### Strategy Pattern
* It defines family of algorithms, encapsulates each one, and makes them interchangeable.
* Identify the aspects of your application that vary and separate them from what stays the same
* Program to Interfaces
* Favor composition over inheritance

### Observer Pattern
* Observer defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

* Strive for loosely coupled designs between objects that interact.

### Decorator Pattern
* Classes should be open for extension, but closed for modification.
* Decorator attaches additional responsibilities to an object dynamically. 
* Decorators provide a flexible alternative to subclassing for extending functionality.

### Factory Pattern
* The factory method pattern defines an interface for creating an object, but lets sub classes decide which class to instantiate. 
* Factory method lets a class defer instantiation to subclasses.
* Depend on abstractions. Do not depend on concrete classes.
* Guidelines
    * No variable should hold a reference to a concrete class. If we use "new" its a violation. Use a factory for creating instances.
    * No class should derive from a concrete class. Derive from an abstraction, like an interface or abstract class.
    * No method should override an implemented method of any of its base classes.

    ### Singleton Pattern
    * It ensures a class has only one instance, and provides a global point of access to it.
    * private constructor, static getter and initalize object during class loading through static instance field.






