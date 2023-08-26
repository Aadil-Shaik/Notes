# JavaScript Notes

credit : Sheryians Coding School

#### Extra :

add defer to load js after html and css have loaded

```bash
	<script src="xyz" defer ></script>
```

## Variables and Constants

 | var       | let, const      | 
 | :-------- | :-------        | 
 |var is ES5 |let,const are ES6|
 |var is function scoped => can be used anywhere in parent function|let is braces scoped|
 |var adds itself to the window object and so it exposes the values | let does't add itself to the window object | 

- var is function scoped

```bash
  function abcd(){
    for(var i=0 ; i<11 ; i++ ){
        console.log(i) ;
    }
    console.log(i) ;
  }

  abcd() ;

  Output: 1 2 3 4 5 6 7 8 9 10 11
  ```

- let is braces scoped

```bash
  function abcd(){
    for(var i=0 ; i<11 ; i++ ){
        console.log(i) ;
    }
    console.log(i) ;
  }

  abcd() ;

  Output: 1 2 3 4 5 6 7 8 9 10 
          Error: i is not defined
  ```

### Window Object

- js uses window object ( browser ) to get the features that are not available in js language

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;example : alert, prompt, console, 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type **window** in console in browser to see all and here variables declared using **var** are added 

**Browser Context API** : It is the set of APIs that allow js to access and interact with the browser's context. The context is th collextion of objects and properties that provide information about the browser, the current page, and the user's environment. 
Window, Document, Location, Navigator (browser's user agent to identify browser, OS and device by the website), Screen

**Stack Memory and Heap Momory :**

Stack stores the order of calculations and heap stores the result from intermediate calculations

### Execution Context

Whenever a function is executed, an imaginary Execution Context is created whcih has 

&nbsp; 1. variables

&nbsp; 2. other funstions inside

&nbsp; 3. lexical environment

```bash
function abcd(){
    var a= 1 ;
    function xyz(){
        var x = 3 ;
    }
}
```

**EC of abcd( )** :

| a &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;xyz()&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;lexical environment|
|:------- | 

- Lexical environment defines the scope of function abcd() and scope chain ( it holds the access of its parents and parent's parents and such but it cannot access children ) in this case it cannot access **x**

- Execution context is a container where the function's code is executed and it is always created whenever a function is called.


### Hoisting

when variables and functions are hoisted, it means that their declarations are moved to the top of the code 

you can use variables regardless of where you declared them

- Only the definition is hoisted not the value inside it. And so, it will throw ' *undefined* '

## Types in js

**Primitive** : call by value

```bash
    var a = 5 ;
    var b = a ;  // changes to 'b' doesn't affect 'a'
```

**Reference** : call by reference => ( ) , [ ] , { } (anything with brackets)

```bash
    var a = [ 1, 2, 3, 4 ] ;
    var b = a ;  // changes to 'b' directly makes changes to 'a'
```
**copy reference values** :

```bash
    var a = [ 1, 2, 3, 4 ] ;
    var b = [...a] ;

    or 

    var a = { Name = "Aadil" };
    var b = {...a} ;
```

Spread operator :

```bash
   const odd = [1,3,5];
   const combined = [2,...odd, 4,6];
   console.log(combined);          // Output => [ 2, 1, 3, 5, 4, 6 ]
```
```bash
   function f(a, b, ...args) {
	  console.log(args);              // Output => [ 3, 4, 5 ]
   }
   f(1, 2, 3, 4, 5);
```

## Operations on Arrays

- Arrays in js are objects with index as keys

- This corresponds to even being able to use negative indexes to store values i.e => arr[-1] = 2 ;

- use Array.isArray( [ ] ) to check if something is array or object    

var arr = [1, 2, 3, 4, 5, 6];

arr.push(7) ; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  => [1, 2, 3, 4, 5, 6, 7]

arr.pop() ; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; => [1, 2, 3, 4, 5, 6]

arr.unshift(0) ; &nbsp; => [0, 1, 2, 3, 4, 5, 6]

arr.shift() ; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; => [1, 2, 3, 4, 5, 6]

arr.splice(include start index, no.of elements to remove)

arr.splice(1,3) ; &nbsp; => [1, 5, 6]

## Objects in js

Object in js is set of key value pairs

**Blank object** : 
```bash
  var a = { };
```

**Object in js** : 

```bash
  var a = 
  {
  name : "Aadil";
  age : 20;
  level : "Max";
  } ;
```
- All **Keys** which have a **Value** are called **Properties**
- When the **Key** has a **Function** for **Value** then that is called **Method**

```bash
  var a = 
  {
  name : "Aadil";
  age : 20;
  level : "Max";
  demo : playachievementsFunction(){};
  } ;
```
**Updating properties**
```bash
  var a = 
  {
  name : "Aadil";
  age : 20;
  level : "Max";
  demo : playachievementsFunction(){};
  } ;

  a.level = "Lowest" ;
```
**Deleting Object prop**

```bash
  var a = 
  {
  name : "Aadil";
  age : 20;
  level : "Max";
  demo : playachievementsFunction(){};
  } ;

  delete a.level ;
```

## Truthy and Falsy

**Falsy** value => 0, false, undefined, null, NaN (not a number), document.all

Everything else is **Truthy**

example: if(1), if(-1) both are **Truthy**

### Special Loops

**for each** :

- used only on arrays 

```bash
    var a = [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ] ;
    a.forEach(function( val ){
        console.log( val+10 ) ;
    })
```
- for each fetches the value not reference so no changes are made on original array

**for in** :

- used with objects

```bash
    var NPC = {
        name = " Vivek " ;
        age = 20 ;
        city = " Tanuku " ;
    }

    for( var key in NPC ){
        console.log( key ) ;
        console.log( NPC[ key ] ) ;
    }
```

## First class functions

- treat functions as values

```js
    function abcs(a){
        a() ;
    }

    abcd( function(){console.log("Hello World!");} )

    Output: Hello World!
```

When a function is treated as normal values or variables. You can save them or pass them as arguments to another function

## Higher Order functions

- A function which accepts another function as parameter or returns a function or both 

eg. forEach function always takes another function instide it so it is a higher order function

## Constructor function

- mold function which creates instances 
- normal function which uses this 
- to use instance, use new keyword

```js
function abcd(color){
    this.width = 100px;
    this.height = 100px;
    this.color = color;
}
```

A function which whenever invoked with "new" keyword, returns an object. If we use "this" keyword inside that function, it returns an object with all of the properties and methods mentioned inside that function which were mentioned inside that function with this keyword.

## iife - immediately invoked function expression

- making private variables
```bash
( function(){
    var a = 12;
} )()       output: console.log(a)  // var a not defined
```
look closesly at the nameless function which is created an executed immediately and it is destroyed. cannot access function as it is nameless.

- To access the private variable, return it's reference. Here we are returning an object

```js
var ans = ( function(){
    var a = 12;

    return{
        getter: function(){
            console.log(a);
        },
        setter: function(){
            a = val;
        }
    }

} )()

ans.getter();       // 12
ans.setter(24);     // 24
ans.getter();       // 12
```

## Prototype

- whenever you create an object, you get a prototype property by default
- it contains helper methods like .length(), .hasOwnProperty() etc

### Prototype Inheritance

```js
var human = {
    canFly: false;
    haveEmotions: true;
    canDie: true;
}
var ITStudent = {
    canWasteTime: true;
    canGoJobless: true;
}
ITStudent.__proto__ = human; 
```

## this call apply bind

#### this:

```js
console.log(this);  // in global scope gives window

function abcd(){
    console.log(this);  // in function scope gives window
}
abcd();

var obj = {
    name: function(){
        console.log(this);  // in method scope gives obj
    }
}
obj.name();
```

- in any method, this keyword refers to the parent object

```js
var button = document.querySelector("button");

button.addEventListener("click", function(){
    console.log(this);      // returns whole button tag as written in html
})

button.addEventListener("click", function(){
    this.style.color = "red";
})
```

#### call apply bind

- when you want to point a function by default to a object

#### call

```js
function abcd(){
    console.log(this);  // gives object instead of window
}

var obj = { age: 24 }

abcd.call(obj)
```
```js
function abcd( val1, val2, val3 ){
    console.log(this, val1);  // this is how you give values after object
}

var obj = { age: 24 }

abcd.call(obj, 1, 2, 3)
```

#### apply

- it's the form of call which limits you to use only 2 parameters as arguments
- you use an array to define all other arguments but array is not passed in the end result

```js
function abcd( val1, val2, val3 ){
    console.log(this, val1);  // only values are printed not array
}

var obj = { age: 24 }

abcd.apply(obj, [1, 2, 3])
```

#### bind

- mostly used in react

```js
function abcd(){
    console.log(this);  // gives no output but bindes abcd() to obj
}

var obj = { age: 24 }

abcd.call(obj);
```

```js
function abcd(){
    console.log(this); 
}

var obj = { age: 24 }

var bindedfunc = abcd.call(obj);
bindedfunc();   // returned obj
```

## Pure functions

&nbsp; 1. it should always return same ouotput for same input

&nbsp; 2. it will never change or update the value of a global variable

