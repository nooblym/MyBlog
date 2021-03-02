# mysql多表查询

## 交叉查询

![交叉查询](image/mysql多表查询-01.png)

语法：
>select * from t1,t2
或
select * from t1 cross join t2

应用场景：
>暂无

## 内连接

语法：
>select * from t1,t2 where t1.field=t2.field
或
select * from t1 inner join t2 on t1.field1=t2.field2

说明：
mysql会用t1.field1列的每一个值与t2.field2的每一个值去匹配，如果相等就会显示这列；如果t1.field1列的某个值没有在t2.field2列匹配到，那不不显示该记录