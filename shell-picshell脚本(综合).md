



> 声明！
> 学习视频来自B站up主 **泷羽sec** 有兴趣的师傅可以关注一下，如涉及侵权马上删除文章，笔记只是方便各位师傅的学习和探讨，文章所提到的网站以及内容，只做学习交流，其他均与本人以及泷羽sec团队无关，切勿触碰法律底线，否则后果自负！！！！有兴趣的小伙伴可以点击下面连接进入b站主页[B站泷羽sec](https://space.bilibili.com/350329294)
# 变量的定义与使用
##  创建shell脚本

以下的脚本编写都是基于`kali`也就是`Debian`操作系统



首先知道一点，`shell`脚本是以`.sh`结尾的可执行文件，可通过`touch`或`vim`等命令创建一个脚本文件

![](https://github.com/MCheshimian/pic/blob/master/shell-pic/1.jpg?raw=true)



然后在`1.sh`文件中编写一个输出的语句

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/1-1.jpg)

## shell脚本的编写

### 脚本解释器

在进行`shell`脚本编写时，首先第一行内容，就是指定该脚本使用哪种脚本解释器，常见的有三种

1. `#! /bin/bash`
2. `#! /bin/sh`
3. `#! /bin/dash`

一般`sh`是很古老的了，一般使用`sh`其实都是在调用其他的解释器，如在`kali`中的`sh`就是指向`dash`的一个链接

也有的脚本不管开头的指向脚本解释器，最终都是由`dash`进行解释

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/2.jpg)

### 变量的声明和定义

#### 对于变量名称的定义

变量名可以由字母、数字和下划线组成，但不能以数字开头。也就是基本和`python`中定义一样，不需要和其他语言(如`c`)中定义变量时，需要在变量的名称前加上`int`等数据类型，才算定义一个变量

#### 对于变量的调用或使用的定义

定义好的变量，需要使用时，需要在变量名称前加上`$`，表示调用或使用该变量

#### 单引号与双引号的区别

在下面的使用3中可以知道，字符串是用`"`**双引号**圈住的

这里使用`'`**单引号**测试，发现对于定义的变量`name`调用时，不会把变量的值显示，而是把`$name`作为字符输出了

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/2-4.jpg)



所有，如果想要在字符串中可以执行变量并使用其值，就需要把字符串使用双引号圈住。

而对于双引号中有单引号并不会影响变量的调用。可参考**使用3**，我在字符串中设置了`I'm`。

###### 使用1

先定义，然后再执行，需要两条语句

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/2-1.jpg)

###### 使用2

定义执行，一条命令。`;`用于隔开，表示一行代码的结束。`&&`是逻辑运算符，也就是前面变量定义成功后，执行后面的命令

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/2-2.jpg)

###### 使用3

在一段字符串中穿插使用变量，这里就是字符串中有`name`但是注意，字符串中的`name`就会显示为`name`，而字符串中的`$name`，会显示为定义的值

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/2-3.jpg)

###### 使用4

对于未定义的变量直接调用或使用，会直接显示为空，也就是不显示

如，这里并未定义`go`，但是可以看到调用时，无任何显示

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/2-5.jpg)

###### 使用5

对于变量与字符连在一起，这时候可以选择空格隔开，或者使用`"`双引号，把变量名单独圈住，也是可以调用变量

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/2-6.jpg)



或者使用`{}`花括号把变量括起来，也是可以达到输出变量值的效果

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/2-7.jpg)

###### 使用6

`set`命令是一个内建的 shell 命令，主要用于设置和显示 shell 环境变量和函数。它可以修改 shell 的运行环境，包括变量的赋值、控制 shell 的行为选项等。单独使用`set`命令（不带参数）会显示所有已定义的 shell 变量和函数

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/2-8.jpg)

这里看到显示的太多了，那么怎么显示我们想要的呢，可以使用`|`  搭配`grep`

`|`是管道符。它的主要作用是将一个命令的输出作为另一个命令的输入，从而实现多个命令的组合使用，以完成更复杂的任务

`grep`是一个强大的文本搜索工具。它用于在文本文件（或标准输入）中查找包含指定模式的行，并将这些行输出。这种模式可以是简单的字符串，也可以是复杂的正则表达式。这里因为刚开始，不搞复杂的，只搜索简单的字符即可



