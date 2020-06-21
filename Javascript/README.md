* JavaScript has a single number type. Internally, it is represented as 64-bit floating point, the same as Java's double. 
* The || operator can be used to fill in default values:
```
var middle = stooge["middle-name"] || "(none)";
var status = flight.status || "unknown";
```
* Every object is linked to a prototype object from which it can inherit properties. All objects created from object literals are linked to Object.prototype, an object that comes standard with JavaScript.
* The prototype link is used only in retrieval. If we try to retrieve a property value from an object, and if the object lacks the property name, then JavaScript attempts to retrieve the property value from the prototype object. And if that object is lacking the property, then it goes to its prototype, and so on until the process finally bottoms out with Object.prototype. If the desired property exists nowhere in the prototype chain, then the result is the undefined value. This is called delegation.
* The typeof operator can be very helpful in determining the type of a property:
```
typeof flight.number      // 'number'
```
* The other approach is to use the hasOwnProperty method, which returns true if the object has a particular property. The hasOwnProperty method does not look at the prototype chain:
```
flight.hasOwnProperty('number')         // true
flight.hasOwnProperty('constructor')    // false
```
* Unfortunately, global variables weaken the resiliency of programs and should be avoided. One way to minimize the use of global variables is to create a single global variable for your application:
```
var MYAPP = {};
```
* Since functions are objects in javascript, they can be used like any other value. Functions can be stored in variables, objects, and arrays. Functions can be passed as arguments to functions, and functions can be returned from functions. Also, since functions are objects, functions can have methods.
```
Functions:

var add = function (a, b) {
	return a+b;
	};
```
It has 4 parts.
1. reserved word function. (function literal)
2. function name. This example is a ananymous function. since it doesnot have a name.
3. parameters.
4. body fo the function.
* An inner function also enjoys access to the parameters and variables of the functions it is nested within.
* The function object created by a function literal contains a link to that outer context. This called closure. This is the source of enormous expressive power.
* Invoking a function suspends the execution of the current function, passing control and parameters to the new function. In addition to the declared parameters, every function receives two additional parameters: this and arguments. The this parameter is very important in object oriented programming, and its value is determined by the invocation pattern. There are four patterns of invocation in JavaScript: the method invocation pattern, the function invocation pattern, the constructor invocation pattern, and the apply invocation pattern. The patterns differ in how the bonus parameter this is initialized.
### Method Invocation Pattern:
When a function is stored as a a property of an object, we call it a method. when a method is invoked, this is bound to that object.
```
var myObject = {
	value:0,
	increment: function (inc) {
		this.value += typeof inc === 'number' ? inc : 1; //this is properly set here.
	}
};

myObject.increment();
document.writeln(myObject.value); //1

myObject.increment(2);
document.writeln(myObject.value); //3
```

### The Function Invocation Pattern:
when a function is not the property of an aobject, then it is invoked as a function. In this pattern, this is bound to the global object. Here inner function does not share the method's access to the object as its "this" is bound to the wrong value. look at the example for workaround(that).
```
myObject.double = function() {
	var that = this; // workaround
	
	var helper = function() {
		that.value = add(that.value, that.value);
		};
	helper();
}

myObject.double();
document.writeln(myObject.value); //6
```
### The constructor invocation pattern:
JavaScript is a prototypal inheritance language. That means that objects can inherit properties directly from other objects.
If a function is invoked with the "new" prefix, then a new object will be created with a hidden link to the value of the function's "prototype" member, and this will be bound to that new object.
```
// Create a constructor function called Quo.
// It makes an object with a status property.

var Quo = function (string) {
    this.status = string;
};

// Give all instances of Quo a public method
// called get_status.

Quo.prototype.get_status = function (  ) {
    return this.status;
};

// Make an instance of Quo.

var myQuo = new Quo("confused");

document.writeln(myQuo.get_status(  ));  // confused
```
Functions that are intended to be used with the new prefix are called constructors. By convention, they are kept in variables with a capitalized name.

### The Apply Invocation Pattern: 
Because JavaScript is a functional object-oriented language, functions can have methods.
The "apply" method lets us construct an array of arguments to use to invoke a function. It also lets us choose the value of "this". The apply method takes two parameters. The first is the value that should be bound to "this". The second is an array of parameters.
```
// Make an array of 2 numbers and add them.

var array = [3, 4];
var sum = add.apply(null, array);    // sum is 7

// Make an object with a status member.

var statusObject = {
    status: 'A-OK'
};

// statusObject does not inherit from Quo.prototype,
// but we can invoke the get_status method on
// statusObject even though statusObject does not have
// a get_status method.

var status = Quo.prototype.get_status.apply(statusObject);
    // status is 'A-OK'
```
A bonus parameter that is available to functions when they are invoked is the arguments array. It gives the function access to all of the arguments that were supplied with the invocation, including excess arguments that were not assigned to parameters. 
* A function always returs a value. If the return value is not specified, then "undefined" is returned.
* If the function was invoked with the "new" prefix and the return value is not a object, then "this"(the new object) is returned instead.
* The throw statement interrupts execution of the function. It should be given an exception object containing a name property that identifies the type of the exception, and a descriptive message property. You can also add other properties.
```
var add = function (a, b) {
    if (typeof a !== 'number' || typeof b !== 'number') {
        throw {
            name: 'TypeError',
            message: 'add needs numbers'
        };
    }
    return a + b;
}
```
* JavaScript does not have block scope even though its block syntax suggests that it does.
* In JavaScript it is best to declare all of the variables used in a function at the top of the function body.
* In JavaScript, inner functions get access to the parameters and variables of the functions they are defined within (with the exception of "this" and "arguments"). 
* In classical languages, objects are instances of classes, and a class can inherit from another class. JavaScript is a prototypal language, which means that objects inherit directly from other objects.
* JavaScript allows an array to contain any mixture of values:
```
var misc = [
    'string', 98.6, true, false, null, undefined,
    ['nested', 'array'], {object: true}, NaN,
    Infinity
];
```
* JavaScript Arrays inherit from Array.prototype
* Unlike other languages, Javascript array length is not an upper bound.
```
var myArray = [];
myArray.length             // 0

myArray[1000000] = true;
myArray.length             // 1000001
```
* Since javascript's arrays are really objects, if we delete an element, it lieaves a hole in the array.
```delete numbers[2];
// numbers is ['zero', 'one', undefined, 'shi', 'go']
```
where as splice method can delete a element, and rearrage other elements(by deleting and reinseting them).
* It is better to declare all variables at the top of each function.
* A better test for null is simply: my_value === null
* parseInt is a function that converts a string into an integer. It stops when it sees a nondigit, so parseInt("16") and parseInt("16 tons") produce the same result.
* In Javascript, 0.1 + 0.2 is not equal to 0.3.

### Events:
* The event target is the object on which the event occurred or with which the event is associated.
* The focus and blur events do not bubble, but all the other form events do. IE defines focusin and focusout events that do bubble as a useful alternative to focus and blur.







