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



### `XML Schema`

`XML Schema` 比 `DTD` 复杂多，提供更多的功能

- 数据类型
- 格式限定
- 数据范围