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

##oracle 执行计划
[关于oracle执行计划的博客](https://www.cnblogs.com/Dreamer-1/p/6076440.html)