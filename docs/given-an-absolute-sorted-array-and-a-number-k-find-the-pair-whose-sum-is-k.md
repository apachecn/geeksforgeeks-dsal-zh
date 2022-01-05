# 给定一个绝对排序数组和一个数字 K，找到和为 K 的对

> 原文:[https://www . geeksforgeeks . org/给定一个绝对排序的数组和一个数字-k-找到其和为-k 的对/](https://www.geeksforgeeks.org/given-an-absolute-sorted-array-and-a-number-k-find-the-pair-whose-sum-is-k/)

给定一个绝对排序数组 **arr[]** 和一个数字 **K** ，任务是在给定数组中找到一对和为 **K** 的元素。**绝对排序数组**是一个数字数组，其中 **|arr[i]| ≤ |arr[j]|** 每当 **i < j** 时。

**示例:**

> **输入:** arr[] = {-49，75，103，-147，164，-197，-238，314，348，-422}，K = 167
> **输出:**3 7
> (arr[3]+arr[7])=(-147+314)= 167。
> 
> **输入:** arr[] = {-8，10，-15，12，24}，K = 22
> **输出:** 1 3

**方法:**对于排序的数组，使用[这篇](https://www.geeksforgeeks.org/given-sorted-array-number-x-find-pair-array-whose-sum-closest-x/)文章中讨论的方法。对于绝对排序数组，根据其属性，通常有三种情况:

1.  这对中的两个数字都是负数。
2.  这对中的两个数字都是正数。
3.  一个是消极的，一个是积极的。

对于情况(1)和(2)，通过仅限制考虑正数或负数，分别使用[双指针方法](https://www.geeksforgeeks.org/two-pointers-technique/)。
对于案例(3)，使用相同的[双指针方法](https://www.geeksforgeeks.org/two-pointers-technique/)，其中我们有一个正数索引和一个负数索引，它们都从最高可能的索引开始，然后向下。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach

#include <bits/stdc++.h>
using namespace std;

// Index Pair Structure
struct indexPair {
    int index_1, index_2;
};

// Function to find positive and
// Negative pairs
indexPair findPositiveNegativePairs(
    const vector<int>& arr, int k)
{

    // result.index_1 for positive number &
    // result.index_2 for negative number
    indexPair result = indexPair{
        static_cast<int>(arr.size() - 1),
        static_cast<int>(arr.size() - 1)
    };

    // Find the last positive or zero number
    while (result.index_1 >= 0
           && arr[result.index_1] < 0) {
        --result.index_1;
    }

    // Find the last negative number
    while (result.index_2 >= 0
           && arr[result.index_2] >= 0) {
        --result.index_2;
    }

    // Loop to find the pair with
    // Desired Sum
    while (result.index_1 >= 0
           && result.index_2 >= 0) {

        // Condition if the current index pair
        // have the desired sum
        if (arr[result.index_1]
                + arr[result.index_2]
            == k) {
            return result;
        }

        // Condition if the current index pairs
        // sum is greater than desired sum
        else if (arr[result.index_1]
                     + arr[result.index_2]
                 > k) {

            // Loop to find the next
            // negative element from last
            do {
                --result.index_1;
            } while (result.index_1 >= 0
                     && arr[result.index_1] < 0);
        }

        // Condition if the current index pairs
        // sum is less than desired sum
        else {

            // Loop to find the next
            // positive or zero number from last
            do {
                --result.index_2;
            } while (result.index_2 >= 0
                     && arr[result.index_2] >= 0);
        }
    }
    return { -1, -1 };
}

// Function to find positive-positive number
// pairs or negative-negative number pairs
template <typename T>
indexPair findPairsOfSameSign(
    const vector<int>& arr, int k, T compare)
{

    // Initializing the index pairs with
    // 0 and the end of array length - 1
    indexPair result
        = indexPair{
              0,
              static_cast<int>(arr.size() - 1)
          };

    // Loop to find the first positive or negative
    // number in the array according to the given
    // comparison template function
    while (result.index_1 < result.index_2
           && compare(arr[result.index_1], 0)) {
        ++result.index_1;
    }

    // Loop to find the last positive or negative
    // number in the array according to the given
    // comparison template function
    while (result.index_1 < result.index_2
           && compare(arr[result.index_2], 0)) {
        --result.index_2;
    }

    // Loop to find the desired pairs
    while (result.index_1 < result.index_2) {

        // Condition if the current index pair
        // have the desired sum
        if (arr[result.index_1]
                + arr[result.index_2]
            == k) {
            return result;
        }

        // Condition if the current index pair
        // is greater than or equal to the desired
        // sum according to the compare function
        else if (compare(arr[result.index_1]
                             + arr[result.index_2],
                         k)) {

            // Loop to find the next positive-positive
            // or negative-negative pairs
            do {
                ++result.index_1;
            } while (result.index_1 < result.index_2
                     && compare(arr[result.index_1], 0));
        }

        // Condition if the current index pair is
        // greater than or equal to the desired
        // sum according to the compare function
        else {

            // Loop to find the next positive-positive
            // or negative-negative pairs
            do {
                --result.index_2;
            } while (result.index_1 < result.index_2
                     && compare(arr[result.index_2], 0));
        }
    }
    return { -1, -1 };
}

// Function to find the pairs whose sum
// is equal to the given desired sum K
indexPair FindPairs(const vector<int>& arr, int k)
{
    // Find the positive-negative pairs
    indexPair result = findPositiveNegativePairs(arr, k);

    // Condition to check if positive-negative
    // pairs not found in the array
    if (result.index_1 == -1
        && result.index_2 == -1) {

        return k >= 0
                   ? findPairsOfSameSign(
                         arr, k, less<int>())
                   : findPairsOfSameSign(
                         arr, k, greater_equal<int>());
    }
    return result;
}

// Driver Code
int main()
{
    vector<int> A;
    A.push_back(-49);
    A.push_back(75);
    A.push_back(103);
    A.push_back(-147);
    A.push_back(164);
    A.push_back(-197);
    A.push_back(-238);
    A.push_back(314);
    A.push_back(348);
    A.push_back(-422);
    int K = 167;
    indexPair result = FindPairs(A, K);

    cout << result.index_2 << ' '
         << result.index_1;

    return 0;
}
```

**Output:** 

```
3 7
```

**时间复杂度:** O(N)