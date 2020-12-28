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

Remember:

The hierarchy, from most to least "important", is:
"new" keyword
Explicit binding
Implicit binding
Free Function Invocation (FFI)
In setTimeout and other Higher Order Functions that use callbacks,
the callbacks are always called as FFI's.
