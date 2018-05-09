# Redis

- Redis Data Types
	- String
	- Hash
	- List
	- Set
	- zset: 按照分数(double类型)排序

	
- Redis Commands
	- redis-cli
	- PING
	- redis-cli -h host -p port -a password

	
- Redis Publish/Subscribe
	- 如果Redis Subscribe客户端断线, 那么这个期间的消息会丢失
	- 如果订阅channel上的消息挤压过多的话,会消耗大量内存, 从而影响Redis本身甚至操作系统,所以设置client-output-buffer-limit 选项

- Redis 事务
	- Redis的事务不同于数据库事务,只是一个批量执行过程, 事务中的任何一条命令执行失败都不会影响事务中其他命令的执行
	- 如果执行一个事物
		- 开始事务
		- 命令入队
		- 执行事务

- Redis脚本

- Redis Connection
	- CONFIG SET protected-mode no才能允许远程连接
	- 远程连接 redis-cli -h hostname
	
- Redis Benchmark
	- command: redis-benchmark -n 10000 -q

	
- Redis 客户端
	- Java: Jedis
	- code example:

```Java
import redis.clients.jedis.Jedis;
 
public class RedisStringJava {
		  public static void main(String[] args) {
        //连接本地的 Redis 服务
        Jedis jedis = new Jedis("localhost");
        System.out.println("连接成功");
        //设置 redis 字符串数据
        jedis.set("runoobkey", "www.runoob.com");
        // 获取存储的数据并输出
        System.out.println("redis 存储的字符串为: "+ jedis.get("runoobkey"));
    }
}
```

- Redis 事物
	- watch: 监视一个(或多个) key ，如果在事务执行之前这个(或这些) key 被其他命令所改动，那么事务将被打断。
	- multi:标记一个事务块的开始。事务块内的多条命令会按照先后顺序被放进一个队列当中，最后由 EXEC 命令原子性(atomic)地执行。


- Redis 优势	
	- 内存存储 速度快
	- 支持数据类型丰富: string，list，set，sorted set，hash
	- 按KEY设置过期时间

- Redis 为什么使用单线程
	- 单线程避免了线程切换和竞态产生的消耗

- 3. redis常见性能问题和解决方案：

	- (1) Master最好不要做任何持久化工作，如RDB内存快照和AOF日志文件

	- (2) 如果数据比较重要，某个Slave开启AOF备份数据，策略设置为每秒同步一次

	- (3) 为了主从复制的速度和连接的稳定性，Master和Slave最好在同一个局域网内

	- (4) 尽量避免在压力很大的主库上增加从库

	- (5) 主从复制不要用图状结构，用单向链表结构更为稳定，即：Master <- Slave1 <- Slave2 <- Slave3...

这样的结构方便解决单点故障问题，实现Slave对Master的替换。如果Master挂了，可以立刻启用Slave1做Master，其他不变。

- oTMS Redis 使用情况
	- 多少台?
