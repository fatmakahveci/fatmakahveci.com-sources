---
title: MongoDB
description: MongoDB
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "MongoDB"
  - "coding"
  - "Database"
comments: true
---
- A document-oriented database, which aims to ease scaling out
- It automatically takes care of balancing data and load across a cluster, redistributing documents automatically and routing reads and writes to the correct machines.
- By allowing embedded documents and arrays, the document-oriented approach makes it possible to represent complex hierarchical relationships with a single record.
- There are also no predefined schemas: a document's keys and values are not of fixed types or sizes so adding or removing fields as needed becomes easier.
- It is type- and case-sensitive.
- It can query for all documents where `<bla_bla>` is an element of the `<bla_bla>` array.
- If there is a common query, you can even create an index on the `<bla_bla>` key to improve the query's speed.
- It allows atomic updates that modify the contents of arrays.
- It understands the structure of embedded documents and can reach inside them to build indexes, perform queries, or make updates.

---

## Basic concepts

### Collection

- MongoDB groups documents into collections.
- Analog of a table in RDBMs
- It has dynamic schemas.
  - A single collection can have any number of different shapes.
  - Defining schemas is good practice forced by
    - MongoDB's document validation functionality
    - Object-document mapping libraries available for many PLs
- It is identified by its name.
  - `""` is not valid.
  - It must not contain `\0` (the null character), which signifies the end of a key.
  - Not start with `system.`.
  - `$` have special properties and should only be used in certain circumstances.
- Naming: `<database_name>.<collection_name>`

#### Why we should use more than one collection

- If we're querying for blog posts, it's a hassle to weed out documents containing author data.
- It's much faster to get a list of collections than to extract a list of the types of documents in a collection.
- Grouping documents of the same kind together in the same collection allows for data locality.
- By putting only documents of a single type into the same collection, we can index our collections more efficiently.

#### Subcollections

- `<collection>.<subcollection>` only for organizational purposes

### Database

- MongoDB groups collections into databases.
- A single instance of MongoDB can host multiple independent databases, each grouping together zero or more collections.
  - Storing all data for a single application in the same database is practical.
  - `/`, `\`, `.`, `"`, `*`, `<`, `>`, `:`, `|`, `?`, `$`, ` `, or `\0` not be contained in naming.
  - Database names are case-insensitive, limited to a max of 64 bytes.
  - Reserved names
    - `admin` db plays a role in authentication and authorization.
    - `local` db stores data specific to a single server.
    - `config` db stores information about each shard.

`show dbs`
`use <database_name>`
`<database_name>`

#### Creating Users

`db.createUser({ user : <user_name>, pwd : <password>, roles : ["readWrite", "dbAdmin"] });`

### Document

- The basic unit of data for MongoDB (~row in RDBMs)
- An ordered set of keys with associated values
- Its representation depends on the PL
- Keys are strings.
  - It must not contain `\0` (the null character), which signifies the end of a key.
  - `.` and `$` have special properties and should only be used in certain circumstances.
  - It cannot contain replicated keys.

### Mongo shell

- Built-in support for administering MongoDB instances and manipulating data using the MongoDB query language.
- `mongo <code1>.js <code2>.js`

---

## Data types

### Arrays

- Arrays can contain different data types as values.
  - `{"x" : [ "pie", 3.14 ]}`

- Ordered operations
  - lists
  - stacks
  - queues
- Unordered operations
  - sets

- Arrays use 0-based indexing.
- You can manipulate the values in array in two ways:
  - by position
  - by position operator `$`

#### Array operators

- `"$push"` adds elements to the end of an array if the array exists. If not, it creates an array.

##### Modifiers with `push`

- `"$each"` pushes multiple values in one operation.
  - i.e. `db.stock.ticker.updateOne({"_id" : "GOOG"}, {"$push" : {"hourly" : {"$each" : [562.776, 562.790, 559.123]}}})`

- `"$slice"` prevents an array from growing beyond a certain size.
  - i.e. `db.movies.updateOne({"genre" : "horror"}, {"$push" : {"top10" : {"$each" : ["Nightmare on Elm Street", "Saw"], "$slice" : -10}}})` limits the array to the last 10 elements pushed.

