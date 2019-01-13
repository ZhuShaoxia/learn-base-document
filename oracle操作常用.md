## 函数表达式
1. 滤空函数
> nvl(a,b): 表示 a 为空，则等于 b

2. 拼接字符串
> || 或 contact

3. 条件表达式
> decode 函数：Oracle 自己的语法

4. 单行函数
	1. 字符函数
		1. lower : 小写
		2. upper : 大写
		3. initcap : 首字母大写
		4. substr(a,b) : 从 a 中，第 b 位开始取
		5. substr(a,b,c) : 从 a 中，第 b 位开始取 c 位
	2. 数值函数
		1. round : 四舍五入
		2. trunc : 截断
		3. mod : 求余
	3. 日期
		1. sysdate 默认格式
	4. 转换函数
		1. tochar()
	5. 通用函数：适用于任何数据类型，同时也适用于空值
		1. nvl2(a,b,c) 当 a=null的时候，返回c；否则返回b
 		2. 2nullif(a,b) 当a=b的时候，返回null；否则返回a
 		3. coalesce 从左到右 找到第一个不为null的值
 		
 5. 多行函数
 	1. avg
 	2. count
 	3. max
 	4. min
 	5. sum

 	
6. 经验总结
	1. 多表查询优于子查询。子查询需要执行多次
	2. where是针对原数据进行筛选，而having子句只是针对汇总后的结果进行筛选

7. 获取字符串长度函数
- length(string) :返回字符串长度，单位字符
- lengthb(string) : 返回字符串长度，单位是字节

8. 查看数据库字符集
> select userenv('language') from dual;
**注**：
一个汉字在Oracle数据库里占多少字节跟数据库的字符集有关，UTF８时，长度为三。
当字符集为 UTF-8 时，每个汉字长度为 3 个字节
							ZHS16GBK时，每个汉字长度为 2 个字节				
	


--
## case表达式

1.简单CASE表达式,使用表达式确定返回值.
<pre>
	CASE **search_expression**
　　WHEN expression1 THEN result1
　　WHEN expression2 THEN result2
　　...
　　WHEN expressionN THEN resultN
　　ELSE default_result
　　END
</pre>
2.搜索CASE表达式,使用条件确定返回值
<pre>
	CASE
　　WHEN **condition1** THEN result1
　　WHEN condistion2 THEN result2
　　...
　　WHEN condistionN THEN resultN
　　ELSE default_result
　　END
</pre>

3.二者区别：
>1. 简单case只能是when后面的表达式完全匹配case后的表达式，相当于 =，所以也不能匹配null。
2. searched case可以作为比较条件，那么可以使用like、!=、between ..and、<、=、is null、is not null等，比简单case的使用更加广泛，完全可以替代简单case。

##ROWNUM
1.定义：ROWNUM是一个序列，是oracle数据库从数据文件或缓冲区中读取数据的顺序。它取得第一条记录则rownum值为1，第二条为2，依次类推

与rowid区别：
rowid 可以说是物理存在的，表示记录在表空间中的唯一位置ID，在DB中唯一。只要记录没被搬动过，rowid是不变的。rowid 相对于表来说又像表中的一般列


##ROW_NUMBER() OVER()
<a href="https://blog.csdn.net/iamiwangbo/article/details/46804345">参考网站</a> oracle分页

**重点**
<a href="https://www.cnblogs.com/lcngu/p/5335170.html">博客关于over的用法解释</a>

1.**OVER**:

* 是一个分析函数，生成一个排序列
* partition 是划分的意思，分组之后 再排序 partition by ...order by...按啥分组再排序
* order by是用来确定排序的基准的，按照那一列来排序
* 　开窗函数，Oracle从8.1.6开始提供分析函数，分析函数用于计算基于组的某种聚合值，它和聚合函数的不同之处是：**对于每个组返回多行**，而聚合函数对于每个组只返回一行。
开窗函数指定了分析函数工作的数据窗口大小，这个数据窗口大小可能会随着行的变化而变化。

## oracle 执行计划
[关于oracle执行计划的博客](https://www.cnblogs.com/Dreamer-1/p/6076440.html)
1. 执行顺序：
根据缩进来判断，缩进最多的最先执行(缩进相同时，最上面的最先执行)
2. 表的访问方式
- TABLE ACCESS FULL(全表扫描)
- TABLE ACCESS BY ROWID(通过rowid的表存取)
- TABLE ACCESS BY INDEX SCAN(索引扫描)
	- INDEX UNIQUE SCAN（索引唯一扫描）:每次至多只返回一条记录,主要针对该字段为主键或者唯一；
	- INDEX RANGE SCAN（索引范围扫描）:使用一个索引存取多行数据；
		发生索引范围扫描的三种情况：
		- 在唯一索引列上使用了范围操作符（如：>   <   <>   >=   <=   between）
		- 在组合索引上，只使用部分列进行查询（查询时必须包含前导列，否则会走全表扫描）
		- 对非唯一索引列上进行的任何查询	
	- INDEX FULL SCAN（索引全扫描）：进行全索引扫描时，查询出的数据都必须从索引中可以直接得到
	- INDEX FAST FULL SCAN（索引快速扫描）:扫描索引中的所有的数据块,它不对查询出的数据进行排序（即数据不是以排序顺序被返回）
	- INDEX SKIP SCAN（索引跳跃扫描）:




## 日常开发中遇到的问题
1. update 语句中 若包含单引号 则用两个单引号代替
2. to_date('2018/11/11','yyyy/MM/dd') 
3. ORACLE采用自下而上的顺序解析WHERE子句,根据这个原理, 当在WHERE子句中有多个表联接时，WHERE子句中排在最后的表应当是返回行数可能最少的表，有过滤条件的子句应放在WHERE子句中的最后。

## 常用 sql 语句
1. 备份表
```SQL
create table newTable;
as 
select * from oldTable;
```

2. 删除表
```SQL
drop table tablename;
```

3. 清空表
```SQL
truncate table tablename;
```

4. 创建索引
```SQL
CREATE INDEX index_name ON table_name(COLUMN_NAME);
CREATE UNIQUE INDEX index_name ON table_name (column_name)
```
5. 给表 或 列 添加注释
comment on table 表名 is 注释名;
comment on column 表名.列名 is 注释名;
