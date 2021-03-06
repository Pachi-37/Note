# `MyBatis`

优秀的持久层框架

使用 `xml` 将 `SQL` 与程序解耦，便于维护



### 开发流程

- 引入开发依赖
- 创建核心配置文件
- 创建实体类
- 创建 `Mapper` 映射文件
- 初始化 `SessionFactory`
- 例用 `SqlSession` 对象操作数据



### 单元测试

对软件中最小的可测试单元进行检查和验证

测试用例：编写一段代码对已有的功能（方法）进行校验



测试用例类为原类命 + `Test/Testor`；方法可以和原方法保持一致或者加上前缀 `test`

> 出现异常不代表测试用例运行有问题，要看结果是否与预期相符合



### 配置文件

默认使用 `Mybatis-config.xml` 配置数据库环境

> 也可以不采用该命名方式，但是要保证文件为 `xml`

最主要的标签为 `<environment>` 主要包含数据库驱动、`URL` 、用户名和密码



##### `environment`

`default` 设置默认指向的数据库

`dataSource` 采用什么方式管理数据库 `(UN)POOLED`



### `SqlSessionFactory`

`Mybatis` 的核心类，用于初始化 `Mybatis`，创建 `SqlSession` 对象

> 必须要保证其全局的唯一性



### `SqlSession`

操作数据库的核心对象，主要使用 `JDBC` 的方式和数据库交互



### `Mybatis` 数据查询

- 创建实体类
- 创建 `Mapper XML`
- 编写 `<select>`
- 开启驼峰命名映射
- 增加 `<mapper>`
- `SqlSession` 执行 `SQL`



### `SQL` 传参

`<parameterType=>` 可以设置传入参数的类型，`#{value}` 传入指定的值

- 单参数传递，只需要指定参数类型就可以了


- 多参数传递，使用指定的 `java.util.Map` 接口



### 多表关联查询

`Map` 排列顺序是根据 `Hash` 值来决定的，为了保证原顺序不变，可以使用 `java.util.LinkedHashMap`来保存结果

`key` 为字段名，`value` 是字段对应的值



### `ResultMap`

可以将查询的结果映射复杂的 `java` 对象

适用于保存 `java` 对象保存多表查询的结果

支持对象关联查询等高级特性



需要创建数据传输对象 `DTO`

```xml
<ResultMap id="rmGoods" type="dto">
    <!-- 映射主键 -->
    <id property="" column=""></id>
    <result property="" cloumn=""></result>
</ResultMap>
<select id="" resultMap="rmGoods"></select>
```



### `Mybatis` 数据写入

##### 新增

```xml
<insert id="insert" parameterType="Goods">
    <selectKey resultType="int" keyProperty="goodId" order="AFTER">
    	<!-- 获取连接中最后产生的 id 号 -->
        select last_insert_id()
    </selectKey>
</insert>
```



### `selectKey` 和 `useGeneratedKeys` 的区别

`selectKey` 必须书写在 `insert` 标签内

```xml
<selectKey resultType="int" keyProperty="goodId" order="AFTER">
    	<!-- 获取连接中最后产生的 id 号 -->
        select last_insert_id()
</selectKey>
```

`useGeneratedKeys`

为新添在 `insert` 标签中的属性

```xml
<insert id="" parameterType="" 
        useGeneratedKeys="true" keyProperty="goodsId" keyCloumn="good_id"></insert>
```



> 二者主要区别：
>
> 显示和隐示：
>
> `selectKey` 需要明确的编写获取主键的 `SQL` 语句；适用于所有关系型数据库
>
> `useGeneratedKeys` 是根据数据库驱动自动生成对应语句；数据库必须支持自增



##### 更新

```xml
<update id="" parameterType="Goods"></update>
```



##### 删除

```xml
<delete id="" parameterType=""></delete>
```



### 预防 `SQL` 注入攻击

- `${}` 文本替代方式，未经任何处理对 `SQL` 替换
  - 在高级或者复杂的查询下需要进行 `SQL` 的组织，需要用到文本替换
- `#{}` 预编译传值



### 日志处理

日志用来记录系统操作事件的记录文件或者文件集合

日志保存历史数据，是诊断问题以及理解系统活动的重要依据



##### 日志门面

- `Simple Logging Facade For Java`
- `Apache Commons-Logging`



##### 日志实现

- `log4j`
- `logback`
- `java.util.logging(jul)`



```xml
<!-- logback.xml -->
<appender name="console" class="ch.qos.logback.core.ConsoleAppender">
	<encoder>
        <!-- 规定日志输出的格式 --> 
        <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36}</pattern>
    </encoder>
    <!-- debug 以上级别的信息都会使用 console -->
    <root level="debug">
            <appender-ref ref="console"/>
    </root>
</appender>
```



##### 日志的级别(由高到低)

- `error` 系统的故障日志
- `warn` 存在风险或者使用不当
- `info` 一般性消息
- `debug` 程序内部用于调试的信息
- `trace` 程序运行的跟踪消息

> 在生产时候建议将最低级别调整为 `info`；开发环节为 `debug`



### 动态 `SQL`

根据参数数据动态组织 `SQL` 技术

```xml
<select id="dynamicSQL" parameterType="java.util.Map" resultType="Goods">
	select ...
    <where>
        <if test="Id != null">
        	and id=#{id}
        </if>
    </where>
</select>
```





### `MyBatis` 二级缓存

- 一级缓存（默认开启）
  - `SQLSession` 会话
- 二级缓存（手动开启）
  - `Mapper NameSpace`

