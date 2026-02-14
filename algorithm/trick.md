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

