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

