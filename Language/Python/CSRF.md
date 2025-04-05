# CSRF

全称为 `Cross Site Request Forgery` 跨栈请求伪造，`one-click attack`.

在使用者不知情的情况下，让使用者的浏览器自动发送请求给目标网站

在使用某一个网站，发送来一个 正确的`Cookie`，随后有访问一个恶意网站，上面有个表单一旦用户发送表单。正常的网站就会收到带有正确 `Cookie`  的请求。

第三方网站发出的 `Cookie` 除了可以用于发动攻击还可以用来进行用户追踪。



##### ` token `

由 `server` 产生 `token` 存放在 `session` 中由此来判断请求者来源是否可靠

```python
import os
from flask_wtf.csrf import CSRFProtect
 
app.config['SECRET_KEY'] = os.urandom(24)
 
csrf = CSRFProtect(app)
```

```html
<form method="post">
    <input type="hidden" name="csrf_token" value="{{ csrf_token() }}"/>
    <input type="text" name="email" class="form-control form-control-lg" placeholder="max@email.com">
</form>

<script>
var csrf = "{{ csrf_token() }}";
axios.post('/auth/login', data, {
        headers: {'x-csrf-token': csrf}
        })
</script>
```



##### `SameSite`

用来防止浏览器因跨站请求发送 `cookies`

- `Strict`

  - 完全禁止第三方 `Cookies`，跨站点时，任何情况都不会发送 `Cookie`

  > 不是所有的浏览器都支持 `Same site` 功能
  >
  > 会导致跳转第三方网站总是需要登录

- `Lax`

  - 放宽部分限制，大部分时候不会发送，但是导航到目标网址的 `Get` 请求除外
    - 链接
    - 预加载
    - `Get` 表单

- `None`

  - 关闭该属性不过同时需要设置 `Secure` 



# ORM

面向对象是把所有的实例看成对象，关系型数据库则是采用实体之间的关系连接数据。

`ORM` 就是通过实例对象来操作数据库



`ORM` 需要有大量的配置，无法应对复杂的查询



- 创建 `Model`

  - 将数据库中的表转变为一个类，叫做创建数据模型
  - 模型中可以描述各个字段在数据库中的定义，并且定义自己的方法

  ```python
  class Person(BaseModel) {
      name = Column(String)
      age = Column(Integer)
      contact= relationship('Contact', uselist=False, backref='student')
      
      def get_info():
          return self.name + " " + self.age
      
      
      def save():
      	add(self)
      	commit(self)
      
  }
  
  class Contact(BaseModel) {
      id = Column(Interger, primary_key=True)
  }
  person = await Person.find()
  ```

- 操作数据库

- 关系

  - 一对一
  - 一对多
  - 多对多
    - 一般需要一张中间表







