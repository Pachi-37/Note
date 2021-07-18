[返回](../JavaWeb.md)

# Maven

项目架构管理工具

###### 约定大于配置

##### 下载安装 `Maven`

##### 配置环境变量

##### 阿里镜像

##### 本地仓库

- 本地仓库
- 远程仓库

##### 使用 `IDEA` 创建 `Maven` 项目

```
GroupId				组Id
ArtifactId			项目名
Version				版本
```



##### 标记文件夹功能



##### 配置 `Tomcat`



##### `pom` 文件

`pom.xml` 是 `maven` 的核心配置

```json
<!-- Maven版本和头文件 -->
<project>

<!-- GAV -->
<groupId>
<artifactId>
<version>

<!-- 项目的打包方式
jar: Java 应用
war: JavaWeb应用
-->
<packaging>
  
<!-- 配置
项目的默认构建编码
编译版本
-->
<properties>

<!-- 项目依赖 -->
<dependencies>

<!-- 项目构建 -->	 
<build>
```

> `Maven` 可以导入该架包依赖的其他架包



##### 可能遇到的问题

`Maven` 资源导出问题

- 在 `build` 配置 `resources`，来防止资源导出失败

```xml
<resources>
	<resource>
		<directory>src/main/java</directory>
		<includes>
			<include>**/*.properties</include>
		</includes>
		<filtering>false</filtering>
	<resource>
<resources>
```

