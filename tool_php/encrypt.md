# 加解密

> 提供常用的加解密方法，支持AES、RSA、Hash、签名等功能。

## 特性
- ✅ MD5加密（支持加盐）
- ✅ 密码哈希（基于PHP原生password_hash）
- ✅ SSL对称加密（AES-256-GCM）
- ✅ HMAC签名（支持多种算法）
- ✅ 双模式调用：实例调用 + 静态调用
- ✅ 符合安全最佳实践
- ✅ PHP8.3+只读属性确保配置安全

## 核心方法
| 方法名                | 功能描述        | 调用示例                                      |
|--------------------|-------------|-------------------------------------------|
| [`md5()`](#md5-md5加密支持加盐)            | MD5加密（支持加盐） | `Crypto::md5('123456', 'salt')`           |
| [`passwordHash()`](#passwordhash-密码哈希)   | 密码哈希        | `Crypto::passwordHash('123456')`          |
| [`passwordVerify()`](#passwordverify-密码验证) | 密码验证        | `Crypto::passwordVerify('123456', $hash)` |
| [`sslEncrypt()`](#sslencrypt-ssl对称加密)     | SSL对称加密     | `Crypto::sslEncrypt('data', $key)`        |
| [`sslDecrypt()`](#ssldecrypt-ssl对称解密)     | SSL对称解密     | `Crypto::sslDecrypt($encrypted, $key)`    |

## 使用示例

### Crypto - 加密引擎说明
```php
use Cdyun\PhpTool\Crypto;

// Sodium引擎 - 推荐使用（性能更高，安全性更强）
// 需要PHP扩展：sodium
$crypto = new Crypto('your_key', Crypto::ENGINE_SODIUM);

// OpenSSL引擎 - 通用选择
// 需要PHP扩展：openssl
$crypto = new Crypto('your_key', Crypto::ENGINE_OPENSSL);

// 自动选择引擎 - 自动选择最优引擎
$crypto = new Crypto('your_key', Crypto::ENGINE_AUTO);
```

### Crypto - 加密模式说明
```php
use Cdyun\PhpTool\Crypto;

// 标准模式 - Base64编码
$crypto = new Crypto('your_key', Crypto::ENGINE_AUTO, Crypto::MODE_STANDARD);
$encrypted = $crypto->encrypt('敏感数据');
// 输出示例: VEhJUz1mYWxzZVZlcnNpb249MS4wJmtleT1zZWN1cmVfazEyMw==

// URL安全模式 - Base64URL编码（无=号，适合URL传输）
$crypto = new Crypto('your_key', Crypto::ENGINE_AUTO, Crypto::MODE_URL_SAFE);
$encrypted = $crypto->encrypt('敏感数据');
// 输出示例: VEhJUz1mYWxzZVZlcnNpb249MS4wJmtleT1zZWN1cmVfazEyMw

// 紧凑模式 - 十六进制编码（最短长度，适合存储）
$crypto = new Crypto('your_key', Crypto::ENGINE_AUTO, Crypto::MODE_COMPACT);
$encrypted = $crypto->encrypt('敏感数据');
// 输出示例: 54484349533b66756c73652076657273696f6e20312e302e303b6b65793d7365637572655f6b313233
```

### Crypto - 基础加解密

```php
use Cdyun\PhpTool\Crypto;

// 创建加密实例
$crypto = new Crypto('your_secret_key_2025');

// 加密数据
$encrypted = $crypto->encrypt('这是需要加密的敏感数据');
echo $encrypted;
// 输出示例: VEhJUz1mYWxzZVZlcnNpb249MS4wJmtleT1zZWN1cmVfazEyMw==

// 解密数据
$decrypted = $crypto->decrypt($encrypted);
echo $decrypted;
// 输出: 这是需要加密的敏感数据

// 使用不同的密钥
$crypto2 = new Crypto('another_key');
$encrypted2 = $crypto2->encrypt('另一个敏感数据');

// 解密（需要使用相同的密钥）
$decrypted2 = $crypto2->decrypt($encrypted2);
```

### Crypto - 静态方法调用

```php
use Cdyun\PhpTool\Crypto;

// 静态加密（使用默认密钥）
$encrypted = Crypto::encrypt('敏感数据');
$decrypted = Crypto::decrypt($encrypted);

// 使用自定义密钥的静态方法
$encrypted = (new Crypto('custom_key'))->encrypt('敏感数据');
$decrypted = (new Crypto('custom_key'))->decrypt($encrypted);
```

### md5() - MD5加密（支持加盐）
```php
// 基础MD5加密
$md5 = Crypto::md5('123456'); // e10adc3949ba59abbe56e057f20f883e

// 加盐MD5加密
$salt = 'your_custom_salt';
$md5WithSalt = Crypto::md5('123456', $salt); // 52c69e3a57331081823331c4e6999d23

// 多次加盐（提高安全性）
$doubleSalt = Crypto::md5(Crypto::md5('123456'), $salt);
```

### passwordHash()  - 密码哈希
```php
$password = 'my_secure_password';
$hash = Crypto::passwordHash($password);
```

### passwordVerify()  - 密码哈希验证
```php
// 密码正确
$isValid = Crypto::passwordVerify('my_secure_password', $hash);

// 密码错误
$isValid = Crypto::passwordVerify('wrong_password', $hash);

// 密码哈希更新（重新哈希）
if (password_needs_rehash($hash, PASSWORD_DEFAULT)) {
    $newHash = Crypto::passwordHash($password);
}
```

### Crypto - HMAC签名

```php
use Cdyun\PhpTool\Crypto\Crypto;

// SHA256签名（默认）
$signature = Crypto::hmac('待签名数据', 'your_secret_key');
echo $signature;
// 输出示例: 3a6eb0790f39ac87c94f3856b2dd2c5d110e0f9b0e9c9d6e7b8c9d0e1f2a3b4c

// SHA512签名
$signature512 = Crypto::hmac('待签名数据', 'your_secret_key', 'sha512');
echo $signature512;
// 输出示例: a4e6b8c0d1e2f3a4b5c6d7e8f9a0b1c2d3e4f5a6b7c8d9e0f1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b1c2

// MD5签名
$signatureMd5 = Crypto::hmac('待签名数据', 'your_secret_key', 'md5');
echo $signatureMd5;
// 输出示例: 1a1dc06f7a0b2c8d9e0f1a2b3c4d5e6f7

// 数据完整性验证
$originalData = '订单数据';
$originalSignature = Crypto::hmac($originalData, 'api_secret');

$receivedData = '订单数据';
$receivedSignature = $_SERVER['HTTP_SIGNATURE'] ?? '';

if (hash_equals($originalSignature, $receivedSignature)) {
    echo '数据完整性验证通过';
} else {
    echo '数据可能被篡改';
}
```

### Crypto - SSL对称加解密

```php
use Cdyun\PhpTool\Crypto;

// 使用自定义密钥进行SSL加密
$key = 'your_ssl_key_32_bytes_long!';
$crypto = new Crypto();

$encrypted = $crypto->sslEncrypt('SSL加密数据', $key);
echo $encrypted;
// 输出示例: VGhpc0lzU1NMY0VuY3J5cHRlZERhdGE=

$decrypted = $crypto->sslDecrypt($encrypted, $key);
echo $decrypted;
// 输出: SSL加密数据
```

### Crypto - 错误处理

```php
use Cdyun\PhpTool\Crypto;

$crypto = new Crypto('your_key');

try {
    $encrypted = $crypto->encrypt('敏感数据');
    $decrypted = $crypto->decrypt($encrypted);
    echo '加解密成功: ' . $decrypted;
} catch (\Exception $e) {
    echo '加解密失败: ' . $e->getMessage();
}

// 密钥错误时的解密异常
try {
    $wrongCrypto = new Crypto('wrong_key');
    $decrypted = $wrongCrypto->decrypt($encrypted);
} catch (\Exception $e) {
    echo '解密失败（密钥错误）: ' . $e->getMessage();
}
```

## 使用场景

```php
use Cdyun\PhpTool\Crypto;

// 场景1：用户敏感信息加密存储
function saveUserSensitiveData(Crypto $crypto, array $data): array
{
    return [
        'id' => $data['id'],
        'name' => $data['name'],
        'encrypted_phone' => $crypto->encrypt($data['phone']),
        'encrypted_id_card' => $crypto->encrypt($data['id_card'])
    ];
}

function getUserSensitiveData(Crypto $crypto, array $userData): array
{
    return [
        'id' => $userData['id'],
        'name' => $userData['name'],
        'phone' => $crypto->decrypt($userData['encrypted_phone']),
        'id_card' => $crypto->decrypt($userData['encrypted_id_card'])
    ];
}

// 场景2：API请求签名验证
function verifyApiRequest(Crypto $crypto, array $params, string $signature): bool
{
    $expectedSignature = Crypto::hmac(json_encode($params), $apiSecret);
    return hash_equals($expectedSignature, $signature);
}

// 场景3：密码安全存储
function registerUser(string $password): string
{
    return Crypto::passwordHash($password);
}

function verifyUserPassword(string $password, string $hash): bool
{
    return Crypto::passwordVerify($password, $hash);
}
```