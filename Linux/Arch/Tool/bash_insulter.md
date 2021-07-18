[返回](Outline.md)

# bash_insulter

bash学习脚本，主要用来辅助bash命令的学习

### 安装

需要的软件 `git`

```bash
git clone http://github.com/hkbakke/bash-insulter.git

sudo cp /bash-insulter/src/bash.command-not-found /etc/
```



##### 编辑 `/etc/bash.bashrc`

添加以下内容，启用脚本

```bash
#Bash Insulter
if [ -f /etc/bash.command-not-found ];then
. /etc/bash.command-not-found
fi
```



终端调到 `bash`



跟新 `bash.bashrc`

```bash
source /etc/bash.bashrc
```



自定义语句，更改 `/etc/bash.command-not-found` 中的 `message`