---
layout: post
title: MongoDB Indexes
---

## What is Index?

Indexes are essentially a way for MongoDB to pre-compute the results of a query.

It works similar to the one in SQL databases.

Without indexes, mongoDB will do a `collection scan` to find documents that match the query.

If the collection gets larger, it will impact the performance.

Using indexes can avoid this down impact.

## How to Create?

* Manual : http://mongodb.github.io/node-mongodb-native/2.0/api/Db.html#createIndex

```
<DB>.<Collection>.createIndex({ <Field Name>: 1});
```
* To create Multikey index, you just need create an index on the array field.

**Careful:**
* be wary of arrays that grow without bound.
* Large documents take up more bandwidth and multikey indexes on large arrays have some significant performance overhead on MongoDB 3.0's default storage engine and MMAPv1.

### examples

```
(Single key index)
db.names.insert({name: 'John'});
db.names.createIndex({name: 1});
db.names.find({name: 'John'});

(Multi key index)
db.names.insert({names: ['John']});
db.names.createIndex({names: 1});
db.names.find({names: 'John'});
```
