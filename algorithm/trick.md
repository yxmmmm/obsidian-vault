#算法

# 通过字母遍历整个map

```c++
for(char ch='A';ch<='G';++ch)
    {
        if(mp[ch]>=m)continue;
        else sum+=m-mp[ch];
    }
```

通过ASCII码遍历map

[CodeForces-1980A](https://vjudge.net/problem/CodeForces-1980A)

# 输入特定字符串执行特定语句

```cpp
while (cin>>op)
    {
        if(op=="end")return;
        if(op=="insert")
        {
            cin>>m;
            s.push(m);
        }
        if(op=="extract"){
            cout<<s.top()<<endl;
            s.pop();
        }
    }
```

[Aizu-ALDS1_9_C](https://vjudge.net/problem/Aizu-ALDS1_9_C)



# 特别大的数($10^{60}$)判断奇偶

```cpp
		string s;
    cin>>s;
    if(s[s.size()-1]%2)cout<<"odd"<<endl;
    else cout<<"even"<<endl;
```

将大数存入字符串中，判断最后一个数的奇偶

[洛谷-P2955](https://vjudge.net/problem/洛谷-P2955)

# 负数取模

```cpp
int k=(x%N+N)%N;
```

负数取模为负数

# 无穷大

在算法竞赛中，我们常常需要用到设置一个常量用来代表“无穷大”。

比如对于int类型的数，有的人会采用INT_MAX，即0x7fffffff作为无穷大。但是以INT_MAX为无穷大常常面临一个问题，即加一个其他的数会溢出。

而这种情况在动态规划，或者其他一些递推的算法中常常出现，很有可能导致算法出问题。

所以在算法竞赛中，我们常采用0x3f3f3f3f来作为无穷大。0x3f3f3f3f主要有如下好处：

0x3f3f3f3f的十进制为1061109567，和INT_MAX一个数量级，即10^9数量级，而一般场合下的数据都是小于10^9的。
0x3f3f3f3f * 2 = 2122219134，无穷大相加依然不会溢出。
可以使用memset(array, 0x3f, sizeof(array))来为数组设初值为0x3f3f3f3f，因为这个数的每个字节都是0x3f。



# 通过空格分割一行的两部分

```cpp
string a, b;
getline(cin, a, ' ');  // 读到第一个空格为止，存入 a
getline(cin, b);       // 读剩余整行，存入 b
```

# 读取整行

```cpp
getline(cin, b);
```

# 边遍历边删除

注意后退一位

```cpp
for (int i = 0; a[i]; i++)
    {
        if (mp[a[i]] == true)
            {
                a.erase(i, 1);
                i--;
            }
    }
```

