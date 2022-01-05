# 找出最多选择 K 对的配对数组的最大花费

> 原文:[https://www . geeksforgeeks . org/find-成对数组的最大成本-最多选择 k 对/](https://www.geeksforgeeks.org/find-the-maximum-cost-of-an-array-of-pairs-choosing-at-most-k-pairs/)

给定一组配对**arr【】**，任务是找到选择最多 **K** 对的最大成本。成对数组的成本被定义为所选对的第一个元素的总和与所选对的第二个元素中的最小值的乘积。例如，如果选择以下配对 *(3，7)、(9，2)**(2，5)* ，则成本为 *(3+9+2)*(2) = 28* 。

**示例:**

> **输入:** arr[] = { {4，7}、{15，1}、{3，6}、{6，8} }，K = 3
> **输出:** 78
> 选择 1、3、4 对，因此成本= (4 + 3 + 6) * 6 = 78。
> 
> **输入:** arr[] = { {62，21}，{31，16}，{19，2}，{32，19}，{12，17} }，K = 4
> **输出:** 2192

**方法:**如果一对中的第二个元素在答案中是固定的，那么 *K-1* (或更少)其他对将从那些第二个元素大于或等于固定的第二个元素的对中选择，并且如果这些选择使得第一个元素的总和最大，答案将是最大的。因此，根据第二个元素对数组进行排序，然后以 *K* 对(或更少)的第一个元素的最大值和为降序进行迭代。借助 Set 数据结构可以取第一元素 *K* 对的最大和。

下面是上述方法的实现:

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Driver function to sort the array elements
// by second element of pairs
bool sortbysec(const pair<int, int>& a,
               const pair<int, int>& b)
{
    return (a.second < b.second);
}

// Function that returns the maximum cost of
// an array of pairs choosing at most K pairs.
int maxCost(pair<int, int> a[], int N, int K)
{
    // Initialize result and temporary sum variables
    int res = 0, sum = 0;

    // Initialize Set to store K greatest
    // element for maximum sum
    set<pair<int, int> > s;

    // Sort array by second element
    sort(a, a + N, sortbysec);

    // Iterate in descending order
    for (int i = N - 1; i >= 0; --i) {
        s.insert(make_pair(a[i].first, i));
        sum += a[i].first;
        while (s.size() > K) {
            auto it = s.begin();
            sum -= it->first;
            s.erase(it);
        }

        res = max(res, sum * a[i].second);
    }

    return res;
}

// Driver Code
int main()
{
    pair<int, int> arr[] = { { 12, 3 }, { 62, 21 }, { 31, 16 }, 
                             { 19, 2 }, { 32, 19 }, { 12, 17 }, 
                             { 1, 7 } };

    int N = sizeof(arr) / sizeof(arr[0]);

    int K = 3;

    cout << maxCost(arr, N, K);

    return 0;
}
```

**Output:**

```
2000

```