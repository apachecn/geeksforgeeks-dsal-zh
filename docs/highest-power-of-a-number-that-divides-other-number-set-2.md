# 一个数除以另一个数的最高幂| Set–2

> 原文:[https://www . geesforgeks . org/除以其他数集的最高幂数-2/](https://www.geeksforgeeks.org/highest-power-of-a-number-that-divides-other-number-set-2/)

给定两个数字 **N** 和 **M** (M > 1) ，任务是找到 M 除 N 的最高幂

**示例:**

> **输入:** N = 12，M = 2
> **输出:** 2
> **说明:**2 除 12 的幂是 1 和 2 (2 <sup>1</sup> = 2 和 2 <sup>2</sup> = 4 均除 12)。
> 较高的功率为 2，因此考虑 2。
> 
> **输入:** N = 500，M = 5
> T3】输出: 3。

**天真与比特操控法:**天真法与比特操控法在本题 [**集 1**](https://www.geeksforgeeks.org/highest-power-of-two-that-divides-a-given-number/) 中已经有提及。

**高效进场**:在**【1，log <sub>B</sub> (A)范围内，使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)手法即可解决任务。**对于范围内的每个数值 **x** ，检查**M<sup>x</sup>T13】是否除以 **N** 。最后，尽可能返回最大的**值****

按照以下步骤解决问题:

*   求 **log <sub>M</sub> (N)** 的值
*   在范围**【1】内运行**二分搜索法**，记录<sub>M</sub>(N)】**。
*   对于每个值 **x** ，检查**M<sup>x</sup>T5】是否除以 **N** ，找到最大的可能值。**

下面是上述方法的实现。

## C++

```
// C++ program to find the Highest
// Power of M that divides N
#include <bits/stdc++.h>
using namespace std;

// Function to find any log(N) base M
int log_a_to_base_b(int a, int b)
{
    return log(a) / log(b);
}

// Function to find the Highest Power
// of M which divides N
int HighestPower(int N, int M)
{
    int start = 0, end = log_a_to_base_b(N, M);
    int ans = 0;
    while (start <= end) {

        int mid = start + (end - start) / 2;
        int temp = (int)(pow(M, mid));

        if (N % temp == 0) {
            ans = mid;
            start = mid + 1;
        }
        else {
            end = mid - 1;
        }
    }
    return ans;
}

// Driver code
int main()
{
    int N = 12;
    int M = 2;
    cout << HighestPower(N, M) << endl;
    return 0;
}
```

**Output**

```
2

```

***时间复杂度***:O(log(log<sub>M</sub>(N))
***辅助空间*** : O(1)