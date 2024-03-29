# java核心技术卷一笔记



### 数据类型

`java` 是一种强类型语言。因此必须为每一个变量声明一种类型

> `Java` 中有一个能够表示任意精度的算数包，通常被称为 “大数值”，虽然被称为大数值，但是它并不是一种新的数据类型，而是一个 `Java` 对象



通常最常用的是 `int` 类型；而 `short` 和 `byte` 通常用于特定的应用场合（底层文件处理或者控制占用存储空间量的大数组）

十六进制表示方式使用前缀 `0x` 或者 `0X`，八进制使用前缀 `0`；二进制使用前缀 `0b` 或者 `0B`

> 八进制容易混淆，通常不使用
>
> 二级制数之间可以添加下划线便于阅读



浮点数用于表示有小数部分的数值。

`double` 表示这种类型的数据精度是 `float` 类型的两倍（有人称之为双精度的数值），大部分情况都使用 `double`

`float` 类型的精度很难满足需求，实际上只有很少的情况下使用（需要单精度数据库，存储大量数据）

> 可以使用十六进制表示浮点数，`0x1.0p-2`
>
> 尾数采用十六进制，指数采用十进制。指数的基数是 `2`

浮点数遵循 `IEEE 754` 规范，表示溢出和出错情况

- 正无穷大
  - `Double.POSITIVE_INFINITY`
- 负无穷大
  - `Double.NEGATIVE_INFINITY`
- `NaN`（不是数）
  - `Double.NaN`

> 整数被 0  除会产生一个异常，而对于浮点数将会得到 无穷大或者 `NaN`



`char` 类型原本是用来表示单个字符；如今，有些 `Unicode` 字符可以用一个 `char` 值描述，另外一些则需要两个

`char` 字面量的值要使用单引号括起来

> `char` 值可以使用十六进制来表示，范围是 `\u0000 ~ \Uffff`
>
> 需要注意到注释中的 `\u`，可能会产生一个语法错误
>
> 例子：
>
> `// \u00A0` 会被替换为换行符
>
> `// c:\user`	`java: 非法的 Unicode 转义 —— \u后面未加十六进制数`

码点和代码单元

大多数常用的 `Unicode` 字符使用一个代码单元就可以表示，而辅助字符则需要一对代码单元表示

> `length()` 方法返回采用 `UTF-16` 编码表示的给定字符串需要的代码单元数量
>
> 想要得到实际的长度，即码点数量，可以调用 `codePointCount`



`Java` 中的 `char` 类型使用的是 `UTF-16` 编码，占用两个字节；对于辅助字符来说 `char` 的长度不够



`Unicode`

码点是指一个编码表中的某个字符对应的代码值。在 `Unicode` 标准中，码点采用十六进制书写，并加上前缀 `U+`

根据码点将 `UTF-16` 分为 17 个代码级别，第一个级别基本多语言基本（包含经典的代码）；其余的里面也包含一些辅助字符

> 通常情况下不使用 `char` ，除非需要处理 `UTF-16` 代码单元



```java
// 获取位置为 n 的代码单元
charAt(n); 

// 获取位置为 i 的码点
int index = greeting.offsetByCodePoints(0, i);
int cp = greeting.codePointAt(index);

// 遍历字符串，并查看每一个码点
int cp = sentence.codePointAt(i);
if (Character.isSupplementaryCodePoint(cp)) i+= 2;
else i++;

// 上一个码点
i--;
if (CharacterssSurrogate(sentence.charAt(i))) i--;
int cp = sentence.codePointAt(i);
```

> 这样的用法很麻烦，可以使用 `codePoints`，将其转换为 `int` 值的流，每一个 `int` 对应一个码点
>
> 要将一个码点转换为一个字符串，可以使用 `String` 的构造函数



##### 总结：

编译器将 `Java` 源文件编译成 `.class` 文件时候需要用到文件的编码，我们一般设置为 `UTF-8`，如果文件是其他编码可能会出错；一旦完成转变之后就变为与平台无关的 `.class` 文件（`Unicode`）



数学函数

`Java` 中没有幂运算，因此需要使用 `pow` 方法来代替

`floorMod` 方法目的是设计来解决负数取余的问题



数值类型之间的转换

使用两个数值进行二元操作时，要先将两个操作数转换为同一种类型

可能出现精度丢失的情况

- `int` 转换为 `float`
- `long` 转换为 `float` 和 `double`

> 如果试图将一个数值从一种类型强制转换为另一种类型，而又超出目标类型的表示范围，会出现一个完全不同的值



