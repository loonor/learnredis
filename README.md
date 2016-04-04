# redis

## 安装
* Archlinux: sudo pacman -S redis
* 配置文件：/etc/redis.conf。（  [配置参数](./redisconfig.md) ）
* 启动服务：redis-server #如果没有带当前目录下的redis.conf,将使用/etc/redis.conf配置
* 启动客户：redis-cli

## redis数据类型

五种数据类型：string（字符串）、hash（哈希）、list（列表）、set（集合）
及zset（sorted set：有序集合）

* String

    string是redis最基本的类型，是二进制安全的。可以包含任何数据，
    如jpg图片或者序列化的对象。

        ```sh
        127.0.0.1:6379> set name "redis very good"
        OK
        127.0.0.1:6379> get name
        "redis very good"
        ```

* Hash

    Redis hash是一个键值对集合,是一个string类型的field和value的映射表，适用于存储对象。

        ```sh
        127.0.0.1:6379> HMSET user:1 username Jim password Jimmm points 200
        OK
        127.0.0.1:6379> HGETALL user:1
        1) "username"
        2) "Jim"
        3) "password"
        4) "Jimmm"
        5) "points"
        6) "200"
        ```
* List
    列表是简单的字符串列表，按照插入顺序排列

```sh
        127.0.0.1:6379> lpush redis string
        (integer) 1
        127.0.0.1:6379> lpush redis hash
        (integer) 2
        127.0.0.1:6379> lpush redis list
        (integer) 3
        127.0.0.1:6379> lpush redis set
        (integer) 4
        127.0.0.1:6379> lpush redis zset
        (integer) 5
        127.0.0.1:6379> LRANGE redis 0 3
        1) "zset"
        2) "set"
        3) "list"
        4) "hash"
        127.0.0.1:6379> LRANGE redis 0 4
        1) "zset"
        2) "set"
        3) "list"
        4) "hash"
        5) "string"
```
* Set
    Set是string类型的无序集合;是通过哈希表实现的，
    所以添加、删除、查找的复杂度都是O(1)。
    > sadd命令添加一个string元素到key对应的set集合中，成功返回1
    > 如果元素已经在集合中返回0,key对应的set不存在，返回错误信息。

        ```sh
        127.0.0.1:6379> sadd db redis
        (integer) 1
        127.0.0.1:6379> sadd db mongodb
        (integer) 1
        127.0.0.1:6379> sadd db raditmq
        (integer) 1
        127.0.0.1:6379> sadd db redis
        (integer) 0
        127.0.0.1:6379> sadd db
        (error) ERR wrong number of arguments for 'sadd' command
        127.0.0.1:6379> SMEMBERS db
        1) "raditmq"
        2) "mongodb"
        3) "redis"
        ```

## Redis命令
* 在远程服务上执行命令，语法：$ redis-cli -h host -p port -a password

  ```redis-cli -h 127.0.0.1 -p 6379 -a "服务端密码"```

*