使用命令`set | grep name`即查询已定义的变量或函数中含有`name`字符的

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/2-9-1.jpg)

![2-9-2](https://github.com/MCheshimian/pic/tree/master/shell-pic/2-9-2.jpg)



`unset`是一个内建的命令，主要用于删除变量或函数

这里删除变量`name`，再去查找会发现已经没有了

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/2-10.jpg)



## shell脚本的执行

正如在1目录中提到了，刚创建的`sh`脚本是没有执行权限的

因为在`linux`操作系统中，由`umask`值控制刚创建的所有文件权限，对于`umask`的值计算，可自行百度，因为一般也很少有人会把`umask`的值设置成新创建的文件具有执行权限。作为了解即可

如果所有新创建的文件都具有执行权限，那么可能会带来安全风险

#### 方法1

给文件加权限，使用`chmod`命令

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/3.jpg)

#### 方法2

使用`bash`、`sh`或`dash`命令来执行脚本文件

因为`bash`和`sh`是具有**执行权限**的程序，它们被允许**读取和处理**文件。当你使用`bash`或`sh`来运行脚本时，就相当于你把脚本文件的内容作为输入传递给了这些 `shell `程序。

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/3-1.jpg)

#### 方法3

`source`命令（在`bash`中也可以写成`.`）是一个内建命令，它的主要作用是在当前 shell 环境中读取并执行文件中的命令。与直接执行脚本文件（通过给文件添加执行权限并运行）不同，`source`命令是将脚本中的命令融入到当前的 shell 进程中。这种方式并不涉及到文件系统对文件执行权限的检查，因为它是基于当前shell的权限和功能来操作的。

一般用于配置文件的加载方面



为测试与方法2有何不同，在`1.sh`文件中加入命令`ls -l`，以长格式显示当前目录下的信息

可以看到，`source`执行的脚本文件中的命令时，作为`1.sh`中的命令`ls -l`的显示，与直接使用命令`ls -l`是一样的

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/3-2.jpg)









# 永久环境变量

## 前言

如前所说，都是临时变量，那么什么是永久变量呢，首先要知道环境变量这一词语。

在windows中，计算机设置中有环境变量这一项，我们平时在终端使用一些命令时，为什么没有指定目录或者不在其目录下的情况时，可以直接使用命令呢，就是因为环境变量。`$PATH`。

诚然在linux系统中也是一样的道理，前面创建的脚本都需要指定目录然后执行，那么如何把脚本假如到环境变量中，使得该脚本也可以像命令一样直接使用。



## 方法1    移动

首先在linux系统中查看环境变量的目录，这些目录下的一些脚本，不需要指定目录，不管在哪个目录下，只要输入命令，就会调取这些目录下的脚本去执行

```shell
echo $PATH
```

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/4.jpg)



如：`ls`，查看其目录`which ls`

然后发现目录`/usr/bin`在环境变量中，那么在使用`ls`时，相当于`/usr/bin/ls`执行了

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/4-1.jpg)



然后把自己创建的脚本移动到这个目录下`/usr/bin`，或者其他环境变量中。这时候就可以直接使用脚本文件的名称，就会执行脚本文件中的代码

这里需要注意，如果是新建的`sh`文件，需要给予可执行权限，不然即使移动到环境变量中，也是不能直接使用的

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/4-2.jpg)





## 方法2 添加

知道环境变量了，并且脚本文件并没有移动到环境变量的目录下的时候，可以把脚本问价所在目录添加到环境变量中，使用`export`指令

```shell
export PATH=/root:$PATH		//必须大写
```

`export`是用于设置环境变量的关键字，使用设置的变量可以在当前`shell`以及由该`shell`启动的子进程中生效



`PATH`环境变量，定义了系统在哪些目录下去寻找可执行程序，如当执行`ls`时，会根据其所指的目录下去寻找对应的可执行文件，然后执行



`/root:PATH`重新定义PATH的值，将`/root`目录添加到原有的`PATH`变量值的最前面（假设原有的`PATH`值存储在变量`PATH`中，这里通过`:PATH`的形式保留原本的值，并添加新的部分），这样的结果是，当系统去查找可执行程序时，会先在`/root`目录下查找，然后再按照原来的`PATH`所指定的其他目录顺序查找