位运算符

> 应用在布尔值上时候，`&` 和 `|` 运算符也会得到一个布尔值。这些运算符和逻辑运算符很类似，不过不采用短路的方式求值
>
> `>>>` 运算符会使用 `0` 来填充高位，和 `>>` 不同，它会使用符号位填充高位；不存在 `<<<` 运算符



枚举

变量的取值在一个有限的集合内。



字符串

`Java` 字符串就是 `Unicode` 字符序列。`Java` 没有内置的字符串类型，而是使用一个预定义类。

不可变字符串

`String` 中没有提供用于修改字符串的方法。字符串存放在公共的存储池中，字符串变量指向存储池中对应的位置

> 共享字符串会带来高效率

检测字符串是否相等

`s.equal(t)` 

> `==` 无法检测两个字符串是否相等，只能确定两个字符串是否存放在同一个位置上
>
> 只有字符串常量进行共享，`+` `substring` 等产生的结果并不会共享，所以无法使用 `==` 来判断字符串是否相等



`StringBuilder` 

构建字符串，有时候需要使用较短的字符串构建字符串，采用字符串连接的方式达到此目的效率比较低

- 增添一部分字符串调用 `append()`
- 需要构建字符串时候使用 `toString()`

> `StringBuilder` 和 `StringBuffer` 两个 `API` 是相同的
>
> `StringBuffer` 允许用于多线程，它的效率要低一点



### 输入输出流



读取输入

- 构造一个 `Scanner` 对象
- 将标准输入流 `System.in` 与之关联

> 输入是可见的，因此不适用于从控制台读取密码；
>
> `Console` 可以读取密码

```java
// 在控制台读取密码
Console cons = System.console();
String username = cons.readLine("User name: ")；
cha[] passwd = cons.readPassword("Password:");
```

> 使用不是很方便，每次只能读取一行输入；没有单独读取一个单词或者数值的方法



格式化输出

使用 `s` 转换符格式化任意的对象。对于任意实现 `Formattable` 接口的对象都将实现 `formatTo` 方法；否则调用 `toString`



文件读写

- 使用 `File` 对象构造出一个 `Scanner` 对象

`Scanner in = new Scanner(Paths.get("niyflle.txt"), "UTF-8");`

> 如果省略编码会使用机器上的默认编码

- `PrintWriter` 文件写入

> 如果文件不存在，创建该文件；可以使用 `System.out` 下的常规命令



### 控制流程



块作用域

使用一对大括号括起来的若干条简单的 `Java` 语句

> 不能在两个嵌套的块中声明同名的变量



循环条件中检验两个浮点数是否相等需要额外小心

> `10 ！= x; x += 0.1`
>
> 因为二进制数无法很好的表示 `0.1` ；将从 `9.999 999 999 999 98` 直接跳到 `10.0999 999 999 999 98`



`switch` 语句有可能触发多个 `case`；如果在结尾没有 `break` 语句这是非常危险的，通常不使用

带有标签的 `break` 语句

```java
// 标签
read_data:
while (. . .) {
	for (. . .) {
        // 结束到循环的标签
		break read.data;
	}
}
```

> 只能跳出语句块，无法跳入语句块



### 大数值

基本的整数和浮点数精度无法满足需求可以使用 `BigInteger` 和 `BigDecimal`

使用静态的 `valueOf()` 方法将普通数值转换为大数值



### 数组

数组排序，使用 `Arrays.sort`

生成随机浮点数

- `Math.Random` 方法返回一个 `0` 到 `1` 之间的随机浮点数
- 使用 `n` 乘这个浮点数





# 对象和类

面向对象程序是由对象组成的，每个对象包含对用户公开的特定功能部分和隐藏的实现部分



### 对象

- 行为
- 状态
- 标识



### 类之间的关系

- 依赖
  - 使用
- 聚合
  - 包含
- 继承
  - 特殊和一般的关系



要想使用对象，必须先构造对象，并指定其初始状态

构造函数是一种特殊的方法，用来构造并初始化对象

> 局部变量不会自动的初始化为 `null`，而必须通过调用 `new` 或者 将它们设置为 `null`



#### `LocalDate` 类

`Date` 是使用距离一个时间点的毫秒数表示的，这个点是所谓的纪元（`GMT`）

> `Date` 用来表示时间；`LocalDate` 用来表示日历



通常不使用构造函数来 `LocalDate` 类的对象，应该使用静态工厂方法来调用构造器