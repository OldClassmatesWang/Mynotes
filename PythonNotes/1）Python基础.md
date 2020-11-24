# 1）Python基础

## 一、编程规范

> 很多语言在学习的一开始都会说明编程规范，不管是网上的教程还是书本上的学习，基本上已经成为了做书做教程思维的一个基本定视，其实学了C，JAVA，kotlin，再学Python，返回头来看这些事情，其实在编程规范上就是从语言编写上区分语言的一个重要的部分。

1. 严格使用**缩进**来体现代码的逻辑从属关系，Python对代码的缩进是硬性要求的，一般以**四个空格**为一个缩进单位

2. 每个import 语句只导入一个模块，最好按照标**准库，扩展库，自定义库**的顺序依次导入，尽量**避免导入整个库**，最好只导入**确实需要使用的对象**

   > 这里可以思考一下，为什么最好不要全部导入的原因就是导入太多冗余遍历会影响程序运行的速度，Python本身的速度就不高，如果不在编写上注意一下提高速度，码量上去之后对速度的影响还是很大的。

3. 最好在类定义、函数定义和一段完整的功能代码之后**增加一个空行**，在运算符两侧**各增加一个空格**，逗号后面增加一个空格

4. 语句过长，可以拆分成多个短一点的语句，可以使用续行符“\”，或者圆括号把多行代码括起来表示一句语句

5. 书写复杂的表达式，在适当的位置写上括号

