---
layout: post
title: JavaScript Promises (SWND course note)
---
This is my note for the following course at Udacity.
[JavaScript Promises](https://www.udacity.com/course/viewer#!/c-ud898/l-5972243496/m-6109728857)

# Promises

Became available in ES6. Before ES6, jQuery was mostly used to achieved this.

## Terms
* Fulfilled(Resolved)
  * the action related to the promise exceeded
* Rejected
  * the action related to the promise failed
* Pending
  * the promise has not yet fulfilled or rejected
* Settled
  * the promise is either fulfilled or rejected

## Timeline

* Promises work different than how event listeners work in terms of timeline.
  * Promises will execute even if it is defined after the promise resolved.

```
(Event listeners)
XXX Event fires # If this happens before the event listener set...
 |
 |
XXX Event listener set  # Will NOT be executed unless the event fires again
 |

(Promises)
XXX Promise resolves  # If this happens before setting action for resolution value
 |
 |
XXX Set action for resolution value # WILL execute
 |
```

* Promises work on the main thread. Therefore, it may block the other code if
the promise runs a long lines of codes

## Syntax

* example code

```js
new Promise(function(resolve, reject) {
  resolve('hi');   # works
  resolve('bye');  # can not happen a second time
});
```

```js
new Promise(function(resolve[, reject]) {
  var value = doSomething();
  if (thingWorked) {
    resolve(value); // SAME value
  } else if (somethingWentWrong) { // If a promise is passed, the promise executes first.
    reject(); // No argment
  }
}).then(function(value) { // SAME value. And the value resolved in the promise gets passed to the function called by '.then'
  // Success!
  return nextThing(value);
}).catch(rejectFunction); // Receives undefined. The value from the promise will be passed into the function called by '.catch'
```

```js
new Promise(fucntion(resolve, reject) {
  var img = document.createElement('img');
  img.src = 'image.jpg';
  img.onload = resolve;
  img.onerror = reject;
  document.body.appendChild(img);
})
.then(finishLading)
.catch(showAlternateImage);
```

# Useful Links
* Great Tutorial about promises
  * http://www.html5rocks.com/en/tutorials/es6/promises/
