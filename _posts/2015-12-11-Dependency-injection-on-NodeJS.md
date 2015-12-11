---
layout: post
title: Dependency Injection On Node.JS
---
*This is my note for the ["M101x Introduction to MongoDB using the MEAN Stack"](https://www.edx.org/course/introduction-mongodb-using-mean-stack-mongodbx-m101x) at edX.
The purpose of this note is to help me to remember what I have learned and what I did later.*

# What Is Dependency Injection?

>Dependency injection is a software engineering practice
that helps you break your code up into small,
easy to maintain, chunks.
The general idea of dependency injection is to separate initialization code from business logic, so your rest API route handlers never have to worry about say, setting up Mongoose models.
(edX)

* StackOverFlow:
  http://stackoverflow.com/questions/130794/what-is-dependency-injection

Using DI, it is going to be easier to refactor.
Without it:
- More models you add, and start building functionality out on top of your models, start having different server configuration, the complexity can quickly spiral out of control
- it is going to be difficult to write unit codes

## Examples

**Bad**

```js

...

var userSchema = new mongoose.Schema({
  name: String
});
var User = mongoose.model('User', userSchema);

User.create({ name: 'John' }, function(error, doc) {
  console.log(require('util').inspect(doc));
});

...

```

**Good?**

```js

...

var userSchema = new mongoose.Schema({
  name: String
});
var User = mongoose.model('User', userSchema);

// Takes the model as a param.
myUserFunction(User);

function myUserFunction(User) {
  User.create({ name: 'John' }, function(error, doc) {
    console.log(require('util').inspect(doc));
  });  
}

...

```

What if you want to add a parameter to the function? What if you want to have the function depend on another Mongoose model. You will need to change all the places that call the function. Cumbersome! This is why you want to use a framework to handle dependency injection for you.

## Wagner

Dependency injector.

https://www.npmjs.com/package/wagner-core

* factory()
  * Wagner lets you register named factories which are functions that return values. These values are known as services.
  * Similar to AngularJS's dependency injector.
* invoke()
  * takes a function and executes it. also inspects the functions's parameter list and pulls in services that match the parameter names.
  * behaves much like AngularJS's invoke function

```js
app.listen(3000);
console.log('Listening on port 3000!');

function setupModels(mongoose, wagner) {
  mongoose.connect('mongodb://localhost:27017/test');

  var userSchema = new mongoose.Schema({
    name: String
  });
  var User = mongoose.model('User', userSchema);

  wagner.factory('User', function() {
    return User;
  });
}

function setupApp(app, wagner) {
  var routeHandler = wagner.invoke(function(User) {
    return function(req, res) {
      User.findOne({ _id: req.params.id }, function(error, user) {
        res.json({ user: user });
      });
    };
  });

  app.get('/user/:id', routeHandler);
}
```
