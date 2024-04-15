---
layout: post
title: 2020 Multi-University Training Contest 2 Total Eclipse
subtitle: 1001.Total Eclipse
header-img: img/in-post/2020-07-27/header.jpg
header-style: text
catalog: true
tags:
  - 并查集
---

## 1001.Total Eclipse
[题目链接-1001.Total Eclipse](http://acm.hdu.edu.cn/showproblem.php?pid=6763)
![image](https://github.com/Fiveneves/Fiveneves.github.io/assets/75442734/d18a7f7f-c5e9-47b8-bd01-4d30d44c29b3)
![image](https://github.com/Fiveneves/Fiveneves.github.io/assets/75442734/83651933-3809-41ed-a83b-077ad3d7d8be)

**题目大意**

$n$个点$m$条边的无向图，每个点有一个正点权，每次选择一个连通子图，将里面的权值都减$1$，求所有点权为$0$的最小操作次数

**解题思路**

$贪心+并查集$
 - 常规思路就是每次选择一个最大的连通块，将里面的数同时减小，知道最小值变为$0$，然后将变成零的点删除，再分裂多个联通块继续执行上述操作
 - 但是这样操作明显会超时，那么我们就可以把操作顺序倒过来，用并查集反向处理连通块，先把大的点权值减成和小的点相同，然后一起删去即可
 - 我们可以按照点的权值大小从大到小进行排序，然后首先加入最大的点，连通块数量$+1$，查询它所连的点是否被加入了，如果加入了，那么就查询一下两个点祖先是否相同，如果不相同，就合并，连通块数量$-1$
 - 每次贡献为连通块的数量与该点的权值和下一个点的权值差的成绩，即是`tmp*(b[p[i-1]]-b[p[i]])`
 - 具体操作见代码

**附上代码**

```cpp
#pragma GCC optimize("-Ofast","-funroll-all-loops")
#include<bits/stdc++.h>
#define lowbit(x) (x &(-x))
using namespace std;
const int INF=0x3f3f3f3f;
const int dir[4][2]={-1,0,1,0,0,-1,0,1};
const double PI=acos(-1.0);
const double eps=1e-10;
const int mod=1e9+7;
const int N=1e5+10;
typedef long long ll;
typedef pair<int,int> PII;
typedef unsigned long long ull;
inline void read(int &x){
    char t=getchar();
    while(!isdigit(t)) t=getchar();
    for(x=t^48,t=getchar();isdigit(t);t=getchar()) x=x*10+(t^48);
}
vector<int> e[N];
int b[N],f[N],p[N],vis[N];
int Find(int x){
    return f[x]==x?x:f[x]=Find(f[x]);
}
bool cmp(int x,int y){
    return b[x]>b[y];
}
int main(){
    
    int t;
    read(t);
    while(t--){
        int n,m;
        read(n);read(m);
        for(int i=1;i<=n;i++){
            vis[i]=0;
            f[i]=p[i]=i;
            e[i].clear();
            read(b[i]);
        }
        while(m--){
            int u,v;
            read(u);read(v);
            e[u].push_back(v);
            e[v].push_back(u);
        }
        ll ans=0,tmp=1;
        sort(p+1,p+n+1,cmp);
        vis[p[1]]=1;//将当前最大的点加入图
        for(int i=2;i<=n;i++){
            ans+=tmp*(b[p[i-1]]-b[p[i]]);
            tmp++;//连通块数量+1
            for(int j=0;j<e[p[i]].size();j++){//遍历该点的边
                int u=p[i],v=e[p[i]][j];
                if(vis[v]){
                    u=Find(u);
                    v=Find(v);
                    if(u!=v){//每与一个不同的集合合并，连通块数-1
                        f[u]=v;
                        tmp--;
                    }
                }
            }
            vis[p[i]]=1;//标记(删除)该点
        }
        ans+=tmp*b[p[n]];
        printf("%lld\n",ans);
    }  
```
