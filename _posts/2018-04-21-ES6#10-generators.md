---
title: "JavaScript ES6 for Beginners #10: Generators"
categories:
  - ES6
tags:
  - programming
  - guide
---

![ES6-card-10](https://albertomontalesi.github.io/assets/images/ES6/ES6-card-10.jpg)



## What is a Generator

A generator function is a function that we can start and stop, for an indefinite amount of time and restart, with the possibility of passing additional data at a later point in time.


To create a generator function we write like this:

``` js
function* fruitList(){
  yield 'Banana';
  yield 'Apple';
  yield 'Orange';
}

const fruits = fruitList();

fruits;
// Generator
fruits.next();
// Object { value: "Banana", done: false }
fruits.next();
// Object { value: "Apple", done: false }
fruits.next();
// Object { value: "Orange", done: false }
fruits.next();
// Object { value: undefined, done: true }
```

Let's have a look at the code piece by piece:

- we declared the function using `function*`
- we used the keyword `yield` before our content
- we start our function using `.next()`
- the last time we call `.next()` we receive and empty object and we get `done: true`

Our function is paused between each `.next()` call.


&nbsp;

### Looping over an array

We can use the `for of` loop to iterate over our generator and `yield` the content at each loop.

``` js
// create an array of fruits
const fruitList = ['Banana','Apple','Orange','Melon','Cherry','Mango'];

// create our looping generator
function* loop(arr) {
  for (const fruit of fruitList) {
    yield `I like to eat ${fruit}`;
  }
}


const fruitGenerator = loop(fruitList);
fruitGenerator.next();
// Object { value: "I like to eat Banana", done: false }
fruitGenerator.next();
// Object { value: "I like to eat Apple", done: false }
fruitGenerator.next().value;
// "I like to eat Melon"
```

- Our new generator will loop over the array and print one value at a time every time we call `.next()`.
- if you are only concerned about getting the value then use `.next().value` and it will not print the status of the generator

&nbsp;
### Finish the generator with `.return()`

Using `.return()` we can return a given value and finish the generator.

``` js
function* fruitList(){
  yield 'Banana';
  yield 'Apple';
  yield 'Orange';
}

const fruits = fruitList();

fruits.return();
// Object { value: undefined, done: true }
```

In this case we got `value: undefined` because we did not pass anything in the `return()`.

&nbsp;

### Catching errors with `.throw()`


``` js
function* gen(){
  try {
    yield "Trying...";
    yield "Trying harder...";
    yield "Trying even harder..";
  }
  catch(err) {
    console.log("Error: " + err );
  }
}

const myGenerator = gen();
myGenerator.next();
// Object { value: "Trying...", done: false }
myGenerator.next();
// Object { value: "Trying harder...", done: false }
myGenerator.throw("ooops");
// Error: ooops
// Object { value: undefined, done: true }
```

As you can see when we called `.throw()` the `generator` finished even though we still had one more `yield` to execute.

&nbsp;



## Combining Generators with Promises

As we have previously seen, Promises are very useful for asynchronous programming and by combining them with generators we can have a very powerful tool at our disposal to avoid problems like the callback hell.

As we are solely discussing ES6, I won't be talking about `async functions` as they were introduce in ES8 (ES2017).


Using a Generator in combination with a Promise will allow us to write asynchronous that feels like synchronous.

The `yield` keyword allows us to pause the function and wait for a promise to return something.

``` js
example goes here

```

---
&nbsp;

This was the tenth part of my ES6 for beginners course, check out the rest of them [here](https://albertomontalesi.github.io/courses/es6).

You can also read this articles on medium, on my [profile](https://medium.com/@labby92).

Thank you for reading.