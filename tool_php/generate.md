# 代码生成

> 提供常用的代码生成方法，支持ID生成、验证码生成、随机数生成等功能。

## 特性
- ✅ UUID生成
- ✅ 订单号生成（时间戳+随机数）
- ✅ 邀请码生成（自定义长度和字符集）
- ✅ URL安全码生成（Base64URL编码）
- ✅ 注册码生成（支持分段显示）
- ✅ 线程安全的随机数生成（random_int）

## 核心方法

| 方法名 | 功能描述 | 调用示例 |
|------|----------|--------|
| [`uuid()`](#uuid-生成uuid) | 生成UUID | `Crypto::uuid()` |
| [`orderNo()`](#orderno-生成订单号) | 生成订单号 | `Crypto::orderNo('')`|
| [`inviteCode()`](#invitecode-生成邀请码) | 生成邀请码    | `Crypto::inviteCode(6, 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789')`|
| [`urlSafeCode()`](#urlsafecode-生成url安全码) | 生成URL安全码 | `Crypto::urlSafeCode(16)`|
| [`registerCode()`](#registercode-生成注册码) | 生成注册码   | `Crypto::registerCode(16, 4, '-')`|

## 使用示例

### uuid() - 生成uuid
```php
$uuid = Generate::uuid();
```

### orderNo() - 生成订单号
```php
// 生成不带前缀的订单号
$orderNo = Generate::orderNo(); // 202512251200001234

// 生成带前缀的订单号
$orderNo = Generate::orderNo('ORD'); // ORD202507261234561234
```

### inviteCode() - 生成邀请码
```php
$inviteCode = Generate::inviteCode(8); // 8位邀请码
```

### urlSafeCode() - 生成URL安全码
```php
$urlSafe = Generate::urlSafeCode(16); // URL安全的随机码
```

### registerCode() - 生成注册码
```php
$registerCode = Generate::registerCode(12, 4); // 12位注册码，每4位分隔
```