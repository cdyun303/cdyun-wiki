# 验证器

## webman/validation

> 基于 illuminate/validation，提供手动验证、注解验证、参数级验证，以及可复用的规则集。

### 安装

```bash
composer require webman/validation
```

### 基本概念
- 规则集复用：通过继承 support\validation\Validator 定义可复用的 rules messages attributes scenes，可在手动与注解中复用。
- 方法级注解（Attribute）验证：使用 PHP 8 属性注解 #[Validate] 绑定控制器方法。
- 参数级注解（Attribute）验证：使用 PHP 8 属性注解 #[Param] 绑定控制器方法参数。
- 异常处理：验证失败抛出 support\validation\ValidationException，异常类可通过配置自定义
- 数据库验证：如果涉及数据库验证，需要安装 composer require webman/database

### 示例

- 基本用法

```php
use support\validation\Validator;

$data = ['email' => 'user@example.com'];

$validator = Validator::make($data, [
    'email' => 'required|email',
])->validate();

// 验证失败处理
if ($validator->fails()) {
    $firstError = $validator->errors()->first();      // string
    $allErrors = $validator->errors()->all();         // array
    $errorsByField = $validator->errors()->toArray(); // array
    // 处理错误...
}
```

- 规则集复用

```php
namespace app\validation;

use support\validation\Validator;

class UserValidator extends Validator
{
    protected array $rules = [
        'id' => 'required|integer|min:1',
        'name' => 'required|string|min:2|max:20',
        'email' => 'required|email',
    ];

    protected array $messages = [
        'name.required' => '姓名必填',
        'email.required' => '邮箱必填',
        'email.email' => '邮箱格式不正确',
    ];

    protected array $attributes = [
        'name' => '姓名',
        'email' => '邮箱',
    ];

    protected array $scenes = [
        'create' => ['name', 'email'],
        'update' => ['id', 'name', 'email'],
    ];
}
```

```php
use app\validation\UserValidator;

// 不指定场景 -> 验证全部规则
$validator = UserValidator::make($data)->validate();

// 指定场景 -> 只验证该场景包含的字段
$validator = UserValidator::make($data)->withScene('create')->validate();

// 验证失败处理
if ($validator->fails()) {
    $firstError = $validator->errors()->first();      // string
    $allErrors = $validator->errors()->all();         // array
    $errorsByField = $validator->errors()->toArray(); // array
    // 处理错误...
}
```

## topthink/think-validate

> ThinkValidate是一个基于PHP8.0的数据验证类库，从ThinkPHP的一个核心组件独立维护，以优异的功能和突出的性能著称，提供了更优秀的性能和开发体验，最新版本要求PHP8.0+。

### 环境要求

- 3.0版本：PHP8.0+ 
- 2.0版本：PHP7.1+

### 使用注意

Webman里不支持think-validate的Validate::rule()方法

### 安装

```bash
composer require topthink/think-validate
```

> 最新的3.0版本要求PHP8.0+，如果你的PHP环境低于8.0，可以安装2.0版本。

### 示例

定义验证器

```php
namespace app\validate;

use think\Validate;

class User extends Validate
{
    protected $rule =   [
        'name'  => 'require|max:25',
        'age'   => 'number|between:1,120',
        'email' => 'email',    
    ];
    
    protected $message  =   [
        'name.require' => '名称必须',
        'name.max'     => '名称最多不能超过25个字符',
        'age.number'   => '年龄必须是数字',
        'age.between'  => '年龄只能在1-120之间',
        'email'        => '邮箱格式错误',    
    ];

    protected $scene = [
        'edit'  =>  ['name','age'],
    ]; 
    
}
```

数据验证

```php
namespace app\controller;

use app\validate\User;
use think\exception\ValidateException;

class Index
{
    public function index()
    {
        $data = [
            'name'  => 'thinkphp',
            'age'   => 10,
            'email' => 'thinkphp@qq.com',
        ];
        // 不指定场景 -> 验证全部规则
        try {
            $validate = new User;
            $validate->failException(true)->check(data);
        } catch (ValidateException $e) {
            // 验证失败 
            var_dump($e->getError()); // 输出错误信息
            var_dump($e->getKey()); // 验证错误的字段名
        }

        // 指定场景 -> 验证该场景包含的字段
        try {
            // 支持使用助手函数 validate() 验证
            validate(app\validate\User::class)
                ->scene('edit')
                ->check($data);
        } catch (ValidateException $e) {
            // 验证失败 输出错误信息
            var_dump($e->getError());
        }
    }
}
```


> 更多用法请参考 [think-validate文档](https://doc.thinkphp.cn/@think-validate/default.html)