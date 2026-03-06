# Redis

> webman/redis是在illuminate/redis的基础上添加了连接池功能，支持协程和非协程环境，用法与laravel相同。

## 安装

```bash
composer require -W webman/redis illuminate/events
```

## 配置

config/redis.php

```php
return [
    'default' => [
        'host'     => '127.0.0.1',
        'username' => null,
        'password' => null,
        'port'     => 6379,
        'database' => 0,
        'pool' => [ // 连接池配置
            'max_connections' => 10,     // 连接池最大连接数
            'min_connections' => 1,      // 连接池最小连接数
            'wait_timeout' => 3,         // 从连接池获取连接最大等待时间
            'idle_timeout' => 50,        // 连接池中连接空闲超时时间，超过该时间会被关闭，直到连接数为min_connections
            'heartbeat_interval' => 50,  // 心跳检测间隔，不要大于60秒
        ],
    ],
    'cache' => [ // 多个 Redis 连接
        'host'     => '127.0.0.1',
        'username' => null,
        'password' => null,
        'port' => 6379,
        'database' => 1,
        'prefix' => 'webman_cache-',
    ]
];
```

## 示例

```php
namespace app\controller;

use support\Request;
use support\Redis;

class UserController
{
    public function db(Request $request)
    {
        $key = 'test_key';
        Redis::set($key, rand());
        return response(Redis::get($key));
    }
}
```

## 接口

```php
Redis::append($key, $value)
Redis::bitCount($key)
Redis::decr($key, $value)
Redis::decrBy($key, $value)
Redis::get($key)
Redis::getBit($key, $offset)
Redis::getRange($key, $start, $end)
Redis::getSet($key, $value)
Redis::incr($key, $value)
Redis::incrBy($key, $value)
Redis::incrByFloat($key, $value)
Redis::mGet(array $keys)
Redis::getMultiple(array $keys)
Redis::mSet($pairs)
Redis::mSetNx($pairs)
Redis::set($key, $value, $expireResolution = null, $expireTTL = null, $flag = null)
Redis::setBit($key, $offset, $value)
Redis::setEx($key, $ttl, $value)
Redis::pSetEx($key, $ttl, $value)
Redis::setNx($key, $value)
Redis::setRange($key, $offset, $value)
Redis::strLen($key)
Redis::del(...$keys)
Redis::exists(...$keys)
Redis::expire($key, $ttl)
Redis::expireAt($key, $timestamp)
Redis::select($dbIndex)
```
等价于
```php
$redis = Redis::connection('default');
$redis->append($key, $value)
$redis->bitCount($key)
$redis->decr($key, $value)
$redis->decrBy($key, $value)
$redis->get($key)
$redis->getBit($key, $offset)
...
```