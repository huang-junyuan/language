# vbs教程

使用`'`或`Rem`开头的行为注释行

```vbscript
'注释行
Rem 注释行
Dim name, msg
msg = "请输入你的名字"
name = InputBox(msg, "名称","默认值")
MsgBox(name)
```

`Dim`用来声明一个变量，在vbs中，变量类型并不是那么重要，因为vbs会自动识别变量类型，而且变量在使用前不一定要先声明，程序会动态分配变量空间。所以上面第三行语句可以删除，效果相同。但是一个变量的基本原则是：先声明，后使用。变量名用字母开头，可以使用下划线和数字，但不能使用vbs已经定义的字，也不能是纯数字。

当msg被再次复制时，原值就会消失。

`InputBox`的第一个参数显示在提示栏里，第二个参数是对话框的标题，第三个参数为输入框中的默认值（第二个和第三个参数可以不填写），返回值为输入的内容（字符串）。



自定义的常量（一般来说，常量名全部大写）

```vbscript
const PI = 3.14
const NAME = "记忆碎片"
```

声明变量

```vbscript
Dim a1, a2, a3
```



运算的符号

* +
* *
* /
* -
* mod （取模/余）
* ^ （幂）
* <>  不等于
* =  赋值以及判断是否相等



字符串可以用`+`来连接起来，一个数字字符串用`*`运算时，被强制转换成数字类型。

`int()`函数的功能是将输入值转化成整数值

```vbscript
a = "1"
b = "2"
c = (int(a) + int(b)) * 2
```



布尔变量

```vbscript
dim a, b
a = true
b = false
```



程序流程控制语句

```vbscript
dim a, b
a = 12
b = 13
if a < b then MsgBox("a小于b")
```

注意：在上面的语句中，then之后只能有一个语句，所以下面的语句会报错

```vbscript
dim a, b
a = 12
b = 13
if a < b then MsgBox("a") MsgBox("b")
```



有多条语句要执行时，使用语句块

```vbscript
dim a
a = InputBox("请输入一个大于100的数")
a = int(a) '强制类型转换
if a > 100 then
	MsgBox("正确")
	MsgBox("Good")
elseif a = 100 then
	MsgBox("老大你耍我")
else
	MsgBox("错误")
end if
```

`elseif`语句可以出现多次



逻辑运算符`and`、`or`

```vbscript
dim a, b
a = int(InputBox("请输入一个大于10的数"))
b = int(InputBox("请再输入一个大于10的数"))
if a > 10 and b > 10 then
	MsgBox("正确")
	MsgBox("Good")
elseif a > 10 or b > 10 then
	MsgBox("只有一个正确")
else
	MsgBox("错误")
end if
```



`select case`选择语句

```vbscript
dim a
a = int(InputBox("请输入1-3的数字", "输入"))
Select case a
case 1
	MsgBox("一")
case 2
	MsgBox("二")
case 3
	MsgBox("三")
case else
	MsgBox("输入错误")
end Select
```



循环结构

```vbscript
do
	msgbox("我是大哥")
loop
```

对话框会不断出现，通过任务管理器关掉进程

`exit do`语句终止循环

```vbscript
dim a
const password = "123"

do
	a = InputBox("请输入密码")
	if a = password then
		MsgBox("密码校验成功")
		exit do
	else
		MsgBox("密码校验失败")
	end if
loop
```



`while`关键字可以放在`do`或者`loop`后面，然后再接一个表达式，当表达式的值为true的时候，才运行循环体。

```vbscript
dim a,ctr
const password = "123"
ctr = 0
do while ctr < 3
	a = InputBox("请输入密码")
	if a = password then
		MsgBox("密码校验成功")
		exit do
	else
		MsgBox("密码校验失败")
		ctr = ctr + 1
	end if
loop
```



for循环

```vbscript
dim i

for i=0 to 5
	MsgBox(i)
next
```

