---
layout: post
title: Using NodeJS testing Framework 'Mocha'
---
# Mocha

*This is my note for the ["M101x Introduction to MongoDB using the MEAN Stack"](https://www.edx.org/course/introduction-mongodb-using-mean-stack-mongodbx-m101x) at edX.
The purpose of this note is to help me to remember what I have learned and what I did later.*

## What is Mocha?

`Mocha` is the most famous testing framework for node.js. And also useful to test client side JavaScript.

The test is inspired by JUnit. So it uses `describe` and `it`.

> Mocha is a feature-rich JavaScript test framework running on Node.js and the browser, making asynchronous testing simple and fun. Mocha tests run serially, allowing for flexible and accurate reporting, while mapping uncaught exceptions to the correct test cases. Hosted on GitHub.
https://mochajs.org/

## How to Use?

* Open and edit `package.json`
```sh
$ vim package.json
```

* Add the following in `package.json`
```json
{
  "dependencies": {
    "mocha": "2.2.4"
  }
}
```

* Run `npm install`

* Write tests
  * sample test, `test.js`, taken from the course is the following. This example uses the built-in nodejs assert module. There are other modules available on NPM.

```js
var assert = require('assert');

describe('my feature', function() {
  it('works', function() {
    assert.equal('A', 'A');
  });

  it('fails gracefully', function() {
    assert.throws(function() {
      throw 'Error!';
    });
  });
});

describe('my other feature', function() {
    it('async', function(done) {
      setTimeout(function() {
        done();
      }, 25);
    });
});
```

* Execute the test
```sh
 $ ./node_modules/.bin/mocha test.js
```
(sample output)

```

  my feature
    ✓ works
    ✓ fails gracefully

  my other feature
    ✓ async


  3 passing (43ms)

```

## Useful Tips

* `-g` option
  * Short for `--grep`. You may run tests whose names match a certain regular expression.  
* `-R` option
  * Short for `--reporter`. You may select different reporter for test output. Default is spec reporter. There are several other built-in reporters available.

### Examples

(e.g.: Matches the test)

```
$ ./node_modules/.bin/mocha -g "fail" test.js


  my feature
    ✓ fails gracefully


  1 passing (14ms)

```

(e.g.: Matches the feature)

```
$ ./node_modules/.bin/mocha -g "other" test.js


  my other feature
    ✓ async


  1 passing (43ms)
```

(e.g.: `dot` reporter)

```
$ ./node_modules/.bin/mocha -R dot test.js


  ․․․

  3 passing (40ms)
```

(e.g.: `xunit` reporter (XML format))

```
$ ./node_modules/.bin/mocha -R xunit test.js
<testsuite name="Mocha Tests" tests="3" failures="0" errors="0" skipped="0" timestamp="Thu, 03 Dec 2015 09:41:00 GMT" time="0.038">
<testcase classname="my feature" name="works" time="0"/>
<testcase classname="my feature" name="fails gracefully" time="0"/>
<testcase classname="my other feature" name="async" time="0.032"/>
</testsuite>
```

(e.g.: `nyan` reporter (kitten))

```
$ ./node_modules/.bin/mocha -R nyan test.js
 3   -_-__,------,
 0   -_-__|  /\_/\
 0   -_-_~|_( ^ .^)
     -_-_ ""  ""

  3 passing (48ms)
```