- `"$sort"` sorts all of the objects in the array by `<field>`.

- `"$ne"` adds values if they are not present.
  - i.e. `db.papers.updateOne({"authors cited" : {"$ne" : "Richie"}}, {$push : {"authors cited" : "Richie"}})`

- `"$addToSet"` adds values if they are not present. It prevents duplications, which is useful where `"$ne"` does not work. `"$addToSet"`+`"$each"` can add multiple unique values, which cannot be done with `"$ne"`+`"$push"`.

- `"$pop"` treats an array like a queue or stack.
  - `{"$pop" : {"key" : 1}}` removes an element from the end of the array. `{"$pop" : {"key" : -1}}` removes it from the beginning.

- `"$pull"` removes all elements that match the given criteria. ([1, 1, 2, 1] - pull 1 -> [2])

  ````js
  db.lists.insertOne({"todo" : ["dishes", "laundry", "dry cleaning"]})
  db.lists.updateOne({}, {"$pull" : {"todo" : "laundry"}}) // todo: dishes, dry cleaning
  ```

### Binary data

- A string of arbitrary bytes

### Boolean

- `{"x" : true}`

### Code

- `{"x" : function() { /* ... */ }}` stores arbitrary JavaScript queries and documents.

### Dates

- `{"x" : new Date()}` returns a string representation of the date.

### Embedded documents

- A document which is used as the value for a key
- `{"x" : {"foo" : "bar"}}`

```javascript
{
    "name"    : "John Doe",
    "address" : {
                  "street" : "123 Park Street",
                  "city"   : "Anytown",
                  "state"  : "NY"
                }
}
```

### Null

- `{"x" : null}`

### Number

- `{"x" : 3.14}`
- `{"x" : NumberInt("3")}`
- `{"x" : NumberLong("3")}`

### Object ID

- `{"x" : ObjectId()}` is a 12-byte ID for documents.

![object_id](/img/object_id.png)

- Default type for `_id`

#### _id

- A special key of each document within a collection.
- It can be any type.

### Regex

- `{"x" : /foobar/i}`

---

## The features provided by MongoDB

### Indexing

- It supports generic secondary indexes and provides unique, compound, geospatial, and full-text indexing.

### Aggregation

- It provides an aggregation framework based on the concept of data processing pipelines.
- Aggregation pipelines allow you to build complex analytics engines by processing data through a series of relatively simple stages on the server side, taking full advantage of database optimizations.

### Special collection and index types

- It supports time-to-live (TTL) collections for data that should expire at a certain time, such as sessions and fixed-size (capped) collections, for holding recent data, such as logs.
- It supports partial indexes limited to only those documents matching a criteria filter to increase efficiency and reduce the amount of storage space required.

### File storage

- It supports an easy-to-use protocol for storing large files and file metadata.

## Querying

- Query for ranges, set inclusion, inequalities, and more by using `$` conditionals.

### `find()`

- It performs queries in MongoDB.
- It returns a subset of documents in a collection.
- `find(<query_criteria>, <specify_the_keys_you_want>)`
  - i.e. `db.users.find({}, {"username" : 1, "email" : 1})` returns only the _username_ and _email_ keys.
  - i.e. `db.users.find({}, {"fatal_weakness" : 0})` returns except the _fatal\_weakness_ key.
- `{}` matches everything in the collection.

### Query conditionals

- `"$lt"`, `"$lte"`, `"$gt"`, `"$gte"`

  ```js
  `db.users.find({"age" : {"$gte" : 18, "$lte" : 30}})` // 18 < age < 30

  // Dates
  start = new Date("01/01/2007")
  db.users.find("registered" : {"$lt" : start}) // before January 1, 2007
  ```

- `"$ne"` := not equal to
  - i.e. `db.users.find({"username" : {"$ne" : "joe"}})`

- `"$in"`, `"$nin"` (not in), and `"$or"` queries for a variety of values for a single key.
- While `"$or"` will always work, use `"$in"` whenever possible as the query optimizer handles it more efficiently.

```js
db.raffle.find({"ticket_no" : {"$in" : [12345, "joe"]}})

