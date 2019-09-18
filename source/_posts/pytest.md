---
title: pytest
date: 2019-09-18 16:32:42
tags: [测试]
categories: python
---

# 目录结构

# 应用

```shell
├── feature        
    ├── in_fc.py             #开发文件
    └── test                 #测试目录
        ├── __init__.py      #子目录需要添加
        └── test_in_fc.py    #测试
```

## in_fc.py文件

```python
def one():
    return 1

def Plus_One(x):
    return x+1
```

## \__init__.py

空

## test_in_fc.py

```python
#!/usr/bin/env python3 -m pytest
# coding=utf-8
import in_fc

def test_one():
    assert in_fc.one() == 1

def test_Plus_One():
    assert in_fc.Plus_One(1) == 2
```

或

```python
#!/usr/bin/env python3 -m pytest
# coding=utf-8
import in_fc

class Test_in_fc:
    def test_one(self):
        assert in_fc.one() == 1
    def test_Plus_One(self):
        assert in_fc.Plus_One(1) == 2
```

## 运行

```shell
/usr/bin/env python3 -m pytest 文件
```

