# 函数(function)
函数是可重用的程序代码块
函数的作用：不仅可以实现代码的服用，更能实现代码的一致性
一致性：只要修改函数的代码，则所有调用该函数的地方都能得到体现

函数：一个程序有一个一个任务组成；函数就是代表一个任务或者一个功能
函数是代码复用的通用机制

### Python函数的分类
![image-20211023112843842](https://www.itbaizhan.com/wiki/imgs/image-20211023112843842.png)
内置函数：
str()、list（）、len（）等都是内置函数，我们可以拿来直接使用
标准库函数：
我们可以通过import语句导入库，然后使用其中定义的函数
第三方库函数：
Python社区也提供了很多高质量的库。下载安装这些库后，也是通过import语句导入，然后可以使用这些第三方库的函数
用户自定义函数:
用户自己定义的函数，显然也是开发中适应用户自生需求定会的函数。

### 函数的定义和调用
Python中，定义函数的语法如下：
```
def 函数名（[参数列表]）：   #def是define的缩写，参数列表可写可不写
	'''文档字符串'''    #用来表示这个函数表示的是什么意思，相当于注释，可写可不写
	函数体/若干语句
```

```
def add(a,b,c):
  '''完成三个数的加法，并返回他们的和'''
  sum = a+b+c
  print("{0}、{1}、{2}三个数的和是：{3}".format(a,b,c,sum))
  return sum
​
add(10,20,30)
add(30,40,50)

```
![image-20211117100503083](https://www.itbaizhan.com/wiki/imgs/image-20211117100503083.png)

##### 函数的一些要点
1.我们使用def来定义函数
Python执行def时，会创建一个函数对象，并绑定到函数名变量上
2.参数列表
圆括号内是形式参数列表，有多个参数则使用逗号隔开
定义时的形式参数不需要声明类型，也不需要制定函数返回值类型
调用时的实际参数必须与形式参数列表一一对应
3.return返回值
如果函数体中包含return语句，则结束函数执行并返回值
如果函数体中不包含return语句，则返回None值
4.调用函数之前，必须要先定义函数，即先调用def创建函数对象
内置函数对象会自动创建
标准库和第三方库函数，通过import导入模块时，会执行模块中的def语句

### 形参和实参
形参和实参的要点：

 圆括号内是形式参数列表，有多个参数则使用逗号隔开
 **定义时的形式参数**不需要声明类型，也不需要指定函数返回值类型
 调用时的实际参数**必须与形参列表一一对应

【操作】定义一个函数，实现两个数的比较，并返回较大的值
```
def printMax(a,b):  
    """  
    实现两个数字大小的比较  
    :param a: 参数1  
    :param b: 参数2  
    :return: 较大的值  
    """    if a>b:  
        print(a,"是较大值")  
        return(a)  
    else:  
        print(b,"是较大值")  
        return(b)  
  
printMax(2,3)
```
### 文档字符串（函数的注释）
```
def printMax(a,b):  
    """  
    实现两个数字大小的比较  
    :param a: 参数1  
    :param b: 参数2  
    :return: 较大的值  
    """    if a>b:  
        print(a,"是较大值")  
        return(a)  
    else:  
        print(b,"是较大值")  
        return(b)  
help(printMax)  

#结果 printMax(a, b)
    实现两个数字大小的比较
    :param a: 参数1
    :param b: 参数2
    :return: 较大的值

print(printMax.__doc__)  

#结果 实现两个数字大小的比较
:param a: 参数1
:param b: 参数2
:return: 较大的值

printMax(2,3)
```
我们调用help(函数名) 可打印输出函数的文档字符串
也可以通过 函数.下划线下划线doc下划线下划线  直接获取函数的文档字符串，自己进行打印   
help（）会比    函数.下划线下划线doc下划线下划线  多输出一个  函数名

### 返回值
return返回值要点：
	如果函数体中包含return语句，则结束函数执行斌返回值
	如果函数体中不包含return语句，则返回None值
	要返回多个值，使用列表、元组、字典、集合将多个值“存起来”即可

【操作】定义一个打印n个星号的无返回值的函数
```
def print_star (n):  
    """  
    n是多少，打印多少个星星  
    :param n: 参数  
    :return: 返回多少个星星  
    """    print("*"*n)  
  
print_star(5)
```
【操作】定义一个返回两个数平均值的函数
```
def my_ave(a,b):  
  
    return float(a+b)/2.0  
  
c = my_ave(1,2)  
print(c)
```

【操作】返回一个列表
```
def printShape(n):  
    s1 = "#"*n  
    s2 = "$"*n  
    return[s1, s2]  
  
s = printShape(3)  
print(s)
```
## 函数也是对象_函数的内存分析
在Python中一切都是对象
在执行def定义的函数后，系统就创建了相应的函数对象
```
def print_star(n):  
    print("*"*n)  
  
print(print_star)  
print(id(print_star))  
  
c=print_star  
c(3)
```
上面代码执行`def`时，系统中会创建函数对象，并通过`print_star`这个变量进行引用：

![image-20211107154257589](https://www.itbaizhan.com/wiki/imgs/image-20211107154257589.png)

我们执行`c=print_star`后，显然将`print_star`变量的值赋给了变量`c`，内存图变成了：

![image-20211107154604781](https://www.itbaizhan.com/wiki/imgs/image-20211107154604781.png)

c和print_star都是指向同一个对象
所以执行c(3)和执行print_star(3) 的效果是完全一致的

Python中，圆括号意味着调用函数。在没有圆括号的情况下，Python会把函数当做普通对象
```
zhengshu=int  
a=zhengshu("234")  
print(a)
```
我们将内置函数int（）赋值给了zhengshu，这样zhengshu和int都是指向了同一个内置函数对象
不过在实际开发中没必要这么做

## 变量的作用域
###### 全局变量：
1. 在函数和类定义之外声明的变量。作用域为定义的模块，从定义位置开始直到模块结束。
2. 全局变量降低了函数的通用性和可读性。应尽量避免全局变量的使用。
3. 要在函数内改变全局变量的值，使用`global`声明一下
###### 局部变量：
1. 在函数体中（包含形式参数）声明的变量。
2. 局部变量的引用比全局变量快，优先考虑使用
3. 如果局部变量和全局变量同名，则在函数内隐藏全局变量，只使用同名的局部变量

【操作】全局变量的作用域测试
```
a=100  
  
def f1():  
    b=3  
    global a  
    a = 4  
    print(a+b)  
  
f1()  
print(a)
```

【操作】 输出局部变量和全局变量
```
a = 100
​
def f1(a,b,c):
  print(a,b,c)
  print(locals())      #打印输出的局部变量
  print("#"*20)
  print(globals())      #打印输出的全局变量
​
f1(2,3,4)

```
输出结果：
```
2 3 4
​
{'c': 4, 'b': 3, 'a': 2}
​
####################
​
{'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <class '_frozen_importlib.BuiltinImporter'>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>, '__file__': 'E:\\PythonExec\\if_test01.py', 'a': 100, 'f1': <function f1 at 0x0000000002BB8620>}

```

### 局部变量和全局变量的效率测试
局部变量的查询和访问速度比全局变量快，优先考虑，尤其是在循环的时候
```
import time  
  
a = 1000  
  
def test01():  
    start = time.time()  
    global a  
    for i in range(1000000):  
        a += 1  
    end = time.time()  
    print("耗时{0}".format(end-start))  
  
import time  
  
  
def test02():  
    start = time.time()  
    c = 1000  
    for i in range(1000000):  
        c += 1  
    end = time.time()  
    print("耗时{0}".format(end-start))  
  
test01()  
test02()
```
## 参数的传递
函数的参数传递本质上是：从实参到形参的赋值操作
Python中“一切皆对象”，所有的赋值操作都是”引用的赋值“
Python中的参数的传递都是”引用的传递“，而不是”值传递“

对”可变对象“进行”写操作“，直接作用于元对象本身
      字典、列表、集合、自定义对象等
对”不可变对象‘进行“写操作’，会产生一个新的”对象空间“，并用新的值填充这块空间
	  数字、字符串、元组、function等

### 传递可变对象的引用

传递参数是可变对象（例如：列表、字典、自定义的其他可变对象等），实际传递的还是对象的引用。在函数体中不创建新的对象拷贝，而是可以直接修改所传递的对象。

【操作】参数传递：传递可变对象的引用
```
b = [10,20]  
def f2(m):  
    print("m:",id(m))  
    m.append(30)  
  
f2(b)  
  
print(b)
```

### 传递不可变对象的引用
传递参数是不可变对象（例如：int、float、字符串、元组、布尔值)
实际传递对的还是对象的引用。在“赋值操作”时，由于不可变对象无法修改，系统会创建一个新对象

【操作】参数传递：传递不可变对象的引用

```
a = 100  
def f1(n):  
    print("n:",id(n))  
    n = n+200    # 这里n创建了一个新的对象
    print("n:", id(n))  
    print(n)  
  
f1(a)  
print("a:",id(a))
```
![[屏幕截图 2026-02-02 170903 1.png]]
### 浅拷贝和深拷贝
我们可以使用内置函数：`copy`(浅拷贝)、`deepcopy`(深拷贝)。
浅拷贝：拷贝对象，但不拷贝子对象的内容，只是拷贝子对象的引用
深拷贝：拷贝对象，并且会连子对象的内存也全部（递归)拷贝一份，对子对象的修改不会影响源对象
```
import copy  
  
def testCopy():  
    "测试浅拷贝"  
    a = [10,20,[5,6]]  
    b = copy.copy(a)  
  
    print("a",a)  
    print("b",b)  
    b.append(30)  
    b[2].append(7)  
    print("浅拷贝之后")  
    print("a",a)  
    print("b",b)  
  
def testDeepCopy():  
    "测试深拷贝"  
    a = [10,20,[5,6]]  
    b = copy.deepcopy(a)  
    print("a",a)  
    print("b",b)  
    b.append(30)  
    b[2].append(7)  
    print("深拷贝之后")  
    print("a",a)  
    print("b",b)  
  
testCopy()  
testDeepCopy()
```

浅拷贝的内存分析：
![[浅拷贝.png]]

深拷贝内存分析：
![[深拷贝.png]]

### 不可变对象中存在可变对象
```
a = (10,20,[5,6])  
print("a",id(a))  
print("a",id(a[2]))  
def test01(m):  
    print("m",id(m))  
    m[2][0] = 888  
    print(m)  
    print("m",id(m))  
    print("m",id(m[2]))  
test01(a)  
print(a)
```
初始状态：
a  →  (id1: 元组)  →  [0] → 10
                    [1] → 20
                    [2] → ───┐
                             ↓
                          (id2: 列表) → [0]: 5
                                         [1]: 6

调用 test01(a) 后：
m 也指向 id1 这个元组

执行 m[2][0] = 888 后：
a  →  (id1: 元组)  →  [0] → 10
                    [1] → 20
                    [2] → ───┐
                             ↓
                          (id2: 列表) → [0]: 888  ← 这里变了！
                                         [1]: 6
a和 m的 id相同：说明函数参数 m接收的是对同一个元组对象的引用。



a[2]的 id在修改前后不变：我们修改了列表的内容，但列表对象本身（它在内存中的位置）没有改变。

a的内容“看起来”变了：元组 a本身确实没变（它仍然持有三个元素的引用），但它所持有的第二个元素（列表）的内部值变了，所以打印 a时显示出变化。

## 参数的类型

![image-20211107160044211](https://www.itbaizhan.com/wiki/imgs/image-20211107160044211.png)

### 位置参数
在调用函数时，实参与实参要一一对应，否则就会报错
```
def f1(a,b,c):  
    print(a,b,c)  
  
f1(1,2,3)  
f1(1,2)
```
### 默认值参数
默认值参数必须放普通位置参数后面
```
def f1(a,b,c=10,d=20):  
    print(a,b,c,d)  
  
f1(1,2)  
f1(1,2,3)  
f1(1,2,3,4)
```
如果给了实参，就用实参的的值，如果没有给，就用默认值

### 命名参数
```
def f1(a,b,c):  
    print(a,b,c)  
  
f1(1,2,3)  
f1(c=3,b=4,a=5)
```
通过命名参数就不需要按照顺序来

### 可变参数
```
*param 生成元组
**param 生成字典
```

```
def f1(a,b,*c):  
    print(a,b,c)  
  
f1(1,2,3,4,5)
```

```
def f1(a,b,**c):  
    print(a,b,c)  
  
f1(1,2,name="gaoqi",age=18)
```

### 强制命名参数
可变参数只能放在普通位置参数的后面，如果想要放在前面就必须要用到强制命名参数

```
def f1(*a,b,c):  
    print(a,b,c)  
  
f1(1,2,b=1,c=2)
```

## lambda函数、匿名函数
lambda表达式的基本格式：
lambda  arg1，arg2，arg3... :表达式

```
f = lambda a,b,c : a+b+c  
print(f)  
print(type(f))  
print(id(f))  
print(f(1,2,3))
```
可以把lambda看成一个简单的函数，a，b，c就是三个参数，a+b+c就是表达式，然后将结果范湖给f
```
f = lambda a,b,c:a+b+c  
print(f)  
print(f(2,3,4))  
g = [lambda a:a*2,lambda b:b*3,lambda c:c*4]  
print(g[0](6),g[1](7),g[2](8))
```

## eval()函数
能把字符串str当成有效的表达式来求值并返回计算结果
语法：eval（source,[global，[locals]]  -->value

参数：

1. `source`：一个Python表达式或函数`compile()`返回的代码对象
2. `globals`：可选。必须是`dictionary`
3. `locals`：可选。任意映射对象

⚠️⚠️⚠️`eval函数`会将字符串当做语句来执行，因此会被注入安全隐患。比如：字符串中含有删除文件的语句。那就麻烦大了。因此，使用时候，要慎重！！！

```
a = 10  
b = 20  
c = eval("a+b")  
print(c)  
  
s = "print('abcde')"  
eval(s)
```

## 递归函数
就是自己调用自己
**![image-20211117171752273](https://www.itbaizhan.com/wiki/imgs/image-20211117171752273.png)**
```
def f1(n):  
    print("start:"+str(n))  
    if n == 1:  
        print("函数终止")  
    else:  
        f1(n-1)  
    print("end:"+str(n))
```

#### 用递归函数进行阶乘运算
```
def factorial(n):  
    if n == 1:  
        return 1  
    return n*factorial(n-1)  
  
print(factorial(5))
```

![image-20211116113627154](https://www.itbaizhan.com/wiki/imgs/image-20211116113627154.png)

### 嵌套函数（内部函数）

嵌套函数就是在函数中定义函数
```
def outer() :  
    print("outer running!!!")  
  
    def inner() :  
        print("inner running!!!")  
  
    inner()  
  
outer()
```

```
def printName(isChinese,name,familyName):  
    def inner_print(a,b):  
        print("{0} {1}".format(a,b))  
    if isChinese:  
        inner_print(familyName,name)  
    else:  
        inner_print(name,familyName)  
  
printName(True,"朗","秦")  
printName(False,"George","Bush")
```

## nonlocal和global关键字
nonlocal用来在内部函数中声明外层的局部变量
global函数内声明全局变量，然后才使用全局变量

```
a = 100  
def outer():  
    b = 10  
  
    def inner():  
        nonlocal b  
        print("inner b:",b)  
        b = 20  
  
        global a  
        a = 1000  
  
    inner()  
    print("outer b:",b)  
  
outer()  
print("a:",a)
```

## LEGB规则
Python在查找名称是按LEGB规则查找
![image-20211116111854538](https://www.itbaizhan.com/wiki/imgs/image-20211116111854538.png)
`Local` 指的就是函数或者类的方法内部

`Enclosed` 指的是嵌套函数（一个函数包裹另一个函数，闭包）

`Global` 指的是模块中的全局变量

`Built in` 指的是Python为自己保留的特殊名称









