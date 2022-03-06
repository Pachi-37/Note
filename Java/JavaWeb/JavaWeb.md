# `JavaWeb`



### `XML`

全称可扩展标记语言



##### 和 `HTML` 的比较

- `XML` 没有预定义标签，`HTML` 存在大量预定义标签
- `XML` 着重在于保存和传输数据，`HTML` 在于显示信息



##### 主要用途

- `java` 程序的配置文件描述
- 用于保存文件产生的数据
- 网络间数据的传输



##### `XML` 文档结构

- 第一行必须是 `XML` 声明
- 有且只有一个根节点
- `XML` 标签的书写规则和 `HTML` 相同



```xml
<?xml version="1.0" encoding="utf-8"?>
```



##### 书写规范

- 合法的标签名

  - 标签名要保证有意义
  - 使用英文小写，单词之间使用 `-` 分隔
  - 多级标签之间不存在重名

- 适当的注释和缩进

- 合理的使用属性

  - 通常把标签唯一的身份信息放置在属性中

- 特殊的字符和 `CDATA` 标签

  - `&lt;	<`
  - `&gt;	>`
  - `&amp;	&`
  - `&apos;	'`
  - `&apot;	"`

  > `CDATA` 标签指定不被 `XML` 解析器解析的文本数据
  >
  > `<![CDATA["开始，到"]]>`

- 有序的子元素





##### `XML` 语义约束

在结构正确的情况下，约束 `XML` 中哪些标签能出现，哪些不能

- `DTD`
- `XML Schema`



##### `DTD`

`Document Type Definition` 文档类型定义

- `<!ELEMENT>`

  - 定义允许出现的结点及其数量

  ```dtd
  <!-- a 结点下只允许出现一个 b -->
  <!ELEMENT a(b)>
  <!-- a 结点下必须包含以下的结点，且按顺序出现 -->
  <!ELEMENT a(b,c)>
  <!-- a 标签体只能是文本,#PCDATA 代表文本元素 -->
  <!ELEMENT a(#PCDATA)>
  ```

  > 定义节点数量，需要在子结点后面添加相对应的描述符
  >
  > `+` 最少出现一次	`*` 不限次	`？` 最多一个

引用 `DTD`

```dtd
<!DOCTYPE 根节点 SYSTEM "dtd文件">
```



###### 数据类型

`PCDATA` 

被解析的字符数据，文本中的标签被当作标签处理，实体会展开

`CDATA`

不会被解析器解析的文本



声明元素

```dtd
<!ELEMENT element-name category>
<!-- EMPTY 声明空元素	只有 PCDATA元素(#PCDATA)	ANY 任何可解析的元素 -->
```



属性

任何标记的属性都必须在 `DTD` 中声明，必须通过关键字来进行说明

```dtd
<!ATTLIST element-name attribute-name attribute-type attribute-value>
```

| 类型               | 描述                          |
| :----------------- | :---------------------------- |
| CDATA              | 值为字符数据 (character data) |
| (*en1*\|*en2*\|..) | 此值是枚举列表中的一个值      |
| ID                 | 值为唯一的 id                 |
| IDREF              | 值为另外一个元素的 id         |
| IDREFS             | 值为其他 id 的列表            |
| NMTOKEN            | 值为合法的 XML 名称           |
| NMTOKENS           | 值为合法的 XML 名称的列表     |
| ENTITY             | 值是一个实体                  |
| ENTITIES           | 值是一个实体列表              |
| NOTATION           | 此值是符号的名称              |
| xml:               | 值是一个预定义的 XML 值       |

默认属性

| 值           | 解释           |
| :----------- | :------------- |
| 值           | 属性的默认值   |
| #REQUIRED    | 属性值是必需的 |
| #IMPLIED     | 属性不是必需的 |
| #FIXED value | 属性值是固定的 |

实体

实体是定义引用普通文本或特殊字符的快捷方式的变量

```dtd
<!ENTITY entity-name "entity-value">
<!-- 实体的引用方式 &entity-name; 	-->
```



### `XML Schema`

`XML Schema` 比 `DTD` 复杂多，提供更多的功能

- 数据类型
- 格式限定
- 数据范围



##### 优点

保护数据通信

- 双方对于内容有相同的 期望值

可扩展性

- `Schema` 之间可以相互引用
- 可以创建基于标准数据类型衍生的数据类型
- 一个文档可以引用多个 `Schema`



每一个 `xml` 引用 `schema` 文件。需要书写在根标签上

- `xmlns=""`	
  - 引用的 `schema` 约束文件
- `targetNamespace`
  - 命名空间，`schema` 特有的属性
  - 定义 `schema` 被 `xml` 引用时的名称
- `xmlns:xsi`
  - 声明当前的 `xml` 文件是 `schema` 的一个实例，是被 `schema` 约束的
- `xsi:schemaLocation`
  - 引用 `schema` 的位置



##### `<schema>` 元素

> `<schema>` 元素是每一个 `XML Schema` 的根元素



##### `XSD` 元素

简易元素

