# MongoDB

## CRUD

### Query:

```
db.collection.find(<query filter>, <projection>)
```

for example:

find customers whose name is teng

```
db.customers.find({"name":"teng"})
```

#### Comparable operator

$lt represents **less than**.

$gt represents **greater than**.

$lte represents **less than or equal to**.

```
db.customers.find({"paid_amount":{$lte:2000}})
```

$in represents the value corresponding to the key includes a range of value.

```
db.customers.find({"paid_amount":{$in:[1000,2000]}})
```

$nin represents not \$in.



#### Logical operators

```
{$operate:[{<expression1>}, {<expression2>},...,{expressionn}]}
```

$or     \$and follow this pattern, \$not follows the following pattern:

```
{field: {$not: {<operator-expression}}}
db.customers.find({"paid_amount":{$not{$gte:3000}}})
```



#### the existence of the attribute

```
{field: {$exists:<boolean>}}
db.customers.find({"paid_amount":{$exists:true,$gte:3000}})
```



#### text query

```
db.collection.find(
{$text:
{
	$search:<string>	
}
}
)
```

```
db.profiles.find({$text:{$search:"teng"}})
```

#### regEx

```
{<filed>: {$regex:/pattern/}}
db.profile.find({name:{$regex: /*teng*/}})
```

#### Nested Document Query

```
db.customers.find({"orders.count":{$gt:150}})
```

#### Array Query

##### Exactly Matching

```
db.GoodsAttribute.find({"AttributeValue":["Small","Large","Medium"]})
```



##### Matching any value

```
db.GoodsAttribute.find({"AttributeValue":"Large"})
```

Matching the Specified position element

```
db.GoodsAttribute.find({"AttributeValue.0":"Large"}")
```



#### Projection and Sorting

##### Projection

the first {} represents the condition of query

the second {} represents the projection of fields, 1 means show, 0 means hidden.

```
db.customers.find({"detail.1.post":5},{_id:0,id:1,name:1})
```

##### Sorting

```
db.customers.find({}).sort({id:-1})
```

##### query jump

Sort firstly, skip 10 documents and find the following 5 documents.

```
db.customers.find({}).skip(10).limit(5).sort({id:-1})
```

### Insert

#### Insert one

```
db.customers.insertOne({})
```

#### Insert Many

```
db.customers.insertMany([{},{}])
```

#### Insert

```
db.customers.insert()
```

### Update

#### updateOne

```
db.collection.updateOne(<filter>, <update>)
```

matching a field and modify it.

```
db.GoodsAttribute.updateOne({"_id":1},{$set:{"AttributeName":"size"}})
```

Set **upsert**, if it could not match any documents, just insert it.

```
db.GoodsAttribute.updateOne({"_id":1},{$set:{"AttributeName":"size"}},{upsert:true})
```

Setting **arrayFilters** to modify one or more element in the array

firstly find any element in price is greater than and equal to 9, set every element which satisfy the condition 11 and filter any every element which doesn't meet condition.

To sum up, set the element which greater than or equal to 6 to 11.

```
db.GoodsAttribute.updateOne({"price":{$gte:9}}, {$set:{"price.$[element]":11}},{arrayFilters:[{'element':{$gte:6}}]})
```

#### UpdateMany

**UpdateMany** has the same grammar pattern like **UpdateOne**. The difference is this command will modify all of matching documents.

##### $unset represents delete document element



```
db.customers.updateMany({"cust_id":125},{$unset:{"name":""}})
```

##### $rename represents renaming document element

```
db.customers.updateMany({},{$rename:{"name":{cust_name}}})
```

##### $mul represents multiply the element by  a number

If the element doesn't exist, inserting a new element and set it 0.

```
db.customers.updateMany({"_id":3},{$mul:{"paid_amout":0.8}})
```

##### $min  \$max

```
db.customers.updateMany({"_id":2},{$min:{"paid_amout:900"}})
```



#### replaceOne

```
db.collection.replaceOne(<filter>, <replacement>)
```

#### Update

update is the combination of updateOne, updateMany and replaceOne.

### Delete

#### deleteOne

```
db.collection.deleteOne(<filter>)
```

#### deleteMany

```
db.collection.deleteMany(<filter>)
```





