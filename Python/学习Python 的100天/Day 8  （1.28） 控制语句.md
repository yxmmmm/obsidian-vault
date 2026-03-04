## 控制语句
分为三类：顺序、选择和循环
顺序：先执行a，再执行b
选择：如果...,再...
循环：如果...则重复执行...
### 选择结构（条件判断结构）
分为单分支、双分支、多分支
#### 单分支选择结构
if语句单分句结构语法形式
```
if  条件表达式:
    语句/语句块
```
【操作】输入一个数字，小于10，则打印这个数字
```
num=imput("输入一个数字：")
if int(num) < 10:
	print(num)
```
##### 条件表达式详解
在循环和选择结构中，条件表达式为False的情况：
False、0、0.0、空值None、空序列对象（空列表、空元组、空集合、空字典、空字符​ 串）、空range对象、空迭代对象。

**其他情况，均为`True`**。

！！！条件表达式中不能出现赋值运算符=
可以出现关系运算符==

#### 双分支选择结构
双分支结构的语法格式如下：
```
if  条件表达式:
    语句1/语句块1
else:
    语句2/语句块2

```
【操作】输入一个数字，小于10，则打印该数字；大于10，则打印“数字太大”
```
num = input("请输入一个数字：")
if int(num) < 10:
	print(num)
else: 
	print("数字太大")
```

