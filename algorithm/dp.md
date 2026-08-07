#算法 #dp

# 背包dp

## 01背包

![6357742c1942e003e5dbc379b946d4c9](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvault6357742c1942e003e5dbc379b946d4c9.jpg)![0a28567b8b49ac732973c95d591a8c5e](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvaultobsidianvault0a28567b8b49ac732973c95d591a8c5e.jpg)

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
const int N = 1000;

int f[N][N];
int v[N], w[N];

signed main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int n, V;
    cin >> n >> V;
    for (int i = 1; i <= n; i++)
        cin >> v[i] >> w[i];

    //二维
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= V; j++)
        {
            f[i][j] = f[i - 1][j];
            if (v[i] <= j)
                f[i][j]=max(f[i][j],f[i-1][j-v[i]]+w[i]);
        }
    }
    cout << f[n][V];
    //一维优化
    for(int i=1;i<=n;i++)
    {
        for(int j=V;j>=v[i];j--)
        {
            f[j]=max(f[j],f[j-v[i]]+w[i]);
        }
    }
    cout<<f[V];
}
```

1. 假如j从小到大遍历f[j-v[i]]已被更改，因此倒序遍历
2. j<v[i]时二维语句无效，因此j只遍历到v[i]即可
3. 由于第i层只用到i-1层数据因此只需要用一维数组更新

## 完全背包

![532696834a85441c7d0e451f824905ea](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvault532696834a85441c7d0e451f824905ea.jpg)

```cpp
#include <bits/stdc++.h>
using namespace std;
#define endl '\n'
#define int long long

const int N = 1010;
int f[N][N];
int v[N], w[N];

signed main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int n, V;
    cin >> n >> V;
    for (int i = 1; i <= n; i++)
        cin >> v[i] >> w[i];

    // 二维
    for (int i = 1; i <= n; i++)
    {
        for (int j = 0; j <= V; j++)
        {
            for (int k = 0; k * v[i] <= j; k++)
            {
                f[i][j] = max(f[i - 1][j], f[i - 1][j - k * v[i]] + k * w[i]);
            }
        }
    }
    cout << f[n][V] << endl;

    // 一维优化
    //   for(int i=1;i<=n;i++)
    //   {
    //       for(int j=v[i];j<=V;j++)
    //       {
    //           f[j]=max(f[j],f[j-v[i]]+w[i]);
    //       }
    //   }
}
```



## 多重背包

![7e0987d66245fa25055b973a4413dcf6](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvaultobsidianvault7e0987d66245fa25055b973a4413dcf6.jpg)![edaf0b08bcdc2a12f8efc8c1accc8fec](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvaultedaf0b08bcdc2a12f8efc8c1accc8fec.jpg)

```cpp
#include <bits/stdc++.h>
using namespace std;
#define endl '\n'
#define int long long

const int N = 12020, M = 2010;
int v[N], w[N];
int n, m;
int f[M];

signed main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    cin >> n >> m;
    int cnt = 0;
    while (n--)
    {
        int a, b, s;
        cin >> a >> b >> s;
        int k = 1;
        //二进制
        while (k <= s)
        {
            cnt++;
            v[cnt] = a * k;
            w[cnt] = b * k;
            s -= k;
            k *= 2;
        }
        //处理多余部分
        if (s > 0)
        {
            cnt++;
            v[cnt] = a * s;
            w[cnt] = b * s;
        }
    }
    n = cnt;
    //01背包
    for (int i = 1; i <= n; i++)
    {
        for (int j = m; j >= v[i]; j--)
            f[j] = max(f[j], f[j - v[i]] + w[i]);
    }
    cout << f[m] << endl;
}
```

朴素三重循环一定tle

利用二进制优化使得时间复杂度$O(V \sum s_i)$降低至$O(V \sum \log s_i)$

可以理解为每一个种类的每一份的地位是相同的都看作完全独立的一份

每一份只有选和不选两种情况01dp

## 分组dp

![8416f90c9819cf8f839d0382d249db65](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvault8416f90c9819cf8f839d0382d249db65.jpg)

```cpp
#include <bits/stdc++.h>
using namespace std;
#define endl '\n'
#define int long long

