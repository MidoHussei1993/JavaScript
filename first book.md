let age = prompt('How old are you?', 100); // the socend parameter to set defulet value
alert(`You are ${age} years old!`); // You are 100 years old!

let isBoss = confirm("Are you the boss?"); //return true or false
alert( isBoss ); // true if OK is pressed


let currentUser = null;
let defaultUser = "John";
let name = currentUser || defaultUser || "unnamed";
alert( name ); // selects "John" – the first truthy value
// null or undefined are false will take anther value
//عكس
// if the first operand is truthy,
// AND returns the second operand:
alert( 1 && 0 ); // 0
alert( 1 && 5 ); // 5
// if the first operand is falsy,
// AND returns it. The second operand is ignored
alert( null && 5 ); // null
alert( 0 && "no matter what" ); // 0
//this will take last value if it false
======================
# function
## Default values
function showMessage(from, text = "no text given") {
alert( from + ": " + text );
}
function showMessage(from, text = anotherFunction()) {
// anotherFunction() only executed if no text given
// its result becomes the value of text
}
function showMessage(from, text) {
// if text is falsy then text gets the "default" value
text = text || 'no text given';
...
}


 ##A function with an empty return or without it returns undefined
##If a function does not return a value, it is the same as if it returns undefined :
unction doNothing() { /* empty */ }
alert( doNothing() === undefined ); // true
function doNothing() {
return;
}
alert( doNothing() === undefined ); // true

# One function – one action
A function should do exactly what is suggested by its name, no more.

# Function Declaration
function sum(a, b) {
return a + b;
}
# Function Expression
let sum = function(a, b) {
return a + b;
};

## A Function Expression 
- is created when the execution reaches it and is usable only from
 - that moment.
- Once the execution flow passes to the right side of the assignment let sum = function…
- here we go, the function is created and can be used (assigned, called, etc. ) from now on.
- Function Declarations are different.
- A Function Declaration can be called earlier than it is defined.
- For example, a global Function Declaration is visible in the whole script, no matter where it is.

sayHi("John"); // Hello, John
function sayHi(name) {
alert( `Hello, ${name}` );
}



sayHi("John"); // error!
let sayHi = function(name) { // (*) no magic any more
alert( `Hello, ${name}` );
};
# Function Expressions are created when the execution reaches them. That would happen only in
the line (*) . Too late.


## arrow function
let sum = (a,b)=> a + b ;



let age = prompt("What is your age?", 18);
let welcome = (age < 18) ?
() => alert('Hello') :
() => alert("Greetings!");
welcome(); // ok now

