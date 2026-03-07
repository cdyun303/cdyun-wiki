# 缓存

## webman/cache

> webman/cache是基于symfony/cache开发的缓存组件，兼容协程和非协程环境，支持连接池。

### 安装

```bash
composer require -W webman/cache
```

### 配置

配置文件路径：`config/cache.php`

```php
return [
    'default' => 'file',
    'stores' => [
        'file' => [
            'driver' => 'file',
            'path' => runtime_path('cache')
        ],
        'redis' => [
            'driver' => 'redis',
            'connection' => 'cache' // 指定对应config/redis.php中的cache配置连接
        ],
        'array' => [
            'driver' => 'array'
        ],
        'apcu' => [
            'driver' => 'apcu'
        ]
    ]
];
```
> - 配置说明：stores.driver支持4种驱动，file、redis、array、apcu。
> - redis 驱动：依赖webman/redis组件，支持跨进程跨服务器共享缓存数据。


### 示例

```php
$key = 'test_key';

// 使用默认驱动，缓存数据
Cache::set($key, rand());

// 使用redis驱动，缓存数据
Cache::store('redis')->set('key', 'value');

// 使用array驱动，缓存数据
Cache::store('array')->set('key', 'value');
```

## webman/think-cache

> think-cache是从thinkphp框架抽离出的一个组件，并添加了连接池功能，自动支持协程和非协程环境。

### 安装

```bash
composer require -W webman/think-cache
```

### 配置

配置文件路径：`config/think-cache.php`

### 示例

```php
  namespace app\controller;

  use support\Request;
  use support\think\Cache;

  class UserController
  {
      public function db(Request $request)
      {
          $key = 'test_key';
          Cache::set($key, rand());
          return response(Cache::get($key));
      }
  }
```

### 接口

```php
// 设置缓存
Cache::set('val','value',600);
// 判断缓存是否设置
Cache::has('val');
// 获取缓存
Cache::get('val');
// 删除缓存
Cache::delete('val');
// 清除缓存
Cache::clear();
// 读取并删除缓存
Cache::pull('val');
// 不存在则写入
Cache::remember('val',10);

// 对于数值类型的缓存数据可以使用
// 缓存增+1
Cache::inc('val');
// 缓存增+5
Cache::inc('val',5);
// 缓存减1
Cache::dec('val');
// 缓存减5
Cache::dec('val',5);

// 使用缓存标签
Cache::tag('tag_name')->set('val','value',600);
// 删除某个标签下的缓存数据
Cache::tag('tag_name')->clear();
// 支持指定多个标签
Cache::tag(['tag1','tag2'])->set('val2','value',600);
// 删除多个标签下的缓存数据
Cache::tag(['tag1','tag2'])->clear();

// 使用多种缓存类型
$redis = Cache::store('redis');

$redis->set('var','value',600);
$redis->get('var');
```


