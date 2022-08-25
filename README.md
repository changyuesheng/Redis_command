# Simple Redis Tutorial
## Redis 指令
### 1. 基本指令
#### 1.1 基本数据库指令
|数据库基本指令|含义|
|-|:-------:|
|select + database_um|指定数据库|
|dbsize|返回数据库键值对数量|
|flushdb|清空当前数据库|
|flushall|清空所有数据库|
|svae|将数据保存到磁盘|
|bgsave|将数据异步保存到磁盘（每两秒保存一次）|
|lastsave|返回最后一次保存的UNIX时间|
#### 1.2 通用数据库操作
|通用指令|含义|
|-|:-------:|
|keys * 或者 keys k*|返回数据库里面所有key或者返回以k开头的所有key|
|exists k1 k2 ...| 查询是否存在k1或者k2，返回查询的key列表中，key存在的数量|
|type key|查询key的value的类型|key不存在返回none|
|del k1 k2 ...|删除指定的key，返回操作成功数目|
|rename k1 k2|重新命名k1，若k2存在，则k2被覆盖|
|renamenx k1 k2|k2 不存在时重命名k1|
|move k1 database_num|将指定的key移动到指定数据库|
|copy k1 k2|将k1的值拷贝给k2|
### 2. string操作指令
#### 2.1 基本操作
|string指令|含义|
|-|:-------:|
|set key value|设置/修改一个键值对|
|get key|查询指定key的value，不存在则返回nil|
|mset k1 v1 k2 v2 ....|添加修改多个键值对|
|mget k1 k2...|获取多个key的value|
|append key value|在key的值后连接参数的value|
|strlen key|查看字符串的长度|
|getrange key startindex endindex|获取key的value指定区间，若为负数，则表示倒数|
|set key value nx|当且仅当key不存在时，设置新的键值对，否则返回nil|
|set key value xx|且仅当key存在时，修改键值对，否则返回nil|
|getset key value|返回key的value，并修改其为新的value，若不存在返回nil|
#### 2.2 value为数值的操作
|string指令|含义|
|-|:-------:|
|incr key|创建value为1的键值对，或者给已经存在的键值对的value加一|
|incrby key 整数|给key的value增加指定数值|
|incrbyfloat key 小数|给key的value增加指定数值|
|decr key|使得key对应的value减一|
|decrby key 整数|给key的value减少指定数值|
#### 2.3 临时键值对
|string指令|含义|
|-|:-------:|
|expire key 秒数|给键值对设置一个存在时间|
|ttl key|查看键值对剩余存在时间|
|pexpire key 毫秒数|给键值对设置一个存在时间|
|pttl key|毫秒版的ttl|
|persist key|取消键值对的生存时间限制|
|setex key 秒数 value|设置键值对和注销时间|
|psetex key 毫秒数 value|设置键值对和注销时间|
### 3. 散列表Hash
#### 3.1 基本操作
|hash指令|含义|
|-|:-------:|
|hset key field1 v1 filed2 v2 field3 v3...|添加/修改一个键与一至多对字段和值|
|hget key field|按照key和field获取value|
|hmegt key field1 field2...|获取同一个key对应的多个field|
|hgetall key|获取key对应的所有field-value值|
|hdel key filed1 filed2...|删除key对应的field|
|hsetnx key field value|当且仅当field不存在时，添加一个field-value键值对|
|hkeys key|获取一个key对应的所有field|
|hvals key|获取一个key下面的所有value|
|hlen key|统计一个key对应多少个键值对|
|hexist key field|查询是否存在某个filed|
|hstrlen key field|查询对应value的长度|
#### 3.2 value是数值
|hash指令|含义|
|-|:-------:|
|hincrby key field 数值|按key和field给value怎加指定数值|
|hincrbyfloat key field 小数值|按key和field给value怎加指定数值|
### 4 列表List
#### 4.1 基本操作
|list指令|含义|
|-|:-------:|
|rpush key v1 v2 ...|在队列右侧加入多个值|
|lpush key v2 v1 ...|在队列左侧加入多个值，注意顺序|
|rpop key number|在队列左边弹出number个数值|
|lpop key number|在队列左侧弹出number个数值|
|rpushx key v1 v2 ...|在队列右侧加入多个值，当且仅当list存在|
|lpushx key v1 v2 ...|在队列左侧加入多个值|
|lset key index value|修改指定位置的值|
|linsert key before/after value value|在指定数据前后插入新数据|
|lindex key index|按照索引查找值|
|lrange key strat end|查询范围内的数据|
|llen key|查看队列长度|
|lrem key count value|从左或者从右删除count数量的value|
|ltrim key start end|修剪list到指定区间|
### 5 集合Set
#### 5.1 基本操作
|set指令|含义|
|-|:-------:|
|sadd key string1 string2...|添加一个至多个成员|
|srem key string1 string2...|删除一个至多个成员|
|scard key|返回key的队列数量|
|smembers key|返回key的所哟成员|
|sismember key string|判断是否存在相应成员|
|smismembers key string1 string2 ...|批量查看是否存在这些成员|
|srandmember key number|随机返回number数量的成员|
|spop key number|随机取出number数量的成员|
|smove k1 k2 string|将指定string从集合1移动到集合2|
|sinter key1 key2|查看两个集合的交集|
|sinterstore newkey key1 key2...|存储交集到指定集合|
|sunion key1 key2...|查看集合的并集|
|sunionstroe newkey key1 key2...|存储并集到指定集合|
|sdiff key1 key2...|查看集合的差集|
|sdiffstroe newkey key1 key2...|存储差集到指定集合|
### 6 有序集合Zset
#### 6.1 基本操作
|zset指令|含义|
|-|:-------:|
|zadd key score1 string1 score2 string2...|添加一到多个成员|
|zrem key string1 string2 ...|删除一到多个成员|
|zcount key minscore maxscore|返回指定区间的成员数量|
|zscore key string|查看成员分数|
|zmscore key string|批量查看成员分数|
|zcard key|查看成员数量|
|zincrby key 分数 string|给指定成员增加分数|
#### 6.2 按区间操作
|zset指令|含义|
|-|:-------:|
|zrange key strat end|查看指定分数区间成员|
|zrangestore newkey key start end|存储指定区间到新的集合|
|zlexcount key startstring endstring|查看指定区间字符串数量|
|zremrangebylex key startstring endstring|删除指定区间字符串|
|zremrangebyscore key minscore maxscore|按照分数删除指定区间字符串|
|zrank key string|查看成员升序排名|
|zrevrank key string|查看成员降序排名|
|zremrangebyrank key minscore maxscore|按照排名删除指定区间字符串|
#### 6.2 交集，并集，差集
|zset指令|含义|
|-|:-------:|
|zinter key_number key1 key2...|查看集合的交集|
|zinterstore newkey key_number key1 key2...|存储集合的交集|
|zunion key_number key1 key2...|查看集合的并集|
|zunionstore newkey key_number key1 key2...|存储集合的并集|
|zdiff key_number key1 key2...|查看集合的差集|
|zdiffstore newkey key_number key1 key2...|存储集合的差集|
### 7 遍历
#### 7.1 遍历整个数据库
|遍历指令|含义|
|-|:-------:|
|scan 游标 match h* type set scount 10|遍历|
#### 7.2 特定键值对的1遍历
|遍历指令|含义|
|-|:-------:|
|hscan key 游标 []match][count]|遍历哈希表|
|sscan key 游标 []match][count]|遍历集合|
|zscan key 游标 []match][count]|遍历有序集合|
### 8 事务
#### 8.1 基本事务
|事务指令|含义|
|-|:-------:|
|multi|开启一个事务
|exec|执行事务
|discard|回滚事务|
#### 8.2 监视
|监视指令|含义|
|-|:-------:|
|watch key1 key2...|开始监视键值对|
|unwatch|停止监视键值对|
















































