﻿---
title: POJ 1731 Orders
date: 2014-08-05 15:57:00
categories: Exercise
toc: true
---
# 题目
源地址：

http://poj.org/problem?id=1731

# 理解
全排列的简单运用

<!-- more -->

# 代码

```
#include <iostream>
#include <algorithm>
#include <string>
using namespace std;

int main(int argc, char const *argv[])
{
    string str;
    while (cin >> str)
    {

        sort(str.begin(), str.end());
        cout << str << endl;
        while (next_permutation(str.begin(), str.end()))
        {
            cout << str << endl;
        }
    }
    return 0;
}

```

# 更新日志
- 2014年08月05日 已AC。