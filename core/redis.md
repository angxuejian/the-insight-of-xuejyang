# Redis


## Install

```bash
sudo apt update
sudo apt install redis-server
```

<details>
    <summary>Example</summary>

```bash
# /etc/redis/redis.conf

bind 127.0.0.1

requirepass x123456

rename-command FLUSHALL ""
rename-command FLUSHDB ""
rename-command CONFIG ""
rename-command SHUTDOWN ""
rename-command KEYS ""

# redis://:x123456@localhost:6379/0 

# r = redis.Redis(
#    host='localhost'|
#    port=6379|
#    password='x123456'|
#    decode_responses=True
# )
```
    

</details>

## Commands

### Redis CLI
| 命令                                      | 作用说明                 |
| --------------------------------------- | -------------------- |
| sudo systemctl start redis-server       | 启动 Redis 服务（systemd） |
| sudo systemctl stop redis-server        | 停止 Redis 服务          |
| sudo systemctl restart redis-server     | 重启 Redis 服务          |
| sudo systemctl status redis-server      | 查看 Redis 服务状态        |
| sudo systemctl enable redis-server      | 开机自启 Redis           |
| sudo systemctl disable redis-server     | 关闭开机自启               |
| redis-benchmark                         | Redis 性能测试           |
| redis-cli                               | 进入 Redis 命令行         |
| redis-cli ping                          | 测试 Redis 是否运行        |
| redis-cli shutdown                      | 关闭 Redis 服务          |
| redis-cli -h localhost -p 6379          | 指定地址连接 Redis         |
| redis-cli -a password                   | 使用密码连接 Redis         |
| redis-cli info                          | 查看 Redis 信息          |
| redis-cli info memory                   | 查看 Redis 内存信息        |
| redis-cli info clients                  | 查看客户端信息              |
| redis-cli config get requirepass        | 查看 Redis 密码配置        |
| redis-cli config set requirepass 123456 | 设置 Redis 密码          |
| redis-cli auth 123456                   | Redis 登录认证           |
| redis-cli select 0                      | 切换数据库                |
| redis-cli flushdb                       | 清空当前数据库              |
| redis-cli flushall                      | 清空所有数据库              |
| redis-cli dbsize                        | 查看 key 数量            |
| redis-cli keys "*"                      | 查看所有 key             |
| redis-cli scan 0                        | 分页扫描 key             |
| redis-cli del key                       | 删除 key               |
| redis-cli expire key 60                 | 设置 key 过期时间          |
| redis-cli ttl key                       | 查看 key 剩余时间          |
| redis-cli set name xuej                 | 设置字符串                |
| redis-cli get name                      | 获取字符串                |
| redis-cli hset user name xuej           | 设置 Hash              |
| redis-cli hget user name                | 获取 Hash 字段           |
| redis-cli lpush tasks a b c             | List 左插入             |
| redis-cli lrange tasks 0 -1             | 获取 List              |
| redis-cli sadd tags python fastapi      | Set 添加元素             |
| redis-cli smembers tags                 | 获取 Set 全部元素          |
| redis-cli zadd rank 100 tom             | 添加有序集合               |
| redis-cli zrevrange rank 0 9 withscores | 获取排行榜                |
| redis-cli publish chat "hello"          | 发布消息                 |
| redis-cli subscribe chat                | 订阅频道                 |


## Python redis

``` bash
pip install redis
```

| 方法                                           | 作用说明         |
| -------------------------------------------- | ------------ |
| redis.set(key, value)                  | 设置字符串        |
| redis.get(key)                         | 获取字符串        |
| redis.mset(mapping)                    | 批量设置         |
| redis.mget(keys)                       | 批量获取         |
| redis.setex(key, time, value)          | 设置值并指定过期时间   |
| redis.psetex(key, milliseconds, value) | 设置毫秒级过期时间    |
| redis.getset(key, value)               | 设置新值并返回旧值    |
| redis.append(key, value)               | 追加字符串        |
| redis.strlen(key)                      | 获取字符串长度      |
| redis.incr(key)                        | 自增 1         |
| redis.incrby(key, amount)              | 指定数值自增       |
| redis.decr(key)                        | 自减 1         |
| redis.exists(key)                      | 判断 key 是否存在  |
| redis.delete(key)                      | 删除 key       |
| redis.unlink(key)                      | 异步删除 key     |
| redis.expire(key, seconds)             | 设置过期时间       |
| redis.pexpire(key, milliseconds)       | 设置毫秒过期时间     |
| redis.ttl(key)                         | 查看剩余过期时间     |
| redis.pttl(key)                        | 查看毫秒剩余时间     |
| redis.persist(key)                     | 移除过期时间       |
| redis.rename(old, new)                 | 重命名 key      |
| redis.type(key)                        | 查看 key 类型    |
| redis.keys(pattern="*")                | 获取所有匹配 key   |
| redis.scan(cursor=0)                   | 分页扫描 key     |
| redis.hset(name, key, value)           | 设置 hash 字段   |
| redis.hget(name, key)                  | 获取 hash 字段   |
| redis.hmset(name, mapping)             | 批量设置 hash    |
| redis.hmget(name, keys)                | 批量获取 hash    |
| redis.hgetall(name)                    | 获取整个 hash    |
| redis.hdel(name, *keys)                | 删除 hash 字段   |
| redis.hexists(name, key)               | 判断字段是否存在     |
| redis.hkeys(name)                      | 获取所有字段       |
| redis.hvals(name)                      | 获取所有值        |
| redis.hlen(name)                       | 获取 hash 长度   |
| redis.lpush(name, *values)             | 左侧插入 list    |
| redis.rpush(name, *values)             | 右侧插入 list    |
| redis.lpop(name)                       | 左侧弹出         |
| redis.rpop(name)                       | 右侧弹出         |
| redis.lrange(name, start, end)         | 获取 list 区间数据 |
| redis.llen(name)                       | 获取 list 长度   |
| redis.sadd(name, *values)              | 添加 set 元素    |
| redis.smembers(name)                   | 获取所有 set 元素  |
| redis.srem(name, *values)              | 删除 set 元素    |
| redis.scard(name)                      | 获取 set 数量    |
| redis.sismember(name, value)           | 判断元素是否存在     |
| redis.zadd(name, mapping)              | 添加有序集合元素     |
| redis.zrange(name, start, end)         | 获取有序集合       |
| redis.zrevrange(name, start, end)      | 倒序获取有序集合     |
| redis.zrem(name, *values)              | 删除有序集合元素     |
| redis.zscore(name, value)              | 获取分数         |
| redis.zcard(name)                      | 获取有序集合数量     |
| redis.publish(channel, message)        | 发布消息         |
| redis.subscribe(channel)               | 订阅频道         |
| redis.ping()                           | 测试连接         |
| redis.close()                          | 关闭连接         |
| redis.flushdb()                        | 清空当前数据库      |
| redis.flushall()                       | 清空所有数据库      |
| redis.dbsize()                         | 查看 key 数量    |
| redis.info()                           | 查看 Redis 信息  |
| redis.info("memory")                   | 查看内存信息       |
| redis.client_list()                    | 查看客户端列表      |
| redis.config_get("*")                  | 获取配置         |
| redis.config_set(key, value)           | 修改配置         |