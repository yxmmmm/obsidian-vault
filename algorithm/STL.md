 #cpp 

# vector
和数组一样类别，长度可变
## 常用方法
### 构造
vector<类型>arr(长度，初始值)
$O(n)$
```cpp
vector<int>arr//构造int数组
vector<int>arr(100)//初始长100int数组
vector<int>arr(100,1)//初始长100int数组初值1

vector<vector<int>> dp(5,vector<int>(6,10))
//5行6列初值10，二维数组
vector<vector<vector<int>>> dp2(5,vector<vector<int>>(6,vector<int>(4)))
//6行4列5高，三维数组
```

## 尾接&尾删
```cpp
int main()
{
	vector<int> arr;
	// init: arr = []
	arr.push_back(1);
	// after: arr = [1]
	arr.push_back(2);
	// after: arr = [1, 2]
	arr.pop_back();
	// after: arr = [1]
	arr.pop_back();
	// after: arr = []

	
	cout<<arr.size()<<endl;//打印长度
	
	arr.clear()//清空
	
	cout<<arr.empty()<<endl;//判空，返回bool
	
	arr.resize(5,3)//修改arr长度为5，初值均为3。改短直接删，改长赋初值
}
```

vector支持比较(字典序)

```cpp
vector<int>a(4,3),b(3,4);

if(a<b)puts("a<b");
//输出a<b
```



## 应用场景

有些情况普通数组没法解决： $n*m$的矩阵， 且 $1\leq n，m\leq 10^6且n*m\leq 10^6$

- 如果用普通数组 `int mat[1000010][1000010]`，浪费内存，会导致 MLE。
- 如果使用 `vector<vector<int>> mat(n + 10, vector<int> (m + 10))`，完美解决该问题。

另外，`vector` 的数据储存在堆空间中，不会爆栈。

## 注意事项
#### 提前指定长度

如果长度已经确定，那么应当直接在构造函数指定长度，而不是一个一个 `.push_back()`. 因为 `vector` 额外内存耗尽后的重分配是有时间开销的，直接指定长度就不会出现重分配了。

```cpp
// 优化前: 522ms
vector<int> a;
for (int i = 0; i < 1e8; i++)
    a.push_back(i);
// 优化后: 259ms
vector<int> a(1e8);
for (int i = 0; i < a.size(); i++)
    a[i] = i;
```

#### 当心 size_t 溢出

vector 获取长度的方法 `.size()` 返回值类型为 `size_t`，通常 OJ 平台使用的是 32 位编译器（有些平台例如 cf 可选 64 位），那么该类型范围为$[0,2^{32} )$ .

```cpp
vector<int> a(65536);
long long a = a.size() * a.size(); // 直接溢出变成0了
```

# deque

强化vector,但效率低的发指

| 作用      | 用法                         | 示例                              |
| --------- | ---------------------------- | --------------------------------- |
| 大小      | `.size()`                    | `dque.size();`                    |
| 进/出队尾 | `.push_back()/.pop_back()`   | `dque.push_back()/.pop_back()`    |
| 进/出队首 | `.push_front()/.pop_front()` | `dque.push_front()/.pop_front();` |
| 取队首/尾 | `.front()/.back()`           | `int b = dque.front()/.back()`    |
| 清除      | `.clear()`                   | `dque.clear()`                    |
| 判空      | `.empty()`                   | `dque.empty()`                    |

# stack

先进后出

```cpp
stack<double>stk;
stk.push(1.0);
stk.pop();
```
## 常用方法


| 作用         | 用法              | 示例                 |
| ------------ | ----------------- | -------------------- |
| 构造         | `stack<类型> stk` | `stack<int> stk;`    |
| 进栈（栈顶） | `.push(元素)`     | `stk.push(1);`       |
| 出栈         | `.pop()`          | `stk.pop();`         |
| 取栈顶       | `.top()`          | `int a = stk.top();` |

## 适用情形
可用vector当栈用.back()取尾部元素相当于对栈顶操作
push_back()=.push()进栈
pop_back=.pop()出栈
.back()=.top()取栈顶

## 注意
**stack不可访问内部元素**

# queue
先进先出

```cpp
queue<int>que;
que.push(1);
que.pop();

cout<<que.back()<<endl
cout<<que.front()<<endl
cout<<que.size()<<endl
cout<<que.empty()<<endl
```

