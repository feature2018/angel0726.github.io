---
title: pyspark-DataFrame
date: 2019-08-19 14:37:32
tags:
---

| 命令                   | 说明                                                         |
| ---------------------- | ------------------------------------------------------------ |
| `df.show(n,truncate)`  | `n` - 要显示的行数。<br/>`truncate` - 如果设置为`True`，则默认截断超过20个字符的字符串。 如果设置为大于1的数字，则截断长字符串以截断长度并将其右对齐。 |
| `df.count()`           | 返回`DataFrame`的行数                                        |
| `df.select(col)`       | 投影一组表达式并返回一个新的`DataFrame`。<br>`col`：列名，或者包含列名的列表 |
| `df.filter(condition)` | 使用给定的条件过滤行。`where()`是`filter()`的别名。          |
|                        |                                                              |
| `df.fillna(value)`     | 空值填充                                                     |
| `df.columns`           | 返回`DataFrame`的列名，是一个`list`                          |
| `df.toPandas`          | 转换为`pandas`的`dataframe`                                  |
| `df.describe()`        | 计算数字和字符串列的统计信息。这包括`count`，`mean`，`stddev`，`min`和`max`。 |
|                        |                                                              |
|                        |                                                              |
|                        |                                                              |

# pyspark.sql.functions

```python
from pyspark.sql.functions import * 
```

| 命令     | 说明     |
| -------- | -------- |
| `isnan`  |          |
|          |          |
| `stddev` | 计算方差 |
|          |          |
|          |          |
|          |          |
|          |          |
|          |          |
|          |          |

