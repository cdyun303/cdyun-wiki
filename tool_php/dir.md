# 目录文件处理

> 提供丰富的文件目录处理功能。

## 使用示例

##### scanFolder() - 搜索指定路径下的【直系】文件夹
```php
$list = Dir::scanFolder($path);
```

##### getFileContent() - 获取文件内容
```php
$content = Dir::getFileContent($path, $fileName);
```

##### listFileContent() - 获取指定路径文件夹下所有直系文件夹中所有指定文件名的php文件内容
```php
$list = Dir::listFileContent($path, $fileName);
```

##### deleteDirFile() - 清除指定文件夹下文件
```php
$list = Dir::deleteDirFile($dir_name);
```

##### scanFile() - 搜索文件夹下全部文件，指定扩展名，暂时不支持中文文件名
```php
$list = Dir::scanFile($path, $ext);
```

##### scanFileTree() - 搜索文件夹下全部文件返回树形结构，指定扩展名，暂时不支持中文文件名
```php
$list = Dir::scanFileTree($path, $prefix, $ext);
```