新建一个`test.sh`文件，并给予可执行权限

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/4-3.jpg)



![](https://github.com/MCheshimian/pic/tree/master/shell-pic/4-4.jpg)





使用`export`只是设置了临时变量，**当命令行(终端)关闭后，就会失效的**，可通过把该代码写入到配置文件中(`.bashrc`)才能永久生效，然后使用`source .bashrc`命令，使得该文件生效（或者重启）

`vi /.bashrc`

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/4-5.jpg)



甚至可以输出环境变量，可以看到并没有该目录，但是可以直接使用，因为是写入文件的，所以是永久环境变量并且可直接执行

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/4-6.jpg)



# 字符串的相关操作

```shell
str="hello"			//=与变量名中间不要空格
echo ${#str}		//输出变量str的字符串长度

echo ${str:0:3}		//截取字符串str，从下标0开始，截取3个字符
如果${str:1:1}//表示截取下标为1的一个字符
${str:2:1}//表示截取下标为2的一个字符
```

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/5.jpg)





# 脚本参数传递

```shell
echo 文件名为					   $0
echo 第一个传参是 			   	  $1
echo 传递的参数作为一个字符串显示   	 $*
echo 传递的参数独立作为每个字符串显示 	$@
echo 传递到脚本的参数个数是		   $#
echo 最后命令的退出状态				$?
echo 脚本运行的当前进程ID 			$$


如文件名为1.sh

其中$1是第一个，第二个就可以是$2，那么就可以是$3....$n
sh 1.sh name		就会显示第一个参数为name

$* 就是将参数当作统一的字符串显示出
$@ 将每个字符串当作独立的字符串显示
$? 为0，表示运行正常，其他数字，则出错
$$ 脚本运行的当前进程ID
```



编写`test.sh`文件，并传参，看输出结果

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/6.jpg)

![6-1](https://github.com/MCheshimian/pic/tree/master/shell-pic/6-1.jpg)





# 数学运算



利用`expr`进行数学运算 (**运算符前后有空格的**)

## 加减法

`expr 1 + 2`	

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/7.jpg)

## 乘法

`expr 2 \* 2`，因为`*`需要转义

![]()



![7-1](https://github.com/MCheshimian/pic/tree/master/shell-pic/7-1.jpg)



## 除法

`expr 6 / 3`

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/7-2.jpg)



## 取模

`expr 5 / 3`

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/7-3.jpg)





## 对于加减乘除混合的

`expr 3 + 7 \* 10 `

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/7-4.jpg)



**需要先计算加减的，使用`()`进行处理，而且，`()`需要转义，前后也有空格**

`expr \(3 + 7\) \* 10`

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/7-5.jpg)





## 通过变量赋值，使用`$`

`num = $(expr 5 \* 10)`

`echo $name`

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/7-6.jpg)

当然还有`((....))`的形式，`let`命令

如：

```bash
((name = 5 * 10))
或者
let "name = 5 * 10"

echo $name
```



# 用户交互


## 前言

我们已经知道如何创建脚本并使用，那么，在平常使用一些命令的时候，命令后面都会跟上参数，也就是我们输入的值，就像`python`中的`input`一样，那么如何实现呢，可以使用`read`关键字来达到这种效果

首先进入`bash`环境，在终端输入`bash`即可

如：

```shell
read name age  //这里就会定义两个变量用于接收用户后面输入的信息，是按照顺序接收


echo $name	//输出变量，发现用户输入的信息会输出
echo $age
```

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/8.jpg)





那么在`python`中，用户交互时，会提示该输入什么，这里怎么实现呢，可以使用`read`的`-p`参数

```shell
read -p "请输入你的姓名：" name
//这时候会在这里显示-p指定的信息在这里，然后用户输入即可
echo $name	//输出用户提交的信息
```

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/8-1.jpg)





那么，如果在与用户进行交互时，用户长时间的不输入信息，也会占据进程的，所以可以限制一个时间段，来避免这种情况。那么就可以使用`read`的`-t`参数

