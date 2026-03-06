# Webman JWT插件

> 提供JWT认证功能

## 安装

```bash
composer require cdyun/webman-jwt
```

## 使用示例

```php
use Cdyun\WebmanJwt\JwtEnforcer;

// 生成token
$token = JwtEnforcer::generateToken($payload);

// 验证token
$payload = JwtEnforcer::validateToken($token);

// 获取配置Config
$config = JwtEnforcer::getConfig($name , $default);
```
## 相关链接

- [Packagist 仓库](https://packagist.org/packages/cdyun/webman-jwt)
- [GitHub 仓库](https://github.com/cdyun303/webman-jwt)
- [问题反馈](https://github.com/cdyun303/webman-jwt/issues)

# 版本要求

- php: >=8.1
- firebase/php-jwt: ^6.11

# 许可证

MIT License