6. 注释两种

   1. #表示单行注释
   2. ''' 表示多行注释，常用于打断说明性文本的注释

## 二、标准库与扩展库

在Python的安装包里面只包含了标准库，并不包含任何扩展库，而扩展库是开发人员根据实际需要才选择的合适库。、

**PIP工具**是Python自带的**管理扩展库的主要方式。**

> pip 命令：
>
> 1. pip freeze  列出已安装的模块及其版本号
> 2. pip install SomePackage 在线安装
> 3. pip install SomePackage.whl 通过whl文件离线安装扩展库
> 4. pip install package1 package2 ... 在线安装多个包
> 5. pip install -r requirements.txt  安装requirement.txt 文件中的指定的扩展库
> 6. pip install --upgrade SomePackage 升级SomePackage 模块
> 7. pip unistall SomePackage 卸载SomePackage 模块

示例：--下载安装扩展库

1. 下载会遇到两种情况
   1. 安装时要求本机有安装好对应版本的C/C++编译器
   2. 扩展库暂时没有与本机对应的官方版本
      1. 这两种的处理方式就是去下载.whl文件
      2. 切换到对应版本的Pythonb 安装目录的scrips 文件夹中’
      3. 然后执行pip命令进行安装
2. 如果没有什么问题就是 
   1. pip install 扩展库名



示例：

![image-20201109164720003](https://whpbucket.oss-cn-beijing.aliyuncs.com/myImg/20201124195524.png)

![image-20201109164802895](https://whpbucket.oss-cn-beijing.aliyuncs.com/myImg/20201124195537.png)





### 1、导入标准库和扩展库

- import 模块名 【as 别名】
- from 模块名 import 对象名【as 别名】
- from 模块名 import *

1）使用import 模块名 as 别名 这种方式将模块导入后，使用时需要在对象名前面加上模块名作为前缀，必须以 “模块名.对象名”进行访问，导入的模块很长就可以为导入的模块设置一个别名，使用别名. 对象名的方式来使用其中的对象‘

示例：

```python
import math           #导入标准库math
math.gcd(56,64)       #计算最大公约数
```

```python
import  random  #导入标准库random
n = random.random()  #获得[0,1)内的随机小数
n = random.randint(1,100)  #获取[1,100) 区间中的随机整数
n = random.randrange(1,100)  #返回随机数区间[1,100} 区间中的随机整数
```

> randint 函数：静态方法
>
> random.randint(lower limit,upper limit) 获取指定范围内的随机整数，包头不包尾
>
> randrange 函数： 静态方法
>
> random.randrange (lower limit, upper limit,step) 获取指定范围内的随机整数，包头不包尾，step 指定的是递增计数
>
> 两个方法都是random标准库内置函数，不能直接来调用，必须通过引入random 模块来调用

```python
import os.path as path             #导入os.path 模块，设置别名为np
path.isfile(r"D:\yunding.txt")     #通过模块别名来调用其中的方法
```

![image-20201109152415420](https://whpbucket.oss-cn-beijing.aliyuncs.com/myImg/20201124195554.png)

缺乏安装扩展库

```python
import numpy as np       #导入扩展库numpy，设置别名 np
a = np.array((1,2,3,4))  #通过模块的别名来访问其中的对象
print(a)
```

根据python 的编码规范，一般建议每个import 语句只导入一个模块，并且要按照**标准库、扩展库和自定义库**的顺序导入

2）from 模块名 import 对象名 [as 别名]

```python
import numpy as np #导入模块设置模块别名
from random import sample as sa #导入random 模块的sample对象，并设置对象的别名为sa
```

这种方式是导入明确对象，可以为导入的对象取一个别名，这样导入可以减少查询次数，提高访问速度（Python速度是短板），同时也可以减少程序员的码量，不需要使用模块名作为前缀

示例：

```python
from os.path import isfile
b = isfile(r'C:\windows')
print(b)
```

```python
from math import sin as f #给导入的对象sin起个别名f
n = f(3) 
print(n)
```

3）from 模块名 import*

一次性导入模块中的所有对象，可以直接使用模块中的所有对象而**不需要再使用模块名作为前缀**，但一般并**不推荐**这样去做

示例：

```python
from math import * #导入标准库math中的所有的对象
sin(3)             #求正弦值
sqrt(9)            #求9的平方根
pi				   #常数Π
e                  #常数e
log2(8)
log10(100)
radians(180)       #把角度转换为弧度
```

### 2、python程序的_ name _属性

首先对于python程序文件来说可以作为模块导入也可以直接运行

_ name _ 属性用于识别程序的使用方式的属性，如果作为模块导入，则_ name _ 属性值为 字符串 _ 模块名 _，也就是说，它的属性值被自动设置为模块名，如果作为程序直接运行，则 _ name _ 的属性值被设置为字符串 _ main _

示例：

```python
def main():         #def 是python中定义函数的关键字
    if _name_ == '_mian_':  #选择结构用来识别当前的运行方式
        print("This program is run directly")
    elif _name_ == 'hello':  #冒号、换行、缩进 表示一个语句块的开始
        print("This program is used as a module")
        
main()  #调用上面定义的函数块
```

那么通过任何方式直接运行上面的程序，都会得到下面的结构

This program is run directly

而使用import hello 导入改模块时，得到的结果如下：

This program is used sd a mdule



> 这块简单来说就是 _ name _ 就是一个表示python程序文件使用方式的属性
>
> 如果 用于模块来使用 则属性值为 _ 模块名 _
>
> 如果 用于直接运行 则属性值为 _ main _



## 三、Python的内置对象

Python中一切皆对象，数据类型是对象，函数的返回也是对象

分类：

- 内置对象
  - 可以直接使用
- 标准库对象
  - 需要导入之后才能使用
- 扩展库对象
  - 需要先安装相应的扩展库后才能导入并使用

### 1、常量与变量

常量是不能改变的字面值

在Python中不仅变量的值是可以变化的，变量的类型也是可以随时改变的。

且不需要提前声明变量名及其类型，赋值语句可以直接创建任意类型的变量。

·示例：

```python
x = 5
print(type(x)) #内置函数type 用来查看变量类型
print(isinstance(x,int))  #内置函数isinstance测试变量是否为指令类型 
```

![image-20201109215020999](C:%5CUsers%5C%E7%99%BD%E6%98%BC%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201109215020999.png)

赋值语句的执行过程：先将等号右侧表达式的值计算出来，然后在内存中寻找一个位置把值存储进去，最好创建变量指向这个内存地址

就是说Python变量并不直接存储值，而是存储值的内存地址或者引用，这也是变量类型可以改变的原因

> 思考：
>
> 如果这样说的话，对于java 来说也一样，变量只是存储了地址，那么为什么java定义变量就必须要定义变量类型，且变量类型不能随时改变呢？

**虽然Python变量的类型可以随时改变**，但是Python仍然是一种**强类型编程语言**，Python 的解释器会根据逻辑运算符右侧表达式的值来**自动推断变量类型**

在定义变量名的时候，标识符要求一样，但是Python 不建议使用系统内置的模块名，类型名，函数名以及已导入的模块名及其成员名组为标识符

### 2、数字类型

Python的数字内置对象有整数，实数，复数

整数类型：

1. 二进制：0b开头
2. 八进制：0o开头
3. 十六进制：0x开头

不必担心数值的大小问题，Python支持**任意大小的数字**

同时具有实数精度计算的问题，所以应该避免实数运算比较问题

```python
a = 3.0;
b = 2.0;
c = 3;
d = 1;
print((a-b)==(c-d))
```

![image-20201110150847082](C:%5CUsers%5C%E7%99%BD%E6%98%BC%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201110150847082.png)

为了提高可读性，Python 3.6x以及更高版本支持在数字中间位置添加单个下划线作为连接符，下划线可以出现在中间的任何位置，但是不能出现在开头和末尾的位置，也不能将下划线连续起来使用

```
100_00_00 正确
_100_00 错误
1__000错误
```

### 3、字符串类型

Python中**没有字符常量和变量的概念**，只有字符串类型的常量和变量，**即使单个字符也是字符串**。Python 使用单引号、双引号、三引号三双引号作为定界符来表示字符串

并且不同的定界符之间可以相互嵌套，Python 3.x 全面支持中文，中文和英文都作为一个字符对待，甚至可以使用中文来命名变量名

加号--作为连接符可以连接字符串

乘号--作为重复符可以重复字符串

使用切片访问字符串中的一部分字符

且Python提供了大量的方法支持查找、替换、排版等操作

```python
x = 'Hello world'
x = "hello world"
x = '''hello world'''
x = '''Tom said , "let's" go'''
x = 'good'+'moring' # 字符串
x = 'good'  #字符串重复
print(x)
```

### 4、列表、元组、字典、集合

这四个是Python内置的容器对象，其中可以包含多个元素，另外，range，map，zip，filter，enumerate 等迭代对象是Python 中比较常用的内置对象，支持某些与容器类对象类似的用法

```python
x_list  = [1,2,3] #定义列表对象
print(x_list[1]) #通过下标访问列表
x_tuple = (1,2,3) #定义元组对象
print(x_tuple[1]) #通过下标访问元组
x_dict = {'a':97,'b':98,'c':99} #定义字典对象，键值对存储
print(x_dict['a']) #通过键访问字典
x_set = {1,2,3} # 定义数组对象
print(x_set[1]) #集合不支持使用下标随机访问
3 in x_set #返回布尔类型
```

## 四、Python中的运算符

| 运算符          | 功能说明                                                     |
| --------------- | ------------------------------------------------------------ |
| +               | 算数加，列表、元组、字符串合并与连接，正号                   |
| -               | 算数减法，集合差集，相反数                                   |
| *               | 算数乘法，序列重复                                           |
| /               | 真除法                                                       |
| //              | 求整商，操作数中有实数，则结构为实数形式的整数               |
| %               | 求余数，字符串格式化                                         |
| **              | 幂运算                                                       |
| <,<=,>,>=,==,!= | 值大小比较，集合的包含关系比较                               |
| or              | 逻辑或                                                       |
| and             | 逻辑与                                                       |
| not             | 逻辑非                                                       |
| in              | 成员测试                                                     |
| is              | 对象实体统一性测试，即测试是否为同一个对象或者内存地址是否相同 |
| \|,^,&,<<,>>,~  | 位或，位异或，位与，左移位，右移位，位求反                   |
| &,\|,^          | 集合交集，并集，对称差集                                     |

### 1、算术运算符

#### +运算符

> 用于算术加法，还可以用于列表、元组、字符串的连接，但<font color = "red">不支持不同类型的对象之间的相加或者连接</font>

示例：

```python
x = [1,2,3] + [4,5,6] #+用于列表的连接
print(x)
x = (1,2,3) + (4,) #用于元组的连接
print(x)
x = "abcd" + "efg" #用于字符串的连接
print(x)
```

![image-20201110204424657](https://whpbucket.oss-cn-beijing.aliyuncs.com/myImg/20201124195612.png)

示例二：

```python
x = 'A' + 1
print(x)
```

![image-20201110204505706](https://whpbucket.oss-cn-beijing.aliyuncs.com/myImg/20201124195628.png)

不支持不同类型的连接，会抛出异常

#### *运算符

*号除了表示算术乘法，还可用于列表，元组，字符串这几个序列类型与整数的乘法，表示序列元素的重复，生成新的序列元素

```python
print([1,2,3]*3)
print((1,2,3)*3)
print("a,bc,"*3)
```

![image-20201110205755395](C:%5CUsers%5C%E7%99%BD%E6%98%BC%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201110205755395.png)

#### /和// 运算符

/表示算术除法，//表示算术求整商

```python
print(3/2) #表示数学意义上的除法
print(15//4) #两个操作数都是整数则结果为整数
print(15.0/4) #操作数中有实数，则结果为实数
print(-15/4) #向下取整
```

![image-20201110210152723](https://whpbucket.oss-cn-beijing.aliyuncs.com/myImg/20201124195645.png)

#### %运算符

用于整数或者实数的求余数运算，还可以用于字符串的格式化

```python
print(789%33) #求整数余数
print(123.45 % 3.2) #可以对实数进行余数运算，但是要注意精度问题
print("%c,%d" % (65,65))
print("%f ,%s " % (65,65
```

![image-20201110211226547](https://whpbucket.oss-cn-beijing.aliyuncs.com/myImg/20201124195656.png)

#### **运算符

表示幂运算

```python
print( 3 ** 2)
print( 9 ** 0.5)
print( 3 ** 2 ** 3)  #幂运算符从右往左计算
```

![image-20201110211356735](https://whpbucket.oss-cn-beijing.aliyuncs.com/myImg/20201124195704.png)

### 2、关系运算符

Python中关系运算符可以连用，要求操作数之间必须比较大小

```python
print(1 < 3 < 5)
print(3 < 5 > 2)
print("Hello" > "world") # 比较字符串大小
print([1,2,3] < [1,2,4]) # 比较列表大小
print({1,2,3} < {1,2,3,4}) # 测试一个集合是不是另一个集合的子集
print({3,2,1} == {1,2,3}) # 测试集合之间的包含关系
print({1,2,3} < {1,2,4})
```

![image-20201110212540121](C:%5CUsers%5C%E7%99%BD%E6%98%BC%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20201110212540121.png)

```python
print('hello' > 3) # 不能比较不同类型的数据，会抛出异常
```

![image-20201110212601674](https://whpbucket.oss-cn-beijing.aliyuncs.com/myImg/20201124195722.png)





> 注：关于Python中字符串的比较
>
> 比较的标准是位比较ASCII码值
>
> 首先Ascii 字符串的比较大小就是比较字符串的ASCII，但是并不是所有字符的ASCII加起来得出结果进行比较，而是从字符串的第一个字符开始比较，谁的ASCII码值大谁就大，如果第一个相同则比较第二个，依此类推，如果都相同则两个字符串大小相等

### 3、成员测试运算符

in运算符用于成员测试，测试一个对象是否包含另一个对象

```python
print( 3 in [1,2,3]) # 测试3是不是在集合当中
print(3 in range(1,10,1)) # 测试3在不在随机生成的范围当中
print('abc' in 'abcdefg') # 字符串包含测试
for i in (3,5,7):
    print(i,end="\t")
'''
用于循环,遍历集合，
这里设置连续按enter键两次才能执行
'''
```

![image-20201110213827857](https://whpbucket.oss-cn-beijing.aliyuncs.com/myImg/20201124195735.png)

### 4、集合运算符

交集：&

并集：|

对称差集：^

差集：-

```python
a = {1,2,3}
b = {3,4,5}
print(a | b) #并集,自动去除重复元素
print(a & b) # 交集
print(a ^ b) # 对称差集，除去交集之后取并
print(a - b) # 差集，源操作数1除去交集
```

![image-20201110214227342](https://whpbucket.oss-cn-beijing.aliyuncs.com/myImg/20201124195748.png)

### 5、逻辑运算符

and or not

具有惰性求值，和逻辑短路的特点

### 6、其他运算符

=，+=，*=，/=，//=，**=，|=，^=

Python不支持 ++ 和 -- 运算，形式上可以这样用，但是其实含义不一样

```python
i = 3
print(++i) #++i 解释为两个正号
print(+(+i)) #与上面的等价
print(--i) #负负得正
print(-(-i)) # 与上式等价
print(---i) # 三个负号取负
```

![image-20201110215310720](https://whpbucket.oss-cn-beijing.aliyuncs.com/myImg/20201124195800.png)

```python
print(i--) # 不支持，抛出异常
print(i++) #不支持++运算符，抛出异常
```

![image-20201110215344138](https://whpbucket.oss-cn-beijing.aliyuncs.com/myImg/20201124195811.png)

## 五、Python中的内置函数

### 1、关于类型转换和判断的函数

#### 1）bin() 

> 将整数转换为二进制

#### 2）oct()

> 将整数转换为八进制

#### 3）hex()

> 将整数转换为十六进制

#### 4）float()

> 将其他数据类型转换为实数

#### 5）complex() 

> 用于生成复数

#### 6）ord()

> 返回单个字符的Unicode码

#### 7）chr()

> 返回unicode码对应的字符

#### 8）str()

> 将任意类型的参数转换为字符串

#### 9）list()

> 将其他类型的数据转换成列表，和创建空列表

#### 10）tuple()

> 将其他类型的数据转换成元组，创建空元组

#### 11）dict()

> 将其他类型的数据转换成字典，创建空字典

#### 12）set()

> 将其他类型的数据转换成集合，创建空集合

#### 13）eval()

> 用来计算字符串的值，有些场合也可用于实现类型转换的功能

#### 14）type()

> 用于返回数据的类型

#### 15）isinstance()

> 用于判断数据的类型返回bool

#### 示例：

```python
# 整数进制变换函数
a = bin(555) #将整数转换为二进制
print(a)
a = oct(555) #将整数转换为八进制
print(a)
a = hex(555) #将整数转换为十六进制
print(a)
```

```python
#其他类型转实数函数

a = float(555) #整数转换为实数
print(a)
a = float('3.5') #字符串转换为实数
print(a)
```

```python
#复数生成函数
a = complex(3,5) #第一个参数是实部，第二个参数是虚部
print(a)
a = complex('inf') # inf代表无穷大，且不区分大小写
print(a)
```

![image-20201123104202284](https://whpbucket.oss-cn-beijing.aliyuncs.com/myImg/20201124202508.png)

```python
#unicode 码制转换函数
a = ord('a') # 字符转unicode函数
print(a)
a = chr(65) # unicode转字符函数
print(a)
```

```python
#任意类型转字符串函数
a = 1234
print(str(a))
a = [1,2,3]
print(str(a))
a = (1,2,3)
print(str(a))
a = {1,2,3}
print(str(a))
```

![image-20201123104551147](https://whpbucket.oss-cn-beijing.aliyuncs.com/myImg/20201124202456.png)

