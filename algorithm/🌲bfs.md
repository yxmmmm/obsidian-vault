#图论 #bfs

典题

https://www.acwing.com/problem/content/849/

图中点的层次

```cpp
#include <bits/stdc++.h>
using namespace std;

const int N = 1e6 + 10;
int n, m;
int h[N], e[N], ne[N], idx;
int d[N], q[N];

// 建边传统艺能
void add(int a, int b)
{
    e[idx] = b;
    ne[idx] = h[a];
    h[a] = idx++;
}

int bfs()
{
    memset(d, -1, sizeof d);//初始化长度数组

    int hh = 0, tt = 0;
    d[1] = 0, q[0] = 1;//存入第一个点

    while (hh <= tt)//判断结束条件
    {
        int t = q[hh++];//弹出队头
        for (int i = h[t]; i != -1; i = ne[i])
        {
            int j = e[i];
            if (d[j] == -1)//每一个点的长度只会记录一次因此必然是最短路径
            {
                d[j] = d[t] + 1;//更新邻居的长度
                q[++tt] = j;//邻居入队
            }
        }
    }
    return d[n];
}

signed main()
{
    cin >> n >> m;
    memset(h, -1, sizeof(h));
    for (int i = 0; i < m; i++)
    {
        int a, b;
        cin >> a >> b;
        add(a, b);
    }
    cout << bfs() << endl;
}
```

应用

拓扑排序

https://www.acwing.com/problem/content/850/

![算法-40](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvault%E7%AE%97%E6%B3%95-40.jpg)

![算法-41](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvault%E7%AE%97%E6%B3%95-41.jpg)

```cpp
#include <bits/stdc++.h>
using namespace std;
const int N = 1e6 + 10;
int h[N], e[N], ne[N];
int idx;
int q[N], d[N];
int n, m;
void add(int a, int b)
{
    e[idx] = b;
    ne[idx] = h[a];
    h[a] = idx++;
}

bool topsort()
{
    int hh = 0, tt = -1;
    for (int i = 1; i <= n; i++)
        if (!d[i])
            q[++tt] = i; // 讲初始0入度点入队

    while (hh <= tt)
    {
        int t = q[hh++];
        for (int i = h[t]; i != -1; i = ne[i])
        {
            int j = e[i];
            d[j]--;        // 去边
            if (d[j] == 0) // 判断j是否0入度
                q[++tt] = j;
        }
    }
    return tt == n - 1; // 若是有向无环图，则tt==n-1
}

int main()
{
    cin >> n >> m;
    memset(h, -1, sizeof h);
    for (int i = 0; i < m; i++)
    {
        int a, b;
        cin >> a >> b;
        add(a, b), d[b]++; // 更新边数
    }

    if (topsort())
    {
        for (int i = 0; i < n; i++)
            printf("%d ", q[i]); // q数组即为所求拓扑序列
    }
    else
    {
        printf("-1");
    }
}
```

