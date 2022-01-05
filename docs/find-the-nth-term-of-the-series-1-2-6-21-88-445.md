# 求数列 1、2、6、21、88、445 的第 n 项。。。

> 原文:[https://www . geesforgeks . org/find-the-n-term-of-series-1-2-6-21-88-445/](https://www.geeksforgeeks.org/find-the-nth-term-of-the-series-1-2-6-21-88-445/)

给定正整数 **N** 。任务是找到该系列的第 n 个术语**:**

> **1，2，6，21，88，445，。。。**

**示例:**

> **输入:**N = 3
> T3】输出: 6
> 
> **输入:**N = 6
> T3】输出: 445

**进场:**

给定的序列遵循以下模式-

> **1，(1 * 1 + 1 = 2)，(2 * 2 + 2 = 6)，(6 * 3 + 3 = 21)，(21 * 4 + 4 = 88)，(88 * 5+5 = 445)……**

以下步骤可用于解决问题-

*   对于每次迭代 **i** ，将其前一个元素乘以 **i** (最初元素为 1)
*   并用**即**相加相乘的元素
*   最后，返回该系列的第**个**项。

下面是上述方法的实现

## C++

```
// C++ program to find N-th term
// of the series-
// 1, 2, 6, 21, 88, 445...
#include <bits/stdc++.h>
using namespace std;

// Function to return Nth term
// of the series
int nthTerm(int N)
{
    // Initializing a variable
    int term = 1;

    // Loop to iterate from 1 to N-1
    for (int i = 1; i < N; i++) 
    {
        // Multiplying and adding previous
        // element with i
        term = term * i + i;
    }

    // returning the Nth term
    return term;
}

// Driver Code
int main()
{
    // Get the value of N
    int N = 6;
    cout << nthTerm(N);
    return 0;
}
```

**Output**

```
445
```

**时间复杂度:** O(N)

**辅助空间:** O(1)