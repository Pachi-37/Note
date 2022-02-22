# Java web 基础部分



### `xml`

可扩展标记语言，编写 `XML` 标签，类似于 `HTML` 拥有良好的人机可读性

> xml 没有预定义标签，主要用于保存和传输数据



结构

- 第一行必须是 `xml` 声明
- 有且只有一个根节点 

```xml
<?xml version="1.0" encoding="utf8"?>
```



书写规则

- 合法的标签名
  - 单词之间使用 `-` 分隔
- 适当的注释与属性
- 处理特殊字符
  - 标签体中出现 `<` `>` 会破坏文档结构
  - 使用实体引用
  - 使用 `CDATA` 标签
    - 指定不应该由 `XML` 解析器进行解析的文本数据

```xml
<![CDATA["开始，到"]]>
```



| `&lt`   | `<`  |      |
| ------- | ---- | ---- |
| `&gt`   | `>`  |      |
| `$amp`  | `&`  |      |
| `&apos` | `'`  |      |
| `&quot` | `"`  |      |



语义约束

规定 `xml` 中允许和不允许出现的元素

- `DTD`
- `XML Schema`



```DTD
<!ELEMENT hr(employee)>
<!-- hr 结点下只允许出现一个 employee 子结点 -->

<!ELEMENT hr(employee age)>
<!-- 必须包含以上元素，且按顺序出现 -->

<!ELEMENT name>

<!-- + 至少出现一次的子结点  * 0..n 个子结点  ?至多一个 -->

<!DOCTYPE 根节点 SYSTEM "dtd文件路径">
```



`DOM` 文档对象模型

`Document Object Model` 定义了访问和操作 `xml` 文档的标准方法，把 `xml` 文档作为树结构来查看 



`XPath` 路径表达式

`xml` 中查询数据的语言，提高在提取数据时候的开发效率



- 基本表达式

| 表达式     | 描述                   |
| ---------- | ---------------------- |
| `/`        | 从根节点选取           |
| `//`       | 全文寻找符合条件的结点 |
| `.`        | 当前结点               |
| `..`       | 父节点                 |
| `@`        | 选取属性               |
| `nodename` | 选取此节点的所有子结点 |



- 谓语表达式

```xml
/book/book[opition]

1				隶属于book的第一个book元素
last()			隶属于book的最后一个元素
position() < 3	最前面两个
@lang			拥有名为lang的属性的元素
price > 3		元素值必须大于3
```

> `Jaxen`



`BS` 模式

- 用户
- 浏览器
- `DNS` 解析目标网址的 `IP`
- `web` 目标服务器主机
- 根据请求返回目标信息



请求与响应

请求：从浏览器发送给服务器的数据包

响应：服务器返回给服务器的结果





# `Servlet` 

服务器小程序，主要用于生成动态 `Web` 内容



`Tomcat` 容器等级

- `Container`
  - `Engine`
    - `HOST`
      - `Servlt`
        - `Context`
          - `warpper`

> `Servlet` 容器管理 `Context` 容器，一个 `Context` 对应一个 `Web` 工程



生命周期

初始化阶段，调用 `init()`

响应客户端请求，调用 `service()`，根据不同的需求调用 `doGet()` 或 `doPost()`

中止阶段，调用 `destory()`



当服务器接收到浏览器发送的`Http协议请求包`之后，自动生成一个请求对象和响应对象

在调用 `doGet/doPost` 方法，负责将请求对象和响应对象作为实参传递到方法

服务器准备推送响应协议包之前，负责将本次请求关联的请求和响应对象销毁





`HttpServletResponse`

主要是将 `doGet` 和 `doPost` 方法的执行结果写到响应体之中交给浏览器

设置 `context-type` 属性，从而控制浏览器使用对应的编译器

设置响应头 `location` ，从而控制浏览器向指定服务器发送请求 



`HttpServletRequest`

在运行 `doPost/doGet` 方法时，读取 `Http` 请求协议包中的信息

读取请求行，请求头或请求体的参数

代替浏览器向 `Http` 服务器申请资源文件的调用



> `uri` 资源文件精准定位地址，实际上是 `URL` 地址的截取（`/网站名/资源文件名`）