## 常用方法
| 作用         | 用法              | 示例                   |
| ------------ | ----------------- | ---------------------- |
| 构造         | `queue<类型> que` | `queue<int> que;`      |
| 进队（队尾） | `.push(元素)`     | `que.push(1);`         |
| 出队（队头） | `.pop()`          | `que.pop();`           |
| 取队首       | `.front()`        | `int a = que.front();` |
| 取队尾       | `.back()`         | `int a = que.back();`  |
| 查看大小     | `.size()`         | `int a = que.size();`  |
| 判空         | `.empty()`        | `int a = que.empty();` |
## 注意⚠️
**不可访问内部元素**

# priority_queue
提供常数时间的**最大元素查找**，对数时间的插入与提取，底层原理是二叉堆。

## 构造
**`priority_queue<类型, 容器, 比较器> pque`**
**比较器默认为less<类型>**

```cpp
priority_queue<int>pque//大顶堆
priority_queue<int, vector<int>, greater<int>> pque2; // 储存int的小顶堆
pque.push(-x)//负数存储实现小顶堆黑科技
```


## 常用方法
| 作用             | 用法                       | 示例                       |
| ---------------- | -------------------------- | -------------------------- |
| 构造             | `priority_queue<类型> que` | `priority_queue<int> que;` |
| 进堆             | `.push(元素)`              | `pque.push(1);`            |
| 出堆（弹出堆顶） | `.pop()`                   | `pque.pop();`              |
| 取堆顶           | `.top()`                   | `int a = pque.top();`      |
| 查看大小         | `.size()`                  | `int a = pque.size();`     |
| 判空             | `.empty()`                 | `int a = pque.empty();`    |
## 注意⚠️
- 仅堆顶可读
- 所有元素不可写
	若刚好更改堆顶元素可曲线救国
	```cpp
	int tp = pque.top();
	pque.pop();
	qpue.push(new);
	```
	**实质是弹出堆顶并涌入一个新的元素**
	
- 无clear指令

# set
提供对数时间的插入、删除、查找的集合数据结构。底层原理是红黑树。

| 集合三要素 | 解释                           | set           | multiset      | unordered_set |
| ---------- | ------------------------------ | ------------- | ------------- | ------------- |
| 确定性     | 一个元素要么在集合中，要么不在 | ✔             | ✔             | ✔             |
| 互异性     | 一个元素仅可以在集合中出现一次 | ✔             | ❌（任意次）   | ✔             |
| 无序性     | 集合中的元素是没有顺序的       | ❌（从小到大） | ❌（从小到大） | ✔             |
## 构造
```cpp
set<int> st1; // 储存int的集合（从小到大） 
set<int, greater<int>> st2; // 储存int的集合（从大到小）

set<int>st;
st.insert(1);//插入
st.erase(1);//删除

if(st.find(1)!=st.end()){
	cout<<"yes"<<endl;
}//st.find()是一个迭代器，当没找到元素时返回尾迭代器
if(st.count(1)){
	cout<<"yes"<<endl;
}//在基础count中.count()只有0/1两种情况

cout<<st.size()<<endl;
st.clear();
cout<<st.empty()<<endl;
```
**增删查均为$o(\log n)$**

| 作用                          | 用法             | 示例                    |
| ----------------------------- | ---------------- | ----------------------- |
| 插入元素                      | `.insert(元素)`  | `st.insert(1);`         |
| 删除元素                      | `.erase(元素)`   | `st.erase(2);`          |
| 查找元素                      | `.find(元素)`    | `auto it = st.find(1);` |
| 返回目标数个数                | `.count(元素)`   | `st.count(3);`          |
| 返回**大于等于**x最小数迭代器 | `.lower_bound()` | `st.lower_bound()`      |
| 返回**大于**x最小数迭代器     | `.upper_bound()` | `st.upper_bound()`      |
`.erase()`

	1. 输入一个数x,删除所有x  O(k+logn) k为x个数
	1. 输入一个迭代器，删除这个迭代器

## 遍历

可使用迭代器进行遍历：

```cpp
for (set<int>::iterator it = st.begin(); it != st.end(); ++it)
    cout << *it << endl;
```

基于范围的循环（C++ 11）：

```cpp
for (auto &ele : st)
    cout << ele << endl;
```


## 适用情形

- 元素去重,维护顺序：$[1,3,7,9,9,3,5]\to[1,3,5,7,9]$
- 元素是否出现过：元素大小$[-10^8,10^8]$ ，元素数量$10^6$ ，vis 数组无法实现，通过 set 可以完成。(同过.count()) *$O(\log n)$*

