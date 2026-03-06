# 时间处理

> 提供便捷的时间处理方法，支持时间格式化、计算、比较等功能。

## 特性
- ✅ 时间格式化
- ✅ 时间计算（加法、减法、差值）
- ✅ 常用时间获取（当前时间、今天、昨天、明天）
- ✅ 时区支持
- ✅ 人性化时间显示、日期范围计算

## 核心方法
| 方法名 | 功能描述 | 调用示例 |
|--------|----------|----------|
| [`format()`](#format-格式化时间) | 格式化时间 | `Time::format(time(), 'Y-m-d')` |
| [`now()`](#now-获取当前时间) | 获取当前时间 | `Time::now()` |
| [`today()`](#today-获取今天日期) | 获取今天日期 | `Time::today()` |
| [`yesterday()`](#yesterday-获取昨天日期) | 获取昨天日期 | `Time::yesterday()` |
| [`tomorrow()`](#tomorrow-获取明天日期) | 获取明天日期 | `Time::tomorrow()` |
| [`add()`](#add-时间加法) | 时间加法 | `Time::add(time(), 3600)` |
| [`sub()`](#sub-时间减法) | 时间减法 | `Time::sub(time(), 3600)` |
| [`diff()`](#diff-时间差) | 时间差 | `Time::diff(time(), time() - 3600)` |
| [`diffForHumans()`](#diffforhumans-人性化时间差) | 人性化时间差 | `Time::diffForHumans(time() - 3600)` |
| [`weekStart()`](#weekstart-获取本周开始时间) | 获取本周开始时间 | `Time::weekStart()` |
| [`weekEnd()`](#weekend-获取本周结束时间) | 获取本周结束时间 | `Time::weekEnd()` |
| [`monthStart()`](#monthstart-获取本月开始时间) | 获取本月开始时间 | `Time::monthStart()` |
| [`monthEnd()`](#monthend-获取本月结束时间) | 获取本月结束时间 | `Time::monthEnd()` |

## 使用示例

### 时间格式化

#### format() - 格式化时间
```php
$formatted = Time::format(time(), 'Y-m-d H:i:s'); // '2025-12-26 12:00:00'
$formatted = Time::format(time(), 'Y年m月d日'); // '2025年12月26日'
$formatted = Time::format(1735200000, 'Y-m-d'); // '2025-12-26'
```

#### now() - 获取当前时间
```php
$now = Time::now(); // '2025-12-26 12:00:00'
$now = Time::now('Y-m-d'); // '2025-12-26'
$now = Time::now('H:i:s'); // '12:00:00'
```

#### today() - 获取今天日期
```php
$today = Time::today(); // '2025-12-26'
$today = Time::today('Y-m-d H:i:s'); // '2025-12-26 00:00:00'
```

#### yesterday() - 获取昨天日期
```php
$yesterday = Time::yesterday(); // '2025-12-25'
$yesterday = Time::yesterday('Y-m-d H:i:s'); // '2025-12-25 00:00:00'
```

#### tomorrow() - 获取明天日期
```php
$tomorrow = Time::tomorrow(); // '2025-12-27'
$tomorrow = Time::tomorrow('Y-m-d H:i:s'); // '2025-12-27 00:00:00'
```

### 时间计算
```php
$timestamp = time();
```

#### add() - 时间加法
```php
$newTime = Time::add($timestamp, 3600); // 加1小时
$newTime = Time::add($timestamp, 86400); // 加1天
$newTime = Time::add($timestamp, 604800); // 加1周
```

#### sub() - 时间减法
```php
$newTime = Time::sub($timestamp, 3600); // 减1小时
$newTime = Time::sub($timestamp, 86400); // 减1天
$newTime = Time::sub($timestamp, 604800); // 减1周
```

#### diff() - 时间差
```php
$diff = Time::diff(time(), time() - 3600); // 3600（秒）
$diff = Time::diff(time() - 86400, time()); // 86400（秒）
```

#### diffForHumans() - 人性化时间差
```php
$human = Time::diffForHumans(time() - 60); // '1分钟前'
$human = Time::diffForHumans(time() - 3600); // '1小时前'
$human = Time::diffForHumans(time() - 86400); // '1天前'
$human = Time::diffForHumans(time() - 2592000); // '1个月前'
$human = Time::diffForHumans(time() - 31536000); // '1年前'
$human = Time::diffForHumans(time() + 3600); // '1小时后'
$human = Time::diffForHumans(time() + 86400); // '1天后'
// 指定基准时间的人性化时间差
$human = Time::diffForHumans(time() - 3600, time() - 7200); // '1小时前'
```

### 周日期范围

#### weekStart() - 获取本周开始时间
```php
$weekStart = Time::weekStart(); // 本周一00:00:00的时间戳
$weekStart = Time::weekStart(time()); // 指定时间所在周的开始时间
$weekStartFormatted = Time::format(Time::weekStart(), 'Y-m-d H:i:s'); // '2025-12-22 00:00:00'
```

#### weekEnd() - 获取本周结束时间
```php
$weekEnd = Time::weekEnd(); // 本周日23:59:59的时间戳
$weekEnd = Time::weekEnd(time()); // 指定时间所在周的结束时间
$weekEndFormatted = Time::format(Time::weekEnd(), 'Y-m-d H:i:s'); // '2025-12-28 23:59:59'
```

#### lastWeekStart() - 获取上周开始时间
```php
$lastWeekStart = Time::lastWeekStart(); // 上周一00:00:00的时间戳
$lastWeekStartFormatted = Time::format(Time::lastWeekStart(), 'Y-m-d H:i:s'); // '2025-12-15 00:00:00'
```

#### lastWeekEnd() - 获取上周结束时间
```php
$lastWeekEnd = Time::lastWeekEnd(); // 上周日23:59:59的时间戳
$lastWeekEndFormatted = Time::format(Time::lastWeekEnd(), 'Y-m-d H:i:s'); // '2025-12-21 23:59:59'
```

### 月日期范围

#### monthStart() - 获取本月开始时间
```php
$monthStart = Time::monthStart(); // 本月1日00:00:00的时间戳
$monthStart = Time::monthStart(time()); // 指定时间所在月的开始时间
$monthStartFormatted = Time::format(Time::monthStart(), 'Y-m-d H:i:s'); // '2025-12-01 00:00:00'
```

#### monthEnd() - 获取本月结束时间
```php
$monthEnd = Time::monthEnd(); // 本月最后一天23:59:59的时间戳
$monthEnd = Time::monthEnd(time()); // 指定时间所在月的结束时间
$monthEndFormatted = Time::format(Time::monthEnd(), 'Y-m-d H:i:s'); // '2025-12-31 23:59:59'
```

#### lastMonthStart() - 获取上月开始时间
```php
$lastMonthStart = Time::lastMonthStart(); // 上月1日00:00:00的时间戳
$lastMonthStartFormatted = Time::format(Time::lastMonthStart(), 'Y-m-d H:i:s'); // '2025-11-01 00:00:00'
```

#### lastMonthEnd() - 获取上月结束时间
```php
$lastMonthEnd = Time::lastMonthEnd(); // 上月最后一天23:59:59的时间戳
$lastMonthEndFormatted = Time::format(Time::lastMonthEnd(), 'Y-m-d H:i:s'); // '2025-11-30 23:59:59'
```

### 年日期范围

#### yearStart() - 获取本年开始时间
```php
$yearStart = Time::yearStart(); // 本年1月1日00:00:00的时间戳
$yearStart = Time::yearStart(time()); // 指定时间所在年的开始时间
$yearStartFormatted = Time::format(Time::yearStart(), 'Y-m-d H:i:s'); // '2025-01-01 00:00:00'
```

#### yearEnd() - 获取本年结束时间
```php
$yearEnd = Time::yearEnd(); // 本年12月31日23:59:59的时间戳
$yearEnd = Time::yearEnd(time()); // 指定时间所在年的结束时间
$yearEndFormatted = Time::format(Time::yearEnd(), 'Y-m-d H:i:s'); // '2025-12-31 23:59:59'
```

#### lastYearStart() - 获取上年开始时间
```php
$lastYearStart = Time::lastYearStart(); // 上年1月1日00:00:00的时间戳
$lastYearStartFormatted = Time::format(Time::lastYearStart(), 'Y-m-d H:i:s'); // '2024-01-01 00:00:00'
```

#### lastYearEnd() - 获取上年结束时间
```php
$lastYearEnd = Time::lastYearEnd(); // 上年12月31日23:59:59的时间戳
$lastYearEndFormatted = Time::format(Time::lastYearEnd(), 'Y-m-d H:i:s'); // '2024-12-31 23:59:59'
```

### 时间判断

```php
$timestamp = time();
```

#### between() - 判断是否在某个时间区间内
```php
$inRange = Time::between($timestamp, time() - 3600, time() + 3600); // true
$inRange = Time::between(time() - 7200, time() - 3600, time()); // false
```

#### isToday() - 判断是否是今天
```php
$isToday = Time::isToday($timestamp); // true
$isToday = Time::isToday(time() - 86400); // false
```

#### isYesterday() - 判断是否是昨天
```php
$isYesterday = Time::isYesterday(time() - 86400); // true
$isYesterday = Time::isYesterday(time()); // false
```

#### isTomorrow() - 判断是否是明天
```php
$isTomorrow = Time::isTomorrow(time() + 86400); // true
$isTomorrow = Time::isTomorrow(time()); // false
```

#### isThisWeek() - 判断是否是本周
```php
$isThisWeek = Time::isThisWeek($timestamp); // true
$isThisWeek = Time::isThisWeek(time() - 604800); // false
```

#### isThisMonth() - 判断是否是本月
```php
$isThisMonth = Time::isThisMonth($timestamp); // true
$isThisMonth = Time::isThisMonth(strtotime('2025-11-01')); // false
```

#### isThisYear() - 判断是否是本年
```php
$isThisYear = Time::isThisYear($timestamp); // true
$isThisYear = Time::isThisYear(strtotime('2024-01-01')); // false
```

### 日期信息获取

#### daysInMonth() - 获取某个月的天数
```php
$days = Time::daysInMonth(12); // 31（12月有31天）
$days = Time::daysInMonth(2, 2024); // 29（2024年2月有29天，闰年）
$days = Time::daysInMonth(2, 2023); // 28（2023年2月有28天，平年）
```

#### dayOfWeek() - 获取某天是周几
```php
$weekday = Time::dayOfWeek(time()); // 0-6（0表示周日，1表示周一，以此类推）
$weekday = Time::dayOfWeek(strtotime('2025-12-26')); // 5（周五）
```

#### dayOfWeekName() - 获取某天是周几（中文名称）
```php
$weekdayName = Time::dayOfWeekName(time()); // '周五'
$weekdayName = Time::dayOfWeekName(strtotime('2025-12-28')); // '周日'
```

#### dayOfYear() - 获取某天是本年第几天
```php
$dayOfYear = Time::dayOfYear(time()); // 360（2025年第360天）
$dayOfYear = Time::dayOfYear(strtotime('2025-01-01')); // 1（第1天）
```

#### weekOfYear() - 获取某天是本年第几周
```php
$weekOfYear = Time::weekOfYear(time()); // 52（第52周）
$weekOfYear = Time::weekOfYear(strtotime('2025-01-01')); // 1（第1周）
```

### 年龄计算

#### age() - 计算年龄
```php
$age = Time::age('1990-01-01'); // 35（假设当前是2025年）
$age = Time::age('2000-12-31'); // 24（假设当前是2025年）
$age = Time::age('2010-06-15'); // 15（假设当前是2025年）
```

### 时间戳转换

#### toTimestamp() - 时间字符串转时间戳
```php
$timestamp = Time::toTimestamp('2025-12-26 12:00:00'); // 1735200000
$timestamp = Time::toTimestamp('2025-12-26'); // 1735152000
$timestamp = Time::toTimestamp('now'); // 当前时间戳
$timestamp = Time::toTimestamp('+1 day'); // 明天同一时间的时间戳
```

#### toMillisecond() - 时间戳转毫秒
```php
$millisecond = Time::toMillisecond(time()); // 1735200000000
$millisecond = Time::toMillisecond(1735200000); // 1735200000000
```

#### fromMillisecond() - 毫秒转时间戳
```php
$timestamp = Time::fromMillisecond(1735200000000); // 1735200000
```

#### millisecond() - 获取当前毫秒时间戳
```php
$millisecond = Time::millisecond(); // 当前时间的毫秒时间戳
```

#### microsecond() - 获取当前微秒时间戳
```php
$microsecond = Time::microsecond(); // 当前时间的微秒时间戳
```

#### microtime() - 获取当前时间戳（带微秒）
```php
$microtime = Time::microtime(); // 1735200000.123456
```

### 时区操作

#### timezone() - 获取当前时区
```php
$timezone = Time::timezone(); // 'Asia/Shanghai'（或其他时区）
```

#### setTimezone() - 设置时区
```php
$success = Time::setTimezone('UTC'); // true
$success = Time::setTimezone('America/New_York'); // true

// 设置时区后获取时间
Time::setTimezone('UTC');
$utcTime = Time::now(); // UTC时间

Time::setTimezone('Asia/Shanghai');
$shanghaiTime = Time::now(); // 上海时间
```

## 实际应用场景

```php
// 订单创建时间显示
$createdAt = time() - 3600; // 1小时前创建
$displayTime = Time::diffForHumans($createdAt); // '1小时前'

// 数据统计时间范围
$weekStart = Time::weekStart();
$weekEnd = Time::weekEnd();
// 查询本周数据：WHERE created_at >= $weekStart AND created_at <= $weekEnd

// 用户生日计算
$birthday = '1990-05-15';
$age = Time::age($birthday); // 35岁

// 活动倒计时
$endTime = strtotime('2025-12-31 23:59:59');
$diff = Time::diff(time(), $endTime); // 距离结束的秒数

// 日程安排
$today = Time::today();
$tomorrow = Time::tomorrow();
$weekStart = Time::weekStart();
$weekEnd = Time::weekEnd();

// 数据归档
$lastMonthStart = Time::lastMonthStart();
$lastMonthEnd = Time::lastMonthEnd();
// 归档上月数据：WHERE created_at >= $lastMonthStart AND created_at <= $lastMonthEnd

// 报表生成
$yearStart = Time::yearStart();
$yearEnd = Time::yearEnd();
// 生成本年报表：WHERE created_at >= $yearStart AND created_at <= $yearEnd

// 定时任务检查
if (Time::isToday($taskTime)) {
    // 执行今天的任务
}

// 工作日判断
$weekday = Time::dayOfWeek(time());
if ($weekday >= 1 && $weekday <= 5) {
    // 周一到周五，工作日
} else {
    // 周六周日，休息日
}

// 高精度时间测量
$startTime = Time::microsecond();
// 执行一些代码
$endTime = Time::microsecond();
$duration = $endTime - $startTime; // 微秒
```
