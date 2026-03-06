# HTTP请求

> 提供简洁的HTTP请求方法，支持GET、POST、文件上传等功能。

## 特性
- ✅ 支持HTTP/HTTPS协议
- ✅ 支持请求超时设置
- ✅ 支持请求头设置
- ✅ 支持请求参数设置
- ✅ 支持响应状态码、响应头、响应体获取
- ✅ 支持异常处理
- ✅ 支持多种HTTP方法（GET/POST/PUT/PATCH/DELETE/HEAD/OPTIONS）
- ✅ 支持多种内容类型（JSON/form/multipart）
- ✅ 灵活的请求选项配置
- ✅ 响应处理和错误处理

## 核心方法
| 方法名                | 功能描述        | 调用示例             |
|--------------------|-------------|-------------------------------------------|
| [`get()`](#get-get请求) | GET请求 | `Curl::get('https://api.example.com', $data)` |
| [`post()`](#post-post请求) | POST请求 | `Curl::post('https://api.example.com', $data)` |
| [`put()`](#put-put请求) | PUT请求 | `Curl::put('https://api.example.com/1', $data)` |
| [`delete()`](#delete-delete请求) | DELETE请求 | `Curl::delete('https://api.example.com/1')` |
| [`head()`](#head-head请求) | HEAD请求 | `Curl::head('https://api.example.com')` |
| [`options()`](#options-options请求) | OPTIONS请求 | `Curl::options('https://api.example.com')` |

## 使用示例

### setDefaultOptions() - 设置默认配置
```php
Curl::setDefaultOptions([
        'timeout' => 60,
        'connect_timeout' => 20,
    ])
```

### getDefaultOptions() - 获取默认配置
```php
Curl::getDefaultOptions()
// 返回默认配置
//  [
//        'timeout' => 60,
//        'connect_timeout' => 20,
//        'verify' => true,
//  ]
```

### reset() - 重置客户端实例
```php
Curl::reset()
```

### options() - OPTIONS请求
```php
$response = Curl::options('https://api.example.com', [], []);
```

### head() - HEAD请求
```php
$response = Curl::head('https://api.example.com', [], [], []);
```

### get() - GET请求
```php
$response = Curl::get('https://api.example.com', [], [], []);

$response = Curl::get('https://api.example.com/users', ['page' => 1, 'limit' => 10]);
```

### post() - POST请求
```php
$response = Curl::post('https://api.example.com', [], [], []);

$response = Curl::post('https://api.example.com', ['name' => 'John', 'email' => 'john@example.com']);
```

### postForm() - POST表单请求
```php
$response = Curl::postForm('https://api.example.com', [], [], []);

$response = Curl::postForm('https://api.example.com', ['name' => 'John', 'email' => 'john@example.com']);
```

### postMultipart() - POST文件上传请求
```php
$response = Curl::postMultipart(
    'https://api.example.com/upload', 
    [
        ['name' => 'file', 'contents' => fopen('/path/to/file.jpg', 'r')]
    ]
);
```

### put() - PUT请求
```php
$response = Curl::put('https://api.example.com/users/1', [], [], []);

$response = Curl::put('https://api.example.com/users/1', ['name' => 'Updated Name']);
```

### putForm() - PUT表单请求
```php
$response = Curl::put('https://api.example.com/users/1', [], [], []);

$response = Curl::put('https://api.example.com/users/1', ['name' => 'Updated Name']);
```

### delete() - PUT请求
```php
$response = Curl::delete('https://api.example.com/users/1', [], [], []);

$response = Curl::delete('https://api.example.com/users/1');
```

### patch() - PATCH请求
```php
$response = Curl::patch('https://api.example.com/users/1', [], [], []);

$response = Curl::patch('https://api.example.com/users/1', [
    'status' => 'active'
]);
```