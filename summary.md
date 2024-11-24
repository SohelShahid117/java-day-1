//5-2 Insert,insertOne, find, findOne, field filtering, project

1.db.test.insertOne([{name:"aadil"}])--->ctrl+enter dite hobe
2.db.test.insertMany([{name:"aadil"},{name:"shahid"}])
3.findeOne:db.test.findOne({gender:"Female"},{gender:1,name:1,email:1})
4.filed filtering || find:db.test.find({gender:"Female"},{gender:1,name:1,email:1})
5.project use:db.test.find({name:"aadil"}).project({name:1,gender:1})

imp:boro file booster e upload na nile mongoDB te upload dite hobe.findeOne e project use korbona.sei khetre normally use korbo--->db.test.findOne({gender:"Female"},{gender:1,name:1,email:1})


//5-3 $eq, $neq, $gt, $lt, $gte, $lte
1.go to : https://www.mongodb.com/docs/manual/reference/operator/query-comparison/
2.synatx: { <field>: { $eq: <value> } },db.test.find({name:{$eq:"aadil"}})
          { field: { $gt: value } },
          { field: { $gte: value } },db.test.find({age:{$gte:99}})
          { field: { $in: [<value1>, <value2>, ... <valueN> ] } },
          { field: { $lt: value } },
          { field: { $lte: value } },db.test.find({age:{$lte:82}}).sort({age:1});//here sorting in ascending order for given 1.
          //for descending order:db.test.find({age:{$lte:10}}).sort({age:-1});
          { field: { $ne: value } },
          { field: { $nin: [ <value1>, <value2> ... <valueN> ] } }

