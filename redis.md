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