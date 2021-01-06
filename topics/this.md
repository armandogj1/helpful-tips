---
title: Keyword 'this'
parent: Topics
# nav_exclude: true
---

# The Keyword _this_

What "this" refers to is entirely dependent on the call-site of the function (i.e. how the function was invoked).

```js
// A simple function
var eat = function () {
  this.eating = true;
};

// calling eat as a Free Function
eat();
// if using strict mode
// this will be undefined
// an error will be thrown
("TypeError: Cannot set property 'eating' of undefined");
// otherwise
// an eating property will be assigned to the global object
```

In order to make sure "this" is bound to what you expect, you must bind it explicitly.

```js
// A simple object
var bob = {
  name: 'bob',
};

// Adding the function as a property of the object
// (aka. creating a method, by reference)
bob.eat = eat;

bob.eat(); // implicit binding aka. Method Invocation
// (this === object to the left of the dot)

eat.call(bob); // using the function with a context of bob
eat.apply(bob); // using the function with a context of bob

var jen = {
  name: 'jen',
};
bob.eat.call(jen); // using bob's method with a context of jen

var jenBound = eat.bind(jen); // explicit binding
jenBound(); // jen bound as context, this will refer to the jen object
```

Using a method as a callback of a Higher Order Function
In setTimeout and other Higher Order Functions that use callbacks,
the callbacks are always called as FFI's

```js
setTimeout(bob.eat, 1000); // the method will be passed as a Free Function losing its context
// setTimeout only gets the function and not the object containing the method.
// Think of it being called like so eat() and not bob.eat(). There is nothing left of the dot

setTimeout(jenBound, 1000); // jen is bound as the context and this will reference jen when invoked

setTimeout(() => bob.eat(), 1000); // defining an arrow function which will invoke bob.eat keeps context
// it does so through closure. The arrow is defined in place and passed as the first argument. bob is in the arrow functions outer scope and closes on it.
// Wherever setTimeout invokes the callback it remembers the values in its scope, which allows it to call the eat method of bob.
// The context is maintained because bob is left of the dot
```