const int N = 110;
int s[N], v[N][N], w[N][N];
int f[N];
signed main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int n, m;
    cin >> n >> m;
    for (int i = 1; i <= n; i++)
    {
        cin >> s[i];
        for (int j = 0; j < s[i]; j++)
            cin >> v[i][j] >> w[i][j];
    }
    for (int i = 1; i <= n; i++)
    {
        for (int j = m; j >= 0; j--)
        {
            for (int k = 0; k < s[i]; k++)
            {
                if (v[i][k] <= j)
                {
                    f[j] = max(f[j], f[j - v[i][k]] + w[i][k]);
                }
            }
        }
    }
    cout << f[m];
}
```

# 线性dp

![f3059d87c47e25e28d9ddbc030924a95](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvaultf3059d87c47e25e28d9ddbc030924a95.jpg)

```cpp
#include <bits/stdc++.h>
using namespace std;
#define endl '\n'
#define int long long

const int N = 510;
int f[N][N];
int a[N][N];
int n, INF = 1e9;

signed main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    cin >> n;
    memset(f, 0x8f, sizeof(f));
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= i; j++)
            cin >> a[i][j];
    }
    f[1][1] = a[1][1];
    for (int i = 2; i <= n; i++)
    {
        for (int j = 1; j <= i; j++)
        {
            f[i][j] = max(f[i - 1][j - 1] + a[i][j], f[i - 1][j] + a[i][j]);
        }
    }
    int res = -INF;
    for (int i = 1; i <= n; i++)
    {
        res = max(res, f[n][i]);
    }
    cout << res << endl;
}
```

![00de498a9f39a78b2323a29951be867c](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvault00de498a9f39a78b2323a29951be867c.jpg)

```cpp
#include <bits/stdc++.h>
using namespace std;
#define endl '\n'
#define int long long

const int N = 1010;
int a[N], f[N];

signed main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int t;
    cin >> t;
    for (int i = 1; i <= t; i++)
        cin >> a[i];

    for (int i = 1; i <= t; i++)
    {
        f[i] = 1;
        for (int j = 1; j < i; j++)
        {
            if (a[j] < a[i])
            {
                f[i] = max(f[i], f[j] + 1);
            }
        }
    }
    int maxx = 0;
    for (int i = 1; i <= t; i++)
    {
        maxx = max(maxx, f[i]);
    }

    cout << maxx << endl;
}
```

![61ee1af842fda0d3eabdf7f644e63299](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvault61ee1af842fda0d3eabdf7f644e63299.jpg)

```cpp
#include <bits/stdc++.h>
using namespace std;
#define endl '\n'
#define int long long

const int N = 1010;
int n, m;
int f[N][N];
char a[N], b[N];

signed main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> n >> m;
    for (int i = 1; i <= n; i++)
        cin >> a[i];
    for (int i = 1; i <= m; i++)
        cin >> b[i];
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= m; j++)
        {
            f[i][j] = max(f[i - 1][j], f[i][j - 1]);
            if (a[i] == b[j])
                f[i][j] = max(f[i][j], f[i - 1][j - 1] + 1); // 只有a[i]==b[j]时才需要第三种
        }
    }
    cout << f[n][m] << endl;
}
```

# 区间dp

![1532af1496a2d80517ed8941c6d6f479](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvault1532af1496a2d80517ed8941c6d6f479.jpg)

```cpp
#include <bits/stdc++.h>
using namespace std;
#define endl '\n'
#define int long long

const int N = 310;
int f[N][N];
int s[N];
int n;

signed main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> n;
    for (int i = 1; i <= n; i++)
        cin >> s[i];
    for (int i = 1; i <= n; i++)
        s[i] += s[i - 1];
    for (int len = 2; len <= n; len++)
    {
        for (int i = 1; i + len - 1 <= n; i++)
        {
            int j = len + i - 1;
            f[i][j] = 1e18;
            for (int k = i; k < j; k++)
                f[i][j] = min(f[i][j], f[i][k] + f[k + 1][j] + s[j] - s[i - 1]);
        }
    }
    cout << f[1][n];
}
```

# 计数dp

完全背包

![da0a6b1acccdf48523f391045d7f3285](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvaultda0a6b1acccdf48523f391045d7f3285.jpg)

划分个数

![54f5901b6e565985957ef082a20976c0](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvault54f5901b6e565985957ef082a20976c0.jpg)

```cpp
#include <bits/stdc++.h>
using namespace std;
#define endl '\n'
#define int long long

