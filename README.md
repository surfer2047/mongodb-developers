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
Using the $unset Command
-----------------------
**Quiz: Using the $unset Command**

Write an update query that will remove the "interests" field in the following document in the users collection.
{ 
    "_id" : "jimmy" , 
    "favorite_color" : "blue" , 
    "interests" : [ "debating" , "politics" ] 
}
Do not simply empty the array. Remove the key : value pair from the document. 

This is a fully functional web shell, so please press enter for your query to get passed to the server, just like you would for the command line shell

```ruby
db.users.update({_id='jimmy'}, {$unset:{interests:1}})
```

Using $push, $pop, $pull, $pushAll, $pullAll, $addToSet Commands
----------------------------------------------------------------

first writing the documents consistring of array, 
```ruby
db.array.insert({_id:0, a:[1,2,3,4,5]})
```
In the above Examples to update the third value of array a , just we will use the update commands with $set
```ruby
db.array.update({id:0,},{$set:{a.2:3}})
``` 
This command will update the value of a=2 to a=3

To add elements to array, we can simply use push command
like It will add the array element at last 
```ruby
db.array.update({_id:0},{$push:{a:6}})
```
To remove the last element of array, we can use *pop* keyword
like
```ruby
db.array.update({_id:0},{$pop:{a:1}})
```

To remove the First element of array, just use the *pop* with value -1

**The $pop:1 will remove the last element of array while $pop:-1 will remove the first element of array**

**$pushall operator**
push all operator add all the specified element at the last of the array
```ruby
db.array.update({_id:0},{$pushall:{a:[1,2,3]}})
```

$pullAll operator: It will remove all the specified element from the array

```ruby
db.array.update({_id:0},{$pullAll:{a:[1,2,3]}})
```

**$addToSet operator**
addToSet operator will only add the non occurance elements on the array, if the element exists on the array, it will do nothing
```ruby
db.array.update({_id:0},{$addToSet:{a:5}})
```
If the element 5 exist in array 'a' it will do nothing else it will add the element 5 onto the array

**Quiz: Using $push, $pop, $pull, $pushAll, $pullAll, $addToSet**


Suppose you have the following document in your friends collection:
```ruby
{ _id : "Mike", interests : [ "chess", "botany" ] }
```

What will the result of the following updates be?
```ruby
db.friends.update( { _id : "Mike" }, { $push : { interests : "skydiving" } } );
db.friends.update( { _id : "Mike" }, { $pop : { interests : -1 } } );
db.friends.update( { _id : "Mike" }, { $addToSet : { interests : "skydiving" } } );
db.friends.update( { _id : "Mike" }, { $pushAll: { interests : [ "skydiving" , "skiing" ] } } );
```
**ANS**:
````ruby
{ _id : "Mike" , "interests" : [ "botany", "skydiving", "skydiving", "skiing" ] 

Upserts
--------
This Operator will update the Documents even, if there is no documents
for instace
```ruby
db.people.update({name:"Manoj"}, {$set:{age:40}}, {upsert:true})
```
