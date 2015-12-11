---
layout: post
title: MongoDB Schema Design Principle
---

## Schema Design Principle

### 1. Store What You Query For
Pros:
 - Fast in-place updates
 - Fast queries
   Better performance than SQL with multi-joins.

 Con:
 - No join

In order to take advantage of mongoDB strength, you should remember that your ** MongoDB schemas should closely match the data you want to display to the end user**.

>In other words, MongoDB's lack of joins
>may seem intimidating to developers
>from a SQL background, however, to paraphrase
>Linux's original architect, Linus Torvalds,
>if you have an API endpoint with multiple joins,
>you're screwed anyway and should fix your API.
>As you'll see when you design the API for your retail app,
>each API endpoint will be primarily
>responsible for loading data from a single collection.

### 2. Principle Of Least Cardinality

MongoDB schema can contain arrays.
In an array, you may store reviews that are associated with the user.
Be careful if you can't limit the number of reviews.
**Arrays that grow without bound are a very bad practice for mongoDB**
- Bad performance
- 16MB limit of document size

### example

Look at the example schema below.
When you want to query a user with corresponding reviews,
you will have to use 2 queries: one for user and one for reviews.

There is no way to do this by one query unless you change the schema.

**example(one-to-many):**
```
(Users)
{
  username: 'val',
  average: 8 // if you want to search by average, for example, you need to pre calculate and store it in the Users document.
}

(Reviews)
{
  score: 6,
  author: 'val' // Do this instead of put reviews array in User document. (smaller array size. least Cardinality.)
}
{
  score: 10,
  author: 'val'
}
```

**example2 (many-to-many):**

* If an events have a hundred of millions of attendees, you would have a mapping collection analogous to an SQL mapping table.
* If you expect only few hundred at most users to attend a meeting, then you can de-normalize this many-to-many relationship by keeping a list of ID's representing attendees.
  * There is a bound for the array growth.
  * It depends on the situation if 500 in an array is too big or not.
```
(Users)
{
  name: 'John'
}
{
  name: 'Jack'
}

(Events)
{
  name: 'Meetup1',
  attendees: []
}
{
  name: 'Meetup2',
  attendees: []
}
```
