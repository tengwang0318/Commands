# redis 

## Start

run `redis-server` to start the redis server

run `redis-cli` to get the redis command-line interface

```
redis-server --port 6379
```

Because redis might sync the data in memory to hard disks, terminating redis process forcedly might cause the loss of data. You should run the following command:

```
redis-cli SHUTDOWN
```

After that, redis will disconnect the connection and make sure data persistence.

### redis-cli command

```
redis-cli h- 127.0.0.1 p- 6379
```

or just 

```
redis-cli
```

### Multiple Database

Redis, by default, has 16 databases, database's name increments from 0.

If you want to change database, just running the following command:

```
select 1
```



Redis doesn't support user-defined database name and set different passwords for different databases. So the client could visit all of databases.

## Grammar

### Key

#### Get keys which match the special pattern

```
KEYS pattern
```

#### judge whether a key exist or not

```
EXISTS key_name
```

#### delete key

```
DEL key_name
```

#### Get type of key

```
TYPE key_name
```

### String Type

string is the basical data structure.

####  Set and Get

```
SET key val
GET key
```

#### Increment Number

```
INCR key
```

If key doesn't exist, key is set to 0. After INCR, the value of key is 1.

#### Increment the specific number

```
INCRBY key increment
```

#### Increment Specified Float

```
INCRBYFLOAT key increment
```

#### Decrment number

```
DECR key
```

#### Decrement the specific number

```
DECRBY key decrment
```

#### Get the length of string

```
STRLEN key
```

#### Set and Get multiple values at the same time

```
MSET key value key2 value2
MGET key1 key2
```

### Hash Type

#### GET and SET

```
HSET key field value
HGET key field
HMSET key field value [field1, value1...]
HMGET key field [field1...]
HGETALL key
```

the convenience of **HSET** is there is not difference between insertion and update.

#### Judge whether the field exists or not

```
HEXISTS key field
```

#### set a value when the field doesn't exist

```
HSETNX key field value
```

**HSETNX** is similar to **HSET**, the difference is that **HSETNX** will not be executed, if the field exists.

#### Increment a value for the value of field

```
HINCRBY key field increment
```

#### Delete a field

```
HDEL key field, [field1, field2]
```

#### Only get the field name or value

```
HKEYS key
HVALS key
```

#### GET the length of field

```
HLEN key
```

### List Type

#### Add elements from head and tail

```
LPUSH key value, [value,...]
RPUSH key value, [value,...]
```

#### Pop elements from head and tail

```
LPOP key
RPOP key
```

#### Get the length of the list

```
LLEN key
```

#### Get the slice of the list

LRANGE will return the slice of the list, included the start and stop.

```
LRANGE key start stop
```

#### Remove the specified element in the list

```
LREM key count value
```

when $count>0$, the command will delete the first count value from left,

when $count<0$, the command will delete the first count value from right

when count == 0, the command will delete all of value in the list.

#### Get and set the specified index element

```
LINDEX key index
LSET key index value
```

#### Retain the element in the specified range

delete the element which is not in the specified range

```
LTRIM key start end
```

#### insert the element from any position

the command will find the pivot position and insert value before/after the pivot position based on the BEFORE/AFTER parameter.

```
LINSERT key BEFORE/AFTER pivot value
```

### Set type

#### Add or Delete element

```
SADD key value1, value2, ...
SREM key value1, value2, ...
```

#### Get all of element in the set

```
SMEMBERS key
```

#### Judge whether element exists or not

```
SISMEMBER key member
```

#### the operation between different sets

```
SDIFF key1 key2 ...
SINTER key1 key2 ...
SUNION key1 key2 ...
```

#### the number of elements in the set

```
SCARD KEY
```

#### pop an element randomly

```
SPOP key
```

#### sorted set

#### Add Elements

we could also use this command to modify score we have set.

```
ZADD key score member [score member ...]
```

#### Get the score of the element

```
ZSCORE key member
```

#### Get elements whose rank is in the specified range

```
ZRANGE key start stop [WITHSCORES]
ZREVRANGE key start stop [WITHSCORES]
```

#### Get elements whose score is in the specified range

```
ZRANGEBYSCORE key start stop [WITHSCORES] [LIMIT offset count]
```

#### ADD the score of a specified element

```
ZINCRBY key increment member
```

#### Get the number of element in the sorted set

```
ZCARD key
```

#### Get the elements whose score is in the specified range

```
ZCOUNT key min max
```

#### Delete one or more elements

```
ZREM key member [member...]
```

#### Delete elements based on their ranks

```
ZREMRANGEBYRANK key start stop
```

#### Delete elements based on the range of scores

```
ZREMRANGEBYSCORE key min max
```

#### Get the rank of the element 

```
ZRANK key member
ZREVRANK key member 
```