db.raffle.find({"$or" : [{"ticket_no" : 725}, {"winner" : true}]})
db.raffle.find({"$or" : [{"ticket_no" : {"$in" : [725, 542, 390]}}, {"winner" : true}]}) // $or can contain other conditionals.
```

- `"$not"` is a meta conditional so it can be applied on top of any other criteria.

### Type-specific queries

#### `null`

- It also matches "does not exist." Thus, querying for a key with the value `null` will return all documents lacking that key.
- If we only want to find keys whose value is `null`, we can check that the key is `null` and exists using the `"$exists"` conditional.
  - i.e. `db.c.find({"z" : {"$eq" : null, "$exists" : true}})`

#### `"$regex"`

- i.e. `db.users.find({"name" : {"$regex" : /joe/i }})` search for case-insensitive i.e. Joe and joe

#### Querying arrays

```js
db.food.insertOne({"fruit" : ["apple", "banana", "peach"]})
db.food.find({"fruit" : "banana"}) // will match
```

- `"$all"` matches a list of elements. Order does not matter.

```js
db.food.insertOne({"_id" : 1, "fruit" : ["apple", "banana", "peach"]})
db.food.insertOne({"_id" : 2, "fruit" : ["apple", "kumquat", "orange"]})
db.food.insertOne({"_id" : 3, "fruit" : ["cherry", "banana", "apple"]})

db.food.find({"fruit" : {"$all" : ["apple", "banana"]}}) // ["cherry", "banana", "apple"], ["apple", "banana", "peach"]

// index @2
db.food.find({"fruit.2" : "peach"}) // ["apple", "banana", "peach"]
```

- `"$size"` queries for arrays of a given size.
  - It cannot be combined with another conditional.
    - i.e. `db.food.find({"fruit" : {"$size" : 3}})` // returns all of the above
  - i.e. `db.blog.posts.findOne(criteria, {"comments" : {"$slice" : 10}})` limits to the first 10 elements.

- `$` operator returns the matching element. It helps when you do not know the index of the element.
  - i.e. `db.blog.posts.find({"comments.name" : "bob"}, {"comments.$" : 1})`

- `"$elemMatch"` forces MongoDB to compare clauses with a single array element.

```js
// For the following documents {"x" : 5}, {"x" : 15}, {"x" : 25}, {"x" : [5, 25]}

db.test.find({"x" : {"$gt" : 10, "$lt" : 20}}) // {"x" : 15}, {"x" : [5, 25]}
db.test.find({"x" : {"$elemMatch" : {"$gt" : 10, "$lt" : 20}}}) // {}
db.test.find({"x" : {"$gt" : 10, "$lt" : 20}}).min({"x" : 10}).max({"x" : 20}) // {"x" : 15}
```

#### Querying on embedded documents

- There are two ways:
  1. query for the whole documents
  2. query for the individual key/value pairs

- Query documents can contain dots, which means "reach into an embedded document".
  - i.e. `db.people.find({"name.first" : "Joe", "name.last" : "Schmoe"})`

### `$where` queries

- It allows you to execute arbitrary JavaScript as part of your query.
- It should not be used unless strictly necessary because it is much slower than a regular query.
- For security, the use of "$where" clauses should be highly restricted or eliminated. End users should never be allowed to execute arbitrary "$where" clauses.

### Cursors

- Queries return a database cursor, which lazily returns batches of documents as you need them.
- The database returns results from `find` using a cursor.
- Metaoperations on a cursor include
  - skipping a certain number of results,
  - limiting the number of results returned, and
  - sorting results by any combination of keys in any direction.

#### How to create a cursor

1. Put some documents into a collection.
2. Do a query on them.
3. Assign the results to a local variable.

```js
for(i=0; i<100; i++) {
  db.collection.insertOne({x : i});
}
var cursor = db.collection.find();

cursor.forEach(function(x) {
  print(x.name);
});

