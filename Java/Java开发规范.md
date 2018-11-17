#### 工具类
1. 比较两个对象是否相等 : Objects.equals
<pre>
	Objects.equals(Object a, Object b){
		return (a == b) || (a != null && a.equals(b))
	}
</pre>

#### 编码规约
1. 不允许任何魔法值（未经定义的变量）直接出现在代码中
2. long 或者 Long 初始赋值时，使用大写的 L ，不能是小写的 l ,小写容易跟数字 1 混淆，造成误解。
3. 循环体内，字符串的链接方式，使用 StringBuilder 的 append 方法进行扩展。
4. 使用工具类 Arrays.asList()把数组转换成集合时，不能使用其修改集合相关的方
法，它的 add/remove/clear 方法会抛出 UnsupportedOperationException 异常。 说明：asList 的返回对象是一个 Arrays 内部类，并没有实现集合的修改方法。Arrays.asList 体现的是适配器模式，只是转换接口，后台的数据仍是数组。
5. if 尽可能维持正常流程代码最外面
6. Math.random() 返回 double 类型，取值范围  0<=x<1 。获取整数用 random.nextInt 或者 nextLong
7. 获取当年前毫秒数： System.currentTimeMillis()
8. 防止NPE，是程序员的基本修养。

#### SQL语句