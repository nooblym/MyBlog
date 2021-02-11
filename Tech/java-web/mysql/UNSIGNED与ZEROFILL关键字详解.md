# unsigned,zerofill关键字详解

**unsigned，zerofill关键字只能用于数字类型的列，以下所有语句都是在字段类型为数字的前提下进行**  

>创建表时使用：create table table_name(col1 num_type [unsigned][zerofill][,...])...
修改表时使用：alter table table_name modify/add col_name num_type  [unsigned][zerofill];

## unsigned关键字

所有数字类型在存储数据的时候最左边都有一位是符号位，“0”表示正，“1”表示负,其余位表示数值位.
使用unsigned关键字会"去掉"数据的符号位，将去掉的符号位表示为数值位，也就是说加上unsigned关键字的列只能存储非负数，而相应的数字列的最大存储数乘以二。  
如：int类型存储范围-2147483648 ~ 2147483647，而加上unsigned关键字后的存储范围就变成0 ~ 4294967294

## zerofill关键字

zerofill关键字会在显示表内容的时候将整型字段数字长度不够的数据前面填充0，以达到设定的长度。
如：
    demo1(id1 int(4),id2 int(4) zerofill)表  
    插入两条记录：  
    insert into demo1 value(1,1);  
    insert into demo1 value(23,23);
    显示记录：
    select * from demo1;
    结果：
id1|id2
---|---
1|0001
23|0023

==如果给数字字段添加zerofill，则系统会自动将unsigned属性添加到该列==