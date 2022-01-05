# 求数列 12，14，24，58，164 的 N 项之和，…

> 原文:[https://www . geesforgeks . org/find-the-sum-n-terms-of-series-12-14-24-58-164/](https://www.geeksforgeeks.org/find-the-sum-of-n-terms-of-the-series-12-14-24-58-164/)

给定一个正整数， **N** 。求系列 **12，14，24，58，164 的第一个 **N 项**的和…..**

**示例**:

> **输入** : N = 5
> 输出 : 272
> 
> **输入** : N = 3
> 输出 : 50

**进场:**

该序列通过使用以下模式形成。对于任何数值 N-

> **S<sub>N</sub>= 3<sup>N</sup>–N<sup>2</sup>+11 * N–1**

插图:

> **输入:** N = 5
> **输出:** 272
> **解释:**
> S<sub>N</sub>= 3<sup>N</sup>–N<sup>2</sup>+11 * N–1
> = 3<sup>5</sup>–5<sup>2</sup>+11 * 5–1
> = 243–25+54

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return sum of
// N term of the series
int findSum(int N)
{
    return (pow(3, N) - 
            pow(N, 2) + 
            11 * N - 1);
}

// Driver Code
int main()
{
    int N = 5;
    cout << findSum(N);
    return 0;
}
```

**Output**

```
272
```

**时间复杂度:** O(1)

**辅助空间:** O(1)