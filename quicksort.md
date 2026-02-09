#排序#算法

# 定义及方法

![算法-2](https://tuchuang-1387570672.cos.ap-nanjing.myqcloud.com/obsidianvault%E7%AE%97%E6%B3%95-2.jpg)

# 代码实现

```cpp
#include<bits/stdc++.h>
using namespace std;
	const int N=1e6+10;
  int q[N];
	int n;
  
void quicksort(int q[],int l,int r)
{
  if(l>=r)return;
  
  int x=q[l],i=l-1,j=r+1;//当以j为分治界点时，x=q[l]||x=q[l+r>>1]
  while(i<j)
  {
    do i++;while(q[i]<x);
    do j--;while(q[j]>x);
    if(i<j)swap(q[i],q[j]);//停止后交换
  }
  
  quicksort(q,l,j);
  quicksort(q,j+1,r);//递归
}

int main(){
  scanf("%d",&n);
  for(int i=0;i<n;i++)scanf("%d",&q[i]);
  
  quicksort(q,0,n-1);
  for(int i=0;i<n;i++){
    printf("%d ",q[i]);
  }
}
```

