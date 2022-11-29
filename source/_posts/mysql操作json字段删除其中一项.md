---
title: mysql操作json字段删除其中一项
categories:
  - mysql
tags:
  - json
mp3: /music/Visions-Acreix.mp3
cover: /img/002211-1666542131a1a3.jpg
date: 2022-11-29 14:41:54
---
## 查询某个数据是否存在于数组

```sql
SELECT
	id,
	jsons
FROM
	table
WHERE
	JSON_CONTAINS(jsons, '"测试"', '$' )= 1
```

## 从数组中删除指定值
```sql
UPDATE table 
SET 
jsons = JSON_REMOVE(jsons, JSON_UNQUOTE(JSON_SEARCH( jsons, 'one', '测试' )))
WHERE JSON_CONTAINS(jsons, '"测试"', '$' )= 1
```

## 关于mysql JSON的函数
```
JSON_ARRAY 生成json数组
JSON_OBJECT 生成json对象
JSON_QUOTE 加"号
JSON_CONTAINS 指定数据是否存在
JSON_CONTAINS_PATH 指定路径是否存在
JSON_EXTRACT 查找所有指定数据
JSON_KEYS 查找所有指定键值
JSON_SEARCH 查找所有指定值的位置
JSON_ARRAY_APPEND  指定位置追加数组元素
JSON_ARRAY_INSERT 指定位置插入数组元素
JSON_INSERT 指定位置插入
JSON_REPLACE 指定位置替换
JSON_SET 指定位置设置
JSON_MERGE 合并
JSON_REMOVE 指定位置移除
JSON_UNQUOTE 去"号
JSON_DEPTH 深度
JSON_LENGTH 长度
JSON_TYPE 类型
JSON_VALID 是否有效json格式
```

## 测试

### JSON_ARRAY