浏览器以 `Get` 方式发送请求，请求参数保存在请求头中

浏览器以 `Post` 方式发送，请求参数保存在请求体当中

> 请求头默认使用 `Tomcat` 进行解码（`UTF-8`），请求体默认使用 `request` 对象负责解码（`ISO-8859-1`）
>
> 在 `Post` 请求之下要先设置对象使用 `utf-8` 编码



> `Http` 状态码
>
> 三位数组成的符号；`Http` 服务器在推送响应包之前，根据本次请求处理情况将状态码写入响应包中【状态栏】
>
> 状态码是服务器提供给浏览器解决问题的结果

> 分类：
>
> 1）组成：`100-599`
>
> 100：该资源文件不是独立的资源文件，浏览器接收到该资源之后任需要继续索取依赖的资源
>
> 200：本次资源文件是一个独立的资源文件
>
> 302：本次浏览器返回的不是一个资源文件而是一个资源文件的地址
>
> 404：未定位到相关的资源文件
>
> 405：服务端已经定位到被访问的资源文件，但是 `Servlet` 无法处理提交方式
>
> 500：服务端已经定位到资源文件，但是 `servlet` 处理期间，由于 `Java` 异常导致处理失败







`Servlet` 容器装载 `Servlet`

- `Servlet` 容器启动时，自动装载某些 `Servlet`

```xml
<servlet>
	<loadon-startup>[1..*]</loadon-startup>
</servlet>
```

> 数字越小代表优先级越高

- `Servlet` 容器启动之后，客户端向 `Servlet` 发送请求
- `Servlet` 类文件被更新，重新装载 `Servlet`



`servlet` 和九大内置对象

| `jsp` 对象    | 获得方式                       |
| ------------- | ------------------------------ |
| `out`         | `resp.getWrite()`              |
| `request`     | `service` 方法中的 `req` 参数  |
| `response`    | `service` 方法中的 `resp` 参数 |
| `session`     | `req.getSession()`             |
| `application` | `getServletContext()`          |
| `exception`   | `Throwable`                    |
| `page`        | `this`                         |
| `pageContext` | `PageContext`                  |
| `Config`      | `getServletConfig`             |



获取初始化参数

`ServletConfig` 接口提供的方法来获取这些参数



多个 `Servlet` 之间的相互调用

- 重定向

  - 用户第一次通过【手动方式】访问 `OneServlet` , `OneServlet` 工作完毕后将 `TwoServlet` 的地址写到响应头 `location` 的地址中

  > `response.sendRedirect("");`

- 请求转发

  - 用户第一次通过【手动方式】访问 `OneServlet`，通过当前的请求对象代替浏览器发送请求

  > `request.getRequestDispatcher("").forward();`



数据共享的方式

1. `ServletContext`
2. `Cookie`
3. `HttpSession`
4. `HttpServletRequest`



`ServletContext`

如果两个 `Servlet` 来自同一个网站，彼此之间通过网站实例对象实现数据的共享

生命周期：

- 服务器启动时，自动为当前对象创建一个全局作用域对象
- 一个网站只有一个全局作用域对象
- 服务器准备关闭时，销毁全局作用域对象



`Cookie` 

如果两个 `Servlet` 来自于同一个网站，并为同一浏览器或用户提供服务，此时借用借助于 `Cookie` 对象进行数据共享

用户第一次向网站发送请求申请 `Servlet` ，在运行期间创建一个 `Cookie` 存储于当前对象相关数据，在服务之后，将当前的 `Cookie` 写到请求头当中

一段时间之后，用户通过同一个浏览器再次向同一个网站发送请求，浏览器需要无条件的将网站之前推送的 `Cookie` 写入到请求头

```
Cookie card = new Cookie();
# 一个Cookie只能存放一个键值对，且这个键值对的值只能为 String
```

销毁机制

默认情况下，只要浏览器关闭，`Cookie` 对象会被销毁

在手动指定情况下，可以要求 `Cookie` 在硬盘中存活时间

```
cookie.setMaxAge(60);
```



`HttpSession`

两个 `Servlet` 在同一个网站，并为同一个浏览器 / 用户提供服务

销毁机制：