* @param {number} x The number to raise.
* @param {number} n The power, must be a natural number.
* @return {number} x raised to the n-th power.
*/
function pow(x, n) {
...

=====================
# OBJECT:
- An empty object (“empty cabinet”) can be created using one of two syntaxes:
let user = new Object(); // "object constructor" syntax
let user = {}; // "object literal" syntax
 let fruit = prompt("Which fruit to buy?", "apple");
let bag = {
[fruit]: 5, // the name of the property is taken from the variable fruit
};
alert( bag.apple ); // 5 if fruit="apple"

let user = {};
alert( user.noSuchProperty === undefined ); // true means "no such property"

- There also exists a special operator "in" to check for the existence of a property.
The syntax is:
let user = { name: "John", age: 30 };
alert( "age" in user ); // true, user.age exists
alert( "blabla" in user ); // false, user.blabla doesn't exist

for (let key in user) {
// keys
alert( key ); // name, age, isAdmin
// values for the keys
alert( user[key] ); // John, 30, true
}

## A variable stores not the object itself, but its “address in memory”, in other words “a
## reference” to it.
let user = { name: "John" };
let admin = user; // copy the reference
- Now we have two variables, each one with the reference to the same object:

const user = {
name: "John"
};
user.age = 25; // (*)
alert(user.age); // 25

const user = {
name: "John"
};
// Error (can't reassign user)
user = {
name: "Pete"
};

let user = { name: "John" };
let permissions1 = { canView: true };
let permissions2 = { canEdit: true };
// copies all properties from permissions1 and permissions2 into user
Object.assign(user, permissions1, permissions2);
// now user = { name: "John", canView: true, canEdit: true }

=============================
# garbage collector
- There’s a base set of inherently reachable values, that cannot be deleted for obvious
- reasons.
- For instance:
## Local variables and parameters of the current function.
- Variables and parameters for other functions on the current chain of nested calls.
- Global variables.
(there are some other, internal ones as well)
============================================
# Symbols are guaranteed to be unique. Even if we create many symbols with the same
- description, they are different values. The description is just a label that doesn’t affect anything.
- For instance, here are two symbols with the same description – they are not equal:
let id1 = Symbol("id");
let id2 = Symbol("id");

id1 == id2 => false

let user = { name: "John" };
let id = Symbol("id");
user[id] = "ID Value";
alert( user[id] ); // we can access the data using the symbol as the key

golbal symbol
// read from the global registry
let id = Symbol.for("id"); // if the symbol did not exist, it is created
// read it again (maybe from another part of the code)
let idAgain = Symbol.for("id");
// the same symbol
alert( id === idAgain ); // true


Symbol.keyFor
For global symbols, not only Symbol.for(key) returns a symbol by name, but there’s a
reverse call: Symbol.keyFor(sym) , that does the reverse: returns a name by a global
symbol.
let sym = Symbol.for("name");
let sym2 = Symbol.for("id");
// get name from symbol
alert( Symbol.keyFor(sym) ); // name
alert( Symbol.keyFor(sym2) ); // id
====================
THIS in method: 
It’s common that an object method needs to access the information stored in the object to do its
job.
For instance, the code inside user.sayHi() may need the name of the user .
To access the object, a method can use the this keyword.
The value of this is the object “before dot”, the one used to call the method.
For instance:
let user = {
name: "John",
age: 30,
sayHi() {
alert(this.name);
}
};
user.sayHi();

let user = {
name: "John",
age: 30,
sayHi() {
alert( user.name ); // leads to an error
}
};
let admin = user;
user = null; // overwrite to make things obvious
admin.sayHi(); // Whoops! inside sayHi(), the old name is used! error!

======================
New keyword 
function User(name) { // this is method act like constructor
this.name = name;
this.isAdmin = false;
}
let user = new User("Jack");
alert(user.name); // Jack
alert(user.isAdmin); // false

is equale

function User(name) {
// this = {}; (implicitly)
// add properties to this
this.name = name;
this.isAdmin = false;
// return this; (implicitly)
}
=============================
let user = new function() {
this.name = "John";
this.isAdmin = false;
// ...other code for user creation
// maybe complex logic and statements
// local variables etc
};
The constructor can’t be called again, because it is not saved anywhere, just created and
called. So this trick aims to encapsulate the code that constructs the single object, without
future reuse.
// this is like static class

----
مهم جدااااااااااااااااااا
Advanced stuff
The syntax from this section is rarely used, skip it unless you want to know everything.
Inside a function, we can check whether it was called with new or without it, using a special
new.target property.
It is empty for regular calls and equals the function if called with new :
function User() {
alert(new.target);
}
// without "new":
User(); // undefined
// with "new":
new User(); // function User { ... }




function User(name) {
if (!new.target) { // if you run me without new
return new User(name); // ...I will add new for you
  }
this.name = name;
}
let john = User("John"); //
alert(john.name); // John

----------------------
function BigUser() {
this.name = "John";
return { name: "Godzilla" }; // <-- returns an object
}
alert( new BigUser().name ); // Godzilla, got that object ^^

And here’s an example with an empty return (or we could place a primitive after it, doesn’t
matter):
function SmallUser() {
this.name = "John";
return; // finishes the execution, returns this
// ...
}
alert( new SmallUser().name ); // John


===========
By the way, we can omit parentheses after new , if it has no arguments:
let user = new User; // <-- no parentheses
// same as
let user = new User();
============================
Methods in constructor
Using constructor functions to create objects gives a great deal of flexibility. The constructor
function may have parameters that define how to construct the object, and what to put in it.
Of course, we can add to this not only properties, but methods as well.
For instance, new User(name) below creates an object with the given name and the
method sayHi :
function User(name) {
this.name = name;
this.sayHi = function() {
alert( "My name is: " + this.name );
};
}
let john = new User("John");
john.sayHi(); // My name is: John
/*
john = {
name: "John",
sayHi: function() { ... }
}
*/

Two functions – one object
let obj = {};
function A() { return obj; }
function B() { return obj; }
alert( new A() == new B() ); // true


==============
let str = "Hello";
str.test = 5; // (*)
alert(str.test); undifined
















































 











