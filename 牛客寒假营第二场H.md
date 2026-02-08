#算法 #blog #哈希
# 题干
链接：[https://ac.nowcoder.com/acm/contest/120562/H](https://ac.nowcoder.com/acm/contest/120562/H)  
## 权值计算
```
Algorithm 1 函数 f 用于计算数组 s 的权值 
1: function f(l, r, s) 
2:     distinct ← ∅ 
3:     total ← 0 
4:     current_count ← 0 
5:     for i ← l to r do 
6:         if s[i] ∉ distinct then 
7:             current_count ← current_count + 1 
8:             distinct ← distinct ∪ {s[i]} 
9:         end if 
10:      total ← total + current_count 
11:     end for 
12:     return total 13: end function
```

如上是一段计算数组权值的伪代码，通过调用 f(1,m,s)f(1,m,s)f(1,m,s) 计算一个长度为 m 的数组 $s_1,s_2,\dots,s_m$​ 的权值，现在 Bingbong 有一个长度为 n 的数组 $a_1,a_2,\dots,a_n$​，请你帮助他求出所有非空子数组的权值之和。  
  
### 名词解释  
子数组：从原数组中，连续的选择一段元素（可以全选、可以不选）得到的新数组。

### 输入描述:

每个测试文件均包含多组测试数据。第一行输入一个整数 $T(1≤T≤104)$，代表数据组数，每组测试数据描述如下：  
  
第一行输入一个整数$n(1≤n≤105)$，表示数组长度。  
第二行输入 n 个整数 $a1,a2,…,an(1≤ai≤109)$，表示数组中的元素。  
  
除此之外，保证单个测试文件的 n 之和不超过 $10^5$。  

### 输出描述:

对于每一组测试数据，新起一行输出一个整数，表示所有子数组的权值之和。

# 思路
## 暴力
这题暴力非常好想，单纯将l和r做一次遍历即可覆盖所有情况，再将所有情况带入翻译成代码的伪代码中即可
```cpp
for(int i=0;i<n;i++)
{

	for(int j=i;j<n;j++)
	{

		sum+=f(i,j-i+1,s);

	}

}
```

除开solve函数中包含的两层循环外还有一个solve循环，时间复杂度为$O(n^3)$，必然超时

## 贡献度思想
### eg
![算竞手稿.jpeg](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvault%E7%AE%97%E7%AB%9E%E6%89%8B%E7%A8%BF.jpeg)
如图，1314数组的以初始1为左界的前缀中不同元素权值的和用$1+2+2+3$表示这是分别枚举前缀并观察前缀元素求和得到
但还有方法是从单个元素对整体贡献度的角度

**初始1对整体贡献4次**
**3对整体贡献3次**
**第三个1被初始1吞并，无贡献**
**4贡献1次**

因此也可表示为$4+3+1$

### 规律

1. 相同左界对不同右界组成的前缀的贡献成等差数列
2. 当相同左界作为右界或中心值时，其在对应的相同左界的前缀中贡献值也为相同的等差数列，听上去很抽象，有图就很清晰了![IMG_A0792C290169-1.jpeg](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvaultIMG_A0792C290169-1.jpeg)

因此解题核心转化为两个部分
1. 有几个合法左界$\to$**前一个一样的数后面**
2. 等差数列长度$\to 1+2\dots+n-i+1$

## 代码实现
```cpp
#include <bits/stdc++.h>
using namespace std;

#define int long long
#define pi acos(-1)

void solve() {
    int n;
    cin>>n;
    map<int,vector<int>>mp;//定义map即初始化了一个数组
    for(int i=1;i<n+1;i++){
        int x;cin>>x;
        mp[x].push_back(i);
    }//将数字和对应的位置存入map中

    int ans=0;
    for(auto &[x,y] :mp){
        y.insert(y.begin(),0);//补0方便首项也套公式
        for(int i=1;i<y.size();i++){
            int l=y[i-1];
            int r=n-y[i]+1;
            ans+=(y[i]-l)*r*(r+1)/2;
        }
    }
    cout<<ans<<endl;
}

signed main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int t = 1;
    cin >> t;

    while (t--) {
        solve();
    }

    return 0;
}
```