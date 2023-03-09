# Day21——递归实现排列数据

把 1∼*n* 这 *n*

 个整数排成一行后随机打乱顺序，输出所有可能的次序。

**输入格式**

一个整数 *n*。

**输出格式**

按照从小到大的顺序输出所有方案，每行 1

 个。 

首先，同一行相邻两个数用一个空格隔开。

其次，对于两个不同的行，对应下标的数一一比较，字典序较小的排在前面。

**数据范围**

1≤*n*≤9

```c++
#include<iostream>
#include<cstdio>
#include<algorithm>
#include<string>

using namespace std;

//利用长度为n的数组，实现深度优先搜索dfs
const int N = 10;//下标为10是第九个位置

int n;
int states[N];//存放当前状态，0表示还没放数，1~n表示放了哪个数
bool used[N];//每个数有没有被用过,true表示被用过，false表示还没被用过

void dfs(int u)
{
    if(u > n)//边界————位置都已经填完
    {
        for(int i = 1; i <= n; i++)  printf("%d ", states[i]);
        puts("");//输出空但是自带换行
        return;
    }
    //依次枚举每个分支,即当前位置可以填哪些数
    for(int i = 1; i <= n; i++ )
    {
        if(!used[i])//当前位置未被使用过
        {
            states[u] =  i;
            used[i] = true;
            dfs(u + 1);
            
            //恢复现场
            states[u] = 0;
            used[i] = false;
        }
    }
}

int main()
{
    scanf("%d", &n);
    
    dfs(1);
    
    return 0;
}
```

