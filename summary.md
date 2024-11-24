//5-2 Insert,insertOne, find, findOne, field filtering, project

1.db.test.insertOne([{name:"aadil"}])--->ctrl+enter dite hobe
2.db.test.insertMany([{name:"aadil"},{name:"shahid"}])
3.findeOne:db.test.findOne({gender:"Female"},{gender:1,name:1,email:1})
4.filed filtering || find:db.test.find({gender:"Female"},{gender:1,name:1,email:1})
5.project use:db.test.find({name:"aadil"}).project({name:1,gender:1})

imp:boro file booster e upload na nile mongoDB te upload dite hobe.findeOne e project use korbona.sei khetre normally use korbo--->db.test.findOne({gender:"Female"},{gender:1,name:1,email:1})

