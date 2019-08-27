---
title: python
date: 2019-08-15 14:27:07
tags: [语言]
categories: python
---





# 基本

| 命令                | 说明                          |
| ------------------- | ----------------------------- |
|                     |                               |
| `max(num,key=func)` | 按照`func`返回`num`中的最大值 |
|                     |                               |
|                     |                               |
|                     |                               |
|                     |                               |
|                     |                               |
|                     |                               |
|                     |                               |



# sys

|             |      |
| ----------- | ---- |
| getsizeof() |      |
|             |      |
|             |      |
|             |      |
|             |      |
|             |      |
|             |      |
|             |      |
|             |      |



# [matplotlib](https://matplotlib.org/index.html)

https://serverpoolauth.ops.ctripcorp.com





# numpy

| 命令                                      | 说明                                           |
| ----------------------------------------- | ---------------------------------------------- |
| `random.randint(start,ene,size)`          | `start`与`end`：取值范围<br>`size`：数组的容量 |
| `np.logical_and(x1, x2, *args, **kwargs)` | 逻辑与                                         |
| `np.logical_or(x1, x2, *args, **kwargs)`  | 逻辑或                                         |
| `np.logical_not(x, *args, **kwargs)`      | 逻辑非                                         |
|                                           |                                                |
|                                           |                                                |
|                                           |                                                |
|                                           |                                                |
|                                           |                                                |



# [pandas](https://pandas.pydata.org/)

## Dataframe

| 命令                           | 说明                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| `df.iloc[]`                    | 指定行                                                       |
| `df(df.b.isin([5,13]))`        | 删除`b`列包含`5、13`的列                                     |
| `df['add_column']=1`           | `df`添加列`add_column`                                       |
| `df.drop()`                    | 删除行或者列<br>`labels`：删除的行或者列名<br>`axis`：行->0；列->1<br>`index` ：直接指定要删除的行<br/>`columns `：直接指定要删除的列<br/>`inplace=False`：默认该删除操作不改变原数据，而是返回一个执行删除操作后的新`dataframe`；<br/>`inplace=True`：则会直接在原数据上进行删除操作，删除后无法返回。 |
| `df.dropna()`                  | 删除空行<br>`axis`：0-行操作（默认），1-列操作 <br/>`how`：`any`-只要有空值就删除（默认），`all`-全部为空值才删除 <br/>`inplace`：`False`-返回新的数据集（默认），`True`-在愿数据集上操作 |
| `df.rename()`                  | `df.rename(columns={'A':'a', 'B':'b', 'C':'c'}, inplace = True)`<br>将列名修改为`['a','b','c'] |
| `df.columns= ['a','b','c']`    | 将列名修改为`['a','b','c']`                                  |
| `df.reset_index(列名,inplace)` | 索引转化为列<br>列名：可以有，可以没有。多索引时，可以指定索引<br>`inplace`：替换原`DataFrame` |
| `df.set_index(列名)`           | 列转化为索引                                                 |
| `df.T`                         | `DataFrame`转置                                              |
| `df.merge()`                   | 类似于数据库的`join`,返回`DataFrame`                         |
| `df['列名'].tolist()`          | 将列转换为`list`                                             |

# 其他

断言 assert