# MongoDB-Notes

- [Install](#Install-MongoDB)

## Install MongoDB
Add a Path of bin folder into System Property.

## mongod
"mongod" is the "Mongo Daemon" it's basically the host process for the database.

### Running a mongod
```
mongod.exe --config mongod.cfg
```

## mongo
"mongo" is the commmand-line shell that connects to a specific instance of mongod

## Import Data
```
mongoimport.exe --db dbname filename.json
```

## Database Commands

### View all databases
```
show dbs
```

### Create a new or switch databases 
```
use dbName
```

### View current Database
```
db.getName()
```

### Delete Database
```
db.dropDatabase()
```

## Collection Commands

### Show Collections
```
show collections
```

### Create a collection named 'comments'
```
db.createCollection('comments')
```

### Drop a collection named 'comments'
```
db.comments.drop()
```

## Row(Document) Commands

### Show all Rows in a Collection
```
db.comments.find()
```

### Show all Rows in a Collection (Prettified)
```
db.comments.find().pretty()
```

### Find the first row matching the object
```
db.comments.findOne({name: 'Harshid'})
```

### Insert One Row
```
db.comments.insert({
    'name': 'Harshid',
    'lang': 'JavaScript',
    'member_since': 5
 })
 ```
 
 ### Insert many Rows
 ```
 db.comments.insertMany([{
    'name': 'Harshid',
    'lang': 'JavaScript',
    'member_since': 5
    }, 
    {'name': 'Rohit',
    'lang': 'Python',
    'member_since': 3
    },
    {'name': 'Ajay',
    'lang': 'Java',
    'member_since': 4
}])
```

### Sort(asc) the number of rows in the output
```
db.comments.find({}, {"name": 1}).sort({"name": 1})
```

### Limit the number of rows in output
```
db.comments.find().limit(2)
```

### Count the number of rows in the output
```
db.comments.find().count()
```

### Skip the number of rows in the output
```
db.comments.find().skip(2)
```

### Delete Row
```
db.comments.remove({name: 'Harshid'})
```

## Update a row
```
db.comments.update({name: 'Shubham'},
{'name': 'Vivek',
    'lang': 'JavaScript',
    'member_since': 51
}, {upsert: true})
```

### Update a row ( $set )
```
db.comments.updateOne({"name": "Ajay"}, { $set: {"name": "Roshan"} })
```

### Update a row ( $unset )
```
db.comments.updateOne({"name": "Ajay"}, { $unset: {"female": 1} })
```

### Update a row ( $push & $pull )
```
db.commments.updateOne({"name": "Ajay"}, { $push: {"likes": 60} })
```

## Find in a MongoDb Database
```
db.comments.find({lang:'Python'})
```

```
db.comments.find({}, {"name": 1})
```

### Find in a array as value
```
db.comments.find({ "tags" : { $all: ["easy","quick"] } }, {"name": 1} )
```

```
db.comments.find({ "tags" : { $in: ["easy","quick"] } }, {"name": 1} )
```

### Find in a Object as value
```
db.comments.find({ "ingredients.name" : "egg" })
```

## Operators

### Increment Operator
```
db.comments.update({name: 'Rohit'},
{$inc:{
    member_since: 2
}})
```

### Rename Operator
```
db.comments.update({name: 'Rohan'},
{$rename:{
    member_since: 'member'
}})
```

### Less than/Greater than/ Less than or Eq/Greater than or Eq
```
db.comments.find({member_since: {$lt: 90}})
```

```
db.comments.find({member_since: {$lte: 90}})
```

```
db.comments.find({member_since: {$gt: 90}})
```

```
db.comments.find({member_since: {$gte: 90}})
```

### OR operator
```
db.comments.find({$or: [{"name": "Harshid", "member_since": {$lte: 50}}]})
```

## Managing Index 

### Get Index
```
db.comments.getIndexes()
```

### Create Index
```
db.comments.createIndex({"name": 1})
```

### Drop Index
```
db.comments.dropIndex({"name": 1})
```

## Authentication & Authorization

### Create user
```
db.createUser(
  {
    user: "HK",
    pwd: passwordPrompt(),
    roles: [ { role: "userAdminAnyDatabase", db: "admin" }, "readWriteAnyDatabase" ]
  }
);
```

```
db.adminCommand({ shutdown: 1 })
```

### Authentication
```
mongo --authenticationDatabase "admin" -u "HK" -p
```

```
db.auth("HK", passwordPrompt())
```

## Backup

```
mongodump
```

```
mongorestore
```
