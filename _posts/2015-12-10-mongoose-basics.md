---
layout: post
title: Mongoose examples
---
# Mongoose
[Mongoose](http://mongoosejs.com/) is the most famous mongoDB ODM that provides functionality
like schema validation on top of the MongoDB node.js driver.

## Datatypes
There are 4 datatypes:
- Schema: a set of rules that define what fields a document may have and what properties the document must satisfy to be considered valid.
- Connection: Sockets.
- Model: Combination of Schema and Connection (at high level)
- Document: Can be thought of as an instantiation of a model.

## Handy Features

Mongoose has numerous handy features that make it an indispensable tool for web development to Node.js.

* `virtuals`:
  * properties that are typically computed from other properties. They are not persisted to database, but they can be accessed just like any other property.
  * e.g. displaying a price of a product
    * where a price of a product is 50, for example. With virtuals, it will be displayed '$50'

```
  var schema = new mongoose.Schema(productSchema);

  var currencySymbols = {
    'USD': '$',
    'EUR': '€',
    'GBP': '£'
  }

  schema.virtual('displayPrice').get(function() {
    return currencySymbols[this.price.currency] + '' + this.price.amount;
  });

  // This is How to reference this property
  console.log(p.displayPrice);
```
