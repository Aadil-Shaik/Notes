## ES6

- let and const are ES6

- Async await both keywords are ES6 (also ES5 doesn't natively have Promises too)

## Arrow function

#### Basic fat arrow function

```js
var abcd = () => {
  //statement
};

abcd();
```

#### Fat arrow function with one paramenter

- you can remove the fat when giving one paramenter

```js
var abcd = (param) => {};
```

#### Fat arrow function with implicit return

```js
    var abcd = () => 7;
    console.log(abcd());     // prints 7
```

## Template Literals

- Easy way to write strings in js

- written between two back-ticks

- writing ${ } between the back-ticks prompts normal javascript

```js
var result = `Hey the final answer is ${num1 + num2}`;
```

### Default Parameters

- give default values when declaring

```js
abcd = (a, b, c) => {
  console.log(a, b, c);
};
abcd(1); // 1 undefined undefined
```

```js
abcd = (a = 0, b = 0, c = 0) => {
  console.log(a, b, c);
};
abcd(1); // 1 0 0
```

### Spread and Rest Operators

#### Spread

```js
var a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 0];

var b = [...a];
```

#### Rest

```js
function abcd(a, b, c, ...d) {
  console.log(a, b, c, d); // 1,2,3, [4,5,6,7,8,9,0]
}

abcd(1, 2, 3, 4, 5, 6, 7, 8, 9, 0);
```

## Destructuring

#### Destructuring an Array

- copy the values in array into variables

```js
var arr = [1, 2, 3];
var [a, b, c] = arr;
console.log(a, b, c); //prints elements of arr array

var [d, , e] = arr; // copies leaving the middle element
```

#### Destructuring an Object

```js
var obj = {
  name: "Aadil",
  age: 20,
  height: 180,
};
var { age, height } = obj;
```

## Classes

- to make objects from particular blueprint

## Try Catch

- Try catch is used to address the error and continue the flow of interpretation of the code

```js
console.log("Hey!");

try {
  console.log(hey);
} catch (err) {
  console.log(err);
}

console.log("Hey2!");
```
