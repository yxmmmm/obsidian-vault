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