int mod = 1e9 + 7;
const int N = 1010;
int f[N][N];
int n;

signed main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    cin >> n;
    f[0][0] = 1;
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= i; j++)
        {
            f[i][j] = (f[i - 1][j - 1] + f[i - j][j]) % mod;
        }
    }
    int ans = 0;
    for (int i = 1; i <= n; i++)
        ans = (ans + f[n][i]) % mod;
    cout << ans;
}
```

# 数位dp

![5cd19700f5e688857d8abbbb191c5489](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvault5cd19700f5e688857d8abbbb191c5489.jpg)![5cd19700f5e688857d8abbbb191c5489](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvault18b7eb3bec48d70f68a20eddb0d106f3.jpg)

```cpp
#include <bits/stdc++.h>
using namespace std;
#define endl '\n'
#define int long long

int power10(int x)
{
    int res = 1;
    while (x--)
        res *= 10;
    return res;
}//10的x次幂

int count(int x, int n)
{
    int m = n;
    int cnt = 0;
    while (m)
    {
        m /= 10;
        cnt++;
    }//得到数位长度

    int res = 0;
    int l;
    for (int i = 1; i <= cnt; i++)
    {
        l = n / power10(i);
        if (x)
            res += l * power10(i - 1);
        else
            res += (l - 1) * power10(i - 1);//x=0时的前导零边界情况

        int d = (n / power10(i - 1)) % 10;
        if (d > x)
            res += power10(i - 1);
        else if (d == x)
            res += n % power10(i - 1) + 1;//000-efg
    }
    return res;
}

signed main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int a, b;
    while (cin >> a >> b, a || b)
    {
        if (a > b)
            swap(a, b);
        for (int i = 0; i <= 9; i++)
            cout << count(i, b) - count(i, a - 1) << ' ';//前缀和思想
        cout << endl;
    }
}
```

# 状压dp

![d82a2a08597c2df18f22a52e6fd97244](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvaultd82a2a08597c2df18f22a52e6fd97244.jpg)

| **位运算表达式**   | **逻辑意义 / 物理功能**                                      |
| ------------------ | ------------------------------------------------------------ |
| **`1 << n`**       | 状态空间的总大小（即 $2^n$），或构造单节点 $n$ 的二进制掩码  |
| **`i >> j & 1`**   | **查询**：状态 $i$ 中，第 $j$ 个节点是否存在（是否被访问过） |
| **`i - (1 << j)`** | **删除**：从状态 $i$ 中删除第 $j$ 个节点（前提是第 $j$ 位为 1） |
| **`i | (1 << j)`** | **添加**：向状态 $i$ 中添加第 $j$ 个节点                     |
| **`i ^ (1 << j)`** | **翻转**：将第 $j$ 位取反（1 变 0，0 变 1）                  |

```cpp
#include <bits/stdc++.h>
using namespace std;
#define endl '\n'
#define int long long
const int N = 20, M = 1 << N;//利用二进制存储路径状态
int f[M][N];
int a[N][N];

signed main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int n;
    cin >> n;
    memset(f, 0x3f, sizeof f);
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            cin >> a[i][j];

    f[1][0] = 0;//初始化起点终点都为0路径长度为0

    for (int i = 0; i < 1 << n; i++)//枚举不同状态
        for (int j = 0; j < n; j++)
            if (i >> j & 1)//判断j是否在路过
                for (int k = 0; k < n; k++)
                    if ((i - (1 << j)) >> k & 1)//回退j并判断k是否路过
                        f[i][j] = min(f[i][j], f[i - (1 << j)][k] + a[k][j]);

    cout << f[(1 << n) - 1][n - 1] << endl;
}
```

![5588e18a5d9b57b35823f74ae1c2d636](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvault5588e18a5d9b57b35823f74ae1c2d636.jpg)

```cpp
#include <bits/stdc++.h>
using namespace std;
#define endl '\n'
#define int long long

