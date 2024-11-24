//5-2 Insert,insertOne, find, findOne, field filtering, project

1.db.test.insertOne([{name:"aadil"}])--->ctrl+enter dite hobe
2.db.test.insertMany([{name:"aadil"},{name:"shahid"}])
3.findeOne:db.test.findOne({gender:"Female"},{gender:1,name:1,email:1})
4.filed filtering || find:db.test.find({gender:"Female"},{gender:1,name:1,email:1})
5.project use:db.test.find({name:"aadil"}).project({name:1,gender:1})

imp:boro file booster e upload na nile mongoDB te upload dite hobe.findeOne e project use korbona.sei khetre normally use korbo--->db.test.findOne({gender:"Female"},{gender:1,name:1,email:1})


//5-3 $eq, $neq, $gt, $lt, $gte, $lte
1.go to : https://www.mongodb.com/docs/manual/reference/operator/query-comparison/
2.synatx: { <field>: { $eq: <value> } },//db.test.find({name:{$eq:"aadil"}})
          { field: { $gt: value } },
          { field: { $gte: value } },//db.test.find({age:{$gte:99}})
          { field: { $in: [<value1>, <value2>, ... <valueN> ] } },
            //db.test.find({age:{$in: [1,3,4,7,9,99]}})
            //db.test.find({age:{$in: [1,3,9,99]}}).sort({ age:-1 })
          { field: { $lt: value } },
          { field: { $lte: value } },
          //db.test.find({age:{$lte:82}}).sort({age:1});//here sorting in ascending order for given 1.
          //for descending order:db.test.find({age:{$lte:10}}).sort({age:-1});
          { field: { $ne: value } },
          { field: { $nin: [ <value1>, <value2> ... <valueN> ] } }

//5-4 $in, $nin, implicit and condition
db.test.find({age:{$in: [1,3,4,7,9,99]}})
db.test.find({age:{$in: [1,3,9,99]}}).sort({ age:-1 })
db.test.find({age:{$nin: [1,3,9,99]}}).sort({ age:-1 })

//implicit and condition
db.test.find({age:{$gte:18,$lte:30}}).project({age:1}).sort({ age:1 })
db.test.find({age:{$gte:18,$lte:30}},{age:1,email:1}).sort({ age:1 })
db.test.find({age:{$gte:18,$lte:30},gender:"Female"},{age:1,email:1,gender:1}).sort({ age:1 })
db.test.find(
    {age:{$gte:18,$lte:30},gender:"Female",interests:{$in: ["Cooking","Gardening","Travelling"]}},
    {age:1,email:1,gender:1,interests:1}).sort({ age:1 })


//5-5 $and, $or, implicit vs explicit
//implicit and
db.test.find({age:{$ne:15,$lt:20}},{age:1,gender:"Male"}).sort({ age:1 })
db.test.find({age:{$ne:15,$lt:20}},{age:1,gender:"Male"}).sort({ age:-1 })

//explicit and:https://www.mongodb.com/docs/manual/reference/operator/query-logical/
//syntax:
{ $and: [ { <expression1> }, { <expression2> } , ... , { <expressionN> } ] }
{ $or: [ { <expression1> }, { <expression2> }, ... , { <expressionN> } ] }
{ field: { $not: { <operator-expression> } } }
{ $nor: [ { <expression1> }, { <expression2> }, ...  { <expressionN> } ] }

db.test.find({
    $and: [
    {age:{$lte:15}},
    {gender:"Male"},
    {age:{$in:[2,4,8,10]}}
    ]}).project({age:1,gender:1}).sort({age:1})

db.test.find({
    $or: [
    {age:{$lte:15}},
    {gender:"Male"},
    {age:{$in:[2,4,8,10]}}
    ]}).project({age:1,gender:1}).sort({age:1})


db.test.find({
    $or: [
    {age:{$lte:25}},
    // {gender:"Male"},
    // {age:{$in:[2,4,8,10]}},
    // {"skills.name":{$eq:"JAVA"}}--->object in array
    {"address.street":{$eq:"1188 Lerdahl Point"}}--->object
    ]})
    // .project({age:1,gender:1,skills:1}).sort({age:1})


//5-6 $exists, $type,$size
go to : https://www.mongodb.com/docs/manual/reference/operator/query-element/
https://www.mongodb.com/docs/manual/reference/operator/query/size/

//syntax:
{ field: { $exists: <boolean> } },
{ field: { $type: <BSON type> } }
{ field: { $size: number } }; //size apply hobe only arrayr khetre
//db.test.find({friends:{$size: 4}})
//db.test.find({friends:{$size: 0}})

//db.test.find({salary:{$type: "string"}})
//db.test.find({salary:{$type: "number"}})

db.test.find({age:{$exists:false}})
//j data golote age filed nai seigolo dekabe 

db.test.find({age:{$exists:true}})
//age filed ase segolo show korbe

//db.collection.find( { field: { $size: 2 } } );


//5-7 $all , $elemMatch
go to : https://www.mongodb.com/docs/manual/reference/operator/query/all/
//syntax:

//aita arrayr khetre
{ <field>: { $all: [ <value1> , <value2> ... ] } }
is equivalent to: { $and: [ { tags: "ssl" }, { tags: "security" } ] }
//db.test.find({interests:{$all:["Travelling","Gaming","Reading"]}}).project({interests:1})

//db.test.find({$and: [{interests:"Gaming"}]})
//db.test.find({$and: [{interests:"Travelling"},{interests:"Gaming"},{interests:"Reading"}]})
//db.test.find({$and: [{"skills.name":"JAVA"},{"skills.level":"Expert"},{"skills.isLearning":true}]})

//aita object er khetre
{ <field>: { $elemMatch: { <query1>, <query2>, ... } } }
db.test.find({skills:{$elemMatch: {name:"JAVA",level:"Expert"}}}).project({skills:1})
