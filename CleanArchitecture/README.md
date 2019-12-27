* The goal of software architecture is to minimize human resources required to build and maintain the system throughout the lifetime.
* The only way to go fast, is to go well.
* Those things that are urgent are rarely of great importance, and those things that are important are seldom of great urgency.
* Business managers are not equipped to evaluate the importance of architecture. That’s what software engineers were hired to do. Therefore it is the responsibility of the software engineering team to assert the importance of architecture over the urgency of the features.

### Object Oriented Programming
* OO is the proper admixture of encapsulation, inheritance and polymorphism.
* Polymorphism allows architects to create plugin architectures.

### Desing Principles
* **Single Responsibility Principle** : A module should be responsible for one and only one actor.
* **The Open Closed Principle** : Allow behavior of the system to be changed by adding new code, rather than changing existing code.
* **The Liskov Susbstitution Principle** : It makes subtypes substitutable with an Interface.
* **The Interface Segregation Principle** : Avoid depending on things which are not going to be used.
* **The Dependency Inversion Principle** : Source code dependencies refer only to abstractions, not to concretions. The code that implements high level policy should not depend on low-level details.

* Good architects try to find ways to add functionality to implementations without making changes to interfaces.

### Component Cohesion
Which class belong in which components?
* **REP: The Reuse/Release Equivalence Principle** :
* **CCP: The Common Closure Principle** :
* **REP: The Common Reuse Principle** :

### Architecture
* Software architects may not write as much code as other programmers do, but they continue to engage in programming tasks.
* A good architecture will allow a system to be born as a monolith, deployed in a single file, but then to grow into a set of independently deployable units, and then all the way to independent services and/or micro-services. Later, as things change, it should allow for reversing that progression and sliding all the way back down into a monolith.
* When faced with a framework, try not to marry it right away. See if there aren’t ways to date it for a while before you take the plunge. Keep the framework behind an architectural boundary if at all possible, for as long as possible. 
* Marking all types as public means we are not taking advantage of the facilities that Java provides with regard to encapsulation.