> 一级缓存操作完之后就会被释放，每个对象之间数据不互通



##### 二级缓存运行原则

二级缓存开启后默认所有查询操作均使用缓存

写操作 `commit` 提交时对 `namespace` 缓存强制清空	 

配置 `useCache=false` 可以不用缓存

配置 `flushCache=true` 强制清空缓存 



```xml
<mapper namespace="">
<cache eviction="LRU" flushInterval="600000" size="512" readOnly="true"/>
<!-- readOnly true 从缓存中取出的是缓存对象本身，效率高 false 每次取出为缓存对象的副本，安全性高 -->
```

> `useCache=false` 针对全局查询结果
>
> `flushCache=true` 立马清空缓存



##### `eviction`

缓存的清除策略，当缓存对象数量达到上限之后，自动触发对应的算法清除缓存对象

- `LRU` 
  - 移除最长时间不被使用的对象
- `FIFO`
  - 按对象进入缓存中的顺序
- `SOFT`
  - 软引用，移除基于垃圾收集器状态和软引用规则的对象
- `WEAK`
  - 弱引用，移除基于垃圾收集器和弱引用规则的对象



### 多表级联查询

实体类体现一对多的关系，可以使用 `List` 对象体现

```xml
<!-- resultMap 可以说明一对多或多对一的映射关系 -->
<resultMap id="rmGoods" type="Goods">
    <!-- 映射主键 -->
	<id property="" cloumn=""></id>
    <!-- 
		collection 得到查询结果之后，对所有 Goods 对象遍历提取 good_id 并带入 goods 命名空间中的 selectByGoodsId SQL 中进行查询赋值给 goodsList
 	-->
    <collection property="goodsList" select="goods.selectByGoodsId" column="goods_id"></collection>
</resultMap>
<select id="oneToMany" resultMap="rmGoods" >
	select *
</select>
```



##### 多对一

多的对象中持有一的实体

```xml
<resultMap id="rmGoods" type="Goods">
	<id></id>
    <!-- cloumn 使用到了 id 会导致 id 无法正确赋值（默认策略） -->
    <result cloumn="id" property="id">
    <association property="good" select="goods.selectById" cloumn="id"></association>
</resultMap>
<select id="selectManyToOne" resultMap="rmGoods">
	select *
</select>
```



### 分页插件 `PageHelper`

- 引入 `PageHelper` 和 `jsqlparser`
- `mybatis-config.xml` 添加插件配置
- 代码中使用 `PageHelper.startPage()` 自动分页



### `MyBatis` 配置 `C3P0` 连接池

创建额外类 `datasource.C3P0DataSourceFactory`



```java
public class C3P0DataSourceFactory extends UnpooledDataSourceFactory {
    public C3P0DataSourceFactory(){
        this.dataSource = new ComboPooledDataSource();
    }
}
```

```xml
<dataSource type="com.company.mybatis.datasource.C3P0DataSourceFactory">
                <property name="driverClass" value="com.mysql.jdbc.Driver"/>
                <property name="jdbcUrl" value="jdbc:mysql://localhost:3306/imooc?useUnicode=true&amp;characterEncoding=UTF-8&amp;useSSL=false"/>
                <property name="user" value="root"/>
                <property name="password" value="123456"/>
                <property name="initialPoolSize" value="5"/>
                <property name="maxPoolSize" value="20"/>
                <property name="minPoolSize" value="5"/>
            </dataSource>
```



### 批处理

##### 批量插入

使用 `<foreach>` 标签对 `collection` 传入的集合进行处理

```xml
<insert id="batch" parameterType="List">\
	insert ... 
    <!-- collection 确定数据源，名字无法随意修改 separator 添加分隔符号-->
    <foreach collection="list" item="item" index="index" separator=",">
    	(#{item.value})
    </foreach>
</insert>
```

> 批量插入数据的局限性：
>
> 无法获取插入数据的 id
>
> 可能生成的 `SQL` 语句过长，服务器拒绝



##### 批量删除

```xml
<delete id="batch" parameterType="List">
	delete ... where id in
    <foreach collection="list" item="item" index="index" open="(" close=")" separator=",">
    	#{item}
    </foreach>
</delete>
```



### 注解

![image-20220223135904159](imgs/image-20220223135904159.png)



##### 使用步骤

- 创建接口

  ```java
  public interface EmployeeDAO {
      @Select("select * from employee where salary between #{min} and #{max} order by eno")
      public List<Employee> selectBySalaryRange(@Param("min") Integer min, @Param("max") Integer max);
  }
  ```

  

- 配置 `mapper`

  ```xml
  <mappers>
  	1.<mapper class="EmployeeDAO"/>
      2.<package name="dao"/>
  </mappers>
  ```

- 书写功能代码



```java
@SelectKey(statement="select last_insert_id()", before = false, keyProperty="id", resultType="Integer.class") // 获取最新插入主键的编号

@Results({
    @Result(cloumn="", property="", id=true) // 设置主键
})
```



# 数据库分页的实现原理

### `Mysql`

```sql
select ... limit 1,10;
```



### `Oracle`

```sql
select t3.* from (
    select t2.*,[rownum] as row from (
    	select t.* from table order by id desc  
    )t2 where rownum <= 20 # 提取行号前20
)t3 where row > 11 # 11 ~ 20
```



### `SQL Server 2000`

```sql
select top 3 * from table
where 
	id not in 
	(select top 15 id from table)
```



### `SQL Server 2012+`

```sql
select * from table order by id offset 4 rows fetch next 5 rows only
```



