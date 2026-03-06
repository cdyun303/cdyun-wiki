# IP地址处理

> 提供IP地址相关的处理方法，支持IP验证、转换、归属地查询等功能。

## 特性
- ✅ 获取IP地址版本
- ✅ 验证IP地址格式
- ✅ 获取IP地址位置信息

## 核心方法
| 方法名 | 功能描述 | 调用示例                                                  |
|--------|----------|-------------------------------------------------------|
| [`getLocation()`](#getlocation-获取ip地址位置信息) | 获取IP地址位置信息 | `Ip::getLocation(192.168.10.88)` |
| [`isValid()`](#isvalid-验证ip地址格式是否有效) | 验证IP地址格式 | `Ip::isValid(192.168.10.88)`                           |
| [`isPrivate()`](#isprivate-检查ip地址是否为私有内部地址) | 检查IP地址是否为私有/内部地址 | `Ip::isPrivate(192.168.10.88)`  |
| [`getVersion()`](#getversion-获取ip地址版本) | 获取IP地址版本 | `Ip::getVersion(192.168.10.88)` |

## 使用示例

### getRealIp() - 获取真实客户端IP地址
```php
$ip = Ip::getRealIp();
```

### isValid() - 验证IP地址格式是否有效
```php
$valid = Ip::isValid('192.168.1.1'); // true
```

### isPrivate() - 检查IP地址是否为私有/内部地址
```php
$private = Ip::isPrivate('192.168.1.1'); // true
```

### getVersion() - 获取IP地址版本
```php
$ip = Ip::isPrivate();
```

### toLong() - 将IP地址转换为长整数
```php
$long = Ip::toLong('192.168.1.1'); // 3232235777
```

### fromLong() - 将长整数转换为IP地址
```php
$ipStr = Ip::toString(3232235777); // '192.168.1.1'
```

### getLocation() - 获取IP地址位置信息
```php
$local = Ip::getLocation('192.168.1.1');
```

### isFromCountry() - 检查IP地址是否来自特定国家
```php
$ip = Ip::isFromCountry('192.168.1.1', 'CN');
```

### getType() - 获取IP地址类型
```php
$type = Ip::getType('192.168.1.1');
```
