﻿---
title: POJ 1183 反正切函数的应用
date: 2014-08-12 01:01:00
categories: Exercise
toc: true
---
# 题目
源地址：

http://poj.org/problem?id=1183

# 理解
题目不难，但是被数据类型坑了= =。
int不够，long long超时，使用unsigned int过了= =，感谢大神，坑了这么久。。

<!-- more -->

# 代码

```
#include <iostream>
#include <cstdio>
using namespace std;

int main(int argc, char const *argv[])
{
    unsigned int m, n, a, sum;
    while (scanf("%d", &a) != EOF)
    {
        for (m = a; ; m++)
            if ((a * a + 1) % m == 0)
                break;
        n = (a * a + 1) / m;
        sum = 2 * a + m + n;
        printf("%d\n", sum);
    }
    return 0;
}

```

# 更新日志
- 2014年08月12日 已AC。