#搜索 #算法 #dfs

例题**n-皇后**

```cpp
//第一种，以行为搜索单位
#include <iostream>
using namespace std;
const int N = 20;
char g[N][N];
bool col[N], dg[N], udg[N];
int n;
void dfs(int u)
{
    if (u == n)
    {
        for (int i = 0; i < n; i++)
            puts(g[i]);//以列为单位输出
        puts("");//换行
        return;//跳出单个进程会退上一进程
    }
    for (int i = 0; i < n; i++)
    {
        if (!col[i] && !dg[u + i] && !udg[n - u + i])//列，两条对角线
        {
            col[i] = dg[u + i] = udg[n - u + i] = true;//占领
            g[u][i] = 'Q';//先占着再说😎
            dfs(u + 1);
            col[i] = dg[u + i] = udg[n - u + i] = false;//回溯
            g[u][i] = '.';
        }
    }
}
int main()
{
    cin >> n;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            g[i][j] = '.';
    dfs(0);
}

//第二种，以格子为单位
#include <iostream>
using namespace std;
const int N = 20;
char g[N][N];
bool rol[N], col[N], dg[N], udg[N];
int n, x, y, s;
void dfs(int x, int y, int s)
{
    if (y == n)
        y = 0, x++;//越界换行
    if (x == n)
    {
        if (s == n)
        {
            for (int i = 0; i < n; i++)
                puts(g[i]);
            puts("");
        }
        return;//返回上一循环
    }
    dfs(x, y + 1, s);
    if (!rol[y] && !col[x] && !dg[x + y] && !udg[n - x + y])
    {
        g[x][y] = 'Q';
        rol[y] = col[x] = dg[x + y] = udg[n - x + y] = true;
        dfs(x, y + 1, s + 1);//同行下一列
        rol[y] = col[x] = dg[x + y] = udg[n - x + y] = false;
        g[x][y] = '.';
    }
}
int main()
{
    cin >> n;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            g[i][j] = '.';
    dfs(0, 0, 0);
}
```

**显然第一种时间复杂度更低**
