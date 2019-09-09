---
title: SQL-spark
date: 2019-08-13 19:49:05
tags: [人工智能,分布式系统,数据库]
categories: spark
permalink: spark/SQL-spark.md
---

![æç«SQLæ¶æ](SQL-spark/spark_sql_architecture.jpg)

# [getting started](https://spark-reference-doc-cn.readthedocs.io/zh_CN/latest/programming-guide/sql-guide.html#dataset)

## SparkSession

Spark 中所有功能的入口是 `SparkSession` 类。要创建一个基本的` SparkSession` 对象, 只需要使用 `SparkSession.builder():`

```scala
// scala
import org.apache.spark.sql.SparkSession

val spark = SparkSession
  .builder()
  .appName("Spark SQL basic example")
  .config("spark.some.config.option", "some-value")
  .getOrCreate()
```

```java
// java
import org.apache.spark.sql.SparkSession;

SparkSession spark = SparkSession
  .builder()
  .appName("Java Spark SQL basic example")
  .config("spark.some.config.option", "some-value")
  .getOrCreate();
```

```python
# python
from pyspark.sql import SparkSession

spark = SparkSession \
    .builder \
    .appName("Python Spark SQL basic example") \
    .config("spark.some.config.option", "some-value") \
    .getOrCreate()
```

## 创建 DataFrame

应用程序可以使用 `SparkSession `从一个现有的 `RDD`，`Hive `表或 `Spark` 数据源创建 `DataFrame`。下面基于一个 `JSON` 文件的内容创建一个 `DataFrame`:

```scala
val df = spark.read.json("examples/src/main/resources/people.json")           //scala

import org.apache.spark.sql.Dataset;
import org.apache.spark.sql.Row;
Dataset<Row> df = spark.read().json("examples/src/main/resources/people.json"); //java

df = spark.read.json("examples/src/main/resources/people.json")               //python
```

##  DataFrame 操作

`DataFrame`为 `Scala`,` Java`, `Python` 以及 `R` 语言中的结构化数据操作提供了一种领域特定语言。

| scala                                   | java                                                 | python                                        |
| --------------------------------------- | ---------------------------------------------------- | --------------------------------------------- |
| `df.printSchema()`                      | `df.printSchema();`                                  | `df.printSchema()`                            |
| `df.select("name")`                     | `df.select("name").show();`                          | `df.select("name").show();`                   |
| `df.select($"name", $"age" + 1).show()` | `df.select(col("name"), col("age").plus(1)).show();` | `df.select(df['name'], df['age'] + 1).show()` |
| `df.filter($"age" > 21).show()`         | `df.filter(col("age").gt(21)).show();`               | `df.filter(df['age'] > 21).show()`            |
| `df.groupBy("age").count().show()`      | `df.groupBy("age").count().show()`                   | `df.groupBy("age").count().show()`            |

```scala
/************************** scala*************************/

// This import is needed to use the $-notation
import spark.implicits._
// Print the schema in a tree format
df.printSchema()
// root
// |-- age: long (nullable = true)
// |-- name: string (nullable = true)

// Select only the "name" column
df.select("name").show()
// +-------+
// |   name|
// +-------+
// |Michael|
// |   Andy|
// | Justin|
// +-------+

// Select everybody, but increment the age by 1
df.select($"name", $"age" + 1).show()
// +-------+---------+
// |   name|(age + 1)|
// +-------+---------+
// |Michael|     null|
// |   Andy|       31|
// | Justin|       20|
// +-------+---------+

// Select people older than 21
df.filter($"age" > 21).show()
// +---+----+
// |age|name|
// +---+----+
// | 30|Andy|
// +---+----+

// Count people by age
df.groupBy("age").count().show()
// +----+-----+
// | age|count|
// +----+-----+
// |  19|    1|
// |null|    1|
// |  30|    1|
// +----+-----+
```

