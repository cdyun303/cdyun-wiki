# 字符串处理

> 提供丰富的字符串处理方法，支持字符串转换、格式化、截取、加密等功能。

## 特性
- ✅ 随机字符串生成
- ✅ 命名转换（驼峰、蛇形、大驼峰）
- ✅ 字符串转义和反转义
- ✅ 字符串修剪
- ✅ 字符串脱敏（手机号、身份证号、邮箱、银行卡号、车牌号、姓名）
- ✅ 字符串验证（手机号、身份证号、邮箱、车牌号、银行卡号）
- ✅ 收货地址解析
- ✅ 字符串格式化和转换
- ✅ 字符串相似度比较
- ✅ 多分隔符字符串分割

## 核心方法
| 方法名 | 功能描述 | 调用示例 |
|--------|----------|----------|
| [`maskPhone()`](#maskphone-手机号脱敏) | 手机号脱敏 | `Str::maskPhone('13800138000')` |
| [`maskEmail()`](#maskemail-邮箱脱敏) | 邮箱脱敏 | `Str::maskEmail('user@example.com')` |
| [`camel()`](#camel-下划线转驼峰) | 下划线转驼峰 | `Str::camel('hello_world')` |
| [`snake()`](#snake-驼峰转下划线) | 驼峰转下划线 | `Str::snake('helloWorld')` |
| [`toBase64()`](#tobase64-base64编码) | base64编码 | `Str::toBase64('hello')` |
| [`fromBase64()`](#frombase64-base64解码) | Base64解码 | `Str::fromBase64('aGVsbG8=')` |

## 使用示例

### 脱敏

#### mask() - 字符串脱敏
```php
$masked = Str::mask('13800138000', 3, 4, '*'); // '138****8000'
$masked = Str::mask('user@example.com', 2, 4, '*'); // 'us****@example.com'
```

#### maskPhone() - 手机号脱敏
```php
$phone = Str::maskPhone('13800138000'); // '138****8000'
$phone = Str::maskPhone('13800138000', 3, 4); // '138****8000'
```

#### maskEmail() - 邮箱脱敏
```php
$email = Str::maskEmail('user@example.com'); // 'us***@example.com'
$email = Str::maskEmail('user@example.com', 2, 3); // 'us***@example.com'
```

#### maskIdCard() - 身份证号脱敏
```php
$idCard = Str::maskIdCard('110101199001011234'); // '110101********1234'
$idCard = Str::maskIdCard('110101199001011234', 6, 8); // '110101********1234'
```

#### maskBankCard() - 银行卡号脱敏
```php
$bankCard = Str::maskBankCard('6222021234567890123'); // '622202********0123'
$bankCard = Str::maskBankCard('6222021234567890123', 6, 10); // '622202********0123'
```

#### maskName() - 姓名脱敏
```php
$name = Str::maskName('张三'); // '张*'
$name = Str::maskName('欧阳修'); // '欧阳*'
$name = Str::maskName('张三丰', 1, 1); // '张*丰'
```

### 字符串长度和截断

#### length() - 字符串长度
```php
$length = Str::length('你好世界'); // 4（使用mb_strlen）
```

#### truncate() - 字符串截断
```php
$truncated = Str::truncate('这是一段很长的文本内容', 10); // '这是一段很长的文...'
$truncated = Str::truncate('这是一段很长的文本内容', 10, '---'); // '这是一段很长的文---'
```

#### limit() - 字符串限制长度
```php
$limited = Str::limit('这是一段很长的文本内容', 10); // '这是一段很长的文...'
$limited = Str::limit('短文本', 10); // '短文本'（不超过长度不截断）
```

#### wordTruncate() - 字符串单词截断
```php
$wordTruncate = Str::wordTruncate('This is a long text content', 10); // 'This is a...'
```

### 字符串命名转换

#### snake() - 驼峰转下划线
```php
$snake = Str::snake('helloWorld'); // 'hello_world'
$snake = Str::snake('HelloWorld'); // 'hello_world'
$snake = Str::snake('HelloWorld', '-'); // 'hello-world'
```
#### toSnake() - 驼峰命名转下划线命名(支持数组键名)
```php
$snake = Str::toSnake('helloWorld'); // 'hello_world'
$snake = Str::toSnake('HelloWorld'); // 'hello_world'
$snake = Str::toSnake(['AaBbCc'=>1]); // ['aa_bb_cc'=>1]
```

#### camel() - 下划线转驼峰
```php
$camel = Str::camel('hello_world'); // 'helloWorld'
$camel = Str::camel('hello-world'); // 'helloWorld'
$camel = Str::camel('hello_world', '-'); // 'helloWorld'
```

#### toCamel() - 下划线命名转驼峰命名(支持数组键名)
```php
$camel = Str::toCamel('hello_world', false); // 'helloWorld'
$camel = Str::toCamel('hello_world', true); // 'HelloWorld'
$camel = Str::toCamel(['aa_bb_cc'=>1], false); // 'aaBbCc'
$camel = Str::toCamel(['aa_bb_cc'=>1], true); // 'AaBbCc'
```

#### studly() - 首字母大写驼峰命名
```php
$camel = Str::studly('hello_world'); // 'HelloWorld'
$camel = Str::studly('hello-world'); // 'HelloWorld'
$camel = Str::studly('hello.world'); // 'HelloWorld'
$camel = Str::studly('aa-bb_cc.dd'); // 'AaBbCcDd'
```

#### ucfirst() - 首字母大写
```php
$ucfirst = Str::ucfirst('hello'); // 'Hello'
```

#### lcfirst() - 首字母小写
```php
$lcfirst = Str::lcfirst('Hello'); // 'hello'
```

#### ucwords() - 单词首字母大写
```php
$ucwords = Str::ucwords('hello world'); // 'Hello World'
```

#### upper() - 全部大写
```php
$upper = Str::upper('hello'); // 'HELLO'
```

#### lower() - 全部小写
```php
$lower = Str::lower('HELLO'); // 'hello'
```

#### swap() - 大小写转换
```php
$swap = Str::swap('Hello'); // 'hELLO'
```

#### title() - 标题格式
```php
$title = Str::title('hello world'); // 'Hello World'
```

### 字符串查找和判断

#### contains() - 是否包含子串
```php
$contains = Str::contains('hello world', 'world'); // true
$contains = Str::contains('hello world', 'php'); // false
```

#### startsWith() - 是否以子串开头
```php
$startsWith = Str::startsWith('hello world', 'hello'); // true
$startsWith = Str::startsWith('hello world', 'world'); // false
```

#### endsWith() - 是否以子串结尾
```php
$endsWith = Str::endsWith('hello world', 'world'); // true
$endsWith = Str::endsWith('hello world', 'hello'); // false
```

#### pos() - 子串首次出现位置
```php
$pos = Str::pos('hello world', 'world'); // 6
$pos = Str::pos('hello world', 'php'); // false
```

#### rpos() - 子串最后一次出现位置
```php
$pos = Str::rpos('hello world world', 'world'); // 12
$pos = Str::rpos('hello world', 'php'); // false
```

#### count() - 子串出现次数
```php
$count = Str::count('hello world world', 'world'); // 2
```

#### match() - 字符串是否匹配正则
```php
$match = Str::match('hello123', '/^[a-z]+\d+$/'); // true
$match = Str::match('hello', '/^[a-z]+\d+$/'); // false
```

### 字符串替换

#### replace() - 字符串替换
```php
$replaced = Str::replace('hello world', 'world', 'php'); // 'hello php'
```

#### replaceArray() - 字符串批量替换
```php
$replaced = Str::replaceArray('hello world', ['hello' => 'hi', 'world' => 'php']); // 'hi php'
```

#### replaceRegex() - 字符串正则替换
```php
$replaced = Str::replaceRegex('hello123world', '/\d+/', '456'); // 'hello456world'
```

#### substrReplace() - 字符串截取并替换
```php
$replaced = Str::substrReplace('hello world', 'php', 6, 5); // 'hello php'
```

### 字符串分割和连接

#### split() - 字符串分割
```php
$parts = Str::split('hello,world,php', ','); // ['hello', 'world', 'php']
```

#### toArray() - 字符串分割为数组
```php
$array = Str::toArray('hello,world,php', ','); // ['hello', 'world', 'php']
```

#### fromArray() - 数组连接为字符串
```php
$string = Str::fromArray(['hello', 'world', 'php'], ','); // 'hello,world,php'
```

#### join() - 字符串连接
```php
$joined = Str::join(['hello', 'world', 'php'], ','); // 'hello,world,php'
```

#### concat() - 字符串拼接
```php
$concat = Str::concat('hello', ' ', 'world'); // 'hello world'
```

### 字符串去除空白

#### trim() - 去除首尾空白
```php
$trimmed = Str::trim('  hello world  '); // 'hello world'
```

#### ltrim() - 去除左侧空白
```php
$ltrim = Str::ltrim('  hello world  '); // 'hello world  '
```

#### rtrim() - 去除右侧空白
```php
$rtrim = Str::rtrim('  hello world  '); // '  hello world'
```
#### clean() - 去除所有空白
```php
$clean = Str::clean('  hello   world  '); // 'helloworld'
```

### 字符串填充

#### padLeft() - 左侧填充
```php
$padded = Str::padLeft('123', 6, '0'); // '000123'
```

#### padRight() - 右侧填充
```php
$padded = Str::padRight('123', 6, '0'); // '123000'
```

#### padBoth() - 两侧填充
```php
$padded = Str::padBoth('123', 7, '*'); // '**123**'
```

### 字符串重复

#### repeat() - 字符串重复
```php
$repeated = Str::repeat('hello', 3); // 'hellohellohello'
```

#### reverse() - 字符串反转
```php
$reversed = Str::reverse('hello'); // 'olleh'
```

### 字符串随机

#### random() - 生成随机字符串
```php
$random = Str::random(16); // 16位随机字符串
```

#### numeric() - 生成随机数字字符串
```php
$numeric = Str::numeric(6); // 6位随机数字字符串
```
#### alpha() - 生成随机字母字符串
```php
$alpha = Str::alpha(8); // 8位随机字母字符串
```

### 字符串编码解码

#### toBase64() - Base64编码
```php
$base64 = Str::toBase64('hello'); // 'aGVsbG8='
```

#### fromBase64() - Base64解码
```php
$decoded = Str::fromBase64('aGVsbG8='); // 'hello'
```

#### toUrlEncode() - URL编码
```php
$urlEncoded = Str::toUrlEncode('hello world'); // 'hello%20world'
```

#### fromUrlEncode() - URL解码
```php
$urlDecoded = Str::fromUrlEncode('hello%20world'); // 'hello world'
```

#### toHtmlEntities() - HTML实体编码
```php
$htmlEncoded = Str::toHtmlEntities('<div>hello</div>'); // '&lt;div&gt;hello&lt;/div&gt;'
```

#### fromHtmlEntities() - HTML实体解码
```php
$htmlDecoded = Str::fromHtmlEntities('&lt;div&gt;hello&lt;/div&gt;'); // '<div>hello</div>'
```

#### toJson() - JSON编码
```php
$json = Str::toJson(['name' => '张三', 'age' => 25]); // '{"name":"张三","age":25}'
```

#### fromJson() - JSON解码
```php
$decoded = Str::fromJson('{"name":"张三","age":25}'); // ['name' => '张三', 'age' => 25]
```

#### toXml() - XML编码
```php
$xml = Str::toXml(['name' => '张三', 'age' => 25], 'root'); // '<root><name>张三</name><age>25</age></root>'
```
#### fromXml() - XML解码
```php
$decoded = Str::fromXml('<root><name>张三</name><age>25</age></root>'); // ['name' => '张三', 'age' => 25]
```

#### toBinary() - 二进制编码
```php
$binary = Str::toBinary('hello'); // '0110100001100101011011000110110001101111'
```

#### fromBinary() - 二进制解码
```php
$decoded = Str::fromBinary('0110100001100101011011000110110001101111'); // 'hello'
```

#### toHex() - 十六进制编码
```php
$hex = Str::toHex('hello'); // '68656c6c6f'
```

#### fromHex() - 十六进制解码
```php
$decoded = Str::fromHex('68656c6c6f'); // 'hello'
```

### 字符串哈希

#### md5() - MD5哈希
```php
$md5 = Str::md5('hello'); // '5d41402abc4b2a76b9719d911017c592'
```

#### sha1() - SHA1哈希
```php
$sha1 = Str::sha1('hello'); // 'aaf4c61ddcc5e8a2dabede0f3b482cd9aea9434d'
```

#### sha256() - SHA256哈希
```php
$sha256 = Str::sha256('hello'); // '2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824'
```

#### sha512() - SHA512哈希
```php
$sha512 = Str::sha512('hello'); // '9b71d224bd62f3785d96d46ad3ea3d73319bfbc2890caadae2dff72519673ca72323c3d99ba5c11d7c7acc6e14b8c5da0c4663475c2e5c3adef46f73bcdec043'
```

### 字符串验证

#### isEmail() - 是否为邮箱
```php
$isEmail = Str::isEmail('user@example.com'); // true
$isEmail = Str::isEmail('invalid-email'); // false
```

#### isUrl() - 是否为URL
```php
$isUrl = Str::isUrl('https://example.com'); // true
$isUrl = Str::isUrl('not-a-url'); // false
```

#### isIp() - 是否为IP地址
```php
$isIp = Str::isIp('192.168.1.1'); // true
$isIp = Str::isIp('not-an-ip'); // false
```

#### isIpv4() - 是否为IPv4地址
```php
$isIpv4 = Str::isIpv4('192.168.1.1'); // true
$isIpv4 = Str::isIpv4('2001:0db8:85a3:0000:0000:8a2e:0370:7334'); // false
```

#### isIpv6() - 是否为IPv6地址
```php
$isIpv6 = Str::isIpv6('2001:0db8:85a3:0000:0000:8a2e:0370:7334'); // true
$isIpv6 = Str::isIpv6('192.168.1.1'); // false
```

#### isPhone() - 是否为手机号
```php
$isPhone = Str::isPhone('13800138000'); // true
$isPhone = Str::isPhone('12345678901'); // false
```

#### isIdCard() - 是否为身份证号
```php
$isIdCard = Str::isIdCard('110101199001011234'); // true
$isIdCard = Str::isIdCard('123456789012345678'); // false
```

#### isBankCard() - 是否为银行卡号
```php
$isBankCard = Str::isBankCard('6222021234567890123'); // true
$isBankCard = Str::isBankCard('1234567890'); // false
```

#### isNumeric() - 是否为数字
```php
$isNumeric = Str::isNumeric('12345'); // true
$isNumeric = Str::isNumeric('abc123'); // false
```

#### isAlpha() - 是否为字母
```php
$isAlpha = Str::isAlpha('hello'); // true
$isAlpha = Str::isAlpha('hello123'); // false
```

#### isAlnum() - 是否为字母数字
```php
$isAlnum = Str::isAlnum('hello123'); // true
$isAlnum = Str::isAlnum('hello world'); // false
```

#### isHex() - 是否为十六进制
```php
$isHex = Str::isHex('1a2b3c'); // true
$isHex = Str::isHex('1g2h3i'); // false
```

#### isBinary() - 是否为二进制
```php
$isBinary = Str::isBinary('01010101'); // true
$isBinary = Str::isBinary('12345678'); // false
```

#### isJson() - 是否为JSON
```php
$isJson = Str::isJson('{"name":"张三"}'); // true
$isJson = Str::isJson('not json'); // false
```

#### isXml() - 是否为XML
```php
$isXml = Str::isXml('<root>hello</root>'); // true
$isXml = Str::isXml('not xml'); // false
```

#### isSerialized() - 是否为序列化数据
```php
$isSerialized = Str::isSerialized('a:1:{i:0;s:5:"hello";}'); // true
$isSerialized = Str::isSerialized('not serialized'); // false
```

#### isBase64() - 是否为Base64
```php
$isBase64 = Str::isBase64('aGVsbG8='); // true
$isBase64 = Str::isBase64('not base64'); // false
```

### 字符串转换

#### toArray() - 字符串转数组
```php
$array = Str::toArray('hello,world,php', ','); // ['hello', 'world', 'php']
```

#### fromArray() - 数组转字符串
```php
$string = Str::fromArray(['hello', 'world', 'php'], ','); // 'hello,world,php'
```

#### toObject() - 字符串转对象
```php
$object = Str::toObject('{"name":"张三","age":25}'); // stdClass Object ( [name] => 张三 [age] => 25 )
```

#### fromObject() - 对象转字符串
```php
$string = Str::fromObject((object)['name' => '张三', 'age' => 25]); // '{"name":"张三","age":25}'
```

#### toQuery() - 字符串转查询字符串
```php
$query = Str::toQuery(['name' => '张三', 'age' => 25]); // 'name=%E5%BC%A0%E4%B8%89&age=25'
```

#### fromQuery() - 查询字符串转数组
```php
$array = Str::fromQuery('name=%E5%BC%A0%E4%B8%89&age=25'); // ['name' => '张三', 'age' => 25]
```

### 字符串格式化

#### format() - 字符串格式化
```php
$formatted = Str::format('Hello, %s! You are %d years old.', '张三', 25); // 'Hello, 张三! You are 25 years old.'
```

#### template() - 字符串模板渲染
```php
$rendered = Str::template('Hello, {{name}}! Age: {{age}}', ['name' => '张三', 'age' => 25]); // 'Hello, 张三! Age: 25'
```

#### indent() - 字符串缩进
```php
$indented = Str::indent('hello', 4); // '    hello'
```

#### unindent() - 字符串去除缩进
```php
$unindented = Str::unindent('    hello'); // 'hello'
```

### 字符串字符操作

#### first() - 获取字符串首字符
```php
$first = Str::first('hello'); // 'h'
```

#### last() - 获取字符串尾字符
```php
$last = Str::last('hello'); // 'o'
```

#### firstN() - 获取字符串前N个字符
```php
$firstN = Str::firstN('hello', 2); // 'he'
```

#### lastN() - 获取字符串后N个字符
```php
$lastN = Str::lastN('hello', 2); // 'lo'
```

#### removeFirst() - 去除首字符
```php
$removed = Str::removeFirst('hello'); // 'ello'
```

#### removeLast() - 去除尾字符
```php
$removed = Str::removeLast('hello'); // 'hell'
```

#### removeFirstN() - 去除前N个字符
```php
$removed = Str::removeFirstN('hello', 2); // 'llo'
```

#### removeLastN() - 去除后N个字符
```php
$removed = Str::removeLastN('hello', 2); // 'hel'
```

### 字符串统计

#### count() - 统计子串出现次数
```php
$count = Str::count('hello world world', 'world'); // 2
```

#### wordCount() - 统计单词数
```php
$wordCount = Str::wordCount('hello world php'); // 3
```

#### charCount() - 统计字符数
```php
$charCount = Str::charCount('hello'); // 5
```

#### byteLength() - 统计字节长度
```php
$byteLength = Str::byteLength('你好'); // 6（UTF-8编码）
```

### 字符串安全

#### escapeHtml() - 转义HTML特殊字符
```php
$escaped = Str::escapeHtml('<div>hello</div>'); // '&lt;div&gt;hello&lt;/div&gt;'
```

#### escapeSql() - 转义SQL特殊字符
```php
$escaped = Str::escapeSql("O'Reilly"); // "O\'Reilly"
```

#### escapeJs() - 转义JavaScript特殊字符
```php
$escaped = Str::escapeJs("It's a test"); // "It\'s a test"
```

#### escapeRegex() - 转义正则表达式特殊字符
```php
$escaped = Str::escapeRegex('hello.world'); // 'hello\.world'
```

### 字符串比较

#### compare() - 字符串比较
```php
$compare = Str::compare('hello', 'hello'); // 0（相等）
$compare = Str::compare('hello', 'world'); // -15（不相等）
```

#### similarity() - 字符串相似度
```php
$similarity = Str::similarity('hello', 'hello'); // 1.0（完全相同）
$similarity = Str::similarity('hello', 'world'); // 0.2（相似度）
```

#### distance() - 字符串编辑距离
```php
$distance = Str::distance('hello', 'hello'); // 0（相同）
$distance = Str::distance('hello', 'world'); // 4（编辑距离）
```