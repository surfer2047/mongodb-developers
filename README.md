mongodb-developers
==================

M101P: MongoDB for Developers


Chapter 2: CRUD
==============
Counting Results
---------------
**How would you count the documents in the scores collection where the type was "essay" and the score was greater than 90**

```ruby
db.scores.count({type:"essay", score:{$gt:90}})
```
Wholesale Updating of a Document
-------------------------------

**Quiz: Wholesale Updating of a Document
Let's say you had a collection with the following document in it:
{ "_id" : "Texas", "population" : 2500000, "land_locked" : 1 }
and you issued the query**

```ruby
db.foo.update({_id:"Texas"},{population:30000000})
What would be the state of the collection after the update?

{ "_id" : "Texas", "population" : 2500000, "land_locked" : 1 }
{ "_id" : "Texas", "population" : 3000000, "land_locked" : 1 }
{ "_id" : "Texas", "population" : 30000000 } (Answer)
{ "_id" : ObjectId("507b7c601eb13126c9e3dcca"), "population" : 2500000 }
```

using $set Command
-------------------
**Quiz: Using the $set Command**

For the users collection, the documents are of the form
{
	"_id" : "myrnarackham",
	"phone" : "301-512-7434",
	"country" : "US"
}
Please set myrnarackham's country code to "RU" but leave the rest of the document (and the rest of the collection) unchanged. 

Hint: You should not need to pass the "phone" field to the update query. 

This is a fully functional web shell, so please press enter for your query to get passed to the server, just like you would for the command line shell.

```ruby
db.users.update({phone:'301-512-7434', {$set:{{country:'RU'}})
```
