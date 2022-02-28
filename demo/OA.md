# OA系统

办公自动化系统



### 需求

- 采用多用户的 `B/S` 架构
- 主用户分配系统账户，下级用户使用该账户登录系统
- 采用分级定岗，一共分为八级



### 具体要求

- `6` 级含以下为 `业务岗`
- `7` 级 `部门经理`
- `8` 级 `总经理`



![image-20220223143043463](imgs/image-20220223143043463.png)



### 框架及组件

![image-20220223143409856](imgs/image-20220223143409856.png)



### `RBAC`

基于角色的权限控制是面向企业安全策略的访问控制方式

核心思想：将控制访问的资源和角色绑定



### `md5` 摘要算法

`MD5` 可以产生一个 128 位的散列值用于唯一标识原数据



- 压缩性，`MD5` 生成的摘要长度固定
- 抗修改
- 不可逆，无法通过反向推算源数据

> `Commons-Codec`