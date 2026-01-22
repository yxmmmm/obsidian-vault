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
