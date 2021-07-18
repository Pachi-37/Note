[返回](../JavaWeb.md)

# Http

`http` (超文本传输协议) 是一种 `请求-响应` 协议

`https`:安全

- `http1.0`
  - `Http/1.0`
    - 客户端和 `web` 服务器连接，只能获得一个 `web` 资源
- `http2.0`
  - `Http/1.1`
  - 可以获得多个 `web` 资源



### `Http请求`

客户端 -- 发请求（`Request`）-- 服务器

```java
Request URL: https://www.baidu.com/	请求地址
Request Method: GET					get方法/post方法
Status Code: 200 OK					状态码
Remote Address: 183.232.231.174:443	远程地址
```



```java
Accept: text/html
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: max-age=0
Connection: keep-alive
```

##### 请求行

- 请求方式 ==`Get` `Post`== `HEAD` `DELETE` `PUT`
  - `get`
    - 请求能够携带的参数比较少，`URL` 地址栏显示数据内容，不安全，但是高效
  - `post`
    - 携带参数没有限制，不会显示内容，安全



##### 消息头

```java
Accept				告诉浏览器，支持的数据类型
Accept-Encoding		
Accept-Language
Cache-Control
Connection			请求完成，断开还是保持连接
```

### `Http响应`

```java
Cache-Control: private					缓存英语
Connection: keep-alive					保持连接
Content-Encoding: gzip					编码
Content-Type: text/html;charset=utf-8
```

##### 响应体

```java
Accept: text/html
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: max-age=0
Connection: keep-alive
    
Refrush 		刷新间隔
Location		让网页重新定位
```

##### 响应状态码

- `200`
  - 请求成功
- `3**`
  - 请求重定向
- `404`
  - 找不到资源

- `5**`
  - 服务器代码错误



## 常见面试

浏览器中地址栏输入地址并回车的一瞬间页面能够展示回来，经历的过程

