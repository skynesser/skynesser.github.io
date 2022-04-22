---
title: floyd
mathjax: true
date: 2022-04-20 20:46:55
tags:
- floyd
categories:
- 图论
---

# floyd
[PDF](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/floyd/%E7%AE%97%E6%B3%95%E8%A7%A3%E6%9E%90/floyd.pdf)

## floyd介绍
>一种基于动态规划的，可以求解任意两点最短距离的算法。

## floyd算法思想

>floyd的基于一种简单的想法，想要更新两个点之间的距离，必须借助于其它的点。
那么我们不妨令$dp[k][i][j]$表示借助前$k$个点$i$和$j$之间的最小距离(实际枚举过程中$k$这一维是没有必要的)。想要借助于某一个点更新的代码是简单的，比如能否借助点$k$缩小$i$之间$j$的距离，就可以这样写：
```cpp
if(dp[i][j] > dp[i][k] + dp[k][j])dp[i][j] = dp[i][k] + dp[k][j];
```
## floyd示例

>一个包含4个点的图
![](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/floyd/%E7%AE%97%E6%B3%95%E8%A7%A3%E6%9E%90/MH2%5BBBNA5%24%7B6A7%28LUQA%5DW%5B5.png)
>1. 初始化(用二维数组读入这个图)
$\begin{bmatrix}0&3&\infty&5
\\ 2&0&\infty&4
\\ \infty&1&0&\infty
\\ \infty&\infty&2&0 \end{bmatrix}
$
>1. 尝试用1号点更新所有的点
$\begin{bmatrix}0&3&\infty&5
\\ 2&0&\infty&4
\\ \infty&1&0&\infty
\\ \infty&\infty&2&0 \end{bmatrix}
$
但是1号点并没有可以更新的点
>3. 用2号点
$\begin{bmatrix}0&3&\infty&5
\\ 2&0&\infty&4
\\ 3&1&0&5
\\ \infty&\infty&2&0 \end{bmatrix}
$
$dp[3][1] > dp[3][2]+dp[2][1]$
$dp[3][4] > dp[3][2]+dp[2][4]$
>4. 用3号点更新
>$\begin{bmatrix}0&3&\infty&5
\\ 2&0&\infty&4
\\ 3&1&0&5
\\ 5&3&2&0 \end{bmatrix}
>$
>5. 用4号点更新
>$\begin{bmatrix}0&3&7&5
\\ 2&0&6&4
\\ 3&1&0&5
\\ 5&3&2&0 \end{bmatrix}
$

## floyd代码模板
```cpp
#include<bits/stdc++.h>

const int N = 1e2+10,INF = 0x3f3f3f3f;

int g[N][N];

int main()
{
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);
    std::cout.tie(nullptr);
    int n,m;
    std::cin>>n>>m;
    for(int i = 1 ; i <= n ; i++)
        for(int j = 1 ; j <= n ; j++)
            if(i == j)g[i][j] = 0;
            else g[i][j] = INF;
    while(m--)
    {
        int a,b,c;
        std::cin>>a>>b>>c;
        g[a][b] = c;
    }
    for(int k = 1 ; k <= n ; k++)
        for (int i = 1; i <= n; i++)
            for (int j = 1; j <= n; j++)
                if (g[i][j] > g[i][k] + g[k][j])g[i][j] = g[i][k] + g[k][j];
    return 0;
}
```

## 时间复杂度
>时间复杂度：$O(n^3)$

## floyd练习
>在博客中搜索即可找到练习和题解
