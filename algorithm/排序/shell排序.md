#算法#排序

# 定义及意义

shell排序就是插入排序的优化，通过生成数列等距整理数列最后进行普通希尔排序实现大幅降低所需时间



# 代码实现

```cpp
int shellsort(A[],n,g)
{
  for(i=g;i<n-1;i++)
  {
    int v=A[i];
    int j=i-g;
    while(A[j]>v&&j>0)
    {
      A[j+g]=A[j];
      j-=g;
    }
    A[j+g]=v;
  }
}
```

