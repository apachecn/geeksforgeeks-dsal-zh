# 找出范围[1，N]内的 N 个数字的排列，使得 K 个数字具有与其索引相同的值

> 原文:[https://www . geeksforgeeks . org/find-n-numbers-in-range-1-n-so-k-numbers-具有与其索引相同的值/](https://www.geeksforgeeks.org/find-permutation-of-n-numbers-in-range-1-n-such-that-k-numbers-have-value-same-as-their-index/)

给定一个正整数 **N** 和一个整数 **K** ，使得 **0 ≤ K ≤ N** ，任务是找到【1，N】的任意**排列** **A** ，使得**索引**的数量 **A <sub>i</sub> = i** 正好是**K**(**1 基索引**)。如果没有这样的排列，打印**1**。

**示例:**

> **输入:** N = 3， **K = 1
> **输出:** 1 3 2
> **解释:**考虑排列 A = [1，3，2]。我们有 A1=1，A2=3 和 A3=2。
> 所以，这个排列正好有 1 个索引，这样 A <sub>i</sub> = i。**
> 
> ****输入:** N = 2，K = 1
> **输出:** -1
> **说明:**共有【1，2】2 种排列，分别为【1，2】和【2，1】。
> 在【1，2】中有 2 个指数，在【2，1】中有 0 个指数，A <sub>i</sub> = i 成立。
> 因此，不存在 Ai=i 成立的恰好有 1 个指数 I 的[1，2]的任何排列。**

****进场:**使用[贪婪](http://www.geeksforgeeks.org/greedy-algorithms/)进场可以解决任务。最初**将**精确固定在 **K** 元素的**索引**上，然后将 **N-K** 元素随机放置在**不同的**位置。按照以下步骤解决问题:**

1.  **以某种方式固定 **K** 位置**
2.  **打乱剩余的 **N-K** 号**
3.  **将剩余元素循环移位 1**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print permutation
void permutation(int N, int K)
{
    if (K == N) {
        for (int i = 1; i <= N; i++) {
            cout << i << ' ';
        }
        cout << '\n';
    }
    else if (K == N - 1) {
        cout << "-1" << '\n';
    }
    else {
        for (int i = 1; i <= K; i++) {
            cout << i << ' ';
        }
        for (int i = K + 2; i <= N; i++) {
            cout << i << ' ';
        }
        cout << K + 1 << '\n';
    }
}

// Driver Code
int main()
{
    int N = 3;
    int K = 1;
    permutation(N, K);
    return 0;
}
```

****Output**

```
1 3 2
```** 

*****时间复杂度*****:**O(N)
***辅助空间*** **:** O(1)**