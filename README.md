# MongoDB Cheat Sheet
Here all Basics command of MongoDB Written.

## Show All Databases

```
show dbs
```

## Show Current Database

```
db
```

## Create Or Switch Database

```
use acme
```

## Drop

```
db.dropDatabase()
```

## Create Collection

```
db.createCollection('posts')
```

## Show Collections

```
show collections
```

## Insert Row

```
db.posts.insert({
  title: 'Post One',
  body: 'Body of post one',
  category: 'News',
  gpa: 3.2,
  tags: ['news', 'events'],
  user: {
    name: 'John Doe',
    status: 'author'
  },
  date: Date()
})
```

## Insert Multiple Rows

```
db.posts.insertMany([
  {
    title: 'Post Two',
    body: 'Body of post two',
    category: 'Technology',
    gpa: 5,
    date: Date()
  },
  {
    title: 'Post Three',
    body: 'Body of post three',
    category: 'News',
    gpa: 2.8,
    date: Date()
  },
  {
    title: 'Post Four',
    body: 'Body of post three',
    category: 'Entertainment',
    gpa:4.5,
    date: Date()
  }
])
```

## Get All Rows

```
db.posts.find()
```

## Get All Rows Formatted

```
db.posts.find().pretty()
```

## Find Rows

```
db.posts.find({ category: 'News' })
```

## Sort Rows

```
# asc
db.posts.find().sort({ title: 1 }).pretty()
# desc
db.posts.find().sort({ title: -1 }).pretty()
```

## Count Rows

```
db.posts.find().count()
db.posts.find({ category: 'news' }).count()
```

## Limit Rows

```
db.posts.find().limit(2).pretty()
```

## Chaining

```
db.posts.find().limit(2).sort({ title: 1 }).pretty()
```

## Foreach

```
db.posts.find().forEach(function(doc) {
  print("Blog Post: " + doc.title)
})
```

## Find One Row

```
db.posts.findOne({ category: 'News' })
```

## Find Specific Fields

```
db.posts.find({ title: 'Post One' }, {
  title: 1,
  author: 1
})
```

## Find Specific Fields : Syntax

```
db.posts.find({ Query }, { Projection })
```

## Update Query : Syntax

```
db.posts.update({ Query }, { Update })
```

## Update Row

```
db.posts.update({ title: 'Post Two' },
{
  title: 'Post Two',
  body: 'New body for post 2',
  date: Date()
},
{
  upsert: true
})
```

## Update Specific Field

```
db.posts.update({ title: 'Post Two' },
{
  $set: {
    body: 'Body for post 2',
    category: 'Technology'
  }
})
```

## Update All Row

```
db.posts.update({ },
{
  $set: {
    fullTime: true;
  }
})
```

## Update Specific Field Using Unset

```
db.posts.updateOne({ title: 'Post Two' },
{
  $unset: { category: '' }
})
```

## Update If Not Exists/ Exists

```
db.posts.update({ fullTime:{ $exists:false } },
{
  $set: {
    fullTime:true;
  }
})
```

## Increment Field (\$inc)

```
db.posts.update({ title: 'Post Two' },
{
  $inc: {
    likes: 5
  }
})
```

## Rename Field

```
db.posts.update({ title: 'Post Two' },
{
  $rename: {
    likes: 'views'
  }
})
```

## Delete Row

```
db.posts.remove({ title: 'Post Four' })
```

## Comparison Operators ( $lt, $gt, $gte, $lte )

```
db.posts.find( category:{ $ne:"Technology" } )
```

## Comparison Operators In Range

```
db.posts.find( gpa{ $gte: 3 , $lte: 5 } )
```

## Comparison Operators ($in, $nin)

```
db.posts.find( category: {$in: ["Technology", "News"]} )
```

## Logical Operators ( $and, $or, $nor )

```
db.posts.find( { $and: [ { category:"News" }, { gpa:{$gte:4} } ] } )
```

## Logical Operators

```
db.posts.find({ gpa: { $not:{ $gte:4 } } })
```

## Sub-Documents

```
db.posts.update({ title: 'Post One' },
{
  $set: {
    comments: [
      {
        body: 'Comment One',
        user: 'Mary Williams',
        date: Date()
      },
      {
        body: 'Comment Two',
        user: 'Harry White',
        date: Date()
      }
    ]
  }
})
```

## Find By Element in Array (\$elemMatch)

```
db.posts.find({
  comments: {
     $elemMatch: {
       user: 'Mary Williams'
       }
    }
  }
)
```

## Index 

```
db.posts.find({category: "News"}).explain('executionStats')
```

## Add Index

```
db.posts.createIndex({ title: 1 })
```

## Return All Index

```
db.posts.getIndexes()
```

## Drop the Index

```
db.posts.dropIndex("name_of_index")
```

## Add Index

```
db.posts.createIndex({ title: 'text' })
```

## Text Search

```
db.posts.find({
  $text: {
    $search: "\"Post O\""
    }
})
```

## Some Example

```
db.posts.find({ gpa : { $ gte:5, $ lte:9 }, fullTime : { $ exists: true } }, { _ id:false, title:true, gpa: true } )
db.posts.find({ post : { $ne : "Post Three" }}, { _ id:false, titile:true, gpa:true }).sort({ gpa:-1 }).limit(3)
```

## Complex Example (Not Important)

```
db.posts.find({
 $and: [{fullTime:true}, {gpa : {$ gte : 2}  }],
    $or : [{category : { $ in : ["Technology", "News"] } }, {gpa: { $ gte : 4 }  }]  },{
      _ id:false, title:true, gpa:true
})
```
