# ThinkPHP Swagger扩展

> 提供Swagger文档功能，支持多应用。

## 安装

```bash
composer require cdyun/thinkphp-swagger
```

## 服务注入

在扩展的composer.json文件中增加如下定义：

```json
"extra": {
    "think": {
        "services": [
            "Cdyun\\ThinkphpSwagger\\SwaggerService"
        ]
    }
},
```

实现系统初始化过程中自动注册SwaggerService服务：

```php
<?php
namespace Cdyun\ThinkphpSwagger;

use think\Route;
use think\Service;

class SwaggerService extends Service
{
    public function boot()
    {
        // 注册路由
        $this->registerRoutes(function (Route $route) {

            // 获取swagger Json信息，http://xxx.com/swagger/openapi.json
            $route->get('swagger/openapi', '\\Cdyun\\ThinkphpSwagger\\SwaggerController@openapi')->ext('json');

            // 访问swagger页面，http://xxx.com/swagger
            $route->get('swagger', '\\Cdyun\\ThinkphpSwagger\\SwaggerController@index');
        });
    }
}
```

## 配置文件

配置文件路径：`config/swagger.php`
```php
<?php

return [
    // 应用分组
    'groups'=>[
        // 应用名称
        'default'=>[
            // 标题，会替换OA\Info中标题
            'title'=>'通用接口文档',
            // 描述，会替换OA\Info中描述
            'description'=>'让开发变得更简单、更通用、更流行。',
        ],
    ]
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

## 访问 Swagger
> 服务注入时配置了路由，直接访问即可。
```
#访问链接
http://域名/swagger
```

## 相关链接

- [Packagist 仓库](https://packagist.org/packages/cdyun/thinkphp-swagger)
- [GitHub 仓库](https://github.com/cdyun303/thinkphp-swagger)
- [问题反馈](https://github.com/cdyun303/thinkphp-swagger/issues)

# 版本要求

- topthink/framework: ^6.0|^8.0
- zircote/swagger-php: ^6.0

# 许可证

MIT License