用户和 `HttpSession` 关联使用的 `Cookie` 只能存放在浏览器内存中；在浏览器关闭意味着，其与用户的联系被切断，由于 `Tomcat` 无法检测浏览器何时关闭，所以会为其设置空闲时间



`HttpServletRequest`

在同一个网站中，两个 `Servlet` 之间通过【请求转发】方式进行调用，彼此之间贡献一个请求协议包



> `HttpSession` 和 `Cookie` 的区别：
>
> `Cookie` 存放在客户端（浏览器内存 / 硬盘）；存储在服务端内存
>
> `Cookie` 对象只能存储 `String` 类型的数据；可以存储任意类型的数据
>
> 一个 `Cookie` 只能存放一个共享数据；使用 `Map` 集合存储任意类型的共享数据



监听器接口

监听器接口用于监控【作用域对象[^1]生命周期的变化时刻】以及【作用域对象共享数据变化的时刻】

```
// 根据实际情况，选择对应的接口实现类
// 重写监听器的接口声明
// 注册监听器
```

[1]: 作用域对象，在某些条件下可以为两个 `Servlet` 对象提供数据共享方案 `ServletContext` `HttpSession` `HttpServletRequest`



`ServletContextListener`

通过这个接口检测全局作用对象被初始化及销毁的时间

```
contextInitlized()
contextDestory()
```



`ServletContextAttributeListener`

检测全局作用对象共享数据的变化

```
contextAdd()
contextReplace()
contextRemove()
```



过滤器 `Filter`

在 `Http` 服务器调用资源文件之前，对 `Http` 服务器进行拦截

- 帮助服务器检测当前请求是否合法
- 帮助当前请求进行增强操作



防止恶意登录

使用会话作为用户令牌信息

> 缺点：
>
> 增加开发难度（每次都需要进行身份判断）
>
> 不能对静态文件进行保护



> 请求协议包的结构
>
> 请求行	`url` `method`
> 请求头	`Cookie`	请求参数 `[get]`
>
> 空白行
>
> 请求体	请求参数`[post]`



> `Http` 响应包
>
> 状态行	状态码
>
> 响应头	`content-type`	`cookie`	`location`
>
> 空白行
>
> 响应体	返回文件内容、文件命令、动态文件运行之后的结果



`MVC` 模式

`Model：JavaBean` 

`View：JSP`

 `Controller：Servlet`



# `JSP` 开发规范



响应对象存在的弊端

适合将少量数据写入响应体，如果处理数量过多，增加开发难度





### `EL` 表达式

一种特殊的命令格式【表达式命令格式】

负责在`JSP` 文件上从全局作用域对象读取指定的共享数据并输出到响应体中



##### 作用域对象的别名

可以使用的作用域对象

`ServletContext` 				`application`		全局作用域对象

`HttpSession`						`session`				会话作用域对象

`HttpServletRequest`	 	`request`				请求作用域对象

`PageContext`						`pageContext`		当前页作用域对象（`JSP` 独有的作用域对象，`Servlet` 不存在的，当前页存在的共享数据仅供当前页使用）主要用来 `JSTL` 标签与 `JSP` 文件共享数据



##### `EL` 表达式提供的别名

`application`			`applicationScope`

`session`					`sessionScope`

`request`					`requestScope`

`pageContext`			`pageScope`



从作用域对象读取指定共享数据关联的引用对象的属性值，并自动的写入到响应体中（通过反射机制）

```jsp
${作用域对象别名.共享数据名.属性名}
```

> `EL` 表达式没有遍历集合的能力



简化版的 `El` 表达式	`${共享数据名}`

> 允许开发成员省略共享数据名

存在的问题：

- 降低程序执行的速度
- 容易导致数据的定位错误



运算表达式



内置对象

通过请求对象拿到当前请求协议包中的请求参数，并将请求参数的内容写到相应体中

```el
${param.请求参数名}
${paramValues.请求参数名[下标]}
```



### `JSTL` 标签



- 核心标签库（`core`）
- 格式化输出标签库（`fmt`）
- `sql` 数据库（`sql`）
- `xml` 操作数据库（`xml`）
- 函数库（`function`）



```xml
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core">
```

