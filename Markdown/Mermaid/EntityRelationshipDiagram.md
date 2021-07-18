[返回](../Mermaid.md)

# Entity Relationship Diagram

[介绍](ER.md)



实体之间的关系由带有表示基数的线表示



# 语法



### 实体和关系

` <first-entity> [<relationship> <second-entity> : <relationship-label>]`

> 只有第一个实体是强制的

```mermaid
erDiagram
TEST ||--|{ ROOM:contains
```

##### 关系

- 第一个实体相对于第二个实体的基数
- 关系是否赋予“子”实体以身份
- 第二个实体相对于第一个实体的基数

基数是一种属性用来实体之间存在多少属性关系

| Value (left) | Value (right) | Meaning                       |
| ------------ | ------------- | ----------------------------- |
| `|o`         | `o|`          | Zero or one                   |
| `||`         | `||`          | Exactly one                   |
| `}o`         | `o{`          | Zero or more (no upper limit) |
| `}|`         | `|{`          | One or more (no upper limit)  |



指定非识别关系 `PERSON }|..|{ CAR : "driver"`



### 属性

`TABLENAME{type name}`