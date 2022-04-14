---
title: BFS--1072 Nightmare
date: 2022-04-14 13:04:12
tags:
categories:
mathjax: true
---

# 1072 Nightmare
![请添加图片描述](https://img-blog.csdnimg.cn/a8105d4852674985a7c8eca5a82638f0.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAdGltZXJfY2F0Y2g=,size_20,color_FFFFFF,t_70,g_se,x_16)


**题意：**
>小明被困在一个迷宫如下中：
>1.小明每次可以花一个单位时间往上下左右的某个方向移动一格。
>2.小明身上有一个炸弹，在第6个单位时间就会爆炸，在第6个单位时间走到终点或者刷新炸弹时间是无效的。
>>举例如下：
>2 1 1 0 1 1 1 0
1 0 4 1 1 0 4 1
1 0 0 0 0 0 0 1
1 1 1 4 1 1 1 3
>>${\color{red}0.障碍}$
>${\color{red}1.平路}$
>${\color{red}2.起点}$
>${\color{red}3.终点}$
>${\color{red}4.可以刷新炸弹时间}$


**思路：**
>只需要在bfs的基础上修改标记数组即可：
>>bfs为了避免重复搜索，一般将某个坐标定义为一个状态：
>一般的，如果我们搜索过$(x,y)$，我们下次再次搜索到这个点时将不会把这个点再次加入队列中。
>
>但是这题中，我们的状态应该多加一个走到该点时的炸弹时间：
>>即我们认为$(x,y,0)(当前炸弹在第0个单位时间)$，$(x,y,1)(当前炸弹在第1个单位时间)$等是不同的状态，所以我们在炸弹时间不同的情况下，一个点可能可以重复入队。
>
>不妨举一个显然的例子：
>2 1 1 1 4
1 0 0 0 1  
1 0 4 1 1
1 0 1 0 0
1 1 1 1 3

标记数组处理如下：

```cpp
bool book[N][N]->bool book[N][N][7]
```

**时间复杂度:**
>$O(n*m)$

**AC代码：**
![在这里插入图片描述](https://img-blog.csdnimg.cn/31f685c131b4472fa6272917ee66fd04.png)

```cpp
#include<bits/stdc++.h>

typedef long long ll;

const int N = 20,M = 2e4+10,INF = 0x3f3f3f3f,mod = 1e9+7;
struct Node{
    int x,y,step,time;
}que[N*N*6];
int g[N][N];
int ne[4][2] = {0,1,1,0,-1,0,0,-1};
bool book[N][N][7];
int n,m,start_x,start_y,end_x,end_y;

bool OK(int x,int y,int t)
{
    if(x<1||y<1||x>n||y>m||g[x][y]==0||book[x][y][t])return false;
    return true;
}

int bfs()
{
    int tail = -1,head = 0;
    que[++tail] = {start_x,start_y,0,0};
    book[start_x][start_y][0] = true;
    while(tail>=head)
    {
        auto temp = que[head++];
        if(temp.x==end_x&&temp.y==end_y)return temp.step;
        if(temp.time==5)continue;//炸弹时间在5其实已经无法拓展
        for(int i = 0 ; i < 4 ; i++)
        {
            int tx = ne[i][0] + temp.x;
            int ty = ne[i][1] + temp.y;
            if(g[tx][ty]==4)
            {
                if(OK(tx,ty,0))
                    que[++tail] = {tx,ty,temp.step+1,0},book[tx][ty][0] = true;
            }
            else
            {
                if(OK(tx,ty,temp.time+1))
                    que[++tail] = {tx,ty,temp.step+1,temp.time+1},book[tx][ty][temp.time+1] = true;
            }
        }
    }
    return -1;
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
        memset(book,false,sizeof book);
        std::cin>>n>>m;
        for(int i = 1 ; i <= n ; i++)
        {
            for(int j = 1 ; j <= m ; j++)
            {
                std::cin>>g[i][j];
                if(g[i][j]==2)
                {
                    start_x = i,start_y = j;
                }
                else if(g[i][j]==3)
                {
                    end_x = i,end_y = j;
                }
            }
        }
        std::cout<<bfs()<<'\n';
    }
    return 0;
}




```