## 注意
#### 不存在下标索引
set 虽说可遍历，但仅可使用迭代器进行遍历，它不存在下标这一概念，无法通过下标访问到数据。
#### 元素只读
set 的迭代器取到的元素是只读的（因为是 const 迭代器），不可修改其值。如果要改，需要先 erase 再 insert.
####  不存在下标索引
set 虽说可遍历，但仅可使用迭代器进行遍历，它不存在下标这一概念，无法通过下标访问到数据

# map
提供对数时间的有序键值对结构。底层原理是红黑树。


| 性质   | 解释                         | map           | multimap      | unordered_map |
| ------ | ---------------------------- | ------------- | ------------- | ------------- |
| 互异性 | 一个键仅可以在映射中出现一次 | ✔             | ❌（任意次）   | ✔             |
| 无序性 | 键是没有顺序的               | ❌（从小到大） | ❌（从小到大） | ✔             |
## 构造
**`map<键类型, 值类型, 比较器> mp`**

- 键类型：要储存键的数据类型
- 值类型：要储存值的数据类型
- 比较器：键比较大小使用的比较器，默认为 `less<类型>`，可自定义

```cpp
map<int, int> mp1;               // int->int 的映射（键从小到大）
map<int, int, greater<int>> st2; // int->int 的映射（键从大到小）

mp[2]=1;//增

if(mp1.find(0)!=mp.end() or mp.count(0))//查
{
	cout<<"yes"<<endl;
}
else
{
	cout<<"no"<<endl;
}

mp.erase(2)//删
```


| 作用                          | 用法               | 示例                    |
| ----------------------------- | ------------------ | ----------------------- |
| 增 / 改 / 查元素              | 中括号 $O(\log n)$ | `mp[1] = 2;`            |
| 查元素（返回迭代器）          | `.find(元素)`      | `auto it = mp.find(1);` |
| 删除元素                      | `.erase(元素)`     | `mp.erase(2);`          |
| 判断元素是否存在              | `.count(元素)`     | `mp.count(3);`          |
| 返回**大于等于**x最小数迭代器 | `.lower_bound()`   | `st.lower_bound()`      |
| 返回**大于**x最小数迭代器     | `.upper_bound()`   | `st.upper_bound()`      |
| 查看大小 / 清空 / 判空        | 略                 | 略                      |
## 遍历
- 迭代器遍历
```cpp
for(map<int,int>::iterator it = mp.begin();it!=mp.end();++it)
	cout<<it->first<<' '<<it->second<<endl;
	//       键              值
```

- 基于范围循环
```cpp
for(auto &pr : mp)
cout<<pr.first<<' '<<pr.second<endl;
```

- 语法糖

```cpp
for(auto &[x,y]:mp)
  cout<<x<<' '<<y<<endl;
```



## 适用情形

需要维护映射的场景可以使用：输入若干字符串，统计每种字符串的出现次数。(`map<string, int> mp`)

## 注意⚠️
#### 中括号访问时默认值

如果使用中括号访问 map 时对应的键不存在，那么会新增这个键，并且值为默认值，因此中括号会影响键的存在性。

```cpp
map<char, int> mp;
cout << mp.count('a') << endl; // 0
mp['a'];                       // 即使什么都没做，此时mp['a']=0已经插入了
cout << mp.count('a') << endl; // 1
cout << mp['a'] << endl;       // 0
```

#### 不可用迭代器计算下标

map 的迭代器不能像 vector 一样相减得到下标。**下面是错误用法：**

```cpp
auto it = mp.find('a');      // 正确，返回2所在位置的迭代器。
int idx = it - mp.begin();   // 错误！不可相减得到下标。
```

# string
## 构造
`string(长度, 初值)`

```cpp
string s1;           // 构造字符串，为空
string s2 = "awa!";  // 构造字符串，并赋值awa!
string s3(10, '6');  // 构造字符串，通过构造函数构造为6666666666
```

## 输入输出
```cpp
string s; 
cin >> s; 
cout << s;
printf("%s",a.c_str());//.c_str()返回数组首地址
```


## 操作

| 作用                   | 用法                          | 示例                            |
| ---------------------- | ----------------------------- | ------------------------------- |
| 修改、查询指定下标字符 | `[]`                          | `s[1] = 'a';`                   |
| 是否相同               | ==                            | `if (s1 == s2) ...`             |
| 字符串连接             | `+`                           | `string s = s1 + s2;`           |
| 尾接字符串             | `+=`                          | `s += "awa";`                   |
| 取子串                 | `.substr(起始下标, 子串长度)` | `string sub = s.substr(2, 10);` |
| 查找字符串             | `.find(字符串, 起始下标)`     | `int pos = s.find("awa");`      |
```cpp
string s1="123123"
if(s1.find(312)!=string::npos)
cout<<"yes"<<endl;
```

