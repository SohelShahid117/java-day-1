show dbs
admin    40.00 KiB
config  108.00 KiB
local    40.00 KiB

use practice
switched to db practice

db.createCollection("test")
{ ok: 1 }
db.getCollection("test")
practice.test

db.getCollection.insertOne({name:"next level developer"})
TypeError: db.getCollection.insertOne is not a function

db.getCollection("test").insertOne({name:"next level developer"})
{
  acknowledged: true,
  insertedId: ObjectId('674296eb0ec7054bb7a57fd5')
}
db.getCollection("test").find()
{
  _id: ObjectId('674296eb0ec7054bb7a57fd5'),
  name: 'next level developer'
}
practice

