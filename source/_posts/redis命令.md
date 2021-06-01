---
title: redis命令
tags: redis
categories: 数据库
abbrlink: 26704
date: 2019-04-20 16:10:55
---

#### redis常用命令
<!--more-->
1. redis键
    1. del key //删除key
    2. dump key //序列化给定key，并返回被序列化的值
    3. exists key //检查key是否存在
    4. expire key seconds/timestamp  //设置过期时间，以秒/Unix时间戳计
    5. keys pattern   //查找所有符合给定模式的key
    6. move key DB   //将当前数据库的key移动到给定的数据库db当中
    7. persist key   //移除key的过期时间，key将持久保持
    8. rename key newkey   //修改key的名称


2. 字符串
    1. set key value    //设置指定key的值
    2. get key       //获取指定key的值
    3. getrance key start end    //返回key中字符串值的子字符
    4. getset key value   //将给定的值设为value，并返回key的旧值
    5. getbit key offset  //对key所储存的字符串值，获取指定偏移量上的位
    6. mget key1 //获取所有给定的值
    7. strlen key    //返回key所储存的字符串值的长度
    8. mset key value   //同时设置一个或多个key-value对
    9. append key value  //如果 key 已经存在并且是一个字符串， APPEND 命令将指定的 value 追加到该 key 原来值（value）的末尾。

3. 哈希 Redis hash 是一个string类型的field和value的映射表，hash特别适合用于存储对象。

    1. hmset key value    //创建一个哈希表
    2. hdel key field1 [field2]  //删除一个或多个哈希表字段
    3. hexists key field   //查看哈希表中指定的字段是否存在
    4. hget key field   //获取在哈希表中指定key的所有字段和值
    5. hincrby key field increment  //为key中的指定字段的整数值加上增量increment
    6. hkeys key   //获取所有哈希表中的字段
    7. hlen key    //获取哈希表中字段的数量
    8. hvals key   //获取哈希表中所有值
    9. hset key field value  //将哈希表中的字段field的值设为value


4. 列表 ：是简单的字符串列表，按照插入顺序排序，你可以添加一个元素到列表的头部或者尾部
    1. lpush key value   //将value值插入key列表中
    2. blpop key1 timeout   //移出并获取列表的第一个元素， 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止。
    3.BRPOP key1 timeout   //移出并获取列表的最后一个元素， 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止。
    4. lindex key index    //通过索引获取列表中的元素
    5. linsert key before|after pivot value  //在列表的元素前或后插入元素
    6. llen key   //获取列表长度
    7. lpop key   //移出并获取列表的第一个元素
    8. lpush key value //将一个值插入到已存在的列表头部
    9. lrem key count value   //移除列表元素
    10. rpushx key value  //为已存在的列表添加值

5. 集合：Redis 的 Set 是 String 类型的无序集合。集合成员是唯一的，这就意味着集合中不能出现重复的数据。
Redis 中集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是 O(1)。

    1. sadd key member1 //向集合添加一个或多个成员
    2. scard key    //获取集合的成员数
    3. sdiff key1   //返回给定所有集合的差集
    4. sinter key1  //返回给定所有的交集
    5. sismember key member  //判断member元素是否是集合key的成员
    6. spop key     //移除并返回集合中的一个随机元素











