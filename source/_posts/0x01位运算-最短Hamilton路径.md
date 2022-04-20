---
title: 0x01位运算--最短Hamilton路径
date: 2022-04-14 12:59:38
tags:
categories:
- 算法进阶指南笔记
mathjax: true
---
## 0x01位运算——最短Hamilton路径
![在这里插入图片描述](https://img-blog.csdnimg.cn/a12eeb73663147e1bb9661387c6a2134.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAdGltZXJfY2F0Y2g=,size_20,color_FFFFFF,t_70,g_se,x_16)
- 说明
>**本题的正解——状态压缩dp，我们将在0x56节详细介绍**
- 思路分析
	>我们可以使用一个**n维的bool数组**记录下某时刻经过了哪些点，未经过哪些点，而这里的**n维的bool数组**，可以用一个n位的二进制数代替。
	>在这个二进制数中，第i位为1则代表这个点已经被拜访过。
	
	>用$F[i,j]$表示当前经过了那些点(用 *i* 表示),现在在 *j* 点的最短距离。
	>状态转移方程(不做详解)：
	>$F[i,j] =min(F[i,j],F[i$^$(1\ll j),k]+weight[k,j])$
	
- 时间复杂度
>$O(n^{2}*2^{n})$
- 代码实现

```cpp
#include<bits/stdc++.h>

typedef long long ll;
typedef unsigned long long ull;

const int N = 20,M = N * N,INF = 0x3f3f3f3f,P = 998244353;

int f[1<<N][N];
int w[N][N];

int main()
{
    std::ios::sync_with_stdio(false);
    int n;
    std::cin>>n;
    for(int i = 0 ; i < n ; i++)
    {
        for(int j = 0 ; j < n ; j++)
        {
            std::cin>>w[i][j];
        }
    }
    memset(f,0x3f,sizeof f);
    f[1][0] = 0;
    for(int i = 1 ; i < 1 << n ; i++)
        for(int j = 0 ; j < n ; j++) if(i >> j & 1)
            for(int k = 0 ; k < n ; k++)if((i ^ 1 << j) >> k & 1)
                f[i][j] = std::min(f[i][j],f[i ^ 1 << j][k] + w[k][j]);
    std::cout<<f[(1<<n)-1][n-1];
    return 0;
}
```
- 题目：
[最短Hamilton路径](https://www.acwing.com/problem/content/93/)
