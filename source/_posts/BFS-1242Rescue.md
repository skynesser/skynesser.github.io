---
title: BFS--1242Rescue
date: 2022-04-14 13:05:30
tags:
categories:
mathjax: true
---
# 1242 Rescue
![请添加图片描述](https://img-blog.csdnimg.cn/c659dee2a5724e41ba5827bd801461e5.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAdGltZXJfY2F0Y2g=,size_20,color_FFFFFF,t_70,g_se,x_16)


**题意：**
>![在这里插入图片描述](https://img-blog.csdnimg.cn/a33afbf4c5f14c9495630f837b252adc.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAdGltZXJfY2F0Y2g=,size_20,color_FFFFFF,t_70,g_se,x_16)
解释如下：
>>${\color{red}a：终点}$
>${\color{red}r：起点}$
>${\color{red}.:路}$
>${\color{red}\#：障碍}$
>${\color{red}x:敌人(需要花一个单位时间打败)}$
>
>输出从起点到终点的最小步数，如果不存在路径，输出"Poor ANGEL has to stay in the prison all his life."。

**思路：**
>我们在拓展时，如果一个点是敌人，则会导致我们需要花2步才能走到这个点，这将导致 BFS 每次出队的不一定是队列中步数最小的点，所以我们要用一个优先队列代替队列，使得每次出队的都是最小步数的点这一性质。

**特别的，关于重载：**

```cpp
struct Node{
    int x,y,step;
    bool operator<(const Node &a)const
    {
        return a.step < step;
    }
};
```

**AC代码：**
![在这里插入图片描述](https://img-blog.csdnimg.cn/b04cdc2d511043abb8ab9210363a44ec.png)

```cpp
#include<bits/stdc++.h>

typedef long long ll;

const int N = 2e2+10,M = 2e4+10,INF = 0x3f3f3f3f,mod = 1e9+7;
struct Node{
    int x,y,step;
    bool operator<(const Node &a)const
    {
        return a.step < step;
    }
};

char a[N][N];
int n,m,start_x,start_y,end_x,end_y;
int ne[4][2] = {0,1,1,0,0,-1,-1,0};
bool book[N][N];

bool OK(int x,int y)
{
    if(x<1||y<1||x>n||y>m||book[x][y]||a[x][y]=='#')return false;
    return true;
}

void bfs()
{
    memset(book,false,sizeof book);
    std::priority_queue<Node> que;
    que.push({start_x,start_y,0});
    book[start_x][start_y] = true;
    while(!que.empty())
    {
        auto temp = que.top();
        que.pop();
        if(temp.x == end_x && temp.y == end_y)
        {
            std::cout<<temp.step<<'\n';
            return;
        }
        for(int i = 0 ; i < 4 ; i++)
        {
            int tx = temp.x + ne[i][0];
            int ty = temp.y + ne[i][1];
            if(!OK(tx,ty))continue;
            if(a[tx][ty]=='x')book[tx][ty] = true,que.push({tx,ty,temp.step+2});
            else book[tx][ty] = true,que.push({tx,ty,temp.step+1});
        }
    }
    std::cout<<"Poor ANGEL has to stay in the prison all his life.\n";
}

int main()
{
//    std::ios::sync_with_stdio(false);
//    std::cin.tie(nullptr);
//    std::cout.tie(nullptr);
    while(std::cin>>n>>m)
    {
        for(int i = 1 ; i <= n ; i++)std::cin>>(a[i]+1);
        for(int i = 1 ; i <= n ; i++)
            for(int j = 1 ; j <= m ; j++)
                if(a[i][j]=='r')start_x = i,start_y = j;
                else if(a[i][j]=='a')end_x = i,end_y = j;
        bfs();
    }
    return 0;
}

```