const int N = 12, M = 1 << N;
int f[N][M];
int n, m;
vector<vector<int>> state(M);//等效二维数组
bool st[M];

signed main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    while (cin >> n >> m, m || n)
    {
        //预处理1：判断状态是否合法
        for (int i = 0; i < 1 << n; i++)
        {
            int cnt = 0;
            bool ok = true;
            for (int j = 0; j < n; j++)//最多移动n-1位
            {
                if (i >> j & 1)
                {
                    if (cnt & 1)//判断cnt奇偶
                    {
                        cnt = 0;
                        ok = false;
                        break;
                    }
                }
                else
                    cnt++;
            }
            if (cnt & 1)//最后一段假如是0是否合法
                ok = false;
            st[i] = ok;
        }

        //预处理2：根据已知i列状态储存合法i-1类状态，减少dp过程无效枚举次数
        for (int i = 0; i < 1 << n; i++)
        {
            state[i].clear();
            for (int j = 0; j < 1 << n; j++)
                if ((i & j) == 0 && st[i | j])
                    state[i].push_back(j);
        }

        memset(f, 0, sizeof f);
        f[0][0] = 1;//初始化引子，第一列不可能有伸出所以状态一定为0，一种情况
        for (int i = 1; i <= m; i++)
        {
            for (int j = 0; j < 1 << n; j++)
            {
                for (auto k : state[j])
                    f[i][j] += f[i - 1][k];
            }
        }
        cout << f[m][0] << endl;//列下标最大到m-1，因此m列不可能有伸出
    }
}
```

# 树形dp

![](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvault6f686c7c6be28b0cb7d9e02728be1bcb.jpg)

```cpp
#include <bits/stdc++.h>
using namespace std;
#define endl '\n'
#define int long long

const int N = 6010;
int e[N], h[N], ne[N], idx;
bool hasfather[N];
int f[N][2];
int happy[N];

void add(int a, int b)
{
    e[idx] = b;
    ne[idx] = h[a];
    h[a] = idx++;
}

void dfs(int u)
{
    f[u][1] = happy[u]; // 先把满意度存入
    for (int i = h[u]; ~i; i = ne[i])
    {
        int s = e[i];
        dfs(s);
        f[u][0] += max(f[s][1], f[s][0]);
        f[u][1] += f[s][0]; // 状态转移方程
    }
}

signed main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int n;
    cin >> n;
    for (int i = 1; i <= n; i++) // 注意下标
        cin >> happy[i];

    memset(h, -1, sizeof h); // 初始化邻接表

    int a, b;
    for (int i = 0; i < n - 1; i++)
    {
        cin >> a >> b;
        add(b, a);
        hasfather[a] = true; // 标记有父节点
    }

    int root = 1;
    while (hasfather[root])
        root++;                          // 找根节点
    dfs(root);                           // 从根节点遍历
    cout << max(f[root][1], f[root][0]); // 取根节点最大值
}
```



# 记忆化搜索

![29a737ce0a99c2386be4b528eb43b7eb](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvault29a737ce0a99c2386be4b528eb43b7eb.jpg)

```cpp
#include <bits/stdc++.h>
using namespace std;
#define endl '\n'
#define int long long

const int N = 310;
int h[N][N]; // 高度
int f[N][N];
int n, m;

int dx[4] = {-1, 0, 1, 0}, dy[4] = {0, 1, 0, -1};//四种方向

int dp(int x, int y)
{
    int &v = f[x][y];//cpp特性，v相当于f[x][y]
    if (v != -1)
        return v;//无需重复递归
    v = 1;//初始化当前位置
    for (int i = 0; i < 4; i++)
    {
        int a = x + dx[i], b = y + dy[i];
        if (a >= 0 && a <= n - 1 && b >= 0 && b <= m - 1 && h[a][b] < h[x][y])
            v = max(v, dp(a, b) + 1);
    }
    return v;
}

signed main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    cin >> n >> m;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++)
            cin >> h[i][j];

    memset(f, -1, sizeof f);//初始化f为-1

    int res = 0;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++)
            res = max(res, dp(i, j));
    cout << res;
}
```

