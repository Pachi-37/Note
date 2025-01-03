# Automatic Completion

### 自动补全

- `CTRL-P`
  - 根据之前书写的单词进行补全
  - 来源
    - 当前文件
    - 缓冲区列表
    - 标签文件

|命令|作用|
| ------- | ---------- |
| `<C-p>` | 前一个选项 |
| `<C-n>` | 后一个选项 |
|||
|||

##### 设置

- 忽略大小写
  - `set ingnorecase`
- 如果想要匹配大写的字符串，而文本存在的为小写，告诉`vim`从键入的内容来推断大小写
  - `set infercase`
- 控制搜索单词的范围
  - `set complete=key,key,key`
  - `set complete -=`  #  禁用
    - `set complete +=`  #  启用

| `key`   | 范围     |
| ------- | -------- |
| `.`     | 当前文件 |
| `b`     | 缓存区文件（非窗口） |
| `d`     | 当前文件和#include指令包含的文件中的定义 |
| `i`     | 通过使用#include指令，当前文件包含的文件 |
| `k`     | 拼写字典的单词 |
| `kfile` | 文件名 |
| `t`     | 标签文件 |
| `u`     | 未加载的缓冲区 |
|`w`|其他窗口文件|

> 注：以上路径选择同样适用于其他命令