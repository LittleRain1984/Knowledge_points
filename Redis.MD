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
