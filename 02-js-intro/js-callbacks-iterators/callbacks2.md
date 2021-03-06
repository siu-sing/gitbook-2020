# Callbacks and Iterators

Programming with functions! Weren't we already doing that? Well yes, but we can use functions more heavily, especially in place of loops.

## Objectives

* Understand how functions can be passed in and out of other functions
* Run syntax to replace loops with the four main JavaScript iterators: forEach, map, reduce, filter
* Learn to sort arrays with `sort`

## Iterators

Iterators are examples of _functional programming_ replacements for `for` loops. We can use these functions to perform common Array operations for us.

What might we want to with an array?

* run some piece of logic on each item
* create a new array with each item being slightly transformed
* filter the array to contain only a subset of items
* combine all the items in some fashion
* sort

We could accomplish all of this using `for` loops, but writing `for` loops is error prone and tiring. JavaScript provides iterator functions for all of these common operations. They are called \(respectively\):

* [forEach](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
* [map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
* [filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
* [reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)
* [sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
* Declare an array
* Call an iterator on the array
* Pass a function to the iterator
* Get results

### forEach

`forEach` is the _functional programming_ replacement for your standard `for` loop. You can take the body from your `for` loop, wrap it in a function, and pass that argument to `forEach`. Let's look at an example:

```javascript
var friends = ["Markus", "Tim", "Ilias", "Elie"];

// old way, with a for loop
for (var i = 0; i < friends.length; i++) {
  console.log("Hello, " + friends[i] + "!");
}

// cool new way, with the .forEach iterator
friends.forEach( buddy =>{
  console.log("Hello, " + buddy + "!");
});

// both output the same thing
// > Hello, Markus!
// > Hello, Tim!
// > Hello, Ilias!
// > Hello, Elie!
```

**Try it**

Use the `.forEach` iterator to loop over the following array of foods and say you like them.

```javascript
var foods = ["pizza", "tacos", "ice cream"];

// your code here

// The output should be
// > "I like pizza"
// > "I like tacos"
// > "I like ice cream"
```

**Try it again**

Use the `.forEach` iterator to loop over the following array of objects and say how delicious each one is.

```javascript
var foods = [
  {name: "Pizza", level: "very"},
  {name: "Tacos", level: "mostly"},
  {name: "Cottage Cheese", level: "not very"}
];

// your code here

// The output should be
// > Pizza is very delicious
// > Tacos is mostly delicious
// > Cottage Cheese is not very delicious
```

### map

Sometimes we want to loop over an array and build a new array in the process. This is what `map` helps us solve. It is like `forEach`, but it returns the new array that is created.

```javascript
var names = ["tim", "ilias", "elie", "markus"];

// old way with for loop
var cased = [];
for (var i = 0; i < names.length; i++) {
  cased.push(names[i].toUpperCase());
}
console.log(cased);

// new way with `map`
var cased = names.map( person => {
  return person.toUpperCase();
});
console.log(cased);

// Should output
// > ["TIM", "ILIAS", "ELIE", "MARKUS"]
// > ["TIM", "ILIAS", "ELIE", "MARKUS"]
```

### filter

Filter is an iterator that loops through your array and filters it down to a subset of the original array. A callback is called on each element of the original array: if it returns true, then the element is included in the new array, otherwise it is excluded.

```javascript
var names = ["tim", "ilias", "elie", "markus"];

var isEven = name => {
  return name.length % 2 === 0;
};
var isOdd = name => {
  return name.length % 2 !== 0;
};

var evenLengthNames = names.filter(isEven);
var oddLengthNames = names.filter(isOdd);

console.log(evenLengthNames);
console.log(oddLengthNames);

// Should output
// > ["elie", "markus"]
// > ["tim", "ilias"]
```

### reduce

Reduce iterates over an array and turns it into one, accumulated value. In some other languages it is called `fold`.

```javascript
var nums = [1,2,3,4];
var add = (a, b) => {
  return a + b;
};

var sum = nums.reduce(add);
console.log(sum);

// Should output:
// > 10
// which is, 1 + 2 + 3 + 4
```

Reduce also usually accepts an option third parameter that will be the initial accumulated value. If it is omitted, then the reduction starts with the first two values in the array.

```javascript
var nums = [1,2,3,4];
var add = (a, b) => {
  return a + b;
};

var sum = nums.reduce(add, 10);
console.log(sum);

// Should output:
// > 20
// which is, 10 + 1 + 2 + 3 + 4
```

### sort

```text
items.sort((a, b) => {

  if (a < b) {
    return -1;
  }
  if (a > b) {
    return 1;
  }

  // equal
  return 0;
});
```

### Pairing Exercises

* create an `index.html` and `script.js`
* repeat all the code above

#### Further

* copy / paste the pokedex into your file
* use `reduce` to help you create an average pokemon weight
* use `map` to get an array of all the first letters of the pokemon names.
* use filter to find `Fearow`

#### Further

Investigate some other array methods: `find`, `flat`, `every` [here.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)

### Resources

Here are some good blog posts that break down `map`, `filter`, and `reduce`.

* [Transforming Arrays with Array\#map](http://adripofjavascript.com/blog/drips/transforming-arrays-with-array-map.html)
* [Transforming Arrays with Array\#filter](http://adripofjavascript.com/blog/drips/filtering-arrays-with-array-filter.html)
* [Transforming Arrays with Array\#reduce](http://adripofjavascript.com/blog/drips/boiling-down-arrays-with-array-reduce.html)
* [Sorting Arrays](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

### Extra

### Write your own callback

We can write a function that does something we can specify outside the function.

```text
var alertFiveTimes = (stringCallback) => {
  for( var i=0; i<5; i++){
    alert( stringCallback() );
  }
};

var encouraging = () => {
  return "awesome!!";
};

var jerk = () => {
  return "ewww, gross";
};

alertFiveTimes( encouraging );
alertFiveTimes( jerk );
```

A more complete example is one that can do a generic operation - in this case on a set of 2 numbers - and then return the result.

The individual operation we can define somewhere else.

```text
var add = (a,b) =>{
  return a + b;
};

var listOfNumbers = [91,52,53,54,5,6,7,8];
var listOfNumbers = [1,1,1,1];

var repeatOperation = (numbers, callback)=>{

  var currentResult = 0;

  for( var i=0; i<numbers.length; i++){
    console.log(currentResult);
    currentResult = callback(currentResult, numbers[i]);
  }

  return currentResult;
};

var total = repeatOperation(listOfNumbers, add);
```

This makes the function we wrote flexible, because it can accomplish more than one kind of task

```text
var subtract = (a,b)=>{
  return a - b;
};

var listOfNumbers = [100,10,10,10];

var total = repeatOperation(listOfNumbers, add);
```

### Returning functions from functions

You can probably guess by now how to return a function from a function:

```javascript
var drinkMaker = (drinkType)=> {
  return function(drinkVolume) {
    return {
      drink: drinkType,
      volume: drinkVolume
    };
  };
};

var cocktailMaker = drinkMaker('cocktail');
var smoothieMaker = drinkMaker('smoothie');

cocktailMaker('4oz');
smoothieMaker('16oz');
```

We'll see that if we print the contents of `cocktailMaker` and `smoothieMaker`, we get functions that were returned from the function `drinkMaker`. Now, we can call these functions and pass in additional arguments. Neat!

Functional programming is a popular topic in the context of js, so we'll be seeing more examples like these in the future. Like with iterators!

### Further Pairing Exercise

* copy paste and run the write your own callback code
  * add your own string-returning function and use the alertFiveTimes function to call it.
* Write a function that uses a loop and does multiplication on two numbers-

Given:

```text
var add = (a,b)=>{
  return a + b;
};
```

Calling the function will look like this:

```text
multiply( add, 2 , 3  );
```

The result should be 6.

* write a console stopwatch function. When is starts, console log the current stopwatch time in seconds in this format: `hours:minutes:seconds`
* write code that will set a countdown timer. Prompt the user for how many seconds they want the timer to last, and when you get their answer, start the timer.
* write your own foreach function that takes a callback parameter that will run for each iteration.

