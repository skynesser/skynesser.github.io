---
title: BFS--胜利大逃亡
date: 2022-04-14 13:05:43
tags:
categories:
mathjax: true
---
# 1253 胜利大逃亡
![请添加图片描述](https://img-blog.csdnimg.cn/dfb5b15bff5b492fb05704943cadf5bc.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAdGltZXJfY2F0Y2g=,size_20,color_FFFFFF,t_70,g_se,x_16)


**题意：**
>![在这里插入图片描述](https://img-blog.csdnimg.cn/1b6d3cc0126c42f99b10473c9635e587.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAdGltZXJfY2F0Y2g=,size_20,color_FFFFFF,t_70,g_se,x_16)

**思路：**
>将BFS原来二维的部分改成三维，其余部分均不变即可。
>注：
>>用cin读入要关流，否则会超时

**读入优化代码：**

```cpp
std::ios::sync_with_stdio(false);
std::cin.tie(nullptr);
std::cout.tie(nullptr);
```

**AC代码：**
![在这里插入图片描述](https://img-blog.csdnimg.cn/028f507c25f14c60ae61e66c890beeb2.png)

```cpp
#include<bits/stdc++.h>

typedef long long ll;

const int N = 60,M = 2e4+10,INF = 0x3f3f3f3f,mod = 1e9+7;
struct Node{
    int x,y,z,step;
}que[N*N*N];

int a,b,c,t;
bool g[N][N][N],book[N][N][N];
int ne[6][3] = {{1,0,0},{-1,0,0},{0,1,0},{0,-1,0},{0,0,1},{0,0,-1}};

bool OK(int x,int y,int z)
{
    if(x<1||y<1||z<1||x>a||y>b||z>c||book[x][y][z]||g[x][y][z])return false;
    return true;
}

void bfs()
{
    int tail = -1,head = 0;
    que[++tail] = {1,1,1};
    book[1][1][1] = true;
    while(tail >= head)
    {
        auto temp = que[head++];
        if(temp.x == a && temp.y == b && temp.z == c)
        {
            std::cout<<temp.step<<'\n';
            return;
        }
        if(temp.step>t)continue;
        for(int i = 0 ; i < 6 ; i++)
        {
            int tx = temp.x + ne[i][0];
            int ty = temp.y + ne[i][1];
            int tz = temp.z + ne[i][2];
            if(!OK(tx,ty,tz))continue;
            book[tx][ty][tz] = true;
            que[++tail] = {tx,ty,tz,temp.step+1};
        }
    }
    std::cout<<-1<<'\n';
}

int main()
{
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);
    std::cout.tie(nullptr);
    int T;
    std::cin>>T;
    while(T--)
    {
        std::cin>>a>>b>>c>>t;
        for(int i = 1 ; i <= a ; i++)
            for(int j = 1 ; j <= b ; j++)
                for(int k = 1 ; k <= c ; k++)std::cin>>g[i][j][k],book[i][j][k] = false;
        bfs();
    }
}
```
