# Webman2.0项目开发脚手架

> Webman2.0项目开发脚手架是一个基于Webman框架的快速开发模板，专为数据处理类项目设计。它提供了一套完整的项目结构和常用功能，帮助开发者快速构建高性能的PHP应用。

## 快速开始

### 安装步骤

1. **安装项目**

```bash
composer create-project cdyun/webman-framework webman
```

2. **安装依赖**

```bash
cd webman

composer install
```

3. **安装常用组件（可选）**

```bash
# PHP8.1+ 通用工具包
composer require cdyun/php-tool

# 数据库
composer require -W webman/database

# Redis
composer require -W webman/redis illuminate/events

# 缓存Cache
composer require -W webman/cache

# 验证器
composer require topthink/think-validate

# JWT插件
composer require cdyun/webman-jwt

# Response插件
composer require cdyun/webman-response

# Swagger应用插件
composer require cdyun/webman-swagger
```

4. **配置环境**

复制 `.env.example` 文件为 `.env` 并修改配置：

```bash
# 编辑 .env 文件，设置数据库连接等信息
cp .env.example .env
```

5. **启动服务**

```bash
# 开发环境
php start.php start

# 生产环境
php start.php start -d
```

5. **访问项目**

打开浏览器访问：`http://localhost:8787`

### 环境要求

- PHP 8.1+
- Webman 2.0+
- Composer >= 2.0

## 目录结构

```
webman/                                   部署目录
├── app                                   应用目录
│   ├── v1                                V1应用
│   │   ├── controller                    控制器
│   │   ├── model                         模型
│   │   ├── view                          视图
│   │   └── ...                           其他
│   │
│   ├── v2                                V2应用
│   │   ├── controller                    控制器
│   │   ├── model                         模型
│   │   ├── view                          视图
│   │   └── ...                           其他
│   │
│   └── functions.php                     业务自定义函数写到这个文件里
│
├── config                                配置目录
│   ├── plugin                            插件配置目录
│   ├── app.php                           应用配置
│   ├── autoload.php                      这里配置的文件会被自动加载
│   ├── bootstrap.php                     进程启动时onWorkerStart时运行的回调配置
│   ├── container.php                     容器配置
│   ├── dependence.php                    容器依赖配置
│   ├── event.php                         事件配置
│   ├── exception.php                     异常配置
│   ├── log.php                           日志配置
│   ├── middleware.php                    中间件配置
│   ├── process.php                       自定义进程配置
│   ├── route.php                         路由配置
│   ├── server.php                        端口、进程数等服务器配置
│   ├── session.php                       session配置
│   ├── static.php                        静态文件开关及静态文件中间件配置
│   ├── translation.php                   多语言配置
│   └── view.php                          视图配置
│
├── process                               自定义进程目录  
│   ├── Http.php                          Http进程
│   └── Monitor.php                       监控进程
│
├── public                                静态资源目录
├── runtime                               应用的运行时目录，需要可写权限
├── vendor                                composer安装的第三方类库目录
├── support                               全局配置类库目录
│   ├── event                             事件类目录
│   │   └── AdminEvent.php                Admin应用事件
│   ├── exception.php                     异常类目录  
│   │   ├── AdminException.php            Admin应用异常
│   │   ├── AppException.php              全局应用异常
│   │   └── AppHandler.php                应用异常处理类    
│   ├── middleware                        中间件类目录
│   │   └── CrossDomainMiddleware.php     跨域中间件
│   ├── Request.php                       请求类
│   ├── Response.php                      响应类
│   └── bootstrap.php                     进程启动后初始化脚本
│
├── .env.example                          环境变量示例文件
├── LICENSE                               MIT开源协议文件
├── README.md                             README.md
├── composer.json                         项目依赖配置文件
└── start.php                             服务启动文件
```

## 主要特性

- ✅ **高稳定性**：webman基于workerman开发，workerman一直是业界bug极少的高稳定性socket框架。
- ✅ **高性能**：webman性能高于传统php-fpm框架10-100倍左右，比go的gin echo等框架性能高1倍左右。
- ✅ **高复用**：无需修改，可以复用现有composer生态。
- ✅ **高扩展性**：支持自定义进程，可以做workerman能做的任何事情。
- ✅ **MIT开源**：使用最为宽松友好的MIT开源协议。

## 许可证

MIT License
