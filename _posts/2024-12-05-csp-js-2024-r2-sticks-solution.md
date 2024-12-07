---
layout: post
title: CSP-J/S 2024 第二轮 入门级 小木棍 题解
date: 2024-12-06 20:44 +0800
last_modified_at: 2024-12-05 20:44:00 +0800
tags: [cpp, csp-j, solution, greedy]
toc: true
---

# CSP-J/S 2024 第二轮 入门级 小木棍 题解

> 题目来源：[ET题库 - 小木棍](https://eternity-sky.github.io/OI/problem.html?id=34)

## 题目分析

这是一道关于数字构造的题目。主要需要考虑：
1. 每个数字需要的木棍数量不同
2. 不能有前导零
3. 要求构造出最小的数字

## 解题思路

1. 首先统计每个数字(0-9)需要的木棍数量
2. 对于给定的n根木棍，我们需要：
   - 判断是否能构造出合法数字
   - 如果可以，找出最小的合法数字

## 代码实现

```cpp
#include <bits/stdc++.h>
using namespace std;

// 每个数字需要的木棍数量
const int sticks[] = {6, 2, 5, 5, 4, 5, 6, 3, 7, 6};  // 0-9分别需要的木棍数

// 判断能否用n根木棍构造出长度为len的数字
bool can_construct(int n, int len) {
    if (len == 1) return n == sticks[1] || n == sticks[7] || n == sticks[4];
    return n >= 2;  // 长度大于1时，总能构造出某个数字
}

// 构造最小的数字
string construct_min(int n) {
    // 特判无法构造的情况
    if (n < 2) return "-1";
    
    string result;
    
    // 处理第一位（不能为0）
    for (int i = 1; i <= 9; i++) {
        if (sticks[i] <= n) {
            result += ('0' + i);
            n -= sticks[i];
            break;
        }
    }
    
    // 如果还有剩余木棍，尽量构造最小的数字
    while (n > 0) {
        bool found = false;
        for (int i = 0; i <= 9; i++) {
            if (sticks[i] <= n) {
                result += ('0' + i);
                n -= sticks[i];
                found = true;
                break;
            }
        }
        if (!found) break;
    }
    
    return n == 0 ? result : "-1";
}

int main() {
    freopen("sticks.in", "r", stdin);
    freopen("sticks.out", "w", stdout);
    
    int T;
    cin >> T;
    while (T--) {
        int n;
        cin >> n;
        cout << construct_min(n) << endl;
    }
    
    return 0;
}
```

## 代码解释

### 1. 预处理数据
```cpp
const int sticks[] = {6, 2, 5, 5, 4, 5, 6, 3, 7, 6};
```
存储每个数字需要的木棍数量。

### 2. 构造最小数字
```cpp
string construct_min(int n) {
    // 处理第一位（不能为0）
    for (int i = 1; i <= 9; i++) {
        if (sticks[i] <= n) {
            result += ('0' + i);
            n -= sticks[i];
            break;
        }
    }
    // ...
}
```
- 先处理第一位，必须是非零数字
- 然后贪心地选择剩余位数

## 关键点分析

1. **贪心策略**：
   - 第一位选择需要最少木棍的非零数字
   - 后续位置选择需要最少木棍的数字（可以是0）

2. **特殊情况处理**：
   - n < 2 的情况无法构造
   - 需要考虑木棍数量不足的情况

## 时间复杂度分析

- 对于每组测试数据：O(n)
- 总时间复杂度：O(T * n)，其中T是测试数据组数

## 注意事项

1. 文件输入输出
```cpp
freopen("sticks.in", "r", stdin);
freopen("sticks.out", "w", stdout);
```

2. 边界条件
- 考虑无法构造的情况
- 注意前导零的处理

## 总结

这道题的关键在于：
1. 正确统计每个数字需要的木棍数量
2. 使用贪心策略构造最小数字
3. 注意处理特殊情况

希望这个题解对你有帮助！如果有任何问题，欢迎在评论区讨论。

--- 