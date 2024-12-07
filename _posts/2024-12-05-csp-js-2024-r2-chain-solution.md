---
layout: post
title: CSP-J/S 2024 第二轮 入门级 接龙 题解
date: 2024-12-05 20:44 +0800
last_modified_at: 2024-12-05 20:44:00 +0800
tags: [cpp, csp-j, solution, dynamic-programming]
toc: true
---


# CSP-J/S 2024 第二轮 入门级 接龙 题解

> 题目来源：[ET题库 - 接龙](https://eternity-sky.github.io/OI/problem.html?id=35)

## 题目分析

这是一道关于序列接龙的题目。主要需要考虑以下几点：
1. 每个人有自己的词库（整数序列）
2. 需要判断是否能在指定轮数内完成接龙
3. 接龙时需要考虑数字的连接关系

## 解题思路

1. 首先需要存储每个人的词库
2. 对于每个查询，我们需要判断是否能在给定轮数内完成接龙
3. 使用动态规划来解决这个问题

## 代码实现

```cpp
#include <bits/stdc++.h>
using namespace std;

const int MAXN = 1005;
const int MAXK = 1005;

vector<int> wordbank[MAXN];  // 存储每个人的词库
int n, k, q;  // n个人，k轮，q个查询

// 判断是否可以完成接龙
bool can_chain(int rounds, int target) {
    // dp[i][j] 表示第i轮使用第j个数是否可行
    vector<vector<bool>> dp(rounds + 1, vector<bool>(MAXK, false));
    
    // 初始化第一轮
    for (int num : wordbank[1]) {
        dp[1][num] = true;
    }
    
    // 动态规划
    for (int i = 1; i < rounds; i++) {
        for (int j = 1; j <= k; j++) {
            if (!dp[i][j]) continue;
            
            // 尝试接下一个数
            for (int next : wordbank[(i % n) + 1]) {
                if (next == j) {
                    dp[i + 1][next] = true;
                }
            }
        }
    }
    
    // 检查最后一轮是否能达到目标
    return dp[rounds][target];
}

int main() {
    freopen("chain.in", "r", stdin);
    freopen("chain.out", "w", stdout);
    
    // 读入数据
    cin >> n >> k >> q;
    for (int i = 1; i <= n; i++) {
        int li;
        cin >> li;
        wordbank[i].resize(li);
        for (int j = 0; j < li; j++) {
            cin >> wordbank[i][j];
        }
    }
    
    // 处理查询
    while (q--) {
        int r, c;
        cin >> r >> c;
        cout << (can_chain(r, c) ? 1 : 0) << endl;
    }
    
    return 0;
}
```

## 代码解释

### 1. 数据结构
```cpp
vector<int> wordbank[MAXN];  // 存储每个人的词库
```
使用vector数组存储每个人的词库，方便访问和管理。

### 2. 动态规划部分
```cpp
vector<vector<bool>> dp(rounds + 1, vector<bool>(MAXK, false));
```
- `dp[i][j]` 表示第i轮使用第j个数是否可行
- 通过两层循环来填充dp数组
- 对于每个可行状态，尝试接下一个数

### 3. 查询处理
```cpp
while (q--) {
    int r, c;
    cin >> r >> c;
    cout << (can_chain(r, c) ? 1 : 0) << endl;
}
```
对每个查询调用can_chain函数判断是否可行。

## 时间复杂度分析

- 预处理：O(n)
- 每次查询：O(rounds * k * max_wordbank_size)
- 总体复杂度：O(q * k * n * max_wordbank_size)

## 注意事项

1. 文件输入输出
```cpp
freopen("chain.in", "r", stdin);
freopen("chain.out", "w", stdout);
```

2. 边界条件处理
- 注意检查rounds和target的合法性
- 考虑特殊情况（如第一轮）

## 总结

这道题是一个典型的动态规划问题，关键在于：
1. 正确定义状态
2. 找到状态转移方程
3. 合理处理边界条件

希望这个题解对你有帮助！如果有任何问题，欢迎在评论区讨论。

---