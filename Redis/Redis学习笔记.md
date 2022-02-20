# Redis

## 1.什么是 `Redis`数据库

完全开源的`key-value`的高性能数据库

## 2.数据库分为了关系型数据库和非关系行数据库

### 2.1 关系型数据库

>   有 `Oracle`、`MySQL `和 `SQL server`
>
>   是指采用了关系模型来组建数据的数据库，其以行和列的形式来存储数据，以便于用户理解

#### 2.1.2 关系型数据库的优缺点

优点：

-   容易理解，贴近逻辑世界的二维表格模型
-   使用方便，丰富的`SQL`语句操作
-   易于维护，具有完整性，大大降低了数据冗余和数据不一致的概率
-   支持`SQL`，可用于复杂逻辑的查询

缺点：

-   因为完整性带来了巨大的代价就是读写性能较差
-   固定的表结构
-   高并发读写需求慢

### 2.2 非关系型数据库

>   常见的有：`NoSQL `、`Redis `、`MongoDB`

#### 2.2.1：非关系型数据库的优缺点

优点：

-   无需经过`SQL`层的解析，读写性能很高
-   基于键值对，数据没有耦合性，容易扩展
-   `NoSQL`数据库，存储格式是 key-value 形式，文档形式，图片形式等等，而关系型数据库则只支持基础类型
-   处理高并发、大批量数据的能力强

缺点：

-   没有`SQL`支持，学习成本高
-   事务处理能力较弱
-   没有完整性的约束，对于复杂的业务场景支持较差

## 3.Redis操作

### 打开服务

可以通过命令符输入命令 `redis-server.exe`

也可以直径双击打开

### 读写Redis数据库

在不关闭服务的前提下，打开另一个`cmd`窗口 `redis-cli.exe`

读写数据

1.  String类型

    ```
    SET name YTZL 	设置name为YTZL
    GET name 		获取
    ```

    `String`类型是`Redis`最基本的数据类型，而且是二进制的十分安全，`String`类型可以包含任何数据，一个键可以存储`512MB`
    <img src="https://gitee.com/yubaicai/blog-image/raw/master/images/QQ%E5%9B%BE%E7%89%8720211121095230.png" alt="Get操作" style="zoom:50%;" />

1.  Hash 哈希

    ```
    HMSET	对象名	name	zs	pwd	123	--设置
    HGETALL：对象名	
    ```

    HASH是一个键值对集合，特别适用于存储对象<img src="https://gitee.com/yubaicai/blog-image/raw/master/images/QQ%E5%9B%BE%E7%89%8720211121095235.png" alt="Hash操作" style="zoom:50%;" />

1.  List 集合

    ``` 
    ListPush  nameList zhangsan	--设置
    ListPush  nameList lisi	--设置
    Lrange nameList 0 1 获取（下标）
    ```

    List 是字符串列表，按照插入顺序排序

    <img src="https://gitee.com/yubaicai/blog-image/raw/master/images/QQ%E5%9B%BE%E7%89%8720211121095240.png" alt="List设置操作" style="zoom:50%;" /><img src="https://gitee.com/yubaicai/blog-image/raw/master/images/QQ%E5%9B%BE%E7%89%8720211121094806.jpg" alt="Redis中List操作" style="zoom: 50%;" />

1.  Set集合

    ```
    SetADD	nameSet	zhngsan --设置
    SADD	nameSet	lisi	--设置
    smembers	nameSet 	--获取
    ```

    Set是String类型的无序列表，每一个成员都是唯一的，意味这不可能出现重复的数据<img src="https://gitee.com/yubaicai/blog-image/raw/master/images/Set.png" alt="Set" style="zoom:50%;" />

1.  Zset集合

    ```
    ZADD	userSet	1	zhngsan	--设置
    ZADD	userSet 2	lisi	--设置
    ZRANGE	userSet	0 1 		--获取(下标)
    ```

    ZSET集合是String类型的集合，且不允许有重复的成员，不同的是每一个元素都会关联一个`double`类型的分数来进行集合中的成员大小排序，并且分数可以重复<img src="https://gitee.com/yubaicai/blog-image/raw/master/images/Zset%E9%9B%86%E5%90%88%E6%93%8D%E4%BD%9C.png" alt="Zset集合操作" style="zoom:50%;" />

1.  基本命令

    1.  是否存在：`EXISTS	keyName`

        若key存在，则返回1 否则返回0

        ![是否存在命令](https://gitee.com/yubaicai/blog-image/raw/master/images/202111211908758.png)

    1.  删除：`DEL keyName keyName ...`

        返回的是被删除的数量

        ![image-20211121190940638](https://gitee.com/yubaicai/blog-image/raw/master/images/202111211909662.png)

    1.  设置过期时间

        `EXPIRE keyName seconds`

        设置成功返回的是1

    1.  `TTL keyName `

        seconds：返回剩余秒数

        -2	：当前key已过期

        -1	：当前key存在但是没有设置过期时间

    1.  查询过期时间（单位是毫秒）

        `PTTL	keyName`

        seconds：返回剩余秒数

        -2：当前key已过期

        -1：当前key已存在但没有设置过期时间

    1.  获取key的数据类型

        `Type keyName`

        返回值是各大数据类型和`none`

    1.  



