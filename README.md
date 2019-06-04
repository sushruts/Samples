# Calculate the Max/Min value from an array
```javascript
  Math.max(1, 2, 3, 4); // 4
  Math.min(1, 2, 3, 4); // 1
  
  var numbers = [1, 2, 3, 4];
  Math.max.apply(null, numbers) // 4
  Math.min.apply(null, numbers) // 1
  
  var numbers = [1, 2, 3, 4];
  Math.max(...numbers) // 4
  Math.min(...numbers) // 1
```

# Reduce in arrays
reduce() function accepts 2 parameters (M: mandatory, O: optional):
(M) a callback reducer function to be applied that deals with a pair of previous (result of previous computation) and next element until end of the list.
(O) an initial value to be used as the first argument to the first call of the callback.
So let’s see a common usage and later a more sophisticated one.

Common usage (accumulation, concatenation)
// my current amazon caddy purchases
```javascript
var items = [{price: 10}, {price: 120}, {price: 1000}];
// our reducer function
var reducer = function add(sumSoFar, item) { return sumSoFar + item.price; };
// do the job
var total = items.reduce(reducer, 0);
console.log(total); // 1130
// Now, cool I received a discount coupon of 20.
var total = items.reduce(reducer,-20);
console.log(total); // 1110
```

# Unique array values
```javascript
const arr = [...new Set([1, 2, 3, 3])];
[1, 2, 3]
```
# Getting a substring
There are 3 methods in JavaScript to get a substring: substring, substr and slice.

slice : returns the part of the string from start to (but not including) end. str.slice(start [, end])
```javascript
let str = "stringify";
alert( str.slice(0, 5) ); // 'strin', the substring from 0 to 5 (not including 5)
alert( str.slice(0, 1) ); // 's', from 0 to 1, but not including 1, so only character at 0

// If there is no second argument, then slice goes till the end of the string:
let str = "stringify";
alert( str.slice(2) ); // ringify, from the 2nd position till the end

//Negative values for start/end are also possible. They mean the position is counted from the string end:
let str = "stringify";
// start at the 4th position from the right, end at the 1st from the right
alert( str.slice(-4, -1) ); // gif
```
substring : returns the part of the string between start and end, this is almost the same as slice, but it allows start to be greater than end. str.substring(start [, end])
```javascript
let str = "stringify";

// these are same for substring
alert( str.substring(2, 6) ); // "ring"
alert( str.substring(6, 2) ); // "ring"

// ...but not for slice:
alert( str.slice(2, 6) ); // "ring" (the same)
alert( str.slice(6, 2) ); // "" (an empty string)

//Negative arguments are (unlike slice) not supported, they are treated as 0.
let str = "stringify";
alert( str.substr(2, 4) ); // ring, from the 2nd position get 4 characters

//The first argument may be negative, to count from the end:
let str = "stringify";
alert( str.substr(-4, 2) ); // gi, from the 4th position get 2 characters
```

|method|selects...|negatives|
|----------------|-------------------------------|-----------------------------|
slice(start, end)|from `start` to `end` (not including `end`)| allows negatives
`substring(start, end)`|between  `start`  and  `end`|negative values mean  `0`
`substr(start, length)`|from  `start`  get  `length`  characters|allows negative  `start`


# ES6, var vs let
The scope of a variable defined with var is function scope or declared outside any function, global.
The scope of a variable defined with let is block scope.
```javascript
function varvslet() {
  console.log(i); // i is undefined due to hoisting
  // console.log(j); // ReferenceError: j is not defined
  for( var i = 0; i < 3; i++ ) {
    console.log(i); // 0, 1, 2
  };
  console.log(i); // 3
  // console.log(j); // ReferenceError: j is not defined
  for( let j = 0; j < 3; j++ ) {
    console.log(j);
  };
  console.log(i); // 3
  // console.log(j); // ReferenceError: j is not defined
}
```
Variable Hoisting
let will not hoist to the entire scope of the block they appear in. By contrast, var could hoist as below.
```javascript
{
  console.log(c); // undefined. Due to hoisting
  var c = 2;
}

{
  console.log(b); // ReferenceError: b is not defined
  let b = 3;
}
```

Closure in Loop
let in the loop can re-binds it to each iteration of the loop, making sure to re-assign it the value from the end of the previous loop iteration, so it can be used to avoid issue with closures.
```javascript
for (var i = 0; i < 5; ++i) {
  setTimeout(function () {
    console.log(i); // output '5' 5 times
  }, 100);  
}

// print 1, 2, 3, 4, 5
for (let i = 0; i < 5; ++i) {
  setTimeout(function () {
    console.log(i); // output 0, 1, 2, 3, 4 
  }, 100);  
}
```

# Getting array items from behind to front
```javascript
var newArray = [1, 2, 3, 4];
console.log(newArray.slice(-1)); // [4]
console.log(newArray.slice(-2)); // [3, 4]
console.log(newArray.slice(-3)); // [2, 3, 4]
console.log(newArray.slice(-4)); // [1, 2, 3, 4] //reverse it using length of array
```

# Bind method in action
```javascript
// Syntax :  fun.bind(thisArg[, arg1[, arg2[, ...]]])
// thisArg: this parameter value to be passed to target function while calling the bound function.
// arg1, arg2, … : Prepended arguments to be passed to the bound function while invoking the target function.
// Return value : A copy of the given function along with the specified this value and initial arguments.

const myCar = {
 brand: 'Ford',
 type: 'Sedan',
 color: 'Red'
};

const getBrand = function () {
 console.log(this.brand);
};

const getType = function () {
 console.log(this.type);
};

const getColor = function () {
 console.log(this.color);
};

getBrand(); // object not bind,undefined

getBrand(myCar); // object not bind,undefined

getType.bind(myCar)(); // Sedan

let boundGetColor = getColor.bind(myCar);
boundGetColor(); // Red
```
