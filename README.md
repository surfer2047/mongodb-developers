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
