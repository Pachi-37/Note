# Vim基本介绍

### 四种模式

- 正常模式

  - 默认进入的模式

- 插入模式

  - 进行文字编辑

- 命令模式

  - 执行vim命令

- 可视模式

  - 选中文本



##### 模式之间切换

- 回到正常模式

  - 无论处于什么模式`<Esc>`可以会回到正常模式

- 插入模式

- 命令模式

  - `：`

- 可视模式



### 移动

​			^

​			k

< h		 		 l >		或使用小键盘

​			j

​			v



### 插入

- `i`：光标之前插入

- `a`：贯标之后追加

- `o`：当前行下插入一行并编辑

- `O` ：当前行上插入一行并编辑



### 删除

`x`：这里使用<X>来删除当前光标指示的一个字符

 

`dd`：删除一行



### 撤销&重做

`u`使用`u`来撤销上一次为文本编辑命令

`U`使用`U`来撤销对一行的命令

`<C-r>`重做



### 保存并退出

`ZZ`



### 不保存强行退出

`:q!`



### Help

`:help `/ `<F1>`

`:help tutor `

-  获取主题帮助


`:help subject `

- 获取命令帮助

`:help 【command】`



| What                  | Prefix  | Example             |
| --------------------- | ------- | ------------------- |
| Normal-mode commands  |         | `:help x`           |
| Control character     | `CTRL-` | `:help CTRL-a`      |
| Visual-mode commands  | `v`     | `:help v_a`         |
| Insert-mode commands  | `i`     | `:help i_<Esc>`     |
| ex-mode commands      | `:`     | `:help :quit`       |
| Command-line editing  | `c`     | `:help c_<Del>`     |
| Vim command arguments | `-`     | `:help -r`          |
| Option                | `''`    | `:help 'expandtab'` |






