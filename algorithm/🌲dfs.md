#图论 #dfs

https://www.acwing.com/activity/content/problem/content/909/

🌲的重心![IMG_B9CA68D0872D-1](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvaultIMG_B9CA68D0872D-1.jpeg)

```cpp
#include <bits/stdc++.h>
using namespace std;
const int N = 10010, M = 2 * N;
int h[N], e[M], ne[M], idx; // 含义见数组模拟链表辨析
bool st[N];                 // 记录是否走过
int ans = N;                // 初始化ans
int n, a, b;
void add(int a, int b)
{
    e[idx] = b;
    ne[idx] = h[a];
    h[a] = idx++;
}

int dfs(int u)
{
    st[u] = true;                          // 标记结点
    int res = 0, sum = 1;                  // sum初始化为自己
    for (int i = h[u]; i != -1; i = ne[i]) // 从目标元素头开始向所有分支深度遍历
    {
        int j = e[i]; // 取每一儿子结点值
        if (!st[j])   // 未标记则继续向下遍历，标记过则代表是父结点，无向图处理手法
        {
            int s = dfs(j);    // 得到的是该分支下的连通块大小
            res = max(res, s); // 更新到当前分支的最大连通块
            sum += s;          // 更新所在连通块
        }
    }
    res = max(res, n - sum); // 比较上面一坨连通块和子连通块大小
    ans = min(ans, res);     // 更新重心
    return sum;
}

signed main()
{
    cin >> n;
    memset(h, -1, sizeof(h));       // 初始化
    for (int i = 0; i < n - 1; i++) // 🌲无环则n个节点必然有n-1条边
    {
        cin >> a >> b;
        add(a, b), add(b, a); // 建立无向图
    }
    dfs(1); // 任意选取结点
    cout << ans << endl;
}
```

