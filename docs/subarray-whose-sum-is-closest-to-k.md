# 和最接近 K 的子阵

> 原文:[https://www . geesforgeks . org/subarray-其和最接近-k/](https://www.geeksforgeeks.org/subarray-whose-sum-is-closest-to-k/)

给定一个正负整数和一个整数 k 的数组，任务是找到和最接近 k 的子数组，如果有多个答案，打印任意一个。

**注意:**这里最接近是指 abs(sum-k)应该最小。

**示例:**

> **输入:** a[] = { -5，12，-3，4，-15，6，1 }，K = 2
> **输出:** 1
> 子阵{-3，4}或{1}的和= 1 最接近 K
> 
> **输入:** a[] = {2，2，-1，5，-3，-2 }，K = 7
> **输出:** 6
> 这里的输出可以是 6 或 8
> 子阵列{ 2，2，-1，5}给出的和为 8，其具有 abs(8-7) = 1，与具有 abs(6-7) = 1 的子阵列{ 2，-1，5}相同。

一种简单的方法是使用前缀和检查所有可能的子阵列和。那种情况下的复杂性将是 0(N<sup>2</sup>)。

一个**高效的解决方案**将是使用 [C++ STL 集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)和[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来解决以下问题。按照下面的算法来解决上面的问题。

*   首先在集合容器中插入第一个元素。
*   将答案*和*初始化为第一个元素，*差*初始化为 abs(A <sub>0</sub> -k)。
*   对从 1 到 N 的所有数组元素进行迭代，并在集合容器的每一步继续将元素添加到前缀 sum。
*   在每次迭代中，由于前缀和已经存在，我们只需要从开始减去一些元素的和，就可以得到任何子阵列的和。贪婪的方法是减去取最接近 k 的和的子阵的和。
*   使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/) ( [下界()](https://www.geeksforgeeks.org/set-lower_bound-function-in-c-stl/)函数可以使用)求从开始最接近(前缀-k)的子阵列的和，因为从前缀和中减去该数将得到在该迭代之前最接近 K 的子阵列和。
*   还要检查下界()返回之前的索引，因为总和可以大于或小于 k
*   如果下界没有返回这样的元素，那么如果当前前缀和小于先前计算的和，则比较并更新当前前缀和。

下面是上述方法的实现。

## C++

```
// C++ program to find the
// sum of subarray whose sum is
// closest to K
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of subarray
// whose sum is closest to K
int closestSubarraySumToK(int a[], int n, int k)
{

    // Declare a set
    set<int> s;

    // initially consider the
    // first subarray as the first
    // element in the array
    int presum = a[0];

    // insert
    s.insert(a[0]);

    // Initially let this difference
    // be the minimum
    int mini = abs(a[0] - k);

    // let this be the sum
    // of the subarray
    // to be searched initially
    int sum = presum;

    // iterate for all the array elements
    for (int i = 1; i < n; i++) {

        // calculate the prefix sum
        presum += a[i];

        // find the closest subarray
        // sum to by using lower_bound
        auto it = s.lower_bound(presum - k);

        // if it is the first element
        // in the set
        if (it == s.begin()) {

            // get the prefix sum till start
            // of the subarray
            int diff = *it;

            // if the subarray sum is closest to K
            // than the previous one
            if (abs((presum - diff) - k) < mini) {

                // update the minimal difference
                mini = abs((presum - diff) - k);

                // update the sum
                sum = presum - diff;
            }
        }

        // if the difference is
        // present in between
        else if (it != s.end()) {

            // get the prefix sum till start
            // of the subarray
            int diff = *it;

            // if the subarray sum is closest to K
            // than the previous one
            if (abs((presum - diff) - k) < mini) {

                // update the minimal difference
                mini = abs((presum - diff) - k);

                // update the sum
                sum = presum - diff;
            }

            // also check for the one before that
            // since the sum can be greater than
            // or less than K also
            it--;

            // get the prefix sum till start
            // of the subarray
            diff = *it;

            // if the subarray sum is closest to K
            // than the previous one
            if (abs((presum - diff) - k) < mini) {

                // update the minimal difference
                mini = abs((presum - diff) - k);

                // update the sum
                sum = presum - diff;
            }
        }

        // if there exists no such prefix sum
        // then the current prefix sum is
        // checked and updated
        else {

            // if the subarray sum is closest to K
            // than the previous one
            if (abs(presum - k) < mini) {

                // update the minimal difference
                mini = abs(presum - k);

                // update the sum
                sum = presum;
            }
        }

        // insert the current prefix sum
        s.insert(presum);
    }

    return sum;
}

// Driver Code
int main()
{
    int a[] = { -5, 12, -3, 4, -15, 6, 1 };
    int n = sizeof(a) / sizeof(a[0]);
    int k = 2;

    cout << closestSubarraySumToK(a, n, k);
    return 0;
}
```

**时间复杂度:** O(N log N)