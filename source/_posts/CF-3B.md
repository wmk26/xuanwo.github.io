---
title: Codeforces Beta Round 3 B Lorry
date: 2014-11-7 10:18:47
categories: Exercise
toc: true
---
# 题目
源地址：

http://codeforces.com/problemset/problem/3/B

# 理解
读懂题略微花了一点时间，主要是生词多，有点吓人= =。有一辆卡车，要装载一些船只，有1和2两种。然后给出n个船的类型和容积，要求给定卡车体积v的情况下，装载的船的最大容积。
一开始的想法是理解成一个背包问题，但是给的v太大，用DP处理可能会超时。后来就用简单一点的思路，直接暴力贪心。把两种船分开，分别进行排序。小脑一动就能明白，最优解肯定是选取价值高的，然后枚举选择i只1船，则选择2船只的个数就是min((v - i) / 2, tc)*其中tc为2船总个数*。
输出上有一个trick，就是每个编号之间都有一个空格= =，因此WA一发。。

<!-- more -->

# 代码

```

#define MAXN 100000+10

int sum1[MAXN], sum2[MAXN], oc, tc, ans[MAXN];
int n, v, a, b, maxv, c1, c2;

struct node
{
    int id,val;
} one[MAXN], two[MAXN];

bool cmp(node x, node y)
{
    return x.val > y.val;
}

void init()
{
    scanf("%d%d", &n, &v);
    oc = tc = 0;
    for(int i=1; i<=n; i++)
    {
        scanf("%d%d", &a, &b);
        if(a == 1)
            one[++oc].val = b, one[oc].id = i;
        else
            two[++tc].val = b, two[tc].id = i;
    }
    sort(one+1, one + oc + 1, cmp);
    sort(two+1, two + tc + 1, cmp);
}


int main(int argc, char const *argv[])
{
    init();
    sum2[0] = sum1[0] = 0;
    for(int i=1; i<=tc; i++) sum2[i] = sum2[i - 1] + two[i].val;
    for(int i=1; i<=oc; i++) sum1[i] = sum1[i - 1] + one[i].val;
    c1 = -1, c2 = -1, maxv = -1;
    for(int i=0; i<=oc; i++)
    {
        if(i > v)
            break;
        int d = sum1[i] + sum2[min((v - i) / 2, tc)];
        if(d > maxv)
        {
            maxv = d;
            c1 = i;
            c2 = min((v - i) / 2, tc);
        }
    }
    if(maxv == -1)
    {
        printf("0\n");
        return 0;
    }
    int cnt = 0;
    printf("%d\n", maxv);
    for(int i=1; i<=c1; i++) ans[++cnt] = one[i].id;
    for(int i=1; i<=c2; i++) ans[++cnt] = two[i].id;
    for(int i=1; i<=cnt; i++)
        printf("%d%c", ans[i], i == cnt? '\n' : ' ');
    return 0;
}

/*
5 3
1 9
2 9
1 9
2 10
1 6

24
3 1 5
**/

```

# 更新日志
- 2014年11月7日 已AC。