## 数值与字符串互转（C++11）

| 源                                             | 目的        | 函数        |
| ---------------------------------------------- | ----------- | ----------- |
| int / long long / float / double / long double | string      | to_string() |
| string                                         | int         | stoi()      |
| string                                         | long long   | stoll()     |
| string                                         | float       | stof()      |
| string                                         | double      | stod()      |
| string                                         | long double | stold()     |
## 注意⚠️
#### 尾接字符串一定要用 `+=`

string 的 += 运算符，将会在原字符串原地尾接字符串。而 + 了再 = 赋值，会先生成一个临时变量，在复制给 string.

通常字符串长度可以很长，如果使用 + 字符串很容易就 TLE 了。

```cpp
// 优化前: 15139ms
string s;
for (int i = 0; i < 5e5; i++)
    s = s + "a";

// 优化后: < 1ms (计时器显示0)
string s;
for (int i = 0; i < 5e5; i++)
    s += "a";
```

#### `.substr()` 方法的奇葩参数

一定要注意，C++ string 的取子串的第一个参数是**子串起点下标**，第二个参数是**子串长度**。

第二个参数不是子串终点！不是子串终点！要与 java 等其他语言区分开来。

#### `.find()` 方法的复杂度

该方法实现为暴力实现，时间复杂度为$O(n^2)$ .

# pair
## 构造
**`pair<第一个值类型, 第二个值类型> pr`**
- 第一个值类型：要储存的第一个值的数据类型
- 第二个值类型：要储存的第二个值的数据类型

`p=make_pair(10,"wf")`

## 赋值
`pair<int, char> pr = {1, 'a'};`
## 取值
直接取值
- 取第一个值：`.first`
- 取第二个值：`.second`
## 判同
直接用 == 运算符

```cpp
pair<int, int> p1 = {1, 2};
pair<int, int> p2 = {1, 3};
if (p1 == p2) { ... } // false
```

## 支持比较

first第一关键字，second第二关键字(字典序)

 ## 存三种元素

`pair<int,pair<int,int>>p`



# bitset

压位，节省8位空间

## 应用

```cpp
bitset<10000> S;
~, &, |, ^//取反，与，或，抑或
>>,<<//位运算
==, !=
[]//取出某一位0/1
count()//返回多少个1
any()//判断是否至少1个1
none()//判断是否全为空
  
set()//所有位置变成1
set(k,v)//把第k位变成v
reset()//所有位变成0
flip()//等价~
flip(k)//第k位取反
```





# 迭代器

## 迭代器用法

对于 vector 容器，它的迭代器功能比较完整，以它举例：

- `.begin()`：头迭代器
- `.end()`：尾迭代器
- `.rbegin()`：反向头迭代器
- `.rend()`：反向尾迭代器
- 迭代器 `+` 整型：将迭代器向后移动
- 迭代器 `-` 整型：将迭代器向前移动
- 迭代器 `++`：将迭代器向后移动 1 位
- 迭代器 `--`：将迭代器向前移动 1 位
- 迭代器 `-` 迭代器：两个迭代器的距离
- `prev(it)`：返回 it 的前一个迭代器
- `next(it)`：返回 it 的后一个迭代器

对于其他容器，由于其结构特性，上面的功能不一定都有（例如 set 的迭代器是不能相减求距离的

## 常见问题

**`.end()` 和 `.rend()` 指向的位置是无意义的值**

对于一个长度为 10 的数组：`for (int i = 0; i < 10; i++)`，第 10 位是不可访问的

对于一个长度为 10 的容器：`for (auto it = a.begin(); it != a.end(); ++it)`，.end 是不可访问的

**不同容器的迭代器功能可能不一样**

迭代器细化的话有正向、反向、双向，每个容器的迭代器支持的运算符也可能不同，因此不同容器的迭代器细节很有可能是不一样的。

**删除操作时需要警惕**

为什么 3 没删掉？

```cpp
vector<int> a{1, 2, 3, 4};
for (auto it = a.begin(); it != a.end(); ++it)
    if (*it == 2 || *it == 3)
        a.erase(it);
// a = [1, 3, 4]
```
**删除一个元素2后，后面的元素都向前移动，it自增导致跳过元素3**

为啥 RE 了？