```java
/************************** java*************************/

// col("...") is preferable to df.col("...")
import static org.apache.spark.sql.functions.col;

// Print the schema in a tree format
df.printSchema();
// root
// |-- age: long (nullable = true)
// |-- name: string (nullable = true)

// Select only the "name" column
df.select("name").show();
// +-------+
// |   name|
// +-------+
// |Michael|
// |   Andy|
// | Justin|
// +-------+

// Select everybody, but increment the age by 1
df.select(col("name"), col("age").plus(1)).show();
// +-------+---------+
// |   name|(age + 1)|
// +-------+---------+
// |Michael|     null|
// |   Andy|       31|
// | Justin|       20|
// +-------+---------+

// Select people older than 21
df.filter(col("age").gt(21)).show();
// +---+----+
// |age|name|
// +---+----+
// | 30|Andy|
// +---+----+

// Count people by age
df.groupBy("age").count().show();
// +----+-----+
// | age|count|
// +----+-----+
// |  19|    1|
// |null|    1|
// |  30|    1|
// +----+-----+
```

```python
#####################             python                ###################

# spark, df are from the previous example
# Print the schema in a tree format
df.printSchema()
# root
# |-- age: long (nullable = true)
# |-- name: string (nullable = true)

# Select only the "name" column
df.select("name").show()
# +-------+
# |   name|
# +-------+
# |Michael|
# |   Andy|
# | Justin|
# +-------+

# Select everybody, but increment the age by 1
df.select(df['name'], df['age'] + 1).show()
# +-------+---------+
# |   name|(age + 1)|
# +-------+---------+
# |Michael|     null|
# |   Andy|       31|
# | Justin|       20|
# +-------+---------+

# Select people older than 21
df.filter(df['age'] > 21).show()
# +---+----+
# |age|name|
# +---+----+
# | 30|Andy|
# +---+----+

# Count people by age
df.groupBy("age").count().show()
# +----+-----+
# | age|count|
# +----+-----+
# |  19|    1|
# |null|    1|
# |  30|    1|
# +----+-----+
```

## SQL查询

通过SQL访问数据库，返回一个DataFrame的类型

```scala
/***************************   scala   *********************************/

// Register the DataFrame as a SQL temporary view
df.createOrReplaceTempView("people")
val sqlDF = spark.sql("SELECT * FROM people")
sqlDF.show()
```

```java
/***************************   java   *********************************/
import org.apache.spark.sql.Dataset;
import org.apache.spark.sql.Row;

// Register the DataFrame as a SQL temporary view
df.createOrReplaceTempView("people");
Dataset<Row> sqlDF = spark.sql("SELECT * FROM people");
sqlDF.show();
```

```python
#############################   python    ###############################

# Register the DataFrame as a SQL temporary view
df.createOrReplaceTempView("people")
sqlDF = spark.sql("SELECT * FROM people")
sqlDF.show()
```

## 全局临时视图

Spark SQL中的临时视图是**会话范围**的，如果创建它的会话终止，它将消失。如果您希望拥有一个在所有会话之间共享的临时视图并保持活动状态，直到Spark应用程序终止，您可以创建一个全局临时视图。

```scala
/*********************************  scala  *************************************/

// Register the DataFrame as a global temporary view
df.createGlobalTempView("people")

// Global temporary view is tied to a system preserved database `global_temp`
spark.sql("SELECT * FROM global_temp.people").show()
// +----+-------+
// | age|   name|
// +----+-------+
// |null|Michael|
// |  30|   Andy|
// |  19| Justin|
// +----+-------+
```

```java
/*********************************  java  *************************************/

// Register the DataFrame as a global temporary view
df.createGlobalTempView("people");

// Global temporary view is tied to a system preserved database `global_temp`
spark.sql("SELECT * FROM global_temp.people").show();
// +----+-------+
// | age|   name|
// +----+-------+
// |null|Michael|
// |  30|   Andy|
// |  19| Justin|
// +----+-------+
```

```python
###############################   python   ################################

# Register the DataFrame as a global temporary view
df.createGlobalTempView("people")

# Global temporary view is tied to a system preserved database `global_temp`
spark.sql("SELECT * FROM global_temp.people").show()
# +----+-------+
# | age|   name|
# +----+-------+
# |null|Michael|
# |  30|   Andy|
# |  19| Justin|
# +----+-------+
```

## 创建dataset

`Dataset`是特定域对象中的强类型集合，它可以使用函数或者相关操作并行地进行转换等操作。每个`Dataset`都有一个称为`DataFrame`的非类型化的视图，这个视图是行的数据集。上面的定义看起来和`RDD`的定义类似，`DataSet`和`RDD`主要的区别是：`DataSet`是特定域的对象集合；然而`RDD`是任何对象的集合。`DataSet`的`API`总是强类型的；而且可以利用这些模式进行优化，然而`RDD`却不行。`DataFrame`是特殊的`Dataset`，它在编译时不会对模式进行检测。在未来版本的Spark，`Dataset`将会替代`RDD`成为我们开发编程使用的`API`（**注意，`RDD`并不是会被取消，而是会作为底层的`API`提供给用户使用**）。

```scala
//   scala
// Note: Case classes in Scala 2.10 can support only up to 22 fields. To work around this limit,
// you can use custom classes that implement the Product interface
case class Person(name: String, age: Long)

// Encoders are created for case classes
val caseClassDS = Seq(Person("Andy", 32)).toDS()
caseClassDS.show()
// +----+---+
// |name|age|
// +----+---+
// |Andy| 32|
// +----+---+

// Encoders for most common types are automatically provided by importing spark.implicits._
val primitiveDS = Seq(1, 2, 3).toDS()
primitiveDS.map(_ + 1).collect() // Returns: Array(2, 3, 4)

// DataFrames can be converted to a Dataset by providing a class. Mapping will be done by name
val path = "examples/src/main/resources/people.json"
val peopleDS = spark.read.json(path).as[Person]
peopleDS.show()
// +----+-------+
// | age|   name|
// +----+-------+
// |null|Michael|
// |  30|   Andy|
// |  19| Justin|
// +----+-------+
```

```java
// java

import java.util.Arrays;
import java.util.Collections;
import java.io.Serializable;

import org.apache.spark.api.java.function.MapFunction;
import org.apache.spark.sql.Dataset;
import org.apache.spark.sql.Row;
import org.apache.spark.sql.Encoder;
import org.apache.spark.sql.Encoders;

public static class Person implements Serializable {
  private String name;
  private int age;

  public String getName() {
    return name;
  }

  public void setName(String name) {
    this.name = name;
  }

  public int getAge() {
    return age;
  }

  public void setAge(int age) {
    this.age = age;
  }
}

// Create an instance of a Bean class
Person person = new Person();
person.setName("Andy");
person.setAge(32);

// Encoders are created for Java beans
Encoder<Person> personEncoder = Encoders.bean(Person.class);
Dataset<Person> javaBeanDS = spark.createDataset(
  Collections.singletonList(person),
  personEncoder
);
javaBeanDS.show();
// +---+----+
// |age|name|
// +---+----+
// | 32|Andy|
// +---+----+

// Encoders for most common types are provided in class Encoders
Encoder<Integer> integerEncoder = Encoders.INT();
Dataset<Integer> primitiveDS = spark.createDataset(Arrays.asList(1, 2, 3), integerEncoder);
Dataset<Integer> transformedDS = primitiveDS.map(
    (MapFunction<Integer, Integer>) value -> value + 1,
    integerEncoder);
transformedDS.collect(); // Returns [2, 3, 4]

// DataFrames can be converted to a Dataset by providing a class. Mapping based on name
String path = "examples/src/main/resources/people.json";
Dataset<Person> peopleDS = spark.read().json(path).as(personEncoder);
peopleDS.show();
// +----+-------+
// | age|   name|
// +----+-------+
// |null|Michael|
// |  30|   Andy|
// |  19| Justin|
// +----+-------+
```

## [与RDD互相转换](https://spark-reference-doc-cn.readthedocs.io/zh_CN/latest/programming-guide/sql-guide.html#rdd)

Spark SQL 支持两种不同的方法将RDDs 转换成 Datasets.

**??????????????????????????????????????????**

## [聚合函数](https://spark-reference-doc-cn.readthedocs.io/zh_CN/latest/programming-guide/sql-guide.html#id4)

DataFrame可以使用聚合函数，例如count()、max()等

### 自定义聚合函数

使用`UserDefinedAggregateFunction a`自定义聚合函数。

```scala

```

## 