while (cursor.hasNext()) {
  obj = cursor.next();
  // do stuff
}
```

### Covered queries

- When an index contains all the values requested by a query, the query is covered.
- If your query is only looking for the fields that are included in the index, it does not need to fetch the document.

## CRUD operations

### Create

- Adding new documents to a collection

- MongoDB will add `_id` key.
- `<database_name>.<collection_name>.insertOne(<document>)`, where `<document> = { <key>: <value> }`.
- `<database_name>.<collection_name>.insertMany([<document1>, <document2>])` passes an array of documents to the database.
  - default: true := ordered, but slow

### Read

- `<database_name>.<collection_name>.findOne();`
- `<database_name>.<collection_name>.find();` displays up to 20 documents.
- `<database_name>.<collection_name>.find().pretty();`, where `pretty()` as a helper function.

### Update

- Updating existing documents
- Updating a document is atomic: if two updates happen at the same time, whichever one reaches the server first will be applied, and then the next one will be applied.

- `<database_name>.<collection_name>.updateOne(<filter_document>, <modifier_document>)`
- `<database_name>.<collection_name>.updateMany(<filter_document>, <modifier_document>)`

- `<database_name>.<collection_name>.replaceOne(<filter_document>, <replace_document>)` fully replaces a matching document with a new one.

- i.e. `db.customers.update({first_name:"Steven"}, {$set:{gender:"male"}});` adds `gender: male` to the document of which `first_name` is `Steven`.

- Your update should always specify a unique document, perhaps by matching on a key like `_id`.

#### Update operators

- Special keys that can alter, add, or remove keys, and even manipulate arrays and embedded documents.

- `$inc` increments the value of the field by the specified amount.
  - If the field does not yet exist, it will be created.
  - It can be used only on values of type integer, long, double, or decimal.

- `$currentDate` sets the value of a field to the current date, either as a Date or a Timestamp.

- `$min` only updates the field if the specified value is less than the existing field value.

- `$max` only updates the field if the specified value is greater than the existing field value.

- `$mul` multiplies the value of the field by the specified amount.

- `$rename` renames a field.

- `$set` sets the value of a field in a document.
  - If the field does not yet exist, it will be created.

- `$setOnInsert` sets the value of a field if an update results in an insert of a document.
  - It does not affect update operations that modify existing documents.

- `$unset` removes the specified field.

#### Upserts

- An upsert is a special type of update.
- If no document is found that matches the filter, a new document will be created by combining the criteria and updated documents.
- If a matching document is found, it will be updated normally.

### Delete

- Removing documents from a collection

- `<database_name>.<collection_name>.deleteOne(<filter_document>)` deletes only a single match even if there are many.
- `<database_name>.<collection_name>.deleteMany(<filter_document>)` deletes all the documents that match a filter.

#### drop

- `<database_name>.<collection_name>.drop()` removes all documents in a collection.

### Security: Choosing the correct level of safety versus speed for all of these operations

- .

---

## Indexes

- `explain` command to see what MongoDB is doing when it executes the query.
  - i.e. `db.users.find({"username": "user101"}).explain("executionStats")`
  - `executionStats` mode helps us understand the effect of using an index to satisfy queries.
  - `totalKeysExamined` := the number of keys within the index MongoDB walked through to generate the result set.
  - `totalDocsExamined` := the number of documents MongoDB looked at while trying to satisfy the query.
  - `executionTimeMillis` := the number of milliseconds it took to execute the query.
  - `nReturned` := the number of results returned.
  - and more...

### Creating an index

- To choose which fields to create indexes for, look through your frequent queries and queries that need to be fast and try to find a common set of keys from those.
- `db.users.createIndex({"username" : 1})`
- If you need to sort on two (or more) criteria, you may need to have index keys go in different directions.
  - i.e. age by asc and name by desc order
- The direction (asc or desc) only matters for multikey sorts.
- If you have more than 32 MB of results MongoDB will just error out, refusing to sort that much data.
  - To avoid this, you must create an index supporting the sort operation or use sort in conjunction with limit to reduce the results to below 32 MB.

### Compound indexes

- `db.users.createIndex({"age" : 1, "username" : 1})` makes an index on both age and username.
- Below holds for most of the situations, when designing a compound index:
  - Keys for equality filters should appear first.
  - Keys used for sorting should appear before multivalue fields.
  - Keys for multivalue filters should appear last.
- This allows the query to find an exact value for the first index key and then search within that for a second index range.

### Implicit indexes

- If an index has N keys, you get a "free" index on any prefix of those keys. For example, if we have an index that looks like {"a": 1, "b": 1, "c": 1, ..., "z": 1}, we effectively have indexes on {"a": 1}, {"a": 1, "b" : 1}, {"a": 1, "b": 1, "c": 1}, and so on.

### How `$` operators use indexes

#### Inefficient operators

- In general, negation is inefficient.
  - `"$ne"` has to scan the entire index.

#### Or queries

- Normally, MongoDB will use one of the indexes you created, not both. However, `"$or"` can use one index per "$or" clause, as "$or" performs two queries and then merges the results.

### Indexing objects and arrays

- MongoDB allows you to reach into your documents and create indexes on nested fields and arrays.

#### Indexing embedded docs

- Indexes can be created on keys in embedded documents in the same way that they are created on normal keys.
  - i.e. `db.users.createIndex({"<field>.<subfield>" : 1})`

#### Indexing arrays

- Indexing an array field indexes each element of the array, not the array itself.
- Array indexes are more expensive than single-value ones. For a single insert, update, or remove, every array entry might have to be updated.

#### Multikey index implications

- If any document has an array field for the indexed key, the index immediately is flagged as a multikey index, which may be a bit slower than non-multikey indexes.

#### Index cardinality

- _Cardinality_ is the number of distinct values for a field in a collection.
- In general, the greater the cardinality of a field, the more helpful an index on that field can be.
  - gender := 2, name := N -> name is better.

### GridFS

- A protocol for storing large files
- It uses subcollections to store file metadata separately from content chunks.

### Special index and collection types

### Geospatial Indexes

#### 1. 2d

- It indexes points stored on a 2D plane.
- 2d indexes support both flat geometries and distance-only calculations on spheres.

#### 2. 2dsphere

- It works with spherical geometries that model the surface of the earth based on the `WGS84 datum`.
- It allows you to specify geometries for points, lines, and polygons in the `GeoJSON` format.
- Queries using spherical geometries will be more performant and accurate with a 2dsphere index.
- You can create a geospatial index using the "2dsphere" type with createIndex.
  - i.e. `db.openStreetMap.createIndex({"loc" : "2dsphere"})`

```js
// A point is given by a two-element array, representing `[longitude, latitude]`.
{
  "name" : "New York City",
  "loc" : {
    "type" : "Point",
    "coordinates" : [50, 2]
  }
}

// A line is given by an array of points.
{
  "name" : "Hudson River",
  "loc" : {
    "type" : "LineString",
    "coordinates" : [[0,1], [0,2], [1,2]]
  }
}

// A polygon is given by an array of points, but with a different "type".
{
  "name" : "New England",
  "loc" : {
    "type" : "Polygon",
    "coordinates" : [[0,1], [0,2], [1,2]]
  }
}
```

#### Types of geospatial queries: intersection, within, nearness

```js
var eastVillage = {
  "type" : "Polygon",
  "coordinates" : [
    [
      [ -73.9732566, 40.7187272 ],
      [ -73.9724573, 40.7217745 ],
      [ -73.9732566, 40.7187272 ]
    ]
]}

db.openStreetMap.find({"loc" : {"$geoIntersects" : {"$geometry" : eastVillage}}}) // intersection operator
db.openStreetMap.find({"loc" : {"$geoWithin" : {"$geometry" : eastVillage}}}) // within operator
db.openStreetMap.find({"loc" : {"$near" : {"$geometry" : eastVillage}}}) // nearness operator
```

#### Using geospatial indexes

![geometric_query1](/img/geometric_query1.png)
![geometric_query2](/img/geometric_query2.png)
