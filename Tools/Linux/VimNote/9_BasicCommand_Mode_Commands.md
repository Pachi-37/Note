### 命令模式

```shell
:set number
#  显示行号	
```

##### `Q`进入命令行模式

`:p`  `:print`  

- 打印当前行

`visual-mode`

- `:'<,'>p`
- `<`特殊标记，可视模式选择文本开头
- `>`特殊标记，可视模式选择文本结尾



### 替换

`substitute`替换文本

- `:range substitute /from/to/flags`
  - `g`  ——  `global`
  - `p`  ——  `print`
  - `c`  ——   `confirm`
    - `y`
      - 替换
    - `n`
      - 跳过此次替换
    - `a`
      - 全部替换
    - `q`
      - 取消替换，退出
    - `CTRL-E`
      - 上翻
    - `CTRL-Y`
      - 下翻



### 读取文件内容

`:read`

- 读取一个文件内容，写在该行之后

`:write`

- 将文件内容写到其他文件
- 无法覆盖已存在文件，使用`!`
- 可以与可视模式组合使用



##### `:shell`

- 使用`exit`返回