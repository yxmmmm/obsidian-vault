#KMP #算法 #数据结构

# 问题

**给定一个文本 𝑡 和一个字符串 𝑠，我们尝试找到并展示 𝑠 在 𝑡 中的所有出现（occurrence)．**

# 原理及方法

![算法-27](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvault%E7%AE%97%E6%B3%95-27.jpg)

![算法-28 2](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvault%E7%AE%97%E6%B3%95-28%202.jpg)

![算法-29 2](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvault%E7%AE%97%E6%B3%95-29%202.jpg)

# 代码实现

```cpp
// s[]是长文本，p[]是模式串，n是s的长度，m是p的长度
求模式串的next数组：
for (int i = 2, j = 0; i <= m; i ++ )
{
    while (j && p[i] != p[j + 1]) j = ne[j];
    if (p[i] == p[j + 1]) j ++ ;
    ne[i] = j;
}

// 匹配
for (int i = 1, j = 0; i <= n; i ++ )
{
    while (j && s[i] != p[j + 1]) j = ne[j];
    if (s[i] == p[j + 1]) j ++ ;
    if (j == m)
    {
        j = ne[j];
        // 匹配成功后的逻辑
    }
}
```

**不难看出，求next数组和匹配的逻辑是一样的因此只要理解其逻辑就能快速写出板子**