```shell
read -t 10 -p "请输入你的姓名：" name
//这时候，如果超过10秒钟，用户不输入任何信息，就会终止退出
echo $name
```

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/8-2.jpg)





那么，对于如果与数据库交互存储数据的话，如果用户的输入总是一些很长不是很有必要的数据的话，可以使用`read`的`-n`参数，来限定用户输入字符的个数

```shell
read -t 10 -n 5 -p "请输入你的姓名：" name
//这时候就会限制用户输入的字符个数，如果超出5个字符就会截取输入的字符并退出
echo $name
```

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/8-3.jpg)



综上所述，都是在终端处理的，那么代码如何写呢

```shell
vim 1.sh

read -p "请输入你的名字" name
echo "你输入的姓名是：$name 请确认"
```

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/8-4.jpg)



# if条件判断

在说`if`之前，先知道关系运算符，不然怎么判断呢

## 关系运算符

```shell
-eq	相等
-lt	小于
-gt	大于
-ne	不等于
-ge	大于等于
-le	小于等于
只能对数值进行判断，字符串不行
这些或对或少都见过，在html编码中可以看到，会把<>=!转换成上面的形式
```



```shell
if的框架

if [条件判断] ; then	//如果条件判断为ture或1，然后执行1，then就是然后的意思
	执行1
else				//如果执行条件不为true或1（也就是否则的意思），执行2
	执行2
fi					//fi表这个if结束，也就是finish的意思

[条件判断]可替换test进行测试，也就是debug的意思
test 条件判断 : then	//就这种形式
```



如，判断，判断两个值是否的大小

```shell
read -p "请输入两个值进行比对大小" num1 num2

#num1=9
#num2=8
if [ $num1 -gt $num2 ] ; then
	echo "$num1大于$num2"
elif [ $num1 -lt $num2 ] ; then
	echo "$num1小于$num2"
else
	echo "$num1等于$num2"
fi
```

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/9.jpg)





# 字符串运算

## 前言

在 Shell 中，比较两个字符串是否相等，使用`[ "$str1" = "$str2" ]`这种形式（注意变量两边要加上双引号，这是为了防止变量值包含空格等特殊字符时出现意外情况）



变量名后面紧接着用等号（注意等号两边不能有空格）连接要赋给变量的值

## 字符串判断

```shell
=		判断两个字符串是否相等，返回true或false
!=		判断两个字符串是否不等，返回true或false
-z		判断字符串长度是否为空
-n		判断字符串长度是否不为空
```



如：

```shell
str1="longyu666"
str2="Longyu666"

#第一种情况
if [ "$str1" = "$str2" ];then
	echo "相等"
else 
	echo "不等"
fi
使用=判断相等
注意：在shell中对于大小写是敏感的

#第二种情况
if [ "$str1" != "$str2" ];then
	echo "不等"
else 
	echo "相等"
fi
使用!=判断不相等，这里会自动变成符号≠

#第三种情况
if [ -z "$str1" ];then
	echo "空"
else
	echo "不为空"
fi
这里-z是检测$str1的长度是否为0，也就是空字符

#第四种情况
if [ -n "$str1" ];then
	echo "不为空"
else
	echo "空"
fi
这里-n是检测$str1的长度不为0，

#第五种情况
if [ "str1" ];then
	echo "str1不为空"
else
	echo "str1为空"
fi
在判断条件中直接以其变量，若变量为空字符串，则不会进入then
```

#### 相等判断

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/10.jpg)

#### 不等判断

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/10-1.jpg)

#### 判断是否为空字符

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/10-2.jpg)



#### 判断是否为不空字符

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/10-3.jpg)



#### 以自身为条件

相当于字符是否有长度为条件，有则相当于`if  true`进入`then`，否则进入`else`

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/10-4.jpg)

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/10-5.jpg)





## 与或运算

```shell
-a		与运算，相当于and
-o		或运算，相当于or
```





以简单的一个字符判断进行扩展

```shell
num1 =9
num2 =8
if [ "$num1" != "9" ];then
	echo "num1不等于9"
else
	echo "num1等于9"
fi
```



大于小于`gt/lt`在shell中只能用于比较数字

以例子说明**与或**

