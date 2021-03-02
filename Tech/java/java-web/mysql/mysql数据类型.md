# MySQL数据类型

- 数字类型
  - 整数: tinyint、smallint、mediumint、int、bigint
  - 浮点数: float、double、real、decimal
- 日期和时间: date、time、datetime、timestamp、year
- 字符串类型
  - 字符串: char、varchar
  - 文本: tinytext、text、mediumtext、longtext
- 二进制(可用来存储图片、音乐等): tinyblob、blob、mediumblob、longblob
- 空间类型：point

## 字符串类型

| 类型 | 单位 | 最大 | 特性 |
| ---- | ----  | ---- | ---- |
| CHAR | 字符 | 最大为255字符 | 存储定长，容易造成空间的浪费 |
| VARCHAR | 字符 | 可以超过255个字符 | 存储变长，节省存储空间 |
| TEXT | 字节 | 总大小为65535字节，约为64KB | - |

- TEXT在MySQL内部大多存储格式为溢出页，效率不如CHAR
- Mysql默认为utf-8，那么在英文模式下1个字符=1个字节，在中文模式下1个字符=3个字节。

## 数字类型

扩展阅读：[unsigned与zerofill详解](UNSIGNED与ZEROFILL关键字详解.md)

### 整形
>对于整形来说，M表示整数类型的==最大显示宽度==,最大显示宽度为255.显示宽度与类型可包含的值范围无关.

| type | Storage | Minumun Value | Maximum Value|
| :------------- | :------------- | :------------- | :------------- |
||(Bytes)|(Signed/Unsigned)|(Signed/Unsigned)|
|TINYINT(M)|1|-128/0|127/255|
|SMALLINT(M)|2|-32768/0|32767/65535|
|MEDIUMINT(M)|3|-8388608/0|8388607/16777215|
|INT(M)/INTEGER(M)|4|-2147483648/0|2147483647/4294967295|
|BIGINT(M)|8|-9223372036854775808/0|9223372036854775807/18446744073709551615|

### 浮点型
>对于浮点型来说，M表示浮点类型存储的总位数，D表示小数占的位数，就算没有小数，整数位也不能超过M-D位

| 属性 | 存储空间 | 精度 | 精确性 | 说明 |
| ---- | ----  | ---- | ---- | ---- |
|FLOAT(M, D)|4 bytes|单精度|非精确| 单精度浮点型，m总个数，d小数位 |
|DOUBLE(M, D)|8 bytes|双精度|比Float精度高| 双精度浮点型，m总个数，d小数位 |

- FLOAT容易造成精度丢失

### 定点数DECIMAL

- 高精度的数据类型，常用来存储交易相关的数据
- DECIMAL(M,N).M代表总精度，N代表小数点右侧的位数（标度）
- 1 < M < 254, 0 < N < 60;
- 存储空间变长
- DECIMAL别名DEC,FIXED,NUMERIC 

## 时间类型

>- mysql支持显示秒精度到微妙fsp指定显示的精度，范围1~6,默认0

| 类型 | Storage(Bytes) | 显示格式   | 精确性 |
| ---- | ----  | ---- | ---- |
| DATE | 3 | yyyy-mm-dd | 精确到年月日 |
| TIME(fsp) | 3 | hh:mm:ss | 精确到时分秒 |
| DATETIME(fsp) |8 | yyyy-mm-dd  hh:mm:ss | 精确到年月日时分秒 |
| TIMESTAMP(fsp) |  | 2015-05-01 11::12:00 | 精确到年月日时分秒 |

- MySQL在`5.6.4`版本之后，`TIMESTAMP`和`DATETIME`支持到微秒。
- `TIMESTAMP`会根据系统时区进行转换，`DATETIME`则不会
- 存储范围的区别  
    - `TIMESTAMP`存储范围：1970-01-01 00::00:01 to 2038-01-19 03:14:07
    - `DATETIME`的存储范围：1000-01-01 00:00:00 to 9999-12-31 23:59:59
- 一般使用`TIMESTAMP`国际化
- 如存时间戳使用数字类型`BIGINT`

## Other

类型|Storage(Bytes)|特性|说明
----|------|-----|----
Bit(M)|||select bin(bit_column+0) from test_user;//显示二进制数 select bit_column+0 from test_user;// 显示十进制数
bool/boolean|1/4|相当于tingint(1)|值为零被视为false。非零值被认为是true

