#博弈论 #sg函数 #胜负dp

# 集合-Nim游戏

https://www.acwing.com/problem/content/895/

```cpp
#include <bits/stdc++.h>
using namespace std;
#define endl '\n'
#define int long long

const int N = 110, M = 10010;
int s[N], f[M];
int n, m;

int sg(int x)
{
    if (f[x] != -1)
        return f[x];

    unordered_set<int> S;
    for (int i = 0; i < m; i++)
    {
        if (x >= s[i])
            S.insert(sg(x - s[i]));
    }
    for (int i = 0;; i++)
        if (!S.count(i))
            return f[x] = i;
}
signed main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    memset(f, -1, sizeof f);
    cin >> m;
    for (int i = 0; i < m; i++)
        cin >> s[i];
    cin >> n;
    int res = 0;
    while (n--)
    {
        int x;
        cin >> x;
        res ^= sg(x);
    }
    if (res)
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
}
```



# Nim游戏

https://www.acwing.com/problem/content/893/

```cpp
#include <bits/stdc++.h>
using namespace std;
#define endl '\n'
#define int long long

signed main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int n;
    cin >> n;
    int res = 0;
    while (n--)
    {
        int x;
        cin >> x;
        res ^= x;//f[x]=x
    }
    if (res)
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
}
```

# [USACO09OPEN] Cow Digit Game S

https://www.luogu.com.cn/problem/P2953

sg函数

```cpp
#include <bits/stdc++.h>
using namespace std;
#define endl '\n'
#define int long long

const int N = 110, M = 10010;
int s[N], f[M];
int n, m;

int sg(int x)
{
    if (f[x] != -1)
        return f[x];

    unordered_set<int> S;
    for (int i = 0; i < m; i++)
    {
        if (x >= s[i])
            S.insert(sg(x - s[i]));
    }
    for (int i = 0;; i++)
        if (!S.count(i))
            return f[x] = i;
}
signed main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    memset(f, -1, sizeof f);
    cin >> m;
    for (int i = 0; i < m; i++)
        cin >> s[i];
    cin >> n;
    int res = 0;
    while (n--)
    {
        int x;
        cin >> x;
        res ^= sg(x);
    }
    if (res)
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
}
```

胜负dp

```cpp
#include <bits/stdc++.h>
using namespace std;
#define endl '\n'
#define int long long
const int N = 110, M = 1000010;
int n;
bool dp[M];

signed main()
{
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    dp[0] = false;
    for (int x = 1; x <= 1000000; x++)
    {
        int xx = x;
        int max = 0, min = 10e9;
        while (xx)
        {
            int tmp = xx % 10;
            if (tmp > max)
                max = tmp;
            if (tmp < min && tmp != 0)
                min = tmp;
            xx /= 10;
        }
        if (!dp[x - max] || !dp[x - min])
            dp[x] = true;
        else
            dp[x] = false;
    }

    int t;
    cin >> t;
    while (t--)
    {
        cin >> n;
        if (dp[n])
            cout << "YES" << endl;
        else
            cout << "NO" << endl;
    }
}
```

