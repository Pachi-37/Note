# manjaro

- rufus			U盘启动（DVD模式）

- BIOS启动  

  - 开机顺序（USB最高）
  - Security boot 关闭

- 换源

  - sudo nano /etc/pacman.conf

  - multitlib

    - ```
      [archlinuxcn]
      SigLevel = Never
      Server = http:……
      ```

      CTRL+x

  - sudo pacman-mirrors -c China

  - sudo pacman -Syyu





### 安装软件

- 录屏软件
  - ![image-20200425182639828](C:\Users\minix\AppData\Roaming\Typora\typora-user-images\image-20200425182639828.png)

- 键盘
  - ![image-20200425182909311](C:\Users\minix\AppData\Roaming\Typora\typora-user-images\image-20200425182909311.png)

#### 更改文本编译器

- sudo pacman -S vim
- Color

![image-20200425183817183](C:\Users\minix\AppData\Roaming\Typora\typora-user-images\image-20200425183817183.png)

- bash
  - ![image-20200425184005387](C:\Users\minix\AppData\Roaming\Typora\typora-user-images\image-20200425184005387.png)
  - ![image-20200425184216750](C:\Users\minix\AppData\Roaming\Typora\typora-user-images\image-20200425184216750.png)



- 其他
  - alias  c clear
  - funcsave  c



### 安装i3

- sudo  pacman -S i3

- super + <enter>

- vim ~/.Xresources

  - ![image-20200425193730437](C:\Users\minix\AppData\Roaming\Typora\typora-user-images\image-20200425193730437.png)

    

### 桌面

- super+数字
- super+《enter》  打开终端
- super + f   /t

### 终端

- ![image-20200425194255545](C:\Users\minix\AppData\Roaming\Typora\typora-user-images\image-20200425194255545.png)

- ![image-20200425194356588](C:\Users\minix\AppData\Roaming\Typora\typora-user-images\image-20200425194356588.png)

super  +  d

​	菜单



### 安装xorg更改按键

- sudo  pacman  -S  xorg
- ![image-20200426065453717](C:\Users\minix\AppData\Roaming\Typora\typora-user-images\image-20200426065453717.png)