##### 三元条件运算符
![image-20211022192109620](https://www.itbaizhan.com/wiki/imgs/image-20211022192109620.png)

Python的三元运算符，用来在某些简单双分支赋值情况。三元条件运算符语法格式如下：
条件为真时的值 if (条件表达式) else 条件为假时的值

上一个案例代码，可以用三元条件运算符实现：
```
num = input("请输入数字：")
print(num if int(num) < 10 else "数字太大")
```

#### 多分支选择结构
多分支选择结构的语法格式如下：
`if 条件表达式1 :`
    `语句1/语句块1`
`elif 条件表达式2:`
    `语句2/语句块2`
`...`
`elif 条件表达式n :`
    `语句n/语句块n`
`[else:`
    `语句n+1/语句块n+1`
`]`
 注：计算机行业，描述语法格式时，使用中括号`[ ]`通常表示可选，非必选。

 ⚠️多分支结构，几个分支之间是有逻辑关系的，不能随意颠倒顺序
  先if，再elif，再else！！！

【操作】输入一个学生的成绩，将其转化成简单描述：不及格(小于60)、及格(60-79)、良好(80-89)、优秀(90-100)
```
score = int(input("输入一个学生的成绩"))
grade = ""
if score < 60:
	grade = "不及格"
elif 60<=score<=79:
	grade = "及格"
elif 80<=score<=89:	
	grade = "良好"
else:	
	grade = "优秀"

print("学生的分数是{0},等级是{1}".format(score,))
```

【操作】已知点的坐标(x,y)，判断其所在的象限
```
x = int(input("请输入x坐标："))
y = int(input("请输入y坐标："))

if x==0 and y==0:
	print("(x,y)是原点")

elif x==0 and y!==0:
	print("(x,y)在x轴上")
elif x!==0 and y==0:
	print("(x,y)在y轴上")
			
elif x>0 and y>0:
	print("(x,y)在第一象限")
elif x<0 and y>0:
	print("(x,y)在第二象限")
elif x<0 and y<0:
	print("(x,y)在第三象限")

else:
	print("(x,y)在第四象限")
```

#### 选择结构的嵌套
选择结构可以嵌套，使用时一定要注意控制好不同级别代码块的缩进量，因为缩进量决定了代码的从属关系。

【操作】输入一个分数。分数在0-100之间。90以上是A,80以上是B，70以上是C，60以上是D。60以下是E
```
score = int(input("请输入分数："))
grade = ""

if score>100 or score<0;
	score = int(input("输入的分数不符合，请重新输入分数："))
else：
	if  90<score<=100;
		grade="A"
	elif 80<score<=90;
		grade="B"
	elif 70<score<=80;
		grade="C"
	elif 60<score<=70;	
		grade="D"
	else:
		grade="E"	

print("分数是：{0},等级是：{1}.format(score,grade)")		
```

下面这串代码也可以表示上述内容：
```
score = int(input("请输入一个在0-100之间的数字："))
degree = "ABCDE"
num = 0
if score>100 or score<0:
  score = int(input("输入错误！请重新输入一个在0-100之间的数字："))
else:
  num = score//10
  if num<6:num=5
  if num==10:num=9	​  

print("分数是{0},等级是{1}".format(score,degree[9-num]))

```
上述代码利用了字符串的索引
eg：54,,44//10=4<6,9-5=4，degree[4]="E"
     87,87//10=8,9-8=1,degree[1]="B"   

### 循环结构
循环结构用来重复执行一条或多条语句。表达这样的逻辑：如果符合条件，则反复执行循环体里的语句。在每次执行完后都会判断一次条件是否为True，如果为True则重复执行循环体里的语句。图示如下：

![image-20211113153730906](https://www.itbaizhan.com/wiki/imgs/image-20211113153730906.png)

循环体里面的语句至少应该包含改变条件表达式的语句，以使循环趋于结束；否则，就会变成一个死循环。

#### while循环结构
while循环的语法格式如下：
while 条件表达式：
    循环体语句

【操作】利用while循环打印从0-10的数字
```
num = 0
while num<=10:
	print(num)
	num +=1
```
注意，在Python中没有++的形式，不能写成num++，应该写成num +=1

【操作】利用while循环，计算1-100之间数字的累加和；计算1-100之间偶数的累加和，计算1-100之间奇数的累加和
```  
#1-100所有数字的和
num=1
sum=0 
while num<=100:
	sum += num
	num += 1
print(sum)
```

```
#1-100所有偶数的和
num=1
sum=0 
while num<=100:
	if num%2==0:
		sum += num
	num += 1
print(sum)
```

```
#1-100所有奇数的和
num=1
sum=0 
while num<=100:
	if num%2==1:
		sum += num
	num += 1
print(sum)
```

#### for循环和可迭代对象遍历
for循环通常用于可迭代对象的遍历。for循环的语法格式如下：
```

for 变量 in 可迭代对象：
	循环体语句
```
【操作】遍历一个元组或列表
```
for i in (20,30,40):  
    print(i*3)  
  
for i in [20,30,40]:  
    print(i*3)
>>>
60
90
120
60
90
120
```

##### 可迭代对象
Python包含以下几种可迭代对象：
1. 序列。包含：字符串、列表、元组、字典、集合
2. 迭代器对象（iterator）
3. 生成器函数（generator）
4. 文件对象

【操作】遍历字符串中的字符
```
for i in 'wo shi q l':  
    print(i)
```

【操作】遍历字典
```
d = {'name':'gaoqi','age':18,'address':'西三旗一号'}  
for i in d :   #遍历字典中所有的key  
    print(i)  
  
for i in d.keys():   #遍历字典中所有的key  
    print(i)  
  
for i in d.values():     #遍历字典中所有的value  
    print(i)  
  
for i in d.items():       #遍历字典中的所有的“键值对”  
    print(i)
```
##### range对象
range对象是一个迭代器对象，用来产生指定范围的数字序列。格式为：
  range(start,end [,step])

生成的数值序列从`start`开始到`end`结束（⚠️不包含`end`）。若没有填写`start`，则默认从0开始。`step`是可选的步长，默认为1。如下是几种典型示例：

`for i in range(10)` 产生序列：0 1 2 3 4 5 6 7 8 9

`for i in range(3,10)` 产生序列：3 4 5 6 7 8 9

`for i in range(3,10,2)` 产生序列：3 5 7 9

👆简称：包头不包尾

【操作】利用for循环，计算1-100之间数字的累加和；计算1-100之间偶数的累加和，计算1-100之间奇数的累加和。

```
sum_all=0  
sum_even=0  
sum_odd=0  
  
for num in range(1,100+1):  
    sum_all+=num  
    if num%2==0:  
        sum_even+=num  
    else:  
        sum_odd+=num  
    num +=1  
    print (sum_all)  
print(sum_even)  
print(sum_odd)
```

#### 嵌套循环
一个循环体内可以嵌入另一个循环，一般称为“嵌套循环”，或者“多重循环”。

【操作】打印如下图案
![image-20211023104124592](https://www.itbaizhan.com/wiki/imgs/image-20211023104124592.png)
```
for x in range(5):  
    for y in range(5):  
        print(x,end="\t")  
    print()
```

在Python中print()会自动打印一个换行符，不想换行时，需要在末尾加上end="",引号内为末尾要添加的内容，表示以引号内内容结尾，不换行
\t表示横向制表符，与tab的作用相同
print()起到换行的作用，与\b的作用相同

##### 嵌套循环练习
【操作】利用嵌套循环打印九九乘法表
九九乘法表：
![image-20211023104257627](https://www.itbaizhan.com/wiki/imgs/image-20211023104257627.png)

```
for m in range(1,10):  
    for n in range(1,m+1):  
        print("{0}*{1}={2}".format(m,n,(m*n)),end="\t")  
    print()
```

**【操作】用列表和字典存储下表信息，并打印出表中工资高于15000的数据**

|姓名|年龄|薪资|城市|
|---|---|---|---|
|高小一|18|30000|北京|
|高小二|19|20000|上海|
|高小五|20|10000|深圳|
```
r1=dict([('name','高小一'),('age',18),('salary','30000'),('city','北京')])  
r2=dict([('name','高小二'),('age',19),('salary','20000'),('city','上海')])  
r3=dict([('name','高小五'),('age',20),('salary','10000'),('city','深圳')])  
tb=[r1,r2,r3]  
  
for i in tb:  
    print(i)  
print()  
  
for x in tb:  
    if int(x.get("salary"))>15000:  
        print(x)
```

#### break语句
break语句可结束整个循环，如果是嵌套语句，则结束最近的一次循环
```
while True:  
    a = input("请输入一个字符（输入Q或q结束）")  
    if a.upper() == 'Q':    #a.upper()只用判断大写
        print("循环结束，退出")  
        break  
    else:  
        print(a)
```

#### continue语句

continue语句用于结束本次循环，继续下一次。多个循环嵌套时，continue也是应用于最近的一层循环。

![image-20211114112248048](https://www.itbaizhan.com/wiki/imgs/image-20211114112248048.png)

【操作】要求输入员工的薪资，若薪资小于0则重新输入。最后打印出录入员工的数量和薪资明细，以及平均薪资
```
salary_sum = 0  
salarys=[]  
employee_number=0  
salary = 0  
  
while True:  
    salary = input("请输入员工的薪资：")  
    if salary.upper() == "Q":  
        print("退出")  
        break  
    if int(salary) < 0:  
        print("输入错误")  
        continue  
    else:  
        salarys.append(salary)  
        employee_number = employee_number + 1  
        salary_sum = salary_sum + int(salary)  
  
print("录入工资：",salarys)  
print("工资总量：",salary_sum)  
print("员工数量：",employee_number)  
print("平均工资：",int(salary_sum)/employee_number)
```

#### else语句
while、for循环可以附带一个else语句（可选）。如果for、while语句没有被break语句结束，则会执行else子句，否则不执行。语法格式如下：
```
while 条件表达式：
	循环体
else：
	语句块
	
# 或者：
for 变量 in 可迭代对象：
	循环体
else：
	语句块
```

【操作】员工一共4人。录入这4位员工的薪资。全部录入后，打印提示“您已经全部录入4名员工的薪资”。最后，打印输出录入的薪资和平均薪资
```
salary_sum = 0  
salarys=[]  
employee_number=0  
salary = 0  
num=0  
  
while num<4:  
    salary = input("请输入员工的薪资：")  
    if salary.upper() == "Q":  
        print("退出")  
        break  
    if int(salary) < 0:  
        print("输入错误")  
        continue  
    else:  
        salarys.append(salary)  
        employee_number = employee_number + 1  
        salary_sum = salary_sum + int(salary)  
        num = num +1  
else:  
    print("您已经全部录入4名员工的薪资")  
  
print("录入工资：",salarys)  
print("工资总量：",salary_sum)  
print("员工数量：",employee_number)  
print("平均工资：",int(salary_sum)/employee_number)
```

#### 代码优化
循环
虽然计算机越来越快，空间也越来越大，我们仍然要在性能问题上“斤斤计较”。编写循环时，遵守下面三个原则可以大大提高运行效率，避免不必要的低效计算：

1. 尽量减少循环内部不必要的计算
2. 嵌套循环中，尽量减少内层循环的计算，尽可能向外提
3. 局部变量查询较快，尽量使用局部变量

 其他优化手段

1. 连接多个字符串，使用join()而不使用+
2. 列表进行元素插入和删除，尽量在列表尾部操作

### zip（）并行迭代多个序列
【操作】测试zip()并行迭代
```
names = ("高琪","高老二","高老三","高老四")  
ages = (18,16,20,25)  
jobs = ("老师","程序员","公务员")  
  
for name,age,job in zip (names,ages,jobs):  
    print("{0} {1} {2}".format(name,age,job))  
  
for i in range(min(len(names),len(ages),len(jobs))):  
    print("{0} {1} {2}".format(names[i],ages[i],jobs[i]))
```
