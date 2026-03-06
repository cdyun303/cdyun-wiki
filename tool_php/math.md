# 数学计算

> 提供常用的数学计算方法，支持精确计算、单位转换等功能。

## 特性
- ✅ 高精度计算（使用bcmath扩展）
- ✅ 支持金融计算（折扣、税费、利息）
- ✅ 支持统计分析（平均数、中位数、标准差）
- ✅ 支持幂运算、平方根等数学操作
- ✅ 结果保留任意小数位数
- ✅ 兼容PHP8.3+特性

## 核心方法
| 方法名 | 功能描述 | 调用示例 |
|--------|----------|----------|
| [`add()`](#add-高精度加法) | 高精度加法 | `Math::add('1.1', '2.2')` |
| [`sub()`](#sub-高精度减法) | 高精度减法 | `Math::sub('3.3', '1.1')` |
| [`mul()`](#mul-高精度乘法) | 高精度乘法 | `Math::mul('2.5', '4')` |
| [`div()`](#div-高精度除法) | 高精度除法 | `Math::div('10', '3')` |
| [`average()`](#average-平均值计算) | 平均数 | `Math::average([1, 2, 3, 4, 5])` |
| [`median()`](#median-计算中位数) | 中位数 | `Math::median([1, 2, 3, 4, 5])` |
| [`discount()`](#discount-折扣计算) | 折扣计算 | `Math::discount('100', '0.2')` |
| [`tax()`](#tax-税费计算) | 税费计算 | `Math::tax('100', '0.13')` |

## 使用示例

### 基础运算

#### add() - 高精度加法
```php
$sum = Math::add(0.1, 0.2); // 0.3（而不是0.30000000000000004）
$sum = Math::add('1.1', '2.2', 2); // 3.30（保留2位小数）
```

#### sub() - 高精度减法
```php
$diff = Math::sub(0.3, 0.1); // 0.2
$diff = Math::sub('5.5', '2.2', 2); // 3.30
```

#### mul() - 高精度乘法
```php
$product = Math::mul(0.1, 0.2); // 0.02
$product = Math::mul('1.5', '2.5', 2); // 3.75
```

#### div() - 高精度除法
```php
$quotient = Math::div(0.3, 0.1); // 3
$quotient = Math::div('10', '3', 2); // 3.33
```

#### mod() - 取模运算
```php
$mod = Math::mod(10, 3); // 1
$mod = Math::mod('10.5', '3'); // 1.5
```

#### pow() - 幂运算
```php
$pow = Math::pow(2, 10); // 1024
$pow = Math::pow('2.5', 3, 2); // 15.62
```

#### sqrt() - 平方根运算
```php
$sqrt = Math::sqrt(16); // 4
$sqrt = Math::sqrt('2', 4); // 1.4142
```

### 取整运算

#### round() - 四舍五入
```php
$rounded = Math::round(3.14159, 2); // 3.14
$rounded = Math::round(3.5, 0); // 4
```

#### ceil() - 向上取整
```php
$ceil = Math::ceil(3.2); // 4
$ceil = Math::ceil(3.8, 1); // 3.8
$ceil = Math::ceil('3.21', 1); // 3.3
```

#### floor() - 向下取整
```php
$floor = Math::floor(3.8); // 3
$floor = Math::floor(3.2, 1); // 3.2
$floor = Math::floor('3.89', 1); // 3.8
```

### 比较运算

#### compare() - 比较两个数的大小
```php
$result = Math::compare(5, 3); // 1（5 > 3）
$result = Math::compare(3, 5); // -1（3 < 5）
$result = Math::compare(5, 5); // 0（相等）
```

#### equal() - 判断两个数是否相等
```php
$equal = Math::equal(0.1 + 0.2, 0.3); // true（解决浮点数比较问题）
$equal = Math::equal('1.000', '1.00', 2); // true（保留2位小数比较）
```

### 格式化

#### format() - 格式化数字
```php
$formatted = Math::format(1234567.89, 2, true); // 1,234,567.89（带千分位）
$formatted = Math::format(1234567.89, 2, false); // 1234567.89（不带千分位）
$formatted = Math::format('1234567.89123', 3, true); // 1,234,567.891
```

### 三角函数

#### sin() - 正弦函数
```php
$sin = Math::sin(Math::deg2rad(30)); // 0.5（30度的正弦值）
$sin = Math::sin(3.14159 / 2); // 1（π/2的正弦值）
```

#### cos() - 余弦函数
```php
$cos = Math::cos(Math::deg2rad(60)); // 0.5（60度的余弦值）
$cos = Math::cos(0); // 1（0度的余弦值）
```

#### tan() - 正切函数
```php
$tan = Math::tan(Math::deg2rad(45)); // 1（45度的正切值）
$tan = Math::tan(3.14159 / 4); // 1（π/4的正切值）
```

#### asin() - 反正弦函数
```php
$asin = Math::asin(1); // 1.5708（π/2）
$asin = Math::asin(0.5); // 0.5236（π/6）
```

#### acos() - 反余弦函数
```php
$acos = Math::acos(0); // 1.5708（π/2）
$acos = Math::acos(0.5); // 1.0472（π/3）
```

#### atan() - 反正切函数
```php
$atan = Math::atan(1); // 0.7854（π/4）
$atan = Math::atan(0); // 0
```

### 对数运算

#### ln() - 自然对数（以e为底）
```php
$ln = Math::ln(Math::exp(1)); // 1
$ln = Math::ln(2.71828); // 1
```

#### log10() - 常用对数（以10为底）
```php
$log10 = Math::log10(100); // 2
$log10 = Math::log10(1000); // 3
```

#### log() - 自定义底数对数
```php
$log = Math::log(8, 2); // 3（2的3次方等于8）
$log = Math::log(100, 10); // 2（10的2次方等于100）
```

### 角度转换

#### rad2deg() - 弧度转角度
```php
$deg = Math::rad2deg(3.14159); // 180（π弧度 = 180度）
$deg = Math::rad2deg(1.5708); // 90（π/2弧度 = 90度）
```

#### deg2rad() - 角度转弧度
```php
$rad = Math::deg2rad(180); // 3.14159（180度 = π弧度）
$rad = Math::deg2rad(90); // 1.5708（90度 = π/2弧度）
```

### 数值操作

#### abs() - 绝对值
```php
$abs = Math::abs(-10); // 10
$abs = Math::abs(10); // 10
$abs = Math::abs('-5.5'); // 5.5
```

#### factorial() - 阶乘
```php
$factorial = Math::factorial(5); // 120（5! = 5×4×3×2×1）
$factorial = Math::factorial(0); // 1（0! = 1）
```

#### gcd() - 最大公约数
```php
$gcd = Math::gcd(12, 18); // 6
$gcd = Math::gcd(24, 36); // 12
```

#### lcm() - 最小公倍数
```php
$lcm = Math::lcm(4, 6); // 12
$lcm = Math::lcm(3, 5); // 15
```

### 金融计算

#### percentage() - 百分比计算
```php
$percentage = Math::percentage(25, 100); // 25（25占100的25%）
$percentage = Math::percentage('30', '150', 2); // 20.00
```

#### discount() - 折扣计算
```php
$discounted = Math::discount(100, 0.8); // 80（打8折）
$discounted = Math::discount('200', '0.7', 2); // 140.00（打7折）
```

#### tax() - 税费计算
```php
$tax = Math::tax(100, 0.1); // 10（100的10%税额）
$tax = Math::tax('500', '0.13', 2); // 65.00（500的13%税额）
```

#### taxIncluded() - 含税金额计算
```php
$taxIncluded = Math::taxIncluded(100, 0.1); // 110（100 + 10%税）
$taxIncluded = Math::taxIncluded('500', '0.13', 2); // 565.00
```

#### taxExcluded() - 不含税金额计算
```php
$taxExcluded = Math::taxExcluded(110, 0.1); // 100（110 / 1.1）
$taxExcluded = Math::taxExcluded('565', '0.13', 2); // 500.00
```

#### simpleInterest() - 简单利息计算
```php
$simpleInterest = Math::simpleInterest(1000, 0.05, 2); // 100（1000本金，5%年利率，2年）
$simpleInterest = Math::simpleInterest('5000', '0.04', 3, 2); // 600.00
```

#### compoundInterest() - 复利计算
```php
$compoundInterest = Math::compoundInterest(1000, 0.05, 2); // 1102.5（1000本金，5%年利率，2年复利）
$compoundInterest = Math::compoundInterest('5000', '0.04', 3, 2); // 5624.32
```

### 随机数生成

#### random() - 生成指定范围内的随机数
```php
$random = Math::random(1, 100); // 1-100之间的随机整数
$random = Math::random('1.5', '5.5', 2); // 1.50-5.50之间的随机数（保留2位小数）
```

### 范围检查

#### inRange() - 数值范围检查
```php
$inRange = Math::inRange(5, 1, 10); // true（5在1-10范围内）
$inRange = Math::inRange(15, 1, 10); // false（15不在1-10范围内）
```

#### clamp() - 限制数值范围
```php
$clamped = Math::clamp(5, 1, 10); // 5（在范围内，保持不变）
$clamped = Math::clamp(15, 1, 10); // 10（超出最大值，限制为10）
$clamped = Math::clamp(-5, 1, 10); // 1（小于最小值，限制为1）
$clamped = Math::clamp('5.5', '1.0', '10.0', 1); // 5.5
```

### 数值判断

#### isPositive() - 判断是否为正数
```php
$isPositive = Math::isPositive(10); // true
$isPositive = Math::isPositive(-5); // false
$isPositive = Math::isPositive(0); // false
```

#### isNegative() - 判断是否为负数
```php
$isNegative = Math::isNegative(-5); // true
$isNegative = Math::isNegative(10); // false
$isNegative = Math::isNegative(0); // false
```

#### isZero() - 判断是否为零
```php
$isZero = Math::isZero(0); // true
$isZero = Math::isZero(0.0000000001, 10); // true（保留10位小数比较）
$isZero = Math::isZero(1); // false
```

#### isEven() - 判断是否为偶数
```php
$isEven = Math::isEven(4); // true
$isEven = Math::isEven(5); // false
```

#### isOdd() - 判断是否为奇数
```php
$isOdd = Math::isOdd(5); // true
$isOdd = Math::isOdd(4); // false
```

#### isPrime() - 判断是否为质数
```php
$isPrime = Math::isPrime(7); // true
$isPrime = Math::isPrime(4); // false
$isPrime = Math::isPrime(2); // true
$isPrime = Math::isPrime(1); // false
```

#### isValid() - 判断数值是否有效
```php
$isValid = Math::isValid(123); // true
$isValid = Math::isValid('123.45'); // true
$isValid = Math::isValid('abc'); // false
$isValid = Math::isValid(INF); // false（无穷大）
$isValid = Math::isValid(NAN); // false（非数字）
```

### 插值运算

#### lerp() - 线性插值
```php
$lerp = Math::lerp(0, 10, 0.5); // 5（0和10的中点）
$lerp = Math::lerp(0, 10, 0.25); // 2.5（0和10的25%位置）
$lerp = Math::lerp('0', '100', '0.75', 1); // 75.0
```

### 统计分析

#### average() - 平均值计算
```php
$avg = Math::average([1, 2, 3, 4, 5]); // 3
$avg = Math::average([1.5, 2.5, 3.5], 2); // 2.50
```

#### median() - 中位数计算
```php
$median = Math::median([1, 2, 3, 4, 5]); // 3
$median = Math::median([1, 2, 3, 4]); // 2.5（2和3的平均值）
$median = Math::median(['1.5', '2.5', '3.5'], 2); // 2.50
```

#### mode() - 众数计算
```php
$mode = Math::mode([1, 2, 2, 3, 3, 3]); // 3（出现次数最多）
$mode = Math::mode([1, 2, 3]); // 1（多个众数时返回第一个）
```

#### standardDeviation() - 标准差计算
```php
$stdDev = Math::standardDeviation([1, 2, 3, 4, 5]); // 1.414
$stdDev = Math::standardDeviation([10, 20, 30], 2); // 10.00
```

## 实际应用场景

```php
// 电商订单金额计算
$subtotal = Math::add('99.99', '49.99'); // 149.98（商品小计）
$discount = Math::discount($subtotal, '0.9'); // 134.98（打9折）
$tax = Math::tax($discount, '0.13'); // 17.55（13%税）
$total = Math::add($discount, $tax, 2); // 152.53（总金额）

// 贷款利息计算
$principal = 100000; // 本金10万
$rate = 0.05; // 年利率5%
$years = 5; // 5年
$simpleInterest = Math::simpleInterest($principal, $rate, $years); // 25000（简单利息）
$compoundInterest = Math::compoundInterest($principal, $rate, $years); // 27628.16（复利）

// 数据分析
$scores = [85, 92, 78, 90, 88, 95, 82];
$avg = Math::average($scores, 2); // 87.14（平均分）
$median = Math::median($scores, 2); // 88.00（中位数）
$stdDev = Math::standardDeviation($scores, 2); // 5.67（标准差）

// 价格范围检查
$price = 99.99;
$minPrice = 50;
$maxPrice = 100;
if (Math::inRange($price, $minPrice, $maxPrice)) {
    echo '价格在合理范围内';
}

// 数值格式化显示
$amount = 1234567.89123;
$formatted = Math::format($amount, 2, true); // 1,234,567.89
```