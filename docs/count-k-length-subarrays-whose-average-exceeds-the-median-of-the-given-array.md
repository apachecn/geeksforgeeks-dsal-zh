# 计算平均长度超过给定数组中值的 K 长度子数组

> 原文:[https://www . geesforgeks . org/count-k-length-子数组-其平均值超过给定数组的中值/](https://www.geeksforgeeks.org/count-k-length-subarrays-whose-average-exceeds-the-median-of-the-given-array/)

给定一个由 **N** 个整数和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是找出大小为 **K** 的[子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的数量，其平均值大于其 [**中值**](https://www.geeksforgeeks.org/median-two-sorted-arrays-different-sizes-ologminn-m/) 和两者的平均值，中值必须是[素数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)或非素数。

**示例:**

> **输入:** arr[] = {2，4，3，5，6}，K = 3
> **输出:** 2
> **说明:**
> 满足给定条件的子阵如下:
> 
> 1.  {2，4，3}:这个子阵的中位数是 3，平均值是(2 + 4 + 3)/3 = 3。因为中值和平均值都是质数，平均值> =中值。所以计数这个子阵列。
> 2.  {4，3，5}:这个子阵的中位数是 4，平均值是(4 + 3 + 5)/3 = 4。因为中值和平均值都是非质数，平均值> =中值。所以计数这个子阵列。
> 
> 因此，子阵列的总数是 2。
> 
> **输入:** arr[] = {2，4，3，5，6}，K = 2
> T3】输出: 3

**方法:**给定的问题可以使用[基于策略的数据结构](https://www.geeksforgeeks.org/policy-based-data-structures-g/)即[有序集](https://www.geeksforgeeks.org/ordered-set-gnu-c-pbds/)来解决。按照以下步骤解决给定的问题:

*   [使用厄拉多塞](https://www.geeksforgeeks.org/sieve-eratosthenes-0n-time-complexity/)的[筛将所有质数](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)和非质数预计算至**10<sup>5</sup>T5。**
*   初始化一个变量，比如**计数**，它存储子阵列的结果计数。
*   找到第一个 **K** 元素的[**平均值**](https://www.geeksforgeeks.org/program-average-array-iterative-recursive/) 和**中值**，如果**平均值> =中值**，并且平均值和中值都是质数或非质数，那么将**计数**增加 **1** 。
*   将第一个 **K** 数组元素存储在**有序集**中。
*   [在范围**【0，N–K】**内遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并执行以下步骤:
    *   从有序 _ 集中移除当前的元素**arr【I】**，并向有序 _ 集中添加 **(i + k) <sup>第</sup>** 元素，即**arr【I+K】**。
    *   使用函数**找到 _ order _ by _ set((K+1)/2–1)**，找到数组的[中值。](https://www.geeksforgeeks.org/program-for-mean-and-median-of-an-unsorted-array/)
    *   求当前子阵列的[平均值。](https://www.geeksforgeeks.org/maximum-average-of-a-subarray-of-size-of-atleast-x-and-atmost-y/)
    *   如果**平均值> =中值**，并且平均值和中值都是质数或非质数，那么将**计数**增加 **1** 。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
#include <stdlib.h>
using namespace __gnu_pbds;

using namespace std;
typedef tree<int, null_type, less_equal<int>,
             rb_tree_tag,
             tree_order_statistics_node_update>
    ordered_set;

const int mxN = (int)1e5;

// Stores whether i is prime or not
bool prime[mxN + 1];

// Function to precompute all the prime
// numbers using sieve of erastothenes
void SieveOfEratosthenes()
{
    // Initialize the prime array
    memset(prime, true, sizeof(prime));

    // Iterate over the range [2, mxN]
    for (int p = 2; p * p <= mxN; p++) {

        // If the prime[p] is unchanged,
        // then it is a prime
        if (prime[p]) {

            // Mark all multiples of p
            // as non-prime
            for (int i = p * p;
                 i <= mxN; i += p)
                prime[i] = false;
        }
    }
}

// Function to find number of subarrays
// that satisfy the given criteria
int countSubarray(int arr[], int n, int k)
{
    // Initialize the ordered_set
    ordered_set s;

    // Stores the sum for subarray
    int sum = 0;
    for (int i = 0; i < (int)k; i++) {
        s.insert(arr[i]);
        sum += arr[i];
    }

    // Stores the average for each
    // possible subarray
    int avgsum = sum / k;

    // Stores the count of subarrays
    int ans = 0;

    // For finding the median use the
    // find_by_order(k) that returns
    // an iterator to kth element
    int med = *s.find_by_order(
        (k + 1) / 2 - 1);

    // Check for the valid condition
    if (avgsum - med >= 0
        && ((prime[med] == 0
             && prime[avgsum] == 0)
            || (prime[med] != 0
                && prime[avgsum] != 0))) {

        // Increment the resultant
        // count of subarray
        ans++;
    }

    // Iterate the subarray over the
    // the range [0, N - K]
    for (int i = 0; i < (int)(n - k); i++) {

        // Erase the current element
        // arr[i]
        s.erase(s.find_by_order(
            s.order_of_key(arr[i])));

        // The function Order_of_key(k)
        // returns the number of items
        // that are strictly smaller
        // than K
        s.insert(arr[i + k]);
        sum -= arr[i];

        // Add the (i + k)th element
        sum += arr[i + k];

        // Find the average
        avgsum = sum / k;

        // Get the median value
        med = *s.find_by_order(
            (k + 1) / 2 - 1);

        // Check the condition
        if (avgsum - med >= 0
            && ((prime[med] == 0
                 && prime[avgsum] == 0)
                || (prime[med] != 0
                    && prime[avgsum] != 0))) {

            // Increment the count of
            // subarray
            ans++;
        }
    }

    // Return the resultant count
    // of subarrays
    return ans;
}

// Driver Code
int main()
{
    // Precompute all the primes
    SieveOfEratosthenes();

    int arr[] = { 2, 4, 3, 5, 6 };
    int K = 3;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << countSubarray(arr, N, K);

    return 0;
}
```

**Output:** 

```
2
```

***时间复杂度:**O(N * log N+N * log(log N))*
***辅助空间:** O(N)*