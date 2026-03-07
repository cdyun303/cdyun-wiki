# 缓存Cache扩展

> 基于TP Cache 的封装，本缓存只支持redis和file驱动。

## 安装

```bash
composer require cdyun/thinkphp-cache
```

## 特性

- ✅ 增加了全局默认参数配置（默认全局标签、默认过期时间）
- ✅ 保留默认file缓存驱动接口，同时增加了单独的redis缓存接口

## 示例

```php
use Cdyun\ThinkphpCache\CacheEnforcer;

file方法：set、get、delete、clear、has、handler
redis方法：setRedis、getRedis、delRedis、clearRedis、hasRedis、redisHandler
```

- ✅ set() / setRedis() 设置缓存项，支持自定义过期时间和标签名
- ✅ get() / getRedis() 获取缓存值，为空时支持set赋值
- ✅ delete() / delRedis() 删除缓存值
- ✅ clear() / clearRedis() 清空缓存，支持按标签清除
- ✅ has() / hasRedis() 判断缓存是否存在
- ✅ handler() / redisHandler() 缓存实例

## 相关链接

- [Packagist 仓库](https://packagist.org/packages/cdyun/thinkphp-cache)
- [GitHub 仓库](https://github.com/cdyun303/thinkphp-cache)
- [问题反馈](https://github.com/cdyun303/thinkphp-cache/issues)

# 版本要求

- php: ^8.1

# 许可证

MIT License