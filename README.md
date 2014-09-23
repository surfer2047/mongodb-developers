mongodb-developers
==================

M101P: MongoDB for Developers


Chapter 2: CRUD
==============
Counting Results
---------------
How would you count the documents in the scores collection where the type was "essay" and the score was greater than 90?

```mongodb
db.scores.count({type:"essay", score:{$gt:90}})
```
Wholesale Updating of a Document
-------------------------------

Quiz: Wholesale Updating of a Document
```ruby
Let's say you had a collection with the following document in it:
{ "_id" : "Texas", "population" : 2500000, "land_locked" : 1 }
and you issued the query:
db.foo.update({_id:"Texas"},{population:30000000})
What would be the state of the collection after the update?

{ "_id" : "Texas", "population" : 2500000, "land_locked" : 1 }
{ "_id" : "Texas", "population" : 3000000, "land_locked" : 1 }
{ "_id" : "Texas", "population" : 30000000 } (Answer)
{ "_id" : ObjectId("507b7c601eb13126c9e3dcca"), "population" : 2500000 }
```

