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

```

