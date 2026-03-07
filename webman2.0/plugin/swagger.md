# Webman Swagger应用插件

> 提供Swagger文档功能，支持多应用，多插件，用户登录后访问，用户登录验证支持默认账户密码和自定义验证接口，用户登录自定义验证接口同时支持内链和外链验证。

## 安装

```bash
composer require cdyun/webman-swagger
```

## 特性

- ✅ 支持多应用，多插件
- ✅ 支持用户登录后，访问swagger文档
- ✅ 用户登录验证支持默认账户密码和自定义验证接口
- ✅ 用户登录自定义验证接口同时支持内链和外链验证

## 访问插件
composer安装完成后记得重启服务，根目录执行php start.php restart
```
#（插件配置了路由）访问链接
http://域名/app/swagger
```

## 配置文件

配置文件路径：`config/app.php`，在配置文件中添加swagger配置
```php
return [
    ...,
    // swagger配置
    'swagger' => [
        // swagger应用分组，支持插件和主应用，下面两个demo可删除
        'groups' => [
            [
                // 扫描指定应用目录，每个应用的OA\Info信息，必须且只能存在一个，所以建议写在每个应用控制器继承的 BaseController.php 上
                'scan_path' => base_path('app/v1'),
                // 分组标题，会替换掉OA\Info中的title
                'title' => 'v1应用接口文档',
                // 分组描述，会替换掉OA\Info中的description
                'description' => '让开发变得更简单、更通用、更流行。',
            ],
            [
                // 分组标题
                'title' => 'admin插件接口文档',
                // 分组描述
                'description' => '让开发变得更简单、更通用、更流行。',
                // 扫描指定应用目录，每个应用的OA\Info信息，必须且只能存在一个，所以建议写在每个应用控制器继承的 BaseController.php 上
                'scan_path' => base_path('plugin/admin'),
            ],
        ],
        // 是否登录功能
        'login' => [
            // 是否开启
            'enable' => true,
            // 登录验证接口, 为空时使用默认。支持内链（/v1/core/login）和外链(http://xxx.com/v1/core/login)
            'check_url' => '',
            // 登录验证接口为空时，默认登录用户名
            'username' => 'cdyun',
            // 登录验证接口为空时，默认登录密码
            'password' => 'swagger'
        ]
    ],
];
```

## 使用注意
> - 每个应用的OA\Info信息，必须且只能存在一个，所以建议写在每个应用控制器继承的 BaseController.php 上；
> - OA\Info中标题和描述信息会被 config/app.php 中信息替换掉；

应用V1

```php
<?php
namespace app\v1\controller;

use support\base\BaseController;
use OpenApi\Attributes as OA;

#[OA\Info(version: '1.0.0', title: 'V1')]
class V1BaseController extends BaseController
{
    /**
     * @OA\Get(
     *     path="/index",
     *     @OA\Response(response="200", description="{ 'code': 0, 'msg': 'ok' }")
     * )
     */
	public function index(Request $request)
    {
        return json(['code' => 0, 'msg' => 'ok']);
    }
    ...其他
}
```

应用V2

```php
<?php
namespace app\v2\controller;

use support\base\BaseController;
use OpenApi\Attributes as OA;

#[OA\Info(version: '2.0.0', title: 'V2')]
class V2BaseController extends BaseController
{
    ...其他
}
```
## 相关链接

- [Packagist 仓库](https://packagist.org/packages/cdyun/webman-swagger)
- [GitHub 仓库](https://github.com/cdyun303/webman-swagger)
- [问题反馈](https://github.com/cdyun303/webman-swagger/issues)

# 版本要求

- php: ^8.1
- guzzlehttp/guzzle: ^7.10
- vlucas/phpdotenv: ^5.6
- workerman/webman-framework: ^2.1
- zircote/swagger-php: ^6.0

# 许可证

MIT License