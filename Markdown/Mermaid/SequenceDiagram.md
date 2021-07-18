[返回](../Mermaid.md)

# `SequenceDiagram`

> 关键字 `end` 使用是可能导致破坏图表
>
> 如果一定要使用，请使用 `()` 或 `[]` 或 `""` 将单词包裹起来



### 语法

`sequenceDiagram`
`participant Alice`
`participant John`
`[Actor][Arrow][Actor]:Message text`

```mermaid
sequenceDiagram
Alice->>John:Hello
John-->>Alice:Hi
```

### 取别名

`sequenceDiagram`
`participant A as Alice`
`participant B as John`
`A->>B:Hello`
`B-->>A:Hi`



### 矢

- `->`

  ```mermaid
  sequenceDiagram
  participant Alice
  Alice -> Alice:Hello
  ```

  

- `-->`

 ```mermaid
  sequenceDiagram
  participant Alice
  Alice --> Alice:Hello
 ```


- `->>`

 ```mermaid
  sequenceDiagram
  participant Alice
  Alice ->> Alice:Hello
 ```


- `-->>`

 ```mermaid
  sequenceDiagram
  participant Alice
  Alice -->> Alice:Hello
 ```

- `-x`

 ```mermaid
  sequenceDiagram
  participant Alice
  Alice -X Alice:Hello
 ```

- `--X`

 ```mermaid
  sequenceDiagram
  participant Alice
  Alice --X Alice:Hello
 ```

> 使用单向箭头来表示消息：
>
> 实线代表主动发出消息
>
> 虚线代表响应
>
> 末尾带`x`代表异步消息，无需等待回应



```mermaid
sequenceDiagram
    Alice->>+John: Hello John, how are you?
    Alice->>+John: John, can you hear me?
    John-->>+Alice: Hi Alice, I can hear you!
    John-->>+Alice: I feel great!
```



### 激活

激活框代表消息处理时的时间间隔

- 使用关键字

`(de)activate [Actor]`

- 使用符号
  - `+ == activate`
  - `- == deactivate`

> 注：消息发出者不能设置非激活状态



### 标注

- `Note right of [Actor]`
- `Note over [Actor],[Actor]`



### 循环

`loop Loop text`

`statements`

`end`

```mermaid
sequenceDiagram
loop Loop Text
Alice --> John:Hello
end
```



### 可替代路径

`alt Describing text`

`statements`

`else`

`state`

`end`



`opt describing text`

`statements`

`end`



```mermaid
sequenceDiagram
alt if
Alic --> Jhon:i
else
Alic --> Jhon:e
end
opt other
Alic --> Jhon:o
end
```



### 展示并行发生事件

`par [Action]`

`and [Action]`

`statements`

```mermaid
sequenceDiagram
par Action_1
Alice --> Jhon:Action1
and Action_2
Alice --> Jhon:Action1
end
```



### 背景加亮

`rect rgb(r,g,b)`

`content`

`end`

```mermaid
sequenceDiagram
rect rgb(213,123,133)
Alice --> Jhon:Hello
end
```



### 代码注释

`%%`



### 显示顺序

`autonumber`

```mermaid
sequenceDiagram
 autonumber
    Alice->>John: Hello John, how are you?
    loop Healthcheck
        John->>John: Fight against hypochondria
    end
    Note right of John: Rational thoughts!
    John-->>Alice: Great!
    John->>Bob: How about you?
    Bob-->>John: Jolly good!
 	
```

 <script>       mermaid.initialize({         sequence: { showSequenceNumbers: true },       });     </script>





