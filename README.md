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
# Arrays :
https://javascript.info/array-method

# Map, Set, WeakMap and WeakSet :
https://javascript.info/map-set-weakmap-weakset

# Array destructuring (Destructuring assignment)
https://javascript.info/destructuring-assignment#array-destructuring

It’s called “destructuring assignment,” because it “destructurizes” by copying items into variables. But the array itself is not modified.

```javascript
// we have an array with the name and surname
let arr = ["A", "B"]
// destructuring assignment
let [firstName, surname] = arr;
alert(firstName); // A
alert(surname);  // B

let [firstName, surname] = "Ilya Kantor".split(' ');


// second element is not needed
let [firstName, , title] = ["This", "is", "good", "example"];
alert( title ); // good
//Properties options.title, options.width and options.height are assigned to the corresponding variables. The order does not matter. This works too:
// changed the order of properties in let {...}
let {height, width, title} = { title: "Menu", height: 200, width: 100 }

```
# Object destructuring
https://javascript.info/destructuring-assignment#object-destructuring
```javascript
let options = {
  title: "Menu",
  width: 100,
  height: 200
};

let {title, width, height} = options;

alert(title);  // Menu
alert(width);  // 100
alert(height); // 200
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

# Array - splice
The arr.splice(str) method is a swiss army knife for arrays. It can do everything: insert, remove and replace elements.
Syntax : arr.splice(index[, deleteCount, elem1, ..., elemN])
It starts from the position index: removes deleteCount elements and then inserts elem1, ..., elemN at their place. Returns the array of removed elements.
```javascript
let arr = ["I", "study", "JavaScript"];
arr.splice(1, 1); // from index 1 remove 1 element
alert( arr ); // ["I", "JavaScript"]

// We remove 3 elements and replace them with the other two:
let arr = ["I", "study", "JavaScript", "right", "now"];
// remove 3 first elements and replace them with another
arr.splice(0, 3, "Let's", "dance");
alert( arr ) // now ["Let's", "dance", "right", "now"]

//splice returns the array of removed elements
let arr = ["I", "study", "JavaScript", "right", "now"];
// remove 2 first elements
let removed = arr.splice(0, 2);
alert( removed ); // "I", "study" <-- array of removed elements

//The splice method is also able to insert the elements without any removals. For that we need to set deleteCount to 0:
let arr = ["I", "study", "JavaScript"];
// from index 2
// delete 0
// then insert "complex" and "language"
arr.splice(2, 0, "complex", "language");
alert( arr ); // "I", "study", "complex", "language", "JavaScript"


//Negative Index are allowed
let arr = [1, 2, 5];
// from index -1 (one step from the end)
// delete 0 elements,
// then insert 3 and 4
arr.splice(-1, 0, 3, 4);
alert( arr ); // 1,2,3,4,5
```

# Custom function to splice string - (array's splice function does not work on strings)

```javascript
function spliceSlice(str, index, count, add) {
  // We cannot pass negative indexes directly to the 2nd slicing operation.
  if (index < 0) {
    index = str.length + index;
    if (index < 0) {
      index = 0;
    }
  }

  return str.slice(0, index) + (add || "") + str.slice(index + count);
}
```
# Getting array items from behind to front
```javascript
var newArray = [1, 2, 3, 4];
console.log(newArray.slice(-1)); // [4]
console.log(newArray.slice(-2)); // [3, 4]
console.log(newArray.slice(-3)); // [2, 3, 4]
console.log(newArray.slice(-4)); // [1, 2, 3, 4] //reverse it using length of array

//Reverse
let arr = [1, 2, 3, 4, 5];
arr.reverse();
alert( arr ); // 5,4,3,2,1
```

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

# closures
https://javascript.info/closure
There is a general programming term “closure”, that developers generally should know.
A closure is a function that remembers its outer variables and can access them. In some languages, that’s not possible, or a function should be written in a special way to make it happen. But as explained above, in JavaScript, all functions are naturally closures (there is only one exclusion, to be covered in The "new Function" syntax).

That is: they automatically remember where they were created using a hidden [[Environment]] property, and all of them can access outer variables.

A closure is a function that returns another function and wraps data. The above string generator qualifies for a closure. The index value is preserved between multiple function calls. The internal function defined can access the variables defined in the parent function. This is a different scope. If you defined one more function in the second level function, that can access all parent’s variables.

Example 1 
```javascript
function makeCounter() {
  let count = 0;
  return function() {
    return count++;
  };
}

let counter1 = makeCounter();
let counter2 = makeCounter();

alert( counter1() ); // 0
alert( counter1() ); // 1

alert( counter2() ); // 0 (independent)
```

Example 2
```javascript
function generator(input) {
  var index = 0;
  return {
     next: function() {
       if (index < input.length) {
            index += 1;
            return input[index - 1];
       }
       return "";
     } 
  }
}
var mygenerator = generator("boomerang");
mygenerator.next(); // returns "b"
mygenerator.next() // returns "o"

mygenerator = generator("toon");
mygenerator.next(); // returns "t"
```

Example 3
```javascript
function Counter() {
  let count = 0;

  this.up = function() {
    return ++count;
  };

  this.down = function() {
    return --count;
  };
}

let counter = new Counter();

alert( counter.up() ); // 1
alert( counter.up() ); // 2
alert( counter.down() ); // 1
```
# Property flags and descriptors
https://javascript.info/property-descriptors

# var, let, const
> **Var:**
>  `var` is function scoped.
>  `var` variables are either function-wide or global, they are visible through blocks.
>  `var` declarations are processed when the function starts (or script starts for globals).
>  `undefined` when accessing a variable before it's declared.

> **let:**
>  `let` is block scoped.
>   ReferenceError when accessing a variable before it's declared.
>  `let` and `const` behave exactly the same way in terms of Lexical Environments.
>   use `let` when one need to reassign a variable. The use case for `let` tends to be for loops.
>  `let`, is a signal that the variable may be reassigned, It also signals that the variable will be used only in the block it’s defined >   in, which is not always the entire containing function.

> **const:**
>  `const` is block scoped.
>  `let` and `const` behave exactly the same way in terms of Lexical Environments.
>  `const` means that the identifier can’t be reassigned.
>  ReferenceError when accessing a variable before it's declared.
>  Can't be reassigned.
