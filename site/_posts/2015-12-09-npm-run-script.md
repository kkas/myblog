---
layout: post
title: npm run-script
---
# More about npm

npm is not just a package manager. `npm help` can give us all the commands that npm can handle.

```sh
$ npm help

Usage: npm <command>

where <command> is one of:
    access, add-user, adduser, apihelp, author, bin, bugs, c,
    cache, completion, config, ddp, dedupe, deprecate, dist-tag,
    dist-tags, docs, edit, explore, faq, find, find-dupes, get,
    help, help-search, home, i, info, init, install, issues, la,
    link, list, ll, ln, login, logout, ls, outdated, owner,
    pack, ping, prefix, prune, publish, r, rb, rebuild, remove,
    repo, restart, rm, root, run-script, s, se, search, set,
    show, shrinkwrap, star, stars, start, stop, t, tag, team,
    test, tst, un, uninstall, unlink, unpublish, unstar, up,
    update, upgrade, v, verison, version, view, whoami

npm <cmd> -h     quick help on <cmd>
npm -l           display full usage info
npm faq          commonly asked questions
npm help <term>  search for help on <term>
npm help npm     involved overview

Specify configs in the ini-formatted file:
    /Users/kentakikui/.npmrc
or on the command line via: npm <command> --key value
Config info can be viewed via: npm help config

npm@2.14.1 /opt/local/lib/node_modules/npm
```

## npm test

`npm test` runs a package's "test" script, if one was provided.

### example

Add `scripts` section in package.json.

```json
{
  "scripts": {
    "test": "mocha test.js",
    "test-kitten": "mocha -R nyan test.js"
  },
  "dependencies": {
    "underscore": "1.5.2",
    "mongodb": "2.0.48",
    "mocha": "2.2.4"
  }
}
```

Run `npm test` will execute the test command that is just defined.
(This is a example test script that I just wrote in the previous blog.)

```sh
$ npm test

> @ test /Users/kentakikui/Develop/edX/MEAN_stack
> mocha test.js



  my feature
    ✓ works
    ✓ fails gracefully

  my other feature
    ✓ async


  3 passing (45ms)

```

We can even run the nyan test(test-kitten) by `npm run test-kitten`.
`npm test` is a shorthand version of `npm run test`.

```sh
$ npm run test-kitten

> @ test-kitten /Users/kentakikui/Develop/edX/MEAN_stack
> mocha -R nyan test.js

 3   -_-__,------,
 0   -_-__|  /\_/\
 0   -_-_~|_( ^ .^)
     -_-_ ""  ""

  3 passing (48ms)

```