```cpp
vector<int> a{1, 2, 3, 4};
for (auto it = a.begin(); it != a.end(); ++it)
    if (*it == 4)
        a.erase(it);
```
**删除一个元素4后，it=a.end()，it自增导致越界**

# 常用算法
## `swap()`

交换两个变量的值

**用法示例**

```cpp
template< class T >
void swap( T& a, T& b );
```

```cpp
int a = 0, b = 1;
swap(a, b);
// now a = 1, b = 0

int arr[10] {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
swap(arr[4], arr[6]);
// now arr = {0, 1, 2, 3, 6, 5, 4, 7, 8, 9}
```

**注意事项**

这个 swap 参数是引用的，不需要像 C 语言一样取地址。

##  `sort()`

使用快速排序给一个可迭代对象排序

**用法示例**

```cpp
template< class RandomIt, class Compare >
void sort( RandomIt first, RandomIt last, Compare comp );
```

默认排序从小到大

```cpp
vector<int> arr{1, 9, 1, 9, 8, 1, 0};
sort(arr.begin(), arr.end());
// arr = [0, 1, 1, 1, 8, 9, 9]
```

如果要从大到小，则需要传比较器进去。

```cpp
vector<int> arr{1, 9, 1, 9, 8, 1, 0};
sort(arr.begin(), arr.end(), greater<int>());
// arr = [9, 9, 8, 1, 1, 1, 0]
```

如果需要完成特殊比较，则需要手写比较器。

比较器函数返回值是 bool 类型，传参是需要比较的两个元素。记我们定义的该比较操作为$ ：

- 若a$b ，则比较器函数应当返回 `true`
- 若 a❌$b ，则比较器函数应当返回 `false`

**注意：** 如果 ，比较器函数必须返回 `false`

```cpp
bool cmp(pair<int, int> a, pair<int, int> b)
{
    if (a.second != b.second)// 1. 首先比较第二个数 (second)
        return a.second < b.second;//如果第二个数不等，按第二个数升序排列
    return a.first > b.first;// 2. 如果第二个数相等，按第一个数 (first) 降序排列 
}

int main()
{
    vector<pair<int, int>> arr{{1, 9}, {2, 9}, {8, 1}, {0, 0}};
    sort(arr.begin(), arr.end(), cmp);
    // arr = [(0, 0), (8, 1), (2, 9), (1, 9)]
}
```

## `lower_bound()` / `upper_bound()`

在**已升序排序**的元素中，应用二分查找检索指定元素，返回对应元素迭代器位置。**找不到则返回尾迭代器。**

- `lower_bound()`: 寻找 $\geq x$ 的第一个元素的位置
- `upper_bound()`: 寻找 $>x$ 的第一个元素的位置

怎么找 $\leq x$ / $<x$ 的第一个元素呢？

-  $>x$的第一个元素的前一个元素（如果有）便是  $\leq x$ 的第一个元素
-  $\geq x$的第一个元素的前一个元素（如果有）便是 $<x$ 的第一个元素

返回的是迭代器，如何转成下标索引呢？减去头迭代器即可。

### 示例
```cpp
vector<int>arr{0,1,1,8,8,9,9};
//找>8的位置
int pos = upper_bound(arr.begin(),arr.end(),8)-arr.begin();
if(pos=arr.size()) cout<<"no"<<endl;
cout<<pos<<endl;
```

##  `reverse()`

反转一个可迭代对象的元素顺序

**用法示例**

```cpp
template< class BidirIt >
void reverse( BidirIt first, BidirIt last );
```

```cpp
vector<int> arr(10);
iota(arr.begin(), arr.end(), 1);
// 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
reverse(arr.begin(), arr.end());
// 10, 9, 8, 7, 6, 5, 4, 3, 2, 1
```
**注意：reverse（）的范围是左闭右开格式，因此取不到右边界的值**

## `max()/min()`

在 C++11 之后，可以使用列表构造语法传入一个列表，这样就能一次性给多个元素找最大值而不用套娃了：

```cpp
// Before C++11
int mx = max(max(1, 2), max(3, 4)); // 4
int mn = min(min(1, 2), min(3, 4)); // 1

// After C++11
int mx = max({1, 2, 3, 4}); // 4
int mn = min({1, 2, 3, 4}); // 1
```

## `unique()`

消除数组的重复**相邻**元素，数组长度不变，但是有效数据缩短，返回的是有效数据位置的结尾迭代器。

例如：$[1,1,4,5,1,4]\to[1,4,5,1,4,?]$，下划线位置为返回的迭代器指向。

