# Linux常用命令

#### `ls `

语法：` ls [-alrtAFR] [name...]`

- `ls -l`：显示文件名，文件形态，权限，拥有者，文件大小 等信息

![](https://markdown-1259282458.cos.ap-nanjing.myqcloud.com/img/20210816153402.png)

- `ls -a`:显示隐藏文件
- 输出详解：以`drwxr-xr-xr@ 14 shenll1997 admin  476 8 15 15:19 elasticsearch`为例
  - `drwxr-xr-x`:
    - `d`:文件类型
      - d:目录
      - l: 链接
      - -:文件
      - 
    - `rwx`:文件拥有者权限 r：读 w：写 x：执行
    - `r-x`:文件所属组的权限
    - 最后一个`r-x`:其他用户的权限
    - 即当前权限为 755。  r：4 w：2  x：1
  - 14 表示该目录中的子项数(包含隐藏文件)
  - shenll1997 文件拥有者
  - admin 所属组
  -  8 15 15:31 最后访问时间
  - 最后是文件名 

---

#### `stat`

显示文件inode的元信息

---

#### `cat`

将文件内容打印到控制台

---

#### `mount`

用于挂载linux系统以外的文件系统。

---

#### `pwd`

显示当前工作目录

---

### 权限管理

#### `chmod`

change mode 改变权限。 只有文件所有者和超级用户可以修改文件或目录的权限。

![](https://markdown-1259282458.cos.ap-nanjing.myqcloud.com/img/20210816161816.png)

语法：`chmod [-cfvR]  mode file...`

该命令有两种模式

- 符号模式
  - `chmod 对象操作符权限`
  - `chmod u+x`:给拥有者加执行权限
  - 对象
    - a：所有人
    - u：拥有者
    - g：所有组
    - o：其他人
  - 操作符
    - `+`:添加
    - `-`：除去
    - `=`；设置为
  - 权限：
    - r
    - w
    - x
- 八进制语法
  - `chmod 754 filename`  :设置权限为`rwxr-xr--`

#### `chown`

Change owner 改变文件拥有者

`chown   owner:group filename` 

---

#### `which`

在$PATH中查找符合条件的文件

---

### 系统控制

#### `ps`

process status 查看当前瞬间进程状态。

#### `grep`

字符串正则表达式匹配工具

#### `top`

#### `kill`

---

#### 杂项

- `exp1|exp2`: 管道符，以exp1的标准输出作为exp2 的输入 
- `exp1 || exp2`:` exp1 || exp2 ` exp1执行失败那么执行exp2
- `exp1 & exp2`:  无论exp1是否成功exp2都被执行
- `exp1 && exp2`:exp1 执行成功才执行 exp2