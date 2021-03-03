# SQL Style Guide

## General 一般原则

### Do 应该做的事情

* 使用一致的、描述性的名称。
* 合理地使用空格和缩进来增强可读性。
* 存储符合 [ISO-8601][iso-8601] 标准的日期格式（`YYYY-MM-DD HH:MM:SS.SSSSS`）。
* 为了提高可移植性，最好仅使用标准 SQL 函数而不是特定供应商的函数。
* 保证代码简洁明了、没有多余的 SQL —— 比如非必要的引号或括号，或者可以推导出的 `WHERE` 子句。
* 必要时在 SQL 代码中加入注释。优先使用 C 语言式的以 `/*` 开始以 `*/` 结束的块注释，或使用以 `--` 开始的行注释，并在末尾换行。

```sql
SELECT file_hash  -- stored ssdeep hash
  FROM file_system
 WHERE file_name = '.vimrc';
```

```sql
/* Updating the file record after writing to the file */
UPDATE file_system
   SET file_modified_date = '1980-02-22 13:19:01.00000',
       file_size = 209732
 WHERE file_name = '.vimrc';
```

### Avoid 应避免的事情

* 驼峰命名法 —— 它不适合快速扫读

  [「stackoverflow」is-there-a-naming-convention-for-mysql](https://stackoverflow.com/questions/7899200/is-there-a-naming-convention-for-mysql)

* 描述性的前缀或匈牙利命名法比如 `sp_` 或 `tbl`。

* 复数形式 —— 尽量使用更自然的集合术语。比如，用“staff”替代“employees”，或用“people”替代“individuals”。

* 被引号包裹的标识符（quoted identifier）—— 如果你必须使用这样的标识符，最好坚持用 SQL92 的双引号来提高可移植性（你可能需要配置你的 SQL 服务器以支持此特性，具体取决于供应商）。

* 面向对象编程的原则不该应用到 SQL 或数据库结构上。

## Naming conventions 命名惯例

### General 一般原则

* 保证名字独一无二且不是[保留字][reserved-keywords]。
* 保证名字长度不超过 30 个字节 —— 实际上，如果你不使用多字节字符集，就是 30 个字符。
* 名字要以字母开头，不能以下划线结尾。
* 只在名字中使用字母、数字和下划线。
* 不要在名字中出现连续下划线 —— 这样很难辨认。
* 在名字中需要空格的地方用下划线代替（`first name` 变为 `first_name`）。
* 尽量避免使用缩写词。使用时一定确定这个缩写简明易懂。

```sql
SELECT first_name
  FROM staff;
```

### Tables 表名

* 使用集合名称，或在不那么理想的情况下使用复数形式。如 `staff`（建议使用）和 `employees`。
* 不要使用类似 `tbl` 或其他的描述性的前缀或匈牙利命名法。
* 表不应该同它的列同名，反之亦然。
* 尽量避免连接两个表的名字作为关系表（relationship table）的名字。与其使用 `cars_mechanics` 做表名不如使用 `services`。

### Columns 列名

* 总是使用单数形式。
* 避免直接使用 `id` 做表的主标识符。
* 避免列名和表名同名，反之亦然。
* 总是使用小写字母，除非是特殊情况，如专有名词。

### Aliasing or correlations 别名与关联名

* 别名应该与它们所指的对象或表达式相关联。
* 一般来说，关联名应该由对象名中每一个单词的首字母组成。
* 如果已经有相同的关联名了，那么在关联名后加一个数字。
* 总是加上 `AS` 关键字，因为这样的明确声明易于阅读。
* 为计算出的数据（`SUM()` 或 `AVG()`）命名时，用一个将这条数据存在表中时会使用的列名。

```sql
SELECT first_name AS fn
  FROM staff AS s1
  JOIN students AS s2
    ON s2.mentor_id = s1.staff_num;
```

```sql
SELECT SUM(s.monitor_tally) AS monitor_total
  FROM staff AS s;
```

### Stored procedures 存储过程名

* 名字一定要包含动词。
* 不要附加 `sp_` 或任何其他这样的描述性的前缀或使用匈牙利表示法。

### Uniform suffix 统一的后缀

下列后缀有统一的意义，能保证 SQL 代码更容易理解。在合适的时候使用正确的后缀。

* `_id` —— 独一无二的标识符，如主键。
* `_status` —— 标志值或任何表示状态的值，比如 `publication_status`。
* `_total` —— 总和或某些值的和。
* `_num` —— 表示该字段包含数值。
* `_name` —— 表示名字，例如 `first_name`。
* `_seq` —— 包含一系列值。
* `_date` —— 表示该列包含日期。
* `_tally` —— 计数值。
* `_size` —— 大小，如文件大小或服装大小。
* `_addr` —— 地址，有形的或无形的，如 `ip_addr`

## Query syntax 查询语句

### Reserved words 保留字

关键字总是大写，如 `SELECT` 和 `WHERE`。

最好使用关键字的全称而不是简写，用 `ABSOLUTE` 而不用 `ABS`。

当标准 ANSI SQL 关键字能完成相同的事情时，不要使用数据库服务器特定的关键字，这样能增强可移植性。

```sql
SELECT model_num
  FROM phones AS p
 WHERE p.release_date > '2014-09-30';
```

### White space 空白字符

正确地使用空白字符对清晰的代码十分重要。不要把代码堆在一起或移除自然语言中的空格。

#### Spaces 空格

用空格使根关键字都结束在同一列上。在代码中间形成一个从上到下的“川流”，这样帮助读者快速扫视代码并将关键字和实现细节分开。川流在排版时应该避免，但是对阅读 SQL 语句是有帮助的。

```sql
(SELECT f.species_name,
        AVG(f.height) AS average_height, AVG(f.diameter) AS average_diameter
   FROM flora AS f
  WHERE f.species_name = 'Banksia'
     OR f.species_name = 'Sheoak'
     OR f.species_name = 'Wattle'
  GROUP BY f.species_name, f.observation_date)

  UNION ALL

(SELECT b.species_name,
        AVG(b.height) AS average_height, AVG(b.diameter) AS average_diameter
   FROM botanic_garden_flora AS b
  WHERE b.species_name = 'Banksia'
     OR b.species_name = 'Sheoak'
     OR b.species_name = 'Wattle'
  GROUP BY b.species_name, b.observation_date);
```

注意 `SELECT` 和 `FROM` 等关键字，都右对齐，而实际的列名和实现细节都左对齐。

注意下列情况总是加入空格：

* 在等号（`=`）前后
* 在逗号（`,`）后
* 成对的单引号（`'`）前后，除非在括号中或后面是逗号 / 分号

```sql
SELECT a.title, a.release_date, a.recording_date
  FROM albums AS a
 WHERE a.title = 'Charcoal Lane'
    OR a.title = 'The New Danger';
```

#### Line spacing 换行

总是换行的情况：

* 在 `AND` 或 `OR` 前
* 在分号后（分隔语句以提高可读性）
* 在每个关键字定义之后
* 将多个列组成一个逻辑组时的逗号后
* 将代码分隔成相关联的多个部分，帮助提高大段代码的可读性

让所有的关键字右对齐、所有的值左对齐，这样就能在查询语句中间留出一个空隙，有助于快速扫读整个查询的定义。


```sql
INSERT INTO albums (title, release_date, recording_date)
VALUES ('Charcoal Lane', '1990-01-01 01:01:01.00000', '1990-01-01 01:01:01.00000'),
       ('The New Danger', '2008-01-01 01:01:01.00000', '1990-01-01 01:01:01.00000');
```

```sql
UPDATE albums
   SET release_date = '1990-01-01 01:01:01.00000'
 WHERE title = 'The New Danger';
```

```sql
SELECT a.title,
       a.release_date, a.recording_date, a.production_date -- 将所有的日期放在一起
  FROM albums AS a
 WHERE a.title = 'Charcoal Lane'
    OR a.title = 'The New Danger';
```

### Indentation 缩进

为确保 SQL 的可读性，一定要遵守下列规则。

#### Joins Join 语句

Join 语句应该缩进到川流的另一侧并在必要的时候添加一个换行。


```sql
SELECT r.last_name
  FROM riders AS r
       INNER JOIN bikes AS b
       ON r.bike_vin_num = b.vin_num
          AND b.engine_tally > 2

       INNER JOIN crew AS c
       ON r.crew_chief_last_name = c.last_name
          AND c.chief = 'Y';
```

#### Subqueries 子查询

子查询应该在川流的右侧对齐并使用其他查询相同的样式。有时候将右括号单独置于一行并同与它配对的左括号对齐是有意义的 —— 尤其是当存在嵌套子查询的时候。

```sql
SELECT r.last_name,
       (SELECT MAX(YEAR(championship_date))
          FROM champions AS c
         WHERE c.last_name = r.last_name
           AND c.confirmed = 'Y') AS last_championship_year
  FROM riders AS r
 WHERE r.last_name IN
       (SELECT c.last_name
          FROM champions AS c
         WHERE YEAR(championship_date) > '2008'
           AND c.confirmed = 'Y');
```

### Preferred formalisms 推荐的形式

* 尽量使用 `BETWEEN` 而不是多个 `AND` 语句。
* 同样地，使用 `IN()` 而不是多个 `OR` 语句。
* 当数据输出数据库时需要处理时，使用 `CASE` 表达式。`CASE` 语句能嵌套形成更复杂的逻辑结构。
* 尽量避免 `UNION` 语句和临时表。如果数据库架构能够不靠这些语句运行，那么多数情况下它就不应该依靠这些语句。


```sql
SELECT CASE postcode
       WHEN 'BN1' THEN 'Brighton'
       WHEN 'EH1' THEN 'Edinburgh'
       END AS city
  FROM office_locations
 WHERE country = 'United Kingdom'
   AND opening_time BETWEEN 8 AND 9
   AND postcode IN ('EH1', 'BN1', 'NN1', 'KW1');
```

## Create syntax 创建语句

声明模式信息时维护可读代码也很重要。所以列定义的顺序和分组一定要有意义。

在 `CREATE` 定义中，每个列定义要缩进 4 个空格。

### Choosing data types 选择数据类型

* 尽量不使用供应商相关的数据类型 —— 这些类型不可移植甚至有可能不能在相同供应商的旧版本系统上使用。
* 只在真的需要浮点数运算的时候才使用 `REAL` 和 `FLOAT` 类型，否则使用 `NUMERIC` 和 `DECIMAL` 类型。浮点数舍入误差是个麻烦。

### Specifying default values 指定默认类型

* 默认值一定与列的类型相同 —— 如果一个列的类型是 `DECIMAL` 那么就不要使用 `INTEGER` 类型的值作为默认值。
* 默认值要紧跟类型声明并在 `NOT NULL` 声明前。

### Constraints and keys 约束和键

约束和键是构成数据库系统的重要组成部分。它们能很快地变得难以阅读和理解，所以遵从指导方针是很重要的。

#### Choosing keys 选择键

设计时应该谨慎选择构成键的列，因为键会影响性能和数据完整性。

1. 键在某种程度上应该是独一无二的。
2. 该值在不同表中的类型应该相同并且尽量不会更改。
3. 该值能否通过某种标准格式（如 ISO 发布的标准）？鼓励与前面第二点一致。
4. 尽量让键保持简单，但在适当情况下不要害怕使用复合键。

以上是定义数据库时合乎逻辑的平衡做法。当需求变更时，键也应该根据情况更新。

#### Defining constraints 定义约束

确定键后，就可以用约束和字值段验证来定义它们。

##### General 概述

* 表至少需要一个键来保证其完整性和可用性。
* 除了 `UNIQUE` 、`PRIMARY KEY` 和 `FOREIGN KEY` 之外（数据库供应商会提供相应的检查），约束应该有名字。

##### Layout and order 布局和顺序

* 在 `CREATE TABLE` 语句后先定义主键。
* 约束的定义应该紧跟它相应的列的定义后。
* 如果该约束与多个列相关，那么让它离相关的列越近越好。实在不行就将它放在表定义的最后。
* 如果是应用于整个表的表级别的约束，那么就将它放在表定义的最后。
* 按照字母顺序安排定义，`ON DELETE` 排在 `ON UPDATE` 前。
* 有道理的话，把所有相关的语句对齐。比如，把所有 `NOT NULL` 定义对齐到同一列。这样做并不难，但是能提高可读性。

##### Validation 校验

* 当字符串的格式已知时，用 `LIKE` 和 `SIMILAR TO` 约束来保证它们的完整性。
* 当数值的范围可以确定时，用范围 `CHECK()` 来防止错误的值进入数据库或在没有提示的情况下截断。大部分情况下至少要确认数值大于零。
* `CHECK()` 约束应该在单独的子句中以便 debug。

##### Example

```sql
CREATE TABLE staff (
    PRIMARY KEY (staff_num),
    staff_num      INT(5)       NOT NULL,
    first_name     VARCHAR(100) NOT NULL,
    pens_in_drawer INT(2)       NOT NULL,
                   CONSTRAINT pens_in_drawer_range
                   CHECK(pens_in_drawer BETWEEN 1 AND 99)
);
```

### Design to avoid 应该避免的设计

* 在关系型数据库的设计中应用面向对象设计思想（原则）—— 面向对象设计思想（原则）并不能很好地适用于关系型数据库的设计，避免这个陷阱。
* 将值存入一列并将其单位存在另一列 —— 列的定义应该让自己的单位不言自明以避免在应用内进行合并。使用 `CHECK()` 来保证插入的数据是合法的。
* [EAV (Entity Attribute Value)][eav] 表 —— 应该用专门的产品来处理这样的无模式数据。
* 因为某些原因（如为了根据时间归档、为了划分跨国组织的区域）将本应该放在一个表中的数据分到多个表中 —— 这样的设计导致以后必须使用 `UNION` 操作而不能直接查询一个表。

## 参考

1. [SQL style guide by Simon Holywell](https://www.sqlstyle.guide/)