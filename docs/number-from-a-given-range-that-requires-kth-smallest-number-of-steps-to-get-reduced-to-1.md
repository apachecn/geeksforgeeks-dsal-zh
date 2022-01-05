# 给定范围内需要第 k 个最小步数才能减少到 1 的数

> 原文:[https://www . geeksforgeeks . org/number-from-a-给定范围-需要-kth-最小步数-get-reduced-1/](https://www.geeksforgeeks.org/number-from-a-given-range-that-requires-kth-smallest-number-of-steps-to-get-reduced-to-1/)

给定三个正整数 **L** 、 **R** 和 **K** ，任务是从范围**【L，R】**中找到该数，该范围要求 **K <sup>th</sup>** 最小步数通过执行以下操作减少到 1:

*   [如果 **X** 为偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则减少 **X** 至 **X/2** 。
*   否则，设置 **X = (3*X + 1)** 。

**示例:**

> **输入:** L = 7，R = 10，K = 4
> **输出:** 9
> **说明:**
> 范围【7，10】内所有数字的步数如下:
> 
> *   7 所需的步数是 16。{7 -> 22 -> 11 -> 34 -> 17 -> 52 -> 26 -> 13 -> 40 -> 20 -> 10 -> 5 -> 16 -> 8 -> 4 -> 2 > 1}
> *   同样，8 所需的步数是 3。
> *   同样，9 所需的步数是 19。
> *   同样，10 步所需的步数是 6。
> 
> 因此，来自给定范围的所有值(按升序排序)所需的步数对于值{8，10，7，9}分别为{3，6，16，19}。因此，数字 9 需要第 K<sup>个最小步数。</sup>
> 
> **输入:** L = 7，R = 10，K = 2
> T3】输出: 10

**方法:**想法是制作单独的函数来计算范围中每个数字的步数，并打印所获得的值中的最小的**K<sup>th</sup>T5。按照以下步骤解决问题:**

*   定义一个函数 **power_value ()** 来计算一个数字所需的步数:
    *   基础条件:如果**号**为 **1** ，则返回 **0** 。
    *   [如果数字为偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则用数值**数字/2** 调用函数 **power_value()** 。
    *   否则，用数值**号* 3 + 1** 调用函数 **power_value()** 。
*   现在，为了找到第 **K <sup>个</sup>最小步数**，执行以下步骤:
    *   初始化一对的[向量，比如**和**。](https://www.geeksforgeeks.org/store-data-triplet-vector-c/)
    *   [遍历**【L，R】**范围内的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，计算当前数 **i** 的幂值，在对 **ans** 的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中插入一对步数和 **i** 。
    *   [按照该数步数的升序](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)对向量进行排序。
*   完成上述步骤后，从开始打印 **K <sup>th</sup>** 最小步数，即**ans[K–1]。第二**作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

vector<ll> v(1000000, -1);

// Function to count the number of
// steps required to reduce val to
// 1 by the given operations
ll power_value(ll val)
{
    // Base Case
    if (val == 1)
        return 0;

    // If val is even, divide by 2
    if (val % 2 == 0) {
        v[val] = power_value(val / 2) + 1;
        return v[val];
    }

    // Otherwise, multiply it
    // by 3 and increment by 1
    else {
        ll temp = val * 3;
        temp++;
        v[val] = power_value(temp) + 1;
        return v[val];
    }
}

// Function to find Kth smallest
// count of steps required for
// numbers from the range [L, R]
ll getKthNumber(int l, int r, int k)
{
    // Stores numbers and their
    // respective count of steps
    vector<pair<ll, ll> > ans;

    // Count the number of steps for
    // all numbers from the range [L, R]
    for (ll i = l; i <= r; i++) {
        if (v[i] == -1)
            power_value(i);
    }

    ll j = 0;

    // Insert in the vector
    for (ll i = l; i <= r; i++) {
        ans.push_back(make_pair(v[i], i));
        j++;
    }

    // Sort the vector in ascending
    // order w.r.t. to  power value
    sort(ans.begin(), ans.end());

    // Print the K-th smallest number
    cout << ans[k - 1].second;
}

// Driver Code
int main()
{
    int L = 7, R = 10, K = 4;
    getKthNumber(L, R, K);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

v = [-1]*(1000000)

# Function to count the number of
# steps required to reduce val to
# 1 by the given operations
def power_value(val):

    # Base Case
    if (val == 1):
        return 0

    # If val is even, divide by 2
    if (val % 2 == 0):
        v[val] = power_value(val // 2) + 1
        return v[val]

    # Otherwise, multiply it
    # by 3 and increment by 1
    else:
        temp = val * 3
        temp+=1
        v[val] = power_value(temp) + 1
        return v[val]

# Function to find Kth smallest
# count of steps required for
# numbers from the range [L, R]
def getKthNumber(l, r, k):

    # Stores numbers and their
    # respective count of steps
    ans = []

    # Count the number of steps for
    # anumbers from the range [L, R]
    for i in range(l, r + 1):
        if (v[i] == -1):
            power_value(i)

    j = 0

    # Insert in the vector
    for i in range(l, r + 1):
        ans.append([v[i], i])
        j += 1

    # Sort the vector in ascending
    # order w.r.t. to  power value
    ans = sorted(ans)

    # Print the K-th smallest number
    print (ans[k - 1][1])

# Driver Code
if __name__ == '__main__':
    L,R,K = 7, 10, 4
    getKthNumber(L, R, K)

    # This code is contributed by mohit kumar 29.
```

**Output:** 

```
9
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*