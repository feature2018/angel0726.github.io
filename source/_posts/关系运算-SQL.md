---
title: 关系运算-SQL
date: 2019-07-31 11:05:24
tags: [数据库,编程语言]
categories: SQL
---

# 集合运算

![数据说明](关系运算-SQL/1564988154852.png)

<!--more-->

## 并

![1564974696180](关系运算-SQL/1564974696180.png)

```sql
Select * from R Union Select * from S;
```

## 差

![1564974788006](关系运算-SQL/1564974788006.png)

```sql
Select * from R Except Select * from S;
```

## 交

![1564974826998](关系运算-SQL/1564974826998.png)

```sql
Select * from R Intersect Select * from S
```



## 笛卡尔积

![1565058855783](关系运算-SQL/1565058855783.png)

```sql
Select * from R,S
```



# 关系运算

## 选择

```sql
SELECT R.学号，R.课程名,R.分数 from R WHERE 分数>85
```

![1564989251630](关系运算-SQL/1564989251630.png)

## 投影

```sql
SELECT 课程名 FROM R;
```

![1564989369086](关系运算-SQL/1564989369086.png)

## 连接

从关系R和关系S的广义笛卡儿积中选取满足给定条件的元组组成新的关系称为R和S的连接

### 自然连接

给定一个关系R和关系S，R与S的等值连接运算结果也是一个关系，记作 $R⋈S$ ，它由关系R和关系S的笛卡尔积中，选取R与S的笛卡尔积中选取相同属性组B上值相等的元组组成。 

```sql
SELECT * from R natual join S
```

![1565060913297](关系运算-SQL/1565060913297.png)

### $\theta$连接

给定一个关系R 和关系S，R 与S 的 $θ$ 连接运算结果也是一个关系，记作$R\underset{A\theta B}{\bowtie} S$，它由关系R和关系S的笛卡尔积中，选取R中属性A与S中属性E之间满足 $θ$ 条件的元组组成。 

```sql
SELECT * from R 
join
SELECT * from S
on R.B<S.H
```

![1565060112787](关系运算-SQL/1565060112787.png)

### 等值连接

给定一个关系R和关系S，R与S的等值连接运算结果也是一个关系，记作$R\underset{A= B}{\bowtie} S$，它由关系R和关系S的笛卡尔积中，选取R中属性A与S中属性B上值相等的元组组成。 

```shell
SELECT * from R 
join
SELECT * from S
on R.B=S.H
```

![1565060172932](关系运算-SQL/1565060172932.png)

### 外连接

两个关系R与S进行连接时，如果关系R(或S)中的元组在S（或R）中找不到相匹配的元组，则为了避免该元组信息丢失，从而将该元组与S（或R）中假定存在的全为空值的元组形成连接，放置在结果关系中，这种连接称之为外连接（Outer Join）

```sql
select * from R left outer join S;
select * from R right outer join S;
select * from R full outer join S;
```

![1565063996276](关系运算-SQL/1565063996276.png)

![1565064351620](关系运算-SQL/1565064351620.png)

## 除

给定关系R (X， Y) 和S (Y， Z)， 其中X， Y， Z为属性组。R中的Y与S中的Y出自相同的域集。R与S的除运算得到一个新的关系P(X)。其中P(X)与S(Y)组成的元组都在R(X,Y)中。
$$
P(X)=R(X,Y) \div S(Y,Z)
$$

```sql
SELECT DISTINCT R.X FROM R  R1
WHERE NOT EXISTS 
(	
    SELECT S.Y FROM S 
    WHERE NOT EXISTS 
    (
        SELECT * FROM R R2 
        where R1.X=R2.X and R2.Y=S.Y
    )
) 
```



![1564990536278](关系运算-SQL/1564990536278.png)

### 习题

![1564994840753](关系运算-SQL/1564994840753.png)

![1564994851980](关系运算-SQL/1564994851980.png)

![1564994863174](关系运算-SQL/1564994863174.png)

- 求至少选择了C001和C003两门课程的学生学号

  ```sql
  select distinct sno from sc A
  where not exists
  (
  	select * from course B where cno in ('C002','C003') and not exists
      (
      	select * from sc C where A.sno=C.sno and B.cno=C.cno
      )
  )
  ```

  