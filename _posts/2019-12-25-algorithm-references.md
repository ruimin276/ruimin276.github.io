---
layout: post
title: 常用算法模板
date: 2019-12-25
Author: Ruimin
categories: 
tags: [sample, markdown]
comments: false
---



# DFS

```c++
int n, e[100][100];
bool book[100];
void dfs(int u)
{
    for (int i = 1; i <= n; i++)
    {
        if (!book[i] && e[u][i])
        {
            book[i] = true;
            dfs(i);
        }
    }
    return;
}
int main()
{
    dfs(1);
}
```

# BFS

```c++
int s, k, a[200050][2], head, tail;
bool b[200050];
int main()
{
    cin >> s >> k;
    a[tail++][0]=s;
    while(a[head][0]!=k)
    {
        if(b[a[head][0]*2]==0)
        {
            a[tail][0]=a[head][0]*2;
            a[tail++][1]=a[head][1]+1;
            b[a[head][0]*2]=1;
        }
        if(b[a[head][0]+1]==0)
        {
            a[tail][0]=a[head][0]+1;
            a[tail++][1]=a[head][1]+1;
            b[a[head][0]+1]=1;
        }
        if(a[head][0]-1>=0&&b[a[head][0]-1]==0)
        {
            a[tail++][0]=a[head][0]-1;
            a[tail++][1]=a[head][1]+1;
            b[a[head][0]-1]=1;
        }
        head++;
    }
    cout<<a[head][1];
    return 0;
}
```




# Max Flow

```c++

void dfs(int u)
{
    if (book[u] == 1)
        return;
    book[u] = 1;
    top++;
    s[top] = u;
    if (u == n)
    {
        int minv = 999999999;
        for (int i = 1; i <= top - 1; i++)//找最大流
        {
            if (minv > e[s[i]][s[i + 1]])
                minv = e[s[i]][s[i + 1]];
        }
        if (minv != 999999999)
        {
            flag = 1;
            for (int i = 1; i <= top - 1; i++)//减去最大流，建反悔边
            {
                e[s[i]][s[i + 1]] -= minv;
                e[s[i + 1]][s[i]] += minv;
            }
            ans += minv;
        }
        top--;
        return;
    }
    for (int i = 1; i <= n; i++)
    {
        if (e[u][i] > 0)
        {
            dfs(i);
        }
    }
    top--;
    return;
}
while (flag)
{
    memset(book, 0, sizeof(book));
    flag = 0;
    dfs(1);
}

```

