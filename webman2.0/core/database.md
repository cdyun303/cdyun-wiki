# 数据库

## webman/database

> webman/database是基于illuminate/database开发的，并加入了连接池功能，支持协程和非协程环境，用法与laravel相同。

### 安装

- 基本功能

```bash
composer require -W webman/database
```

- 基本功能，并增加分页、数据库事件、记录SQL

```bash
composer require -W webman/database illuminate/pagination illuminate/events symfony/var-dumper
```

### 配置

配置文件路径：`config/database.php`，参考webman官方配置文件。

```php
return [
    // 默认数据库
    'default' => 'mysql',

    // 各种数据库配置
    'connections' => [
        'mysql' => [
            'driver'      => 'mysql',
            'host'        => '127.0.0.1',
            'port'        => 3306,
            'database'    => 'test',
            'username'    => 'root',
            'password'    => '',
            'unix_socket' => '',
            'charset'     => 'utf8',
            'collation'   => 'utf8_unicode_ci',
            'prefix'      => '',
            'strict'      => true,
            'engine'      => null,
            'options' => [
                PDO::ATTR_EMULATE_PREPARES => false, // 当使用swoole或swow作为驱动时是必须的
            ],
            'pool' => [ // 连接池配置
                'max_connections' => 5, // 最大连接数
                'min_connections' => 1, // 最小连接数
                'wait_timeout' => 3,    // 从连接池获取连接等待的最大时间，超时后会抛出异常。仅在协程环境有效
                'idle_timeout' => 60,   // 连接池中连接最大空闲时间，超时后会关闭回收，直到连接数为min_connections
                'heartbeat_interval' => 50, // 连接池心跳检测时间，单位秒，建议小于60秒
            ],
        ],
    ],
];
```

> 配置说明：除了pool配置外，其它配置与laravel相同。

### 示例

```php
namespace app\controller;

use support\Request;
use support\Db;

class UserController
{
    public function db(Request $request)
    {
        $default_uid = 29;
        $uid = $request->get('uid', $default_uid);
        $name = Db::table('users')->where('uid', $uid)->value('username');
        return response("hello $name");
    }
}
```
> 用法与laravel相同，使用Db::table()方法来操作数据库。

## webman/think-orm

> webman/think-orm 是基于 top-think/think-orm 开发的数据库组件，支持连接池，支持协程和非协程环境。

### 安装

```bash
composer require -W webman/think-orm
```

### 配置

配置文件路径：`config/think-orm.php`，根据实际情况修改配置文件。

### 示例

```php
namespace app\controller;

use support\Request;
use support\think\Db;

class FooController
{
    public function get(Request $request)
    {
        $user = Db::table('user')->where('uid', '>', 1)->find();
        return json($user);
    }
}
```
> 支持think-orm的模型，用法与think-orm相同。


