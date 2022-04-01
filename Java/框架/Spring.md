# `Spring`

核心框架  `IoC` 容器和 `AOP` 面向切面编程





### `Spring IoC`

`Inverse of Control` 是一种设计理念，由代理人创建和管理对象，消费者通过代理人来获取对象

`IoC` 的目的是为了降低对象之间的直接耦合

> 对象的创建权转嫁到中间角色，采用 `java` 中的反射技术实现运行是对象的创建



##### `DI` 依赖注入

利用 `java` 中的反射技术来实现	



##### 实例化 `Bean` 的三种方式

- 基于构造方法对象实例化

   ```xml
    <!-- 例用参数名实例化 -->
    <constructor-arg name="" value=""/>
    
    <!-- 例用参数位置实例化 -->
    <constructor-arg index="" value=""/>
   ```

    

- 基于静态工厂实例化

   ```xml
    <bean id="" class="Factory" factory-method="method"/>
   ```

    

- 基于工厂实例方法实例化

  ```xml
  <bean id="factoryInstance" class="FactoryInstance"/>
  <bean id="" factory-bean="factoryInstance" factory-method="method"/>
  ```
  



> `bean` 中 `id` 和 `name` 属性
>
> 都是设置对象在 `IoC` 容器的唯一标识，在同一配置文件中都不允许重复
>
> 允许在多个配置文件中重复出现，新对象覆盖旧对象
>
> `id` 要求更加严格，一次只能定义一个对象标识
>
> `name` 一次允许定义多个对象标识



### 路径表达式

`classpath` 代表编译之后 `class` 文件夹

![image-20220331154419847](imgs/image-20220331154419847.png)

### 依赖注入

- 基于 `setter` 方法注入对象
  - 默认属性赋值是调用 `setter` 方法进行赋值
  - `ref="beanId"` 属性关联赋值
- 基于构造方法注入对象



##### 注入 `List`

```xml
<bean id="" class="">
	<property name="someList">
    <list>
        <value></value>
        <ref bean=""></ref>
    </list>
    </property>
</bean>
```

> `set` 和 `map` 使用方法也类似
>
> `properties` 类似于 `map`，不过其中键值只能为 `string`，常用保存文本信息
>
> 引用设置可以直接设置属性



### 查看容器内对象

- `getBeanDefinitionNames()`
  - 获取 `beanId` 数组

> 未取名的对象命名规则 ：
>
> 完整类命`#number`，提取数据时如果只写完整类名，默认提取第一个元素
