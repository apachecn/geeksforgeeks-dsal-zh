# 求和可被 M 整除的最大范围【L，R】

> 原文:[https://www . geesforgeks . org/find-最大范围-lr-其和可被 m 整除/](https://www.geeksforgeeks.org/find-the-maximum-range-lr-whose-sum-is-divisible-by-m/)

给定一个由正数组成的数组 **arr[]** ，任务是找到其和可被 **M** 整除的最大范围【L，R】。如果没有范围存在，返回-1。

**示例:**

> **输入:** arr[] = {3，7，5，2，5，10}，M = 3
> **输出:** 1 3
> **说明:**1 到 3 的数之和是 3+7+5，也就是 15。
> 
> **输入:**
> A[] = {4，8，12，16，20}
> M = 11
> **输出:**
> -1

**天真的方法:**天真的方法是，我们可以迭代数组中所有可能的 L 和 R，检查和是否可分。如果是，则存储数组的长度。

**高效方法:**这里的想法是使用一个[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。

*   最初，计算这些值的前缀和。
*   一旦前缀和被计算出来，每个值都被取模 **M** 的值代替。
*   最终值相等的指数是总和可被 m 整除的范围。
*   找到相同值的最大范围。

下面是上述方法的实现，

```
// C++ implementation of the above approach.
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum range
// whose sum is divisible by M.
pair<int, int> maxrange(int n,
                        int a[], int m)
{
    int pre[n + 5];
    map<int, set<int> > mpp;
    int value, l, r, lans = -1,
                     rans = -1, ans = 0;

    // Calculate the prefix sum
    pre[0] = a[0];
    for (int i = 1; i < n; i++) {
        pre[i] = a[i] + pre[i - 1];
    }

    // Replacing the values with modulo M
    // and inserting the indices into the map
    for (int i = 0; i < n; i++) {
        pre[i] = pre[i] % m;
        mpp[pre[i]].insert(i);
    }

    // Calculate the range [L, R]
    for (auto it = mpp.begin(); it != mpp.end(); it++) {
        if (it->first == 0) {
            value = *((it->second).rbegin()) + 1;
            l = 1;
            r = value;
        }
        else {
            value = *((it->second).rbegin())
                    - *((it->second.begin()));
            l = *((it->second.begin())) + 2;
            r = *((it->second).rbegin()) + 1;
        }
        if (value > ans && l <= r) {
            ans = value;
            lans = l;
            rans = r;
        }
    }

    return make_pair(lans, rans);
}

// Driver code
int main()
{
    int A[] = { 3, 7, 5, 2, 5, 10 };
    int N = sizeof(A) / sizeof(A[0]);
    int M = 3;
    pair<int, int> value = maxrange(N, A, M);
    if (value.first == -1) {
        cout << -1 << "\n";
    }
    else {
        cout << value.first << " "
             << value.second << "\n";
    }
    return 0;
}
```

**Output:**

```
1 3

```