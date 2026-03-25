# 数组处理

> 提供丰富的数组处理方法，支持多维数组操作、数组排序、过滤、映射等功能。

## 特性
- ✅ 树形结构转换（数组转树、树转数组）
- ✅ 层级结构转换
- ✅ 路径结构转换
- ✅ 常用数组操作（get/set/has/only/except）
- ✅ 数组深度合并
- ✅ 多维数组分组
- ✅ 多维数组统计（count/sum/avg/max/min）
- ✅ 多维数组转JSON/JSON转数组
- ✅ 非递归算法，支持大数据量
- ✅ 支持点语法和数组嵌套键访问

## 核心方法
| 方法名 | 功能描述 | 调用示例 |
|--------|----------|----------|
| [`first()`](#first-数组首元素) | 获取数组第一个元素 | `Arr::first([1, 2, 3])` |
| [`last()`](#last-数组尾元素) | 获取数组最后一个元素 | `Arr::last([1, 2, 3])` |
| [`find()`](#find-查找满足条件的元素) | 查找满足条件的元素 | `Arr::find([1, 2, 3], fn($n) => $n > 1)` |
| [`tree()`](#tree-数组转树形结构) | 数组转树形结构 | `Arr::tree($list, 'id', 'pid')` |
| [`list()`](#list-树形结构转数组) | 树形结构转数组 | `Arr::list($tree)` |
| [`deepMerge()`](#deepMerge-深度合并数组) | 深度合并数组 | `Arr::deepMerge($arr1, $arr2)` |

## 兼容性说明
数组处理模块会自动检测PHP版本，在PHP 8.4+环境下使用原生数组函数以获得最佳性能：

- `array_first()` - 获取数组第一个元素
- `array_last()` - 获取数组最后一个元素
- `array_find()` - 查找满足条件的元素
- `array_find_key()` - 查找满足条件的键名
- `array_any()` - 检查是否存在满足条件的元素
- `array_all()` - 检查是否所有元素都满足条件

> 在PHP 8.4以下版本，模块会使用兼容的实现，确保代码在不同PHP版本下都能正常运行。

## 使用示例

### 树形结构转换

#### tree() / toTree() - 数组转树形结构
```php
use Cdyun\PhpTool\Arr;

$data = [
    ['id' => 1, 'name' => '部门1', 'parent_id' => 0],
    ['id' => 2, 'name' => '部门2', 'parent_id' => 1],
    ['id' => 3, 'name' => '部门3', 'parent_id' => 1],
    ['id' => 4, 'name' => '部门4', 'parent_id' => 2],
    ['id' => 5, 'name' => '部门5', 'parent_id' => 100]
];

// 按指定根节点ID，将扁平化数组转换为树形结构，会过滤掉非指定根节点及子节点的数据
$tree = Arr::toTree($data, 5, 'id', 'parent_id', 'children');
// 输出:
// [
//     [
//         'id' => 5,
//         'name' => '部门5',
//         'parent_id' => 100,
//         'children' => []
//     ]
// ]

// 数组转树形结构
$tree = Arr::tree($data, 'id', 'parent_id', 'children');
// 输出:
// [
//     [
//         'id' => 1,
//         'name' => '部门1',
//         'parent_id' => 0,
//         'children' => [
//             [
//                 'id' => 2,
//                 'name' => '部门2',
//                 'parent_id' => 1,
//                 'children' => [
//                     ['id' => 4, 'name' => '部门4', 'parent_id' => 2, 'children' => []]
//                 ]
//             ],
//             [
//                 'id' => 3,
//                 'name' => '部门3',
//                 'parent_id' => 1,
//                 'children' => []
//             ]
//         ]
//     ],
//     [
//         'id' => 5,
//         'name' => '部门5',
//         'parent_id' => 100,
//         'children' => []
//     ]
// ]
```

#### list() - 树形结构转数组
```php
$flat = Arr::list($tree, 'children');
```

#### level() - 数组转层级结构
```php
$level = Arr::level($data, 'id', 'parent_id', 'level');
// 输出:
// [
//     ['id' => 1, 'name' => '部门1', 'parent_id' => 0, 'level' => 1],
//     ['id' => 2, 'name' => '部门2', 'parent_id' => 1, 'level' => 2],
//     ['id' => 3, 'name' => '部门3', 'parent_id' => 1, 'level' => 2],
//     ['id' => 4, 'name' => '部门4', 'parent_id' => 2, 'level' => 3]
// ]
```

#### path() - 数组转路径结构
```php
$path = Arr::path($data, 'id', 'parent_id', 'name', 'path', '/');
// 输出:
// [
//     ['id' => 1, 'name' => '部门1', 'parent_id' => 0, 'path' => '部门1'],
//     ['id' => 2, 'name' => '部门2', 'parent_id' => 1, 'path' => '部门1/部门2'],
//     ['id' => 3, 'name' => '部门3', 'parent_id' => 1, 'path' => '部门1/部门3'],
//     ['id' => 4, 'name' => '部门4', 'parent_id' => 2, 'path' => '部门1/部门2/部门4']
// ]
```

#### getParentIds() - 获取叶子节点的所有父节点ID
```php
 $arr = [
     ['id' => 1, 'name' => '部门1', 'parent_id' => 0, 'path' => '部门1'],
     ['id' => 2, 'name' => '部门2', 'parent_id' => 1, 'path' => '部门1/部门2'],
     ['id' => 3, 'name' => '部门3', 'parent_id' => 1, 'path' => '部门1/部门3'],
     ['id' => 4, 'name' => '部门4', 'parent_id' => 2, 'path' => '部门1/部门2/部门4']
 ];
$path = Arr::path($arr, 4, 'parent_id');
// 输出的是字符串类型的id:
// ['1','2']
```

### 数组访问和操作

#### deepMerge() - 数组深度合并
```php
use Cdyun\PhpTool\Arr;

$arr1 = [
    'user' => ['name' => '张三', 'age' => 25],
    'settings' => ['theme' => 'dark']
];

$arr2 = [
    'user' => ['age' => 26, 'email' => 'user@example.com'],
    'settings' => ['language' => 'zh-CN']
];

$merged = Arr::deepMerge($arr1, $arr2);
// 输出:
// [
//     'user' => ['name' => '张三', 'age' => 26,'email' => 'user@example.com'],
//     'settings' => ['theme' => 'dark', 'language' => 'zh-CN']
// ]
```

#### get() - 数组获取值（支持点语法）
```php
$value = Arr::get($arr1, 'user.name'); // '张三'
$value = Arr::get($arr1, ['user', 'age']); // 25
$value = Arr::get($arr1, 'user.email', 'default@example.com'); // 'default@example.com'
```

#### set() - 数组设置值
```php
$result = Arr::set($arr1, 'user.age', 26);
```

#### has() - 数组判断是否存在键
```php
$exists = Arr::has($arr1, 'user.name'); // true
$exists = Arr::has($arr1, 'user.email'); // false
```

#### only() - 数组仅保留指定键
```php
$only = Arr::only($arr1, ['user.name', 'user.age']);
// 输出: ['user' => ['name' => '张三', 'age' => 25]]
```

#### except() - 数组排除指定键
```php
$except = Arr::except($array1, ['settings']);
// 输出: ['user' => ['name' => '张三', 'age' => 25]]
```

### 多维数组处理

#### group() - 多维数组分组
```php
use Cdyun\PhpTool\Arr;

$flatArray = [
    ['id' => 1, 'name' => '部门1', 'parent_id' => 0],
    ['id' => 2, 'name' => '部门2', 'parent_id' => 1],
    ['id' => 3, 'name' => '部门3', 'parent_id' => 1],
    ['id' => 4, 'name' => '部门4', 'parent_id' => 2]
];

// 多维数组分组
$grouped = Arr::group($flatArray, 'parent_id');
// 输出:
// [
//     0 => [['id' => 1, 'name' => '部门1', 'parent_id' => 0]],
//     1 => [
//         ['id' => 2, 'name' => '部门2', 'parent_id' => 1],
//         ['id' => 3, 'name' => '部门3', 'parent_id' => 1]
//     ],
//     2 => [['id' => 4, 'name' => '部门4', 'parent_id' => 2]]
// ]
```

#### count() - 多维数组统计
```php
// 多维数组统计
$count = Arr::count($flatArray, 'parent_id');
// 输出: [0 => 1, 1 => 2, 2 => 1]
```

#### sum() - 多维数组求和
```php
$sum = Arr::sum($flatArray, 'id'); // 10
```

#### avg() - 多维数组求平均值
```php
$avg = Arr::avg($flatArray, 'id'); // 2.5
```

#### max() - 多维数组求最大值
```php
$min = Arr::max($flatArray, 'id'); // 4
```

#### min() - 多维数组求最小值
```php
$min = Arr::min($flatArray, 'id'); // 1
```

### PHP 8.4+数组函数

#### first() - 数组首元素

```php
use Cdyun\PhpTool\Arr;

// PHP 8.4+使用原生array_first
$first = Arr::first([1, 2, 3, 4, 5]); // 1
$first = Arr::first([]); // null
```

#### last() - 数组尾元素
```php
// PHP 8.4+使用原生array_last
$last = Arr::last([1, 2, 3, 4, 5]); // 5
$last = Arr::last([]); // null
```

#### find() - 查找满足条件的元素
```php
// PHP 8.4+使用原生array_find
$found = Arr::find([1, 2, 3, 4, 5], fn($n) => $n > 2); // 3
$found = Arr::find([1, 2, 3, 4, 5], fn($n) => $n > 10); // null
```

#### findKey() - 查找满足条件的键名
```php
// PHP 8.4+使用原生array_find_key
$foundKey = Arr::findKey(['a' => 1, 'b' => 2, 'c' => 3], fn($n) => $n > 1); // 'b'
$foundKey = Arr::findKey(['a' => 1, 'b' => 2, 'c' => 3], fn($n) => $n > 10); // null
```

#### any() - 检查是否存在满足条件的元素
```php
// PHP 8.4+使用原生array_any
$hasAny = Arr::any([1, 2, 3, 4, 5], fn($n) => $n > 3); // true
$hasAny = Arr::any([1, 2, 3, 4, 5], fn($n) => $n > 10); // false
```

#### all() - 检查是否所有元素都满足条件
```php
// PHP 8.4+使用原生array_all
$allMatch = Arr::all([1, 2, 3, 4, 5], fn($n) => $n > 0); // true
$allMatch = Arr::all([1, 2, 3, 4, 5], fn($n) => $n > 2); // false
```

### 数组查找和判断

#### map() - 数组映射
```php
$mapped = Arr::map([1, 2, 3, 4, 5], fn($n) => $n * 2); // [2, 4, 6, 8, 10]
```

#### filter() - 数组过滤
```php
$filtered = Arr::filter([1, 2, 3, 4, 5], fn($n) => $n > 2); // [3, 4, 5]
$filtered = Arr::filter([1, 2, 0, null, false]); // [1, 2]（过滤空值）
```

#### reduce() - 数组归约
```php
$sum = Arr::reduce([1, 2, 3, 4, 5], fn($carry, $n) => $carry + $n, 0); // 15
```

#### find() - 查找满足条件的第一个元素的键值
```php
$findVal = Arr::find([1, 2, 3, 4, 5], fn($n) => $n > 3); // 4
$findVal = Arr::find(['a' => 10, 'b' => 20, 'c' => 30], fn($n) => $n > 20); // 30
```

#### findKey() - 查找满足条件的第一个元素的键名
```php
$findKeyVal = Arr::findKey([1, 2, 3, 4, 5], fn($n) => $n > 3); // 3
$findKeyVal = Arr::findKey(['a' => 10, 'b' => 20, 'c' => 30], fn($n) => $n > 20); // 'c'
```

#### some() - 检查是否存在满足条件的元素（别名方法）
```php
$hasSome = Arr::some([1, 2, 3, 4, 5], fn($n) => $n > 3); // true
```

#### every() - 检查是否所有元素都满足条件（别名方法）
```php
$allMatch = Arr::every([1, 2, 3, 4, 5], fn($n) => $n > 0); // true
```

#### contains() - 数组是否包含指定元素
```php
$contains = Arr::contains([1, 2, 3, 4, 5], 3); // true
$contains = Arr::contains([1, 2, 3, 4, 5], '3', false); // true（非严格比较）
$contains = Arr::contains([1, 2, 3, 4, 5], '3', true); // false（严格比较）
```

#### containsKey() - 数组是否包含指定键名
```php
$containsKey = Arr::containsKey(['a' => 1, 'b' => 2], 'a'); // true
```

#### isEmpty() - 数组是否为空
```php
$isEmpty = Arr::isEmpty([]); // true
$isEmpty = Arr::isEmpty([1, 2, 3]); // false
```

#### isAssoc() - 数组是否为关联数组
```php
$isAssoc = Arr::isAssoc(['a' => 1, 'b' => 2]); // true
$isAssoc = Arr::isAssoc([1, 2, 3]); // false
```

#### isIndexed() - 数组是否为索引数组
```php
$isIndexed = Arr::isIndexed([1, 2, 3]); // true
$isIndexed = Arr::isIndexed(['a' => 1, 'b' => 2]); // false
```

### 数组排序

```php
use Cdyun\PhpTool\Arr;

$users = [
    ['id' => 3, 'name' => '张三', 'age' => 25],
    ['id' => 1, 'name' => '李四', 'age' => 30],
    ['id' => 2, 'name' => '王五', 'age' => 28]
];
```

#### sort() - 升序/降序
```php
// 升序
$sorted = Arr::sort($users, 'age', 'asc');
// 输出: 
//  [
//      ['id' => 3, 'name' => '张三', 'age' => 25],
//      ['id' => 2, 'name' => '王五', 'age' => 28],
//      ['id' => 1, 'name' => '李四', 'age' => 30]
//  ]

// 降序
$sorted = Arr::sort($users, 'age', 'desc');
// 输出:
//  [
//      ['id' => 1, 'name' => '李四', 'age' => 30],
//      ['id' => 2, 'name' => '王五', 'age' => 28],
//      ['id' => 3, 'name' => '张三', 'age' => 25]
//  ]
```

#### multiSort() - 多维数组排序
```php
// 先按age升序，age相同时按id降序
$multiSorted = Arr::multiSort($users, ['age', 'id'], ['asc', 'desc']);
```

#### reverse() - 数组反转
```php
$reversed = Arr::reverse([1, 2, 3, 4, 5]); // [5, 4, 3, 2, 1]
$reversed = Arr::reverse(['a' => 1, 'b' => 2], true); // ['b' => 2, 'a' => 1]（保留键名）
```

#### shuffle() - 数组打乱
```php
$shuffled = Arr::shuffle([1, 2, 3, 4, 5]); // 随机打乱顺序
```

### 数组去重

#### unique() - 数组去重
```php
$unique = Arr::unique([1, 2, 2, 3, 3, 3, 4, 4, 4, 4]); // [1, 2, 3, 4]
$unique = Arr::unique([1, '1', 2, '2'], true); // [1, '1', 2, '2]（严格比较）
$unique = Arr::unique([1, '1', 2, '2'], false); // [1, 2]（非严格比较）
```

#### multiUnique() - 多维数组去重
```php
$users = [
    ['id' => 1, 'name' => '张三'],
    ['id' => 2, 'name' => '李四'],
    ['id' => 1, 'name' => '张三']
];
$unique = Arr::multiUnique($users, 'id');
// 输出:
//  [
//      ['id' => 1, 'name' => '张三'],
//      ['id' => 2, 'name' => '李四']
//  ]
```

### 数组分页和切片

#### paginate() - 数组分页
```php
$array = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12];
$page1 = Arr::paginate($array, 1, 5); // [1, 2, 3, 4, 5]
$page2 = Arr::paginate($array, 2, 5); // [6, 7, 8, 9, 10]
$page3 = Arr::paginate($array, 3, 5); // [11, 12]
```

#### slice() - 数组切片
```php
$sliced = Arr::slice([1, 2, 3, 4, 5], 1, 3); // [2, 3, 4]
$sliced = Arr::slice(['a' => 1, 'b' => 2, 'c' => 3, 'd' => 4], 1, 2, true); // ['b' => 2, 'c' => 3]（保留键名）
```

#### chunk() - 数组分割
```php
$chunked = Arr::chunk([1, 2, 3, 4, 5, 6, 7, 8, 9, 10], 3);
// 输出: [[1, 2, 3], [4, 5, 6], [7, 8, 9], [10]]
```

### 数组合并和差集

#### merge() - 数组合并
```php
$merged = Arr::merge([1, 2, 3], [4, 5, 6]); // [1, 2, 3, 4, 5, 6]
```

#### mergeRecursive() - 数组合并（保留键名）
```php
$merged = Arr::mergeRecursive(['a' => 1], ['b' => 2]); // ['a' => 1, 'b' => 2]
```

#### diff() - 数组差集
```php
$diff = Arr::diff([1, 2, 3, 4, 5], [2, 4]); // [1, 3, 5]
```

#### diffKey() - 数组差集（带键名）
```php
$diff = Arr::diffKey(['a' => 1, 'b' => 2, 'c' => 3], ['b' => 2]); // ['a' => 1, 'c' => 3]
```

#### intersect() - 数组交集
```php
$intersect = Arr::intersect([1, 2, 3, 4, 5], [2, 4, 6]); // [2, 4]
```

#### intersectKey() - 数组交集（带键名）
```php
$intersect = Arr::intersectKey(['a' => 1, 'b' => 2, 'c' => 3], ['b' => 2, 'c' => 4]); // ['b' => 2, 'c' => 3]
```

### 数组转换

#### toJson() - 多维数组转JSON
```php
$json = Arr::toJson(['name' => '张三', 'age' => 25]); // '{"name":"张三","age":25}'
```

#### fromJson() - JSON转多维数组
```php
$array = Arr::fromJson('{"name":"张三","age":25}'); // ['name' => '张三', 'age' => 25]
```

#### flatten() - 数组扁平化
```php
$flattened = Arr::flatten([1, [2, [3, [4, 5]]]]); // [1, 2, 3, 4, 5]
```

#### keys() - 数组键名
```php
$keys = Arr::keys(['a' => 1, 'b' => 2, 'c' => 3]); // ['a', 'b', 'c']
```

#### values() - 数组键值
```php
$values = Arr::values(['a' => 1, 'b' => 2, 'c' => 3]); // [1, 2, 3]
```

#### flip() - 键名与键值翻转
```php
$flipped = Arr::flip(['a' => 1, 'b' => 2, 'c' => 3]); // [1 => 'a', 2 => 'b', 3 => 'c']
```

#### column() - 数组列提取
```php
$users = [
    ['id' => 1, 'name' => '张三', 'age' => 25],
    ['id' => 2, 'name' => '李四', 'age' => 30]
];
$names = Arr::column($users, 'name'); // ['张三', '李四']
$indexed = Arr::column($users, 'name', 'id'); // [1 => '张三', 2 => '李四']
```

### 数组键值操作

#### mapKeys() - 数组映射键名
```php
$mapped = Arr::mapKeys(['a' => 1, 'b' => 2], fn($key) => strtoupper($key)); // ['A' => 1, 'B' => 2]
```

#### mapValues() - 数组映射键值
```php
$mapped = Arr::mapValues(['a' => 1, 'b' => 2], fn($value) => $value * 2); // ['a' => 2, 'b' => 4]
```

#### combine() - 数组合并键值
```php
$combined = Arr::combine(['a', 'b', 'c'], [1, 2, 3]); // ['a' => 1, 'b' => 2, 'c' => 3]
```

#### fillKeys() - 数组填充键值
```php
$filled = Arr::fillKeys(['a', 'b', 'c'], 0); // ['a' => 0, 'b' => 0, 'c' => 0]
```

#### fill() - 数组填充
```php
$filled = Arr::fill(0, 5, 0); // [0, 0, 0, 0, 0]
```

### 数组随机操作

#### random() - 数组随机元素
```php
$random = Arr::random([1, 2, 3, 4, 5]); // 随机返回其中一个元素
```

#### randomMany() - 数组随机多个元素
```php
$randomMany = Arr::randomMany([1, 2, 3, 4, 5], 3); // 随机返回3个元素
```

### 数组元素操作

```php
$array = [1, 2, 3, 4, 5];
```

#### shift() - 数组弹出第一个元素
```php
$first = Arr::shift($array); // 1，$array变为[2, 3, 4, 5]
```

#### pop() - 数组弹出最后一个元素
```php
$last = Arr::pop($array); // 5，$array变为[2, 3, 4]
```

#### unshift() - 数组头部添加元素
```php
$count = Arr::unshift($array, 0); // 4，$array变为[0, 2, 3, 4]
```

#### push() - 数组尾部添加元素
```php
$count = Arr::push($array, 5); // 5，$array变为[0, 2, 3, 4, 5]
```

#### remove() - 数组删除指定元素
```php
$removed = Arr::remove([1, 2, 3, 2, 4, 2], 2); // [1, 3, 4]
```

#### removeKey() - 数组删除指定键名
```php
$removed = Arr::removeKey(['a' => 1, 'b' => 2, 'c' => 3], 'b'); // ['a' => 1, 'c' => 3]
```