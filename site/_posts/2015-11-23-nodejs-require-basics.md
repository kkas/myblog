---
layout: post
title: Node.js require() basics
---
# Node.js require() basics

*This is my note for the ["M101x Introduction to MongoDB using the MEAN Stack"](https://www.edx.org/course/introduction-mongodb-using-mean-stack-mongodbx-m101x) at edX.
The purpose of this note is to help me to remember what I have learned and what I did later.*

* index.js

```js

// this is the main entry file and has access to all the other files.

// By default in NodeJS, all the files have their own scopes and the code in a file are not
// accessible by other files outside.
// Using global variables to share code is almost always mistake.
// Instead, 'require' function is a great way to share code between files.

// myfile.js
var fn = require('./myfile.js');
fn();

// test directory.
// NodeJS looks a index.js file in this directory.
// So, `require('./test')` is equivalent to `require('./test/index.js')`
var otherFn = require('./test').other;
otherFn();
```
* myfile.js

```js
// module.exports property. It is ok to think this as a return value of calling require of this file by using
// 'require'
module.exports = function() {
  console.log('Hello from myfile.js');
};
```
* test/index.js

```js
// Here uses exprots.other, rather than 'module.exports'.
// exports variable is a convinient shorthand for module.exports.
// This will do the same thing if you use 'modules.exports.other'
// The only difference is that you can not directly assign to the
// exports variable.
// Also note that the directory 'test' is ommited. 'require'
// resolves file names relativ eto the current file directory.
exports.other = require('./myotherfile');
```

* test/myotherfile.js

```js
module.exports = function() {
  console.log('Hello from test directory');
}
```

### output

```
$ node index.js
Hello from myfile.js
Hello from test directory
```
