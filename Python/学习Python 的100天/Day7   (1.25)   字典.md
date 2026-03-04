## 字典
字典是“键值对”的无序可变序列，字典中的每个元素都是一个“键值对”，包含：“键对象”和“值对象”。可以通过“键对象”实现快速获取、删除、更新对应的“值对象”。

一个典型的字典的定义方式：
a={'name':'ql','age':18,'job':'programmer'}
列表中我们通过“下标数字”找到对应的对象。字典中通过“键对象”找到对应的“值对象"。
1. “键”是任意的不可变数据，比如：整数、浮点数、字符串、元组。
2. 但是：列表、字典、集合这些可变对象，不能作为“键”。
3. 并且“键”不可重复。
4. “值”可以是任意的数据，并且可重复。

### 字典的创建
1.我们可以通过{}、dict()来创建字典对象。
```
a = {'name':'gaoqi','age':18,'job':'programmer'}
b = dict(name='gaoqi',age=18,job='programmer')
a = dict([("name","gaoqi"),("age",18)])
c = {} #空的字典对象
d = dict() #空的字典对象

```
2.通过zip()创建字典对象
```
k = ['name','age','job']
v = ['gaoqi',18,'teacher']
d = dict(zip(k,v))
print(d) #{'name': 'gaoqi', 'age': 18, 'job': 'techer'}

```
3.通过fromkeys创建值为空的字典
```
f = dict.fromkeys(['name','age','job'])
print(f) #结果：{'name': None, 'age': None, 'job': None}

```
### 字典元素的访问
为了测试各种访问方法，我们这里设定一个字典对象：
```
a = {'name':'gaoqi','age':18,'job':'programmer'}
```
 1.通过 [键] 获得“值”。若键不存在，则抛出异常。
```
 a = {'name':'gaoqi','age':18,'job':'programmer'}
b = a['name']
print(b)
```
2.通过get()方法获得“值”。推荐使用，优点是：指定键不存在，返回None；也可以设定指定键不存在时默认返回的对象。推荐使用get()获取“值对象”
```
a={'name':'gaoqi','age':18.'job':'programmer'}
b= a.get('name')
c= a.get('gender','不存在')
print(b)    #gaoqi
print(c)    #不存在
```
3.列出所有的键值对
```
a={'name':'gaoqi','age':18,'job':'programmer'}
b=a.items()
print(b)   #dict_items([('name','gaoqi'),('age'，18),('job','programmer')])
```
4.列出所有的键，列出所有的值
```
a={'name':'gaoqi','age':18,'job':'programmer'}
k=a.keys()
v=a.values()
print(k)  #dict_keys(['name','age','job'])
print(v)  #dict_values(['gaoqi',18,'programmer'])
```
5.len()键值对的个数
```
a={'name':'gaoqi','age':18,'job':'programmer'}
num=len(a)
print(num) #结果 3
```
6.检测一个“键”是否在字典中
```
a={'name':'gaoqi','age':18,'job':'programmer'}
print("name" in a ) #结果  True
```

### 字典元素添加、修改、删除
给字典添加”键值对“，如果”键“已存在，则新的键值对会覆盖旧的键值对
不存在，则新增键值对
```
a={'name':'gaoqi','age':18,'job':programmer}
a['age']=16
a['address']='西三旗1号院'
print(a)
# {'name':'gaoqi','age':16,'job':programmer,'address':西三旗1号院}
```
使用update()将新字典中的所有键值对全部添加到旧字典对象上。如果key有重复，就覆盖
```
a = {'name':'gaoqi','age':18,'job':'programmer'}
b = {'name':'gaoxixi','money':1000,'gender':'男的'}
a.update(b)
print(a)
# {'name':'gaoxixi','age':18,'job':'programmer','money':1000,'gender':'男的'}
```
字典中元素的删除
del()删除键值对
clear()删除所有的键值对
pop()删除指定的键值对并返回对应的值对象
```
a = {'name':'gaoqi','age':18,'job':'programmer'}
del(a['name'])
print(a)    #{'age': 18, 'job': 'programmer'}
age = a.pop('age')
print(age)   #18

```
popitem():随机删除和返回键值对
字典是无序可变的序列，所以没有所谓的第一个元素和最后一个元素的概念
```
a = {'name':'gaoqi','age':18,'job':'programmer'}
r1 = a.popitem()
r2 = a.popitem()
r3 = a.popitem()
print(a)  #{}

```

### 序列解包
序列解包可以用于元组、列表、字典。序列解包可以让我们方便的对多个变量赋值
```
x,y,z=(20,30,10)
(a,b,c)=(9,8,10)
[m,n,p]=[10,20,30]

```
字典中的序列解包默认是对”键“进行操作；如果需要对键值对操作，则需要items();
如果是对‘’值‘’进行操作，则需要使用values()
```
s = {'name':'gaoqi','age':18,'job':'teacher'}
a,b,c=s  #默认对键进行操作
print(a)  #name 
a,b,c=s.items()  #对键值对操作
print(a)  #('name':'gaoqi')
a,b,c=s.value()  #对值进行操作
print(a)  #gaoqi 
```

### 表格数据使用字典和列表存储和访问
|姓名|年龄|薪资|城市|
|---|---|---|---|
|高小一|18|30000|北京|
|高小二|19|20000|上海|
|高小五|20|10000|深圳|

```

```