仅包含文本元素，不包含其他其他元素或者属性

```xml
<element name="" type="">
```



##### 属性

简单元素无法拥有属性。一个元素拥有属性会被当作复合类型；属性本身可以作为简易类型声明

```xml
<xs:attribute name="" value="">
```



##### 限定

用于为 `XML` 元素或者属性定义可接受的值被称为 `facet`

```xml
<!-- 对元素范围限定 -->
<element name="">
	<simpleType>
    	<restriction base="integer">
        	<maxInclusive value=""/>
            <minInclusive value=""/>
        </restriction>
    </simpleType>
</element>

<!-- 使用枚举类型 -->
<element name="">
	<simpleType>
    	<restriction base="integer">
        	<enumeration value=""/>
        </restriction>
    </simpleType>
</element>
```



| 限定             | 描述                                                 |
| :--------------- | :--------------------------------------------------- |
| `enumeration`    | 定义枚举                                             |
| `fractionDigits` | 定义最大正小数                                       |
| `length`         | 定义允许的长度                                       |
| `maxExclusive`   | 定义数值的上限 （不包含）                            |
| `maxInclusive`   | 定义数值的上限 （包含）                              |
| `maxLength`      | 定义最大长度                                         |
| `minExclusive`   | 定义数值的下限（不包含）                             |
| `minInclusive`   | 定义数值的下限（包含）                               |
| `minLength`      | 定义允许的最小长度                                   |
| `pattern`        | 定义可接受的字符的精确序列                           |
| `totalDigits`    | 定义所允许的阿拉伯数字的精确位数，必须大于0          |
| `whiteSpace`     | 定义空白字符（换行、回车、空格以及制表符）的处理方式 |



##### 复合元素类型

- 空元素
- 包含其他元素
- 仅包含文本
- 包含元素和文本





### `DOM` 文档对象模型

`Document Object Model` 定义访问和操作 `XML` 文档的标准方法



### `Dom4j`

简单易用的解析 `XML` 的开源库

- 将 `XML` 视为 `Document` 对象
- `XML` 标签被定义为 `Element` 对象 



### `Xpath`

`Xpath` 是一门在 `XML` 文档中查找信息的语言（对元素和属性遍历）



##### 结点

- 元素
- 属性
- 命名空间
- 处理指令
- 注释
- 文档（根）结点



##### 基本值

无父结点和子结点



##### 项目

基本值或者节点



##### 基本表达式

| 表达式     | 描述                                                       |
| :--------- | :--------------------------------------------------------- |
| `nodename` | 选取此节点的所有子节点。                                   |
| /          | 从根节点选取。                                             |
| //         | 从匹配选择的当前节点选择文档中的节点，而不考虑它们的位置。 |
| .          | 选取当前节点。                                             |
| ..         | 选取当前节点的父节点。                                     |
| @          | 选取属性。                                                 |



##### 谓语表达式

基本表达式再添加约束条件

| 路径表达式                         | 结果                                                         |
| :--------------------------------- | :----------------------------------------------------------- |
| /bookstore/book[1]                 | 选取属于 bookstore 子元素的第一个 book 元素。                |
| /bookstore/book[last()]            | 选取属于 bookstore 子元素的最后一个 book 元素。              |
| /bookstore/book[last()-1]          | 选取属于 bookstore 子元素的倒数第二个 book 元素。            |
| /bookstore/book[position()<3]      | 选取最前面的两个属于 bookstore 元素的子元素的 book 元素。    |
| //title[@lang]                     | 选取所有拥有名为 lang 的属性的 title 元素。                  |
| //title[@lang='eng']               | 选取所有 title 元素，且这些元素拥有值为 eng 的 lang 属性。   |
| /bookstore/book[price>35.00]       | 选取 bookstore 元素的所有 book 元素，且其中的 price 元素的值须大于 35.00。 |
| /bookstore/book[price>35.00]/title | 选取 bookstore 元素中的 book 元素的所有 title 元素，且其中的 price 元素的值须大于 35.00。 |



### `Jaxen`

开源的 `Xpath` 库 



### `JASON`

数据由键值描述，由逗号分隔

大括号代表一个完整的对象，拥有多个键值对

中括号用于保存数组，多个对象之间使用逗号分隔 



### `FastJASON`

阿里巴巴的著名 `json` 序列化和反序列化工具包



### `jQuery` `Ajax`



##### `jQuery`  选择器

选择元素并进行处理



```html
jQuery(选择器表达式)
$(选择器表达式)
```





##### `Ajax`

可以在不刷新的情况下，实现页面的局部更新



##### 使用

- 创建 `XmlHttpRequest`
  - 因为 `XmlHttpReque` 不是 `w3c` 标准，不同的浏览器创建方法不一样
- 发送 `Ajax` 请求
- 处理服务器响应



```javascript
// 创建 XMLHttpRequest 对象
var xmlhttp;
if (window.XMLHttpRequest) {
    xmlhttp = new XMLHttpRequest();
} else {
    xmlhttp = new ActiveXObject("Microsoft.XMLHTTP")
}
```

