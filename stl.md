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
vector<vecter<vecter<int>>> dp2(5,vecter<vecter<int>>(6,vecter<int>(4)))
//6行4列5高，三维数组
```

## 尾接&尾删
```cpp
int main()
{
	vecter<int> arr;
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

# stack
先进后出

```cpp
stack<double>stk;
stk.push_back(1.0);
stk.pop_back();
```
## 常用方法
  

| 作用             | 用法              | 示例                   |
| -------------- | --------------- | -------------------- |
| 构造             | `stack<类型> stk` | `stack<int> stk;`    |
| 进栈             | `.push(元素)`     | `stk.push(1);`       |
| 出栈             | `.pop()`        | `stk.pop();`         |
| 取栈顶            | `.top()`        | `int a = stk.top();` |

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
| 作用   | 用法              | 示例                     |
| ---- | --------------- | ---------------------- |
| 构造   | `queue<类型> que` | `queue<int> que;`      |
| 进队   | `.push(元素)`     | `que.push(1);`         |
| 出队   | `.pop()`        | `que.pop();`           |
| 取队首  | `.front()`      | `int a = que.front();` |
| 取队尾  | `.back()`       | `int a = que.back();`  |
| 查看大小 | `.size()`       | `int a = que.size();`  |
| 判空   | `.empty()`      | `int a = que.empty();` |
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
```


## 常用方法
| 作用   | 用法                       | 示例                         |
| ---- | ------------------------ | -------------------------- |
| 构造   | `priority_queue<类型> que` | `priority_queue<int> que;` |
| 进堆   | `.push(元素)`              | `pque.push(1);`            |
| 出堆   | `.pop()`                 | `pque.pop();`              |
| 取堆顶  | `.top()`                 | `int a = pque.top();`      |
| 查看大小 | `.size()`                | `int a = pque.size();`     |
| 判空   | `.empty()`               | `int a = pque.empty();`    |
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

# set
提供对数时间的插入、删除、查找的集合数据结构。底层原理是红黑树。

| 集合三要素 | 解释              | set     | multiset | unordered_set |
| ----- | --------------- | ------- | -------- | ------------- |
| 确定性   | 一个元素要么在集合中，要么不在 | ✔       | ✔        | ✔             |
| 互异性   | 一个元素仅可以在集合中出现一次 | ✔       | ❌（任意次）   | ✔             |
| 无序性   | 集合中的元素是没有顺序的    | ❌（从小到大） | ❌（从小到大）  | ✔             |
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

| 作用       | 用法            | 示例                      |
| -------- | ------------- | ----------------------- |
| 插入元素     | `.insert(元素)` | `st.insert(1);`         |
| 删除元素     | `.erase(元素)`  | `st.erase(2);`          |
| 查找元素     | `.find(元素)`   | `auto it = st.find(1);` |
| 判断元素是否存在 | `.count(元素)`  | `st.count(3);`          |
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
-  不存在下标索引
set 虽说可遍历，但仅可使用迭代器进行遍历，它不存在下标这一概念，无法通过下标访问到数据。
- 元素只读
set 的迭代器取到的元素是只读的（因为是 const 迭代器），不可修改其值。如果要改，需要先 erase 再 insert.