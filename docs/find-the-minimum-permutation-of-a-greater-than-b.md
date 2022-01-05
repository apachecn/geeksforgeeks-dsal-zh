# 求 A 大于 B 的最小排列

> 原文:[https://www . geesforgeks . org/find-a 的最小排列大于 b/](https://www.geeksforgeeks.org/find-the-minimum-permutation-of-a-greater-than-b/)

给定两个数字 **A** 和 **B** ，任务是找到 **A** 的数字排列，使其刚好大于给定的数字 **B** ，即找到大于 **B** 的 **A** 的最小值排列。如果没有这样的排列，那么打印-1
**示例:**

> **输入:** A = 9236，B = 3125
> **输出:** 3269
> **说明:**
> 由 A 的数字组成的大于 3125 的最小数为 3269。
> **输入:** A = 1234，B = 9879
> **输出:** -1

**方法:**想法是使用[next _ arrangement()](https://www.geeksforgeeks.org/stdnext_permutation-prev_permutation-c/)和 [stol()](https://www.geeksforgeeks.org/stdstol-and-stdstoll-functions-in-c/) 。可以按照以下步骤计算答案:

1.  将两个数字都作为字符串输入，利用[next _ arrange()](https://www.geeksforgeeks.org/stdnext_permutation-prev_permutation-c/)。
2.  使用 [stol()](https://www.geeksforgeeks.org/stdstol-and-stdstoll-functions-in-c/) 找到 **B** 的长值。
3.  然后找到数字 **A** 的最低排列。
4.  对于 **A** 的每个排列，检查该数是否大于 **B** 。
5.  如果任何排列大于数字 B，那么它就是可能的答案之一。从所有可能的答案中选择最少的一个。
6.  如果没有这样的号码，打印 **-1** 。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find the greater permutation

#include <bits/stdc++.h>
using namespace std;
#define ll long long
#define inf 999999999999999999

// Function to find the greater permutation
ll solve(string a, string b)
{
    ll n, val, ans = inf;

    // Convert the string B to long
    val = stol(b);
    n = a.length();

    // To find the lowest permutation
    // of the number
    sort(a.begin(), a.end());

    // Find if the lowest permutation of A is
    // greater than the given number B
    if (stol(a) > val) {
        ans = min((ll)stol(a), ans);
    }

    // Find all the permutations of A
    while (next_permutation(a.begin(),
                            a.end())) {
        if (stol(a) > val) {
            ans = min((ll)stol(a), ans);
        }
    }

    // If ans is not the initial value
    // then return ans
    if (ans != inf) {
        return ans;
    }
    // Else return -1
    else {
        return -1;
    }
}

// Driver code
int main()
{
    string a, b;
    ll ans;
    a = "9236";
    b = "3145";
    ans = solve(a, b);
    cout << ans;
}
```

**Output:** 

```
3269
```

时间复杂度:O(n * log n)