# What is hoisting in JavaScript?

In JavaScript, a name enters a scope in one of four basic ways:

Language-defined: All scopes are, by default, given the names this and arguments.
Formal parameters: Functions can have named formal parameters, which are scoped to the body of that function.
Function declarations: These are of the form function foo() {}.
Variable declarations: These take the form of var foo;
Function declarations and variable declarations are always moved (“hoisted”) invisibly to the top of their containing scope by the JavaScript interpreter. Function parameters and language-defined names are, obviously, already there. This means that code like this:

```JavaScript
function foo() {
	bar();
	var x = 1;
}
is actually interpreted like this:

function foo() {
	var x;
	bar();
	x = 1;
}
```

It turns out that it doesn’t matter whether the line that contains the declaration would ever be executed. The following two functions are equivalent:

```JavaScript
function foo() {
	if (false) {
		var x = 1;
	}
	return;
	var y = 1;
}
function foo() {
	var x, y;
	if (false) {
		x = 1;
	}
	return;
	y = 1;
}
```


Notice that the assignment portion of the declarations were not hoisted. Only the name is hoisted. This is not the case with function declarations, where the entire function body will be hoisted as well. But remember that there are two normal ways to declare functions. Consider the following JavaScript:

```JavaScript
function test() {
	foo(); // TypeError "foo is not a function"
	bar(); // "this will run!"
	var foo = function () { // function expression assigned to local variable 'foo'
		alert("this won't run!");
	}
	function bar() { // function declaration, given the name 'bar'
		alert("this will run!");
	}
}


test();
```
In this case, only the function declaration has its body hoisted to the top. The name ‘foo’ is hoisted, but the body is left behind, to be assigned during execution.

That covers the basics of hoisting, which is not as complex or confusing as it seems. Of course, this being JavaScript, there is a little more complexity in certain special cases.

# Important Notes.
1. Function decleration is hoisted in js
2. Function expression is not hoisted in js

# What is Function Decleration in js?
foo()
function foo(){
    console.log(foo)
}

how js interpreter hoist this

```JavaScript
function foo(){
    console.log(foo)
}
foo()
```

# What is Function Expression in js?

``` JavaScript
user("Shakir","xyz@gmail.com")
let user = function(name, email){
    console.log(name, email)
}
```
how does the interpreter hoist this

```JavaScript
let user;
user("Shakir","xyz@gmail.com");
user = function(name, email){
    console.log(name, email)
} 

var a = 1;
function b() {  
    a = 10;  
    return;
    function a () {}
    
}
b();
console.log(a);

var a;
function b() {  
    a = 10;  
    return;
    function a () {}
    
}
a = 1;
b();

console.log(a)
```

> copy from article written by: Ben Cherry
