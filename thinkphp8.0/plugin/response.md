# 请求响应Response扩展

> 提供响应处理功能

## 安装

```bash
composer require cdyun/thinkphp-response
```

## 配置文件

配置文件路径：`config/cdyun.php`

```php
return [
    //  响应信息
    'response' => [
        //  返回码
        'code' => [
            //  成功返回码
            'success' => (int)env('code.success_code', 0),
            //  失败返回码
            'error' => (int)env('code.error_code', -1),
        ],
        //  是否开启加密
        'enable' => false,
        //  不需要加密的url，上传URL不需要加密
        'url' => ['/web_api/core/ocr/scan', '/web_api/core/upload/direct'],
        //  RSA私钥
        'rsa_private' => '',
    ],
];
```

## 使用示例

### 常规用法
```php
use Cdyun\ThinkphpResponse\ResponseEnforcer;

//获取配置
ResponseEnforcer::getConfig($name = null, $default = null);

//success
ResponseEnforcer::success($msg = '操作成功', $data = null, $header = []);

//error - 错误响应始终不会加密
ResponseEnforcer::error($msg = '操作失败', $data = null,  $header = []);

//abort
ResponseEnforcer::abort($msg = '服务器内部错误', $code = 500);

//paginate
ResponseEnforcer::paginate( $data = [], $totalCount = 0, $msg = '加载完成', $header = []);

//result
ResponseEnforcer::result($result, array $header = [], bool $isEncrypt = false);
```

### 加密/解密
```php
use Cdyun\ThinkphpResponse\EncryptorEnforcer;

//获取配置
ResponseEnforcer::getConfig($name = null, $default = null);

//RSA解密
EncryptorEnforcer::rsaDecrypt($data);

//AES解密
EncryptorEnforcer::aesDecrypt($data, $key, $iv);

//AES加密
EncryptorEnforcer::aesEncrypt($data, $key, $iv);
```

## 相关链接

- [Packagist 仓库](https://packagist.org/packages/cdyun/thinkphp-response)
- [GitHub 仓库](https://github.com/cdyun303/thinkphp-response)
- [问题反馈](https://github.com/cdyun303/thinkphp-response/issues)

# 版本要求

- php: >=8.1

# 许可证

MIT License