Skip to content
Search or jump to…

Pull requests
Issues
Marketplace
Explore
 
@MidoHussei1993 
Learn Git and GitHub without any code!
Using the Hello World guide, you’ll start a branch, write comments, and open a pull request.


1
00MidoHussei1993/JavaScript
 Code Issues 0 Pull requests 0 Projects 0 Wiki Security Insights Settings
JavaScript
/
first book
 

1
let age = prompt('How old are you?', 100); // the socend parameter to set defulet value
2
alert(`You are ${age} years old!`); // You are 100 years old!
3
​
4
let isBoss = confirm("Are you the boss?"); //return true or false
5
alert( isBoss ); // true if OK is pressed
6
​
7
​
8
let currentUser = null;
9
let defaultUser = "John";
10
let name = currentUser || defaultUser || "unnamed";
11
alert( name ); // selects "John" – the first truthy value
12
// null or undefined are false will take anther value
13
//عكس
14
// if the first operand is truthy,
15
// AND returns the second operand:
16
alert( 1 && 0 ); // 0
17
alert( 1 && 5 ); // 5
18
// if the first operand is falsy,
19
// AND returns it. The second operand is ignored
20
alert( null && 5 ); // null
21
alert( 0 && "no matter what" ); // 0
22
//this will take last value if it false
23
======================
24
function
25
Default values
26
function showMessage(from, text = "no text given") {
27
alert( from + ": " + text );
28
}
29
function showMessage(from, text = anotherFunction()) {
30
// anotherFunction() only executed if no text given
31
// its result becomes the value of text
32
}
33
function showMessage(from, text) {
34
// if text is falsy then text gets the "default" value
35
text = text || 'no text given';
36
...
37
}
38
​
39
​
40
 A function with an empty return or without it returns undefined
41
If a function does not return a value, it is the same as if it returns undefined :
42
unction doNothing() { /* empty */ }
43
alert( doNothing() === undefined ); // true
44
function doNothing() {
45
return;
46
}
47
alert( doNothing() === undefined ); // true
48
​
49
 One function – one action
@MidoHussei1993
Commit changes
Commit summary
Update first book
Optional extended description
Add an optional extended description…
 Commit directly to the master branch.
 Create a new branch for this commit and start a pull request. Learn more about pull requests.
 
© 2019 GitHub, Inc.
Terms
Privacy
Security
Status
Help
Contact GitHub
Pricing
API
Training
Blog
About
