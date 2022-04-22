---
title: floyd-1217Arbitrage
mathjax: true
date: 2022-04-20 20:48:26
tags:
- floyd
categories:
- 题解
---

# floyd-1217Arbitrage
[PDF](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/floyd/%E9%A2%98%E8%A7%A3/floyd-1217Arbitrage.pdf)

## 题意
>![](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/floyd/%E9%A2%98%E8%A7%A3/KOOEC%7DXIJSYCB%24%5DSIL%7BK5T4.png)
给出$n$种货币，并给出$m$种兑换规则，是否存在某种兑换方式，可以赚得金额。

## 思路
>对于所有的货币，转换成点，对于两种货币之间的汇率，可以理解为路径的权值，使用floyd算法，若存在货币从自己到自己的汇率大于1，则可以赚的金额。

更新汇率代码：
```cpp
if(g[i][k]*g[k][j] > g[i][j])g[i][j] = g[i][k] * g[k][j];
```

## 时间复杂度：
>$O(n^3)$

## AC代码
![](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/floyd/%E9%A2%98%E8%A7%A3/S6%60%7D%2424%246W0_%5B%7EN_1%7D4%7BQXB.png)
```cpp
#include<bits/stdc++.h>

const int N = 40;

double g[N][N];

int main()
{
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);
    std::cout.tie(nullptr);
    int n;
    int T = 1;
    while(std::cin>>n)
    {
        if(n==0)break;
        std::map<std::string,int> mp;
        int idx = 0;
        for(int i = 1 ; i <= n ; i++)
        {
            std::string s;
            std::cin>>s;
            mp[s] = ++idx;
        }
        int m;
        std::cin>>m;
        for(int i = 1 ; i <= n ; i++)
            for(int j = 1 ; j <= n ; j++)
                if(i == j)g[i][j] = 1;
                else g[i][j] = 0;
        while(m--)
        {
            std::string a,b;
            double c;
            std::cin>>a>>c>>b;
            g[mp[a]][mp[b]] = c;
        }

        for(int k = 1 ; k <= n ; k++)
        {
            for(int i = 1 ; i <= n ; i++)
                for(int j = 1 ; j <= n ; j++)
                {
                    if(g[i][k]*g[k][j] > g[i][j])g[i][j] = g[i][k] * g[k][j];
                }
        }

        bool flag = false;
        for(int i = 1 ; i <= n ; i++)if(g[i][i] > 1){flag = true;break;}
        std::cout<<"Case "<<T++<<": ";
        if(flag)std::cout<<"Yes\n";
        else std::cout<<"No\n";
    }
    return 0;
}
```
