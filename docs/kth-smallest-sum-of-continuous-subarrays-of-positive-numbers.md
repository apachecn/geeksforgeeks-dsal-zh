# k 个正数连续子阵的最小和

> 原文:[https://www . geeksforgeeks . org/kth-正数连续子阵的最小和/](https://www.geeksforgeeks.org/kth-smallest-sum-of-continuous-subarrays-of-positive-numbers/)

给定一个正数排序数组，我们的任务是找到连续子阵的第 k 个最小和。

示例:

> 输入:a[] = {1，2，3，4，5，6}
> k = 4
> 输出:3
> 说明:排序后的子阵和的列表:{1，2，3，3，4，5，5，6，6，7，9，9，10，11，12，14，15，15，18，20，21}。第四个最小的元素是 3。
> 
> 输入:a[] = {1，2，3，4，5，6}
> k = 13
> 输出:10

一种**简单的方法**是首先通过预先计算前缀和来生成所有连续的子阵列和(这可以在 O(N^2 完成)。对求和数组进行排序，并给出第 k 个最小元素。

一个更好的方法是使用二分搜索法。首先，我们将预计算前缀和数组。现在，我们对第 k 个最小和的可能候选数应用二分搜索法，该最小和将在范围[0，数组的总和]内。现在让我们假设我们有一个名为 calculateRank 的函数，它将给出连续子阵列和的排序数组中任何数字的秩。在二分搜索法，我们将使用这个 calculateRank 函数来检查中间元素的等级是否小于 K，如果是，那么我们将起点减少到中间+1，否则如果它大于或等于 K，那么将终点减少到中间-1，并且更新答案变量。
现在让我们回到计算银行功能。这里，我们也将使用二分搜索法，但在我们的前缀和数组。我们将迭代我们的数组，假设我们在第 I 个索引上，我们将计算有多少子数组可以用起始元素作为这个第 I 个元素，它的和小于我们必须计算其秩的中间元素。我们对所有元素做，并把每个元素的计数加起来，我们得到中间元素的等级。为了计算从第一个索引开始的子阵列的数量，我们在前缀和上应用二进制。

C++实现使事情变得更清楚。

```
// CPP program to find k-th smallest sum
#include "algorithm"
#include "iostream"
#include "vector"
using namespace std;

int CalculateRank(vector<int> prefix, int n, int x)
{
    int cnt;

    // Initially rank is 0.
    int rank = 0;
    int sumBeforeIthindex = 0;
    for (int i = 0; i < n; ++i) {

        // Calculating the count the subarray with
        // starting at ith index
        cnt = upper_bound(prefix.begin(), prefix.end(), 
                sumBeforeIthindex + x) - prefix.begin();

        // Subtracting the subarrays before ith index.
        cnt -= i;

        // Adding the count to rank.
        rank += cnt;
        sumBeforeIthindex = prefix[i];
    }
    return rank;
}

int findKthSmallestSum(int a[], int n, int k)
{
    // PrefixSum array.
    vector<int> prefix;

    // Total Sum initially 0.
    int sum = 0;
    for (int i = 0; i < n; ++i) {
        sum += a[i];
        prefix.push_back(sum);
    }

    // Binary search on possible
    // range i.e [0, total sum]
    int ans = 0;
    int start = 0, end = sum;
    while (start <= end) {

        int mid = (start + end) >> 1;

        // Calculating rank of the mid and 
        // comparing with K
        if (CalculateRank(prefix, n, mid) >= k) {

            // If greater or equal store the answer
            ans = mid;
            end = mid - 1;
        }
        else {
            start = mid + 1;
        }
    }

    return ans;
}

int main()
{
    int a[] = { 1, 2, 3, 4, 5, 6 };
    int k = 13;
    int n = sizeof(a)/sizeof(a[0]);
    cout << findKthSmallestSum(a, n, k);
    return 0;
}
```

**Output:**

```
10

```

**时间复杂度:** O(N Log N Log SUM)。这里 N 是元素个数，SUM 是数组和。

CalculateRank 函数需要 O(N log N)个时间，称为 Log SUM 个时间。