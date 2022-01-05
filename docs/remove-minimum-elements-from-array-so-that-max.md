# 从数组中移除最小元素，使最大< = 2 *最小

> 原文:[https://www . geesforgeks . org/remove-从数组中移除最少元素-so-max/](https://www.geeksforgeeks.org/remove-minimum-elements-from-array-so-that-max/)

给定一个数组 **arr** ，任务是移除最少数量的元素，这样在移除之后， **max(arr) < = 2 * min(arr)** 。

**示例:**

> **输入:** arr[] = {4，5，3，8，3}
> **输出:** 1
> 从数组中移除 8。
> 
> **输入:** arr[] = {1，2，3，4}
> **输出:** 1
> 从数组中移除 1。

**方法:**让我们将每个值固定为最小值，比如 **x** ，并找出在范围**【x，2 * x】**内的项数。这可以使用前缀和来完成，我们可以使用[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)(实现自平衡 BST)来代替数组，因为值可以很大。不在**【x，2 * x】**范围内的其余术语必须删除。因此，在 **x** 的所有值中，我们选择范围**【x，2 * x】**中项数最大的值。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum removals from 
// arr such that max(arr) <= 2 * min(arr)
int minimumRemovals(int n, int a[])
{
    // Count occurrence of each element
    map<int, int> ct;
    for (int i = 0; i < n; i++)
        ct[a[i]]++;

    // Take prefix sum
    int sm = 0;
    for (auto mn : ct) {
        sm += mn.second;
        ct[mn.first] = sm;
    }

    int mx = 0, prev = 0;
    for (auto mn : ct) {

        // Chosen minimum
        int x = mn.first;
        int y = 2 * x;
        auto itr = ct.upper_bound(y);
        itr--;

        // Number of elements that are in
        // range [x, 2x]
        int cr = (itr->second) - prev;
        mx = max(mx, cr);
        prev = mn.second;
    }

    // Minimum elements to be removed
    return n - mx;
}

// Driver Program to test above function
int main()
{
    int arr[] = { 4, 5, 3, 8, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minimumRemovals(n, arr);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from bisect import bisect_left as upper_bound

# Function to return the minimum removals from
# arr such that max(arr) <= 2 * min(arr)
def minimumRemovals(n, a):

    # Count occurrence of each element
    ct = dict()
    for i in a:
        ct[i] = ct.get(i, 0) + 1

    # Take prefix sum
    sm = 0
    for mn in ct:
        sm += ct[mn]
        ct[mn] = sm

    mx = 0
    prev = 0;
    for mn in ct:

        # Chosen minimum
        x = mn
        y = 2 * x
        itr = upper_bound(list(ct), y)

        # Number of elements that are in
        # range [x, 2x]
        cr = ct[itr] - prev
        mx = max(mx, cr)
        prev = ct[mn]

    # Minimum elements to be removed
    return n - mx

# Driver Code
arr = [4, 5, 3, 8, 3]
n = len(arr)
print(minimumRemovals(n, arr))

# This code is contributed by Mohit Kumar
```

**Output:**

```
1

```