```shell
num1 =9
num2 =8
#定义num1 = 9和num2 = 8时，这些变量实际上是字符串类型
if [ "$num1" != "9" -a "$num2" -lt "9" ];then
	echo "两者都满足了"
else
	echo "未满足"
fi
注意：-a连接两个条件，相当于and
#-lt是小于的意思，具体可以看上一篇文章



if [ "$num1" != "9" -o "$num2" -lt "9" ];then
	echo "两个或一个满足了"
else
	echo "两个都没有满足"
fi
注意：-o连接两个条件，相当于or
```

#### 与运算

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/11.jpg)

#### 或运算

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/11-1.jpg)





# 字符串运算

## 前言

在 Shell 中，比较两个字符串是否相等，使用`[ "$str1" = "$str2" ]`这种形式（注意变量两边要加上双引号，这是为了防止变量值包含空格等特殊字符时出现意外情况）



变量名后面紧接着用等号（注意等号两边不能有空格）连接要赋给变量的值

## 字符串判断

```shell
=		判断两个字符串是否相等，返回true或false
!=		判断两个字符串是否不等，返回true或false
-z		判断字符串长度是否为空
-n		判断字符串长度是否不为空
```



如：

```shell
str1="longyu666"
str2="Longyu666"

#第一种情况
if [ "$str1" = "$str2" ];then
	echo "相等"
else 
	echo "不等"
fi
使用=判断相等
注意：在shell中对于大小写是敏感的

#第二种情况
if [ "$str1" != "$str2" ];then
	echo "不等"
else 
	echo "相等"
fi
使用!=判断不相等，这里会自动变成符号≠

#第三种情况
if [ -z "$str1" ];then
	echo "空"
else
	echo "不为空"
fi
这里-z是检测$str1的长度是否为0，也就是空字符

#第四种情况
if [ -n "$str1" ];then
	echo "不为空"
else
	echo "空"
fi
这里-n是检测$str1的长度不为0，

#第五种情况
if [ "str1" ];then
	echo "str1不为空"
else
	echo "str1为空"
fi
在判断条件中直接以其变量，若变量为空字符串，则不会进入then
```

#### 相等判断

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/10.jpg)

#### 不等判断

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/10-1.jpg)

#### 判断是否为空字符

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/10-2.jpg)



#### 判断是否为不空字符

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/10-3.jpg)



#### 以自身为条件

相当于字符是否有长度为条件，有则相当于`if  true`进入`then`，否则进入`else`

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/10-4.jpg)

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/10-5.jpg)





## 与或运算

```shell
-a		与运算，相当于and
-o		或运算，相当于or
```





以简单的一个字符判断进行扩展

```shell
num1 =9
num2 =8
if [ "$num1" != "9" ];then
	echo "num1不等于9"
else
	echo "num1等于9"
fi
```



大于小于`gt/lt`在shell中只能用于比较数字

以例子说明**与或**

```shell
num1 =9
num2 =8
#定义num1 = 9和num2 = 8时，这些变量实际上是字符串类型
if [ "$num1" != "9" -a "$num2" -lt "9" ];then
	echo "两者都满足了"
else
	echo "未满足"
fi
注意：-a连接两个条件，相当于and
#-lt是小于的意思，具体可以看上一篇文章



if [ "$num1" != "9" -o "$num2" -lt "9" ];then
	echo "两个或一个满足了"
else
	echo "两个都没有满足"
fi
注意：-o连接两个条件，相当于or
```

#### 与运算

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/11.jpg)

#### 或运算

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/11-1.jpg)





# until循环

## 前言

循环与前面的`for`和`while`循环一样，涉及到循环的主要目的就是进行遍历等

这个`until`循环也是一样，用中文翻译这个关键字就是**直到....才**



## 实操

```shell
#!/bin/bash
i=0
until [ ! $i -lt 10 ]
do
	echo $i
	((i++))
done
可以看到这里的结构与前面的循环结构类似
唯一的一点是until关键字

这里的!可以理解为不的意思，与后面的-lt联合解释，就是不小于
until后面的判断是 直到i的值不小于10 (也就是大于10) 才会结束循环
换句话说就是当i的值小于10的时候，会执行循环

这段代码的功能就是输出0-9的数字

```

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/17.jpg)



# case语句

## 前言

与众多的编程语言一样，`shell`中也有`case`分支语句，这个语句的用处很是广泛，而且也是可以配合其他的语句进行使用的



这里进行`case`语句的简单了解，想要更深入的了解，可以自己去想什么地方能用到`case`分支语句

就比如一个简单的终端交互，用户输入对应的数字使用对应的功能，使用`if`语句过于繁杂，这个语句就可以解决

## 实操

#### 数字型

```shell
read -p "请输入一个数值：" num
case $num in
	1)echo "你输入的数字是1"
	echo "对吗"
	;;
	2)echo "你输入的数字是2"
	echo "对吗"
	;;
	*)echo "你输入的是其他数字"
	echo "对吗"
	;;
esac
```

解释：

上面的`read`不用多说了，前面讲过好几次了，是读取用户的输入

`case $num in`这个是分支的开始。就相当于进行分支判断了，判断`num`在下面的哪个分支中

也就是这个`num`的值与下面的`1)、2)...`能够对应的上



比如，输入`1`  那么`num`的值是1，然后与`case`分支比较，发现与`1)`一样，就会执行`1)`中的命令等

那么当用户的输入没有匹配到的话，就会执行`*)`分支中的语句，这个其实相当于其他语言中的`default`一样，当用户输入的值无法匹配，默认就会输出这条分支中的语句



那么，每一个小分支中的`;;`是什么意思呢，表示这条小分支的结束，在这里就相当于结束，除非还有其他的命令。

`esac`表示这整个`case`分支语句的结束



![](https://github.com/MCheshimian/pic/tree/master/shell-pic/18.jpg)

![18-1](https://github.com/MCheshimian/pic/tree/master/shell-pic/18-1.jpg)



#### 字符型

当然上面是数字形式，这里也可以是字符串的形式

```shell
read -p "请输入一个数值：" name
case $name in
	"long")echo "你的名字是long"
	echo "对吗"
	;;
	"yu")echo "你的名字是yu"
	echo "对吗"
	;;
	*)echo "对不起"
	echo "我不知道你的名字"
	;;
esac
```

这里`case`的分支中，`"long")`当然也可以不加双引号，但是建议使用，因为如果输入有空格的话，就会匹配不到该分支



![](https://github.com/MCheshimian/pic/tree/master/shell-pic/19.jpg)

![19-2](https://github.com/MCheshimian/pic/tree/master/shell-pic/19-2.jpg)



# 函数的基本知识

## 前言

与`c`语言中一样，定义函数的方式

下面是定义函数的两种方式

```shell
函数名(){
	函数体
}

或者
function 函数名(){
	函数体
}
```

## 实操

#### 定义变量

```shell
echostr(){
	echo "longyu666"
}
echostr
```



#### 调用方式一

在上述代码的情况下直接输入函数名

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/20-1.jpg)



**这里需要注意以下，函数的调用需要在函数声明之后，不然会提示未找到**

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/20.jpg)





#### 调用方式二

类似于传参的形式，不过`bash`中的传参与其他语言中不同，这里是使用`$1` `$2`...`$n`作为第1、2...、n个参数

```shell
echostr(){
	echo "你的字符串是$1"
}
echostr longyu666
```

与执行脚本一样，当在执行脚本后跟着一个传参时，`$1`就是其第一个传参，`$2`第二个传参......

这里就是在调用函数的使用，通过执行脚本时的第一个传参，`$1`接收该参数值，并在函数体中输出

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/20-2.jpg)



或者，在`shell`脚本中调用，而不是执行脚本时传参

```shell
echostr(){
	echo "你的字符串是$1"
}
str="longyu666"
echostr $str
```

那么这个时候，先定义一个变量`str`，然后在通过函数调用，那么这个时候的`$1`就是调用函数时的第一个参数值

因为在调用函数的时候，并没有把执行脚本时的传参给函数使用，这里的函数使用的是变量为传参

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/20-3.jpg)





当然，也可以多参数的传递，不过需要注意，当在`shell`脚本中，通过函数名+变量的形式调用函数的时候，这个时候的传参`$1`，`$2`等，只能接收调用函数时的传参

而不接受执行脚本时的传参`bash fun.sh longyu666`。



下面这个两种在一起去看结果

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/20-4.jpg)





当然这里也可以与`read`联合使用的

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/20-5.jpg)





# 脚本互相调用

## 前言

在`shell`中，与`python`中一样，像是导入的形式一样，可以加载其他文件中的资源，可以互相调用

## 实操

#### 脚本间的互相调用

创建一个`1.sh`

```shell
vim 1.sh 

echo "hello word"
```

创建一个`2.sh`文件

```shell
vim 2.sh

bash 1.sh    或./1.sh，但是这需要有执行权限

或者这里使用bash执行
使用source使得文件生效
source ./1.sh  //因为1.sh有输出，所以会导致执行echo
这里需要指定路径，./表示当前路径，或者使用绝对路径
如果不加路径，会显示当前目录下的文件和目录，这个可以自己测试
```

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/21.jpg)

![21-1](https://github.com/MCheshimian/pic/tree/master/shell-pic/21-1.jpg)

![21-2](https://github.com/MCheshimian/pic/tree/master/shell-pic/21-2.jpg)



#### 脚本调用变量

创建一个`1.sh`脚本

```shell
vim 1.sh

name="dijia"
age=999
```

这时候再创建`2.sh`脚本

```shell
vim 2.sh

source 1.sh
echo "my name is $name and i am $age years old"
```

解释，这里的`source`在这里是用于加载文件的作用，类似于`python`中的`import`或`c`中的`include`

因为加载了`1.sh`，所以`1.sh`中的变量是可以在`2.sh`中使用的

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/22.jpg)



# 重定向

## 前言

输入重定向和输出重定向

输出重定向是指把前面命令执行的结果重定向到某处

输入重定向是指，把文件中的数据重定向到某处

`>`是输出重定向，若指定的文件有内容，会覆盖原内容

`>>`是输出重定向，若指定的文件有内容，会在文件末尾追加内容

`<`是输入重定向，可以把文件中的内容作为某个命令的参数，或者循环的范围等

## 实操

### 输出重定向

```shell
ls > 1.txt	//把当前目录下的文件或目录重定向到1.txt文件中
cat 1.txt	//验证

who > 1.txt
cat 1.txt

echo "test" > 1.txt
cat 1.txt

echo "555" >> 1.txt
cat 1.txt
```



![](https://github.com/MCheshimian/pic/tree/master/shell-pic/23.jpg)

![24](https://github.com/MCheshimian/pic/tree/master/shell-pic/24.jpg)





````shell
ls >/dev/null	一般使用ls会有回显，但是重定向到这里，相当于垃圾箱，无回显

这里有一个find命令，可以使得在使用find命令寻找的时候，只显示正确数据，其他的数据不显示

find / -name "nmap" 2>/dev/null
````

`2>/dev/null`：这是一个重定向操作。

在 Linux/Unix 系统中，文件描述符

1. 0通常代表标准输入，
2. 1代表标准输出，
3. 2代表标准错误输出。

这里的2>表示将标准错误输出重定向，/dev/null是一个特殊的设备文件，它就像一个 “黑洞”，任何写入其中的数据都会被丢弃。所以将标准错误输出重定向到/dev/null，就使得查找过程中产生的如权限不足、文件系统某些部分无法访问等错误信息不会在终端上显示出来，而只会显示符合条件的查找结果（如果有的话）到标准输出（也就是终端屏幕上，如果没有进一步重定向标准输出的话）。

当然如果想要知道哪些错误输出，可以把错误输出到一个文件中，而不是`/dev/null`中



![](https://github.com/MCheshimian/pic/tree/master/shell-pic/25.jpg)

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/26.jpg)

### 输入重定向

以简单的一个`ls`命令测试

首先创建一个文件

```shell
vim dir.txt
/home/kali
/home/var

然后在终端执行ls

ls -l < dir.txt	//注意这里只会把文件第一行的去进行输入，因为命令单条执行，并非循环
这里是在dir.txt的目录下，所以没有其他路径
这里会把dir.txt文件中的内容，传递给ls -l命令，就会显示这些目录下的文件或目录
因为ls -l 后面可以跟着路径来查看指定目录下的文件或目录的
```

![](https://github.com/MCheshimian/pic/tree/master/shell-pic/27.jpg)





























































































