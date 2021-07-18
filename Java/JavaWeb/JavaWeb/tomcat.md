[返回](../JavaWeb.md)

# Tomcat

### 安装Tomcat



### Tomcat的启动和配置



### 配置

`server.xml`

- 可以配置启动的端口号

  - `tomcat 8080`
  - `mysql 3306`
  - `http 80`
  - `https 443`

  ```shell
  <Connector port="8080" protocol="HTTP/1.1"
                 connectionTimeout="20000"
                 redirectPort="8443" />
  ```

  

- 可以配置主机的名称

  - 默认主机名为 `localhost`
  - 默认网站存放位置 `webapps`

  ```shell
  <Host name="localhost"  appBase="webapps"
              unpackWARs="true" autoDeploy="true">
  ```



 网站是如何进行访问 

 输入域名

 检查本机 `hosts` 配置文件有没有映射

 ​	直接返回对应的Ip地址

​	 查询 `DNS` 服务器

配置环境变量



### 发布网站

- 网站，放到服务器指定的 `web` 应用文件夹下

```shell
网站目录结构
--webapps: Tomcat服务器的web目录
	--Root
	--【web_name】：网站的目录名
		- WEB-INF
			- classes：Java程序
			- lib：web依赖
			- web.xml
		- index.html ：默认的首页
		- static
```

