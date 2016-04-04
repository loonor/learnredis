# redis

## 安装
* Archlinux: sudo pacman -S redis
* 配置文件：/etc/redis.conf
   [配置参数](./redisconfig.md) 
* 启动服务：redis-server #如果没有带当前目录下的redis.conf,将使用/etc/redis.conf配置
* 启动客户：redis-cli
## redis数据类型

五种数据类型：string（字符串）、hash（哈希）、list（列表）、set（集合）
及zset（sorted set：有序集合）

* String

    string是redis最基本的类型，是二进制安全的。可以包含任何数据，
    如jpg图片或者序列化的对象。

    `
127.0.0.1:6379> set name "redis very good"
OK
127.0.0.1:6379> get name
"redis very good"
    `