```cpp
template< class ForwardIt >
ForwardIt unique( ForwardIt first, ForwardIt last );
```

**用法示例**

单独使用 unique 并不能达成去重效果，因为它只消除**相邻**的重复元素。但是如果序列有序，那么它就能去重了。

但是它去重后，序列尾部会产生一些无效数据：$[1,1,2,4,4,4,5]\to[1,2,4,5,?,?,?]$，为了删掉这些无效数据，我们需要结合 erase.

最终，给 vector 去重的写法便是：

```cpp
vector<int> arr{1, 2, 1, 4, 5, 4, 4};
sort(arr.begin(), arr.end());
//1 1 2 4 4 4 5
//1 2 4 5 * * * 
arr.erase(unique(arr.begin(), arr.end()), arr.end());
//         unique()返回有效数字后一位的位置
```

## 数学函数

所有函数参数均支持 `int` / `long long` / `float` / `double` / `long double`

| 公式                                            | 示例         |
| ----------------------------------------------- | ------------ |
| $f(x)=\left \| x \right \|$                     | `abs(-1.0)`  |
| $f(x)=e^x$                                      | `exp(2)`     |
| $f(x)=\ln x$                                    | `log(3)`     |
| $f(x)=x^y$                                      | `pow(2, 3)`  |
| $f(x)=\sqrt{ x }$                               | `sqrt(2)`    |
| $f(x)=\left \lceil x \right \rceil$             | `ceil(2.1)`  |
| $f(x)=\left \lfloor x \right \rfloor$           | `floor(2.1)` |
| $f(x)=\left \langle x \right \rangle$(四舍五入) | `round(2.1)` |

### 注意⚠️
1. $\left\lfloor  \frac{a}{b} \right\rfloor$
	- 别用：`floor(1.0 * a / b)`
	- 要用：`a / b`
2. $\left \lceil \frac {a}{b} \right \rceil$
	- 别用：`ceil(1.0 * a / b)`
    - 要用：`(a + b - 1) / b` （$\left\lceil  \frac{a}{b}  \right\rceil=\left\lfloor  \frac{a+b-1}{b}  \right\rfloor$）
3. $\lceil \sqrt{ x } \rceil$
	- 别用：`(int) sqrt(a)`
	- 要用：二分查找
4. $a^b$
	- 别用：`pow(a, b)`
	- 要用：快速幂
5. $\lceil \log_{2}a \rceil$
	- 别用：`log2(a)`
	- 要用：`__lg` （不规范，但是这是竞赛）/ `bit_width`（C++20 可用）

## `gcd()` / `lcm()`

（C++17）返回最大公因数 / 最小公倍数

```cpp
int x = gcd(8, 12); // 4
int y = lcm(8, 12); // 24
```

当然，`gcd` / `lcm` 函数也挺好写，直接写也行（欧几里得算法）：

```cpp
int gcd(int a, int b)
{
    if (!b)
        return a;
    return gcd(b, a % b);
}

int lcm(int a, int b)
{
    return a / gcd(a, b) * b;
}
```

# 语法🍬

## auto关键字

声明变量用auto代替类型名字，编译器在编译期间自动推导变量类型

```cpp
auto x=10;//int 
auto x=3.14;//double
auto x='a';//char
```



## 基于范围的for循环

```cpp
int main(){
  int a[]={1,1,4,5,1,4};
  for(int el: a)cout<<el<<endl;
}
```

## 结构化绑定（c++17）

示例1:pair输出

```cpp
pair<int,int>u={1,2};
cout<<u.first<<" "<<u.second<<endl;//正常输出 

auto [x,y]=u;//结构化绑定
cout<<x<<" "<<y<<endl;
```

示例2:vector<pair<int,int>>

```cpp
vector<pair<int,int>>seq;

for(auto u:seq)
{
  int x=seq.first;
  int y=seq.second;
}//正常写法

for(auto [x,y]:seq)
{
  //....
}
```

## lambda表达式

允许在任何地方定义函数

基础用法

```cpp
auto funcname = [&](type1 x1,type2 x2)->returntype{
  //...
};
```

- lambda表达式是语句，不能忘分号
- 当采用 [&]时，Lambda 函数可以修改外部的变量，采用[=]时则不行
- -> returnType 可省略。

示例1

```cpp
int main()
{
  auto touppercase=[=](string s)->string{
    for(auto ele:s)
    {
      ele=toupper(ele)
      return s;
    }
  }
  cout<<touppercase("hello world")<<endl;
}
```

