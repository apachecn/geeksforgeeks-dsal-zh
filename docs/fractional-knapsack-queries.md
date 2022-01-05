# 分数背包查询

> 原文:[https://www.geeksforgeeks.org/fractional-knapsack-queries/](https://www.geeksforgeeks.org/fractional-knapsack-queries/)

给定一个整数数组，由正权重“W”和分别作为一对的值“V”组成，以及一些由指定背包容量的整数“C”组成的查询，如果允许打破项目，找到可以放入背包的产品的最大值。

**示例:**

> **输入:** arr[] = { {1，2}，{1，3}，{3，7} }，q = {1，2，3，4，5}
> **输出:** {3，5.33333，7.66667，10，12}
> 对于‘C’= 1，我们将用值为 3 的元素填充 knap-sack。
> 对于‘C’= 2，首先我们填充值为 3 的元素，然后剩余 1 容量
> 填充值为 7 的元素。
> 对于‘C’= 3，首先我们填充值为 3 的元素，然后剩余 2 个容量
> 填充值为 7 的元素。
> 对于‘C’= 4，首先我们填充值为 3 的元素，然后剩余 3 个容量
> 填充值为 7 的元素。
> 对于‘C’= 5，首先我们用值为 3 的元素填充，接下来的 3 个容量
> 用值为 7 的元素填充，剩下的 1 用值为 1 的元素填充。

建议你先看完[分数背包](https://www.geeksforgeeks.org/fractional-knapsack-problem/)这篇文章，再看这篇文章。

**简单方法:**一个简单的方法是按照 V/W 值的降序对数组进行排序，即存在值/权重比。然后，对于每个查询，我们将在 knap-sack 没有完全满的情况下迭代数组并总结所需的整数值。
**时间复杂度:** O(q*n*log(n))

**高效的方法:**可以通过对权重和值执行排序数组的 prefix_sum 来优化查询。
下面是算法:

1.  按值/重量比降序排列数组。
2.  查找前缀-数组的权重和值。

*   执行二分搜索法运算，找到第一个权重(W)大于“C”的前缀为“和”的元素。严格来说，在“W”的前缀和数组中找到“C”值的上限。假设这个元素位于索引“X”处。*   Include sum of values from index {0, X-1} and the fractional value from index ‘X’ that can be accommodated in remaining capacity.

    下面是上述方法的实现:

    ```
    // C++ program to implement above approach
    #include <bits/stdc++.h>
    using namespace std;

    // Function on the basis of which we will
    // perform the sorting
    bool comp(pair<int, int> a, pair<int, int> b)
    {
        return (double)a.second / a.first >
                       (double)b.second / b.first;
    }

    // Function to sort the array on its value/weight
    // and perform-sum on both weight and value
    void preProcess(pair<int, int> arr[], int n)
    {
        sort(arr, arr + n, comp);
        for (int i = 1; i < n; i++) {
            arr[i].first += arr[i - 1].first;
            arr[i].second += arr[i - 1].second;
        }
    }

    // Function to answer queries
    double maxValue(int w, pair<int, int> arr[], int n)
    {
        // If w is large enough
        // to cover all weights
        if (arr[n - 1].first <= w)
            return arr[n - 1].second;

        // Value to search on arr
        pair<int, int> search_bound = { w, INT_MAX };

        // Index of the item which we will put
        // partially in our knap-sack
        int x = upper_bound(arr, arr + n, search_bound) - arr;

        // Required value
        if (x == 0)
            return (double)w * arr[0].second / arr[0].first;
        else
            return arr[x - 1].second +
                  (double)(w - arr[x - 1].first) * 
                  (arr[x].second - arr[x - 1].second) /
                  (arr[x].first - arr[x - 1].first);
    }

    void PrintQueries(int query[], pair<int, int> arr[],
                                            int n, int m)
    {
        for (int i = 0; i < m; i += 1) {
            cout << maxValue(query[i], arr, n) << endl;
        }
    }

    // Driver code
    int main()
    {
        // Input array representing the data of w[] and v[]
        pair<int, int> arr[] = { { 1, 2 }, { 1, 3 }, { 3, 7 } };
        int query[5] = { 1, 2, 3, 4, 5 };

        // Size of the array
        int n = sizeof(arr) / sizeof(pair<int, int>);
        int m = sizeof(query) / sizeof(query[0]);

        // Pre-processing
        preProcess(arr, n);

        PrintQueries(query, arr, n, m);

        return 0;
    }
    ```

    **Output:**

    ```
    3
    5.33333
    7.66667
    10
    12

    ```

    **时间复杂度:** O((n+q)*log(n))