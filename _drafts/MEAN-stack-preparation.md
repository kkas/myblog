# MEAN Stack

*This is my note for the ["M101x Introduction to MongoDB using the MEAN Stack"](https://www.edx.org/course/introduction-mongodb-using-mean-stack-mongodbx-m101x) at edX.
The purpose of this note is to help me to remember what I have learned and what I did later.*


## What is MEAN Stack?
is a software, full stack.
MEAN: - M(MongoDB), E(ExpressJS), A(AngularJS), N(NodeJS)

## Preparation

### Versions
* Mac OSX 10.10.5 (Yosemite)
* MongoDB: 3.0.7
* Node.js: v0.12.7
  * npm: 2.14.1
* mongoose:

### MongoDB standalone installation

(Detailed instruction can be found at [here](https://docs.mongodb.org/manual/installation/).)

1. Download it from [www.mongodb.org/downloads](https://www.mongodb.org/downloads)
1. Proceed the following steps.

```sh
$ cd ~/Downloads/

# Use `curl` instead of `wget` since it is not installed on Yosemite by default.
$ curl https://fastdl.mongodb.org/osx/mongodb-osx-x86_64-3.0.7.tgz -o mongodb-osx-x86_64-3.0.7.tgz

# Unpack the download archive
$ tar -zxvf mongodb-osx-x86_64-3.0.7.tgz
x mongodb-osx-x86_64-3.0.7/README
x mongodb-osx-x86_64-3.0.7/THIRD-PARTY-NOTICES
x mongodb-osx-x86_64-3.0.7/GNU-AGPL-3.0
x mongodb-osx-x86_64-3.0.7/bin/mongodump
x mongodb-osx-x86_64-3.0.7/bin/mongorestore
x mongodb-osx-x86_64-3.0.7/bin/mongoexport
x mongodb-osx-x86_64-3.0.7/bin/mongoimport
x mongodb-osx-x86_64-3.0.7/bin/mongostat
x mongodb-osx-x86_64-3.0.7/bin/mongotop
x mongodb-osx-x86_64-3.0.7/bin/bsondump
x mongodb-osx-x86_64-3.0.7/bin/mongofiles
x mongodb-osx-x86_64-3.0.7/bin/mongooplog
x mongodb-osx-x86_64-3.0.7/bin/mongoperf
x mongodb-osx-x86_64-3.0.7/bin/mongosniff
x mongodb-osx-x86_64-3.0.7/bin/mongod
x mongodb-osx-x86_64-3.0.7/bin/mongos
x mongodb-osx-x86_64-3.0.7/bin/mongo

# Add the mongo core server to your path
$ ln -s ~/Downloads/mongodb-osx-x86_64-3.0.7/bin/mongod /usr/local/bin/mongod

# Make sure it is added propery.
$ mongod --version
db version v3.0.7
git version: 6ce7cbe8c6b899552dadd907604559806aa2e9bd

# Add the mongo shell in your path as well.
$ ln -s ~/Downloads/mongodb-osx-x86_64-3.0.7/bin/mongo /usr/local/bin/mongo
$ mongo --version
 MongoDB shell version: 3.0.7

# Create a dir for storing data
$ kentakikui (master) Develop $ mkdir -p edX/MEAN_stack/data/db/

# Start the server with `dbpath` option to use the dir
$ mongod --dbpath ~/Develop/edX/MEAN_stack/data/db/
2015-11-20T19:04:14.612+0900 I JOURNAL  [initandlisten] journal dir=/Users/kentakikui/Develop/edX/MEAN_stack/data/db/journal
2015-11-20T19:04:14.613+0900 I JOURNAL  [initandlisten] recover : no journal files present, no recovery needed
2015-11-20T19:04:14.640+0900 I JOURNAL  [durability] Durability thread started
2015-11-20T19:04:14.640+0900 I JOURNAL  [journal writer] Journal writer thread started
2015-11-20T19:04:14.641+0900 I CONTROL  [initandlisten] MongoDB starting : pid=86861 port=27017 dbpath=/Users/kentakikui/Develop/edX/MEAN_stack/data/db/ 64-bit host=kikui-no-MacBook-Pro.local
2015-11-20T19:04:14.641+0900 I CONTROL  [initandlisten] db version v3.0.7
2015-11-20T19:04:14.641+0900 I CONTROL  [initandlisten] git version: 6ce7cbe8c6b899552dadd907604559806aa2e9bd
2015-11-20T19:04:14.641+0900 I CONTROL  [initandlisten] build info: Darwin mci-osx108-13.build.10gen.cc 12.3.0 Darwin Kernel Version 12.3.0: Sun Jan  6 22:37:10 PST 2013; root:xnu-2050.22.13~1/RELEASE_X86_64 x86_64 BOOST_LIB_VERSION=1_49
2015-11-20T19:04:14.641+0900 I CONTROL  [initandlisten] allocator: system
2015-11-20T19:04:14.641+0900 I CONTROL  [initandlisten] options: { storage: { dbPath: "/Users/kentakikui/Develop/edX/MEAN_stack/data/db/" } }
2015-11-20T19:04:14.642+0900 I INDEX    [initandlisten] allocating new ns file /Users/kentakikui/Develop/edX/MEAN_stack/data/db/local.ns, filling with zeroes...
2015-11-20T19:04:14.687+0900 I STORAGE  [FileAllocator] allocating new datafile /Users/kentakikui/Develop/edX/MEAN_stack/data/db/local.0, filling with zeroes...
2015-11-20T19:04:14.687+0900 I STORAGE  [FileAllocator] creating directory /Users/kentakikui/Develop/edX/MEAN_stack/data/db/_tmp
2015-11-20T19:04:14.816+0900 I STORAGE  [FileAllocator] done allocating datafile /Users/kentakikui/Develop/edX/MEAN_stack/data/db/local.0, size: 64MB,  took 0.128 secs
2015-11-20T19:04:14.961+0900 I NETWORK  [initandlisten] waiting for connections on port 27017
```
```
# Now you can connect to the database using `mongo` shell
$ mongo
MongoDB shell version: 3.0.7
connecting to: test
> db.test.insert({ hello: "world" });
WriteResult({ "nInserted" : 1 })
> db.test.findOne({ hello: "world" });
{ "_id" : ObjectId("564ef1689f60b8be21b31faf"), "hello" : "world" }
> db
test
> exit
bye
```

* notes
  * `mongod`: mongoDB core server
  * `mongo`: the mongoDB shell
  * mongoDB stores obejcts as BSON (Binary JSON), which is a strict superset of JSON.

### Node.js
(it was installed alread on my mac.)
nodejs comes with npm.

```
$ node -v
v0.12.7
$ npm -v
2.14.1
```

1. Create a `package.json`. Create a file with `vim` and add the following.
```js
{
  "dependencies": {
      "underscore": "1.5.2"
  }
}
```
1. Install the package.
```sh
$ ls node_modules/underscore/
LICENSE           README.md         package.json      underscore-min.js underscore.js
```

### MongoDB Driver
this driver connects the mongoDB and node.js.
* https://www.npmjs.com/package/mongodb

[What is `Mongoose`?](http://mongoosejs.com/)

[(Quote from the course)](https://courses.edx.org/courses/course-v1:MongoDBx+M101x+3T2015/courseware/4cf555e7a26d4fbb87503adf07ef03ce/e244ef26acf5453bb246041bf86df1d3/)
> `Mongoose` is an object document mapper,
or ODM for short, that provides functionality
like schema validation on top of the MongoDB node.js driver.
However, since Mongoose is a layer on top of the MongoDB
driver, and uses the driver to talk to the MongoDB server
MongoD, it helps to start with a low level driver
before using the high level tools.
