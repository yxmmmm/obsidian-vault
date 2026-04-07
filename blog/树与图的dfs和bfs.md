#blog #图论

## 树与图的dfs

### [树的重心](https://www.acwing.com/activity/content/problem/content/909/)

![img](https://pic-out.zhimg.com/v2-fc12df120736bd3ed68bad2ae0d20a9d~resize:1440:q75.jpg?animatedImageAutoPlay=false&animatedImagePlayCount=1&auth_key=1775571479-0-0-99a3f0edd751f2fcbcd12c4b63c53b4d&bizSceneCode=article_draft&expiration=1775571479&incremental=false&mid=18e0d87e3931e3e37d85f63de498200e&overTime=60&precoder=false&protocol=v2&retryCount=3&sampling=false&sceneCode=editor_copy_outbound&source=bfcaadb1)

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

## 树与图的bfs

### [图中点的层次](https://www.acwing.com/problem/content/849/)

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

### 应用

[拓扑排序](https://www.acwing.com/problem/content/850/)

![img](https://pic-out.zhimg.com/v2-cdfc984cf3fbec2d2f17508d069ba87a~resize:1440:q75.jpg?animatedImageAutoPlay=false&animatedImagePlayCount=1&auth_key=1775571479-0-0-b1977369cd0a4d04b4be328dec3476f4&bizSceneCode=article_draft&expiration=1775571479&incremental=false&mid=18e0d87e3931e3e37d85f63de498200e&overTime=60&precoder=false&protocol=v2&retryCount=3&sampling=false&sceneCode=editor_copy_outbound&source=bfcaadb1)



![img](https://pic-out.zhimg.com/v2-cc7a8cd92cfc50d9f6d86ddf85605d30~resize:1440:q75.jpg?animatedImageAutoPlay=false&animatedImagePlayCount=1&auth_key=1775571479-0-0-fe893798083a2ccb3e86e862221a9047&bizSceneCode=article_draft&expiration=1775571479&incremental=false&mid=18e0d87e3931e3e37d85f63de498200e&overTime=60&precoder=false&protocol=v2&retryCount=3&sampling=false&sceneCode=editor_copy_outbound&source=bfcaadb1)

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

## 遇到的问题

- Q：为何dfs是无向图bfs是有向图
- A：dfs的核心是回溯在走到头后需要不断回退，而且树的重心中没有讲父结点指向儿子结点所以用双向边；而bfs以层为单位，不存在回退，因此单向边够用。



- Q：拓扑排序中，如果一开始就把好几个点都扔进队列，那它们的顺序不是乱的吗
- A：拓扑排序的顺序不是单一的，只需要前面元素位置比后面元素靠前即可，判定问题交给special judge就好啦🤣