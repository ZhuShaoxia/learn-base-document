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