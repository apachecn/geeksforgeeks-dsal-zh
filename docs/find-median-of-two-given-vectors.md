# 求两个给定向量的中值

> 原文:[https://www . geeksforgeeks . org/find-给定向量的中位数/](https://www.geeksforgeeks.org/find-median-of-two-given-vectors/)

给定两个向量，不同大小的 **a** 和 **b** ，其中数组 a 有 **m** 个元素，数组 b 有 **n** 个元素。Thes 的任务是找到两个向量的中值。这个问题是两个不同大小排序数组[中值](https://www.geeksforgeeks.org/median-of-two-sorted-arrays-of-different-sizes/)问题的扩展。

**示例:**

> **输入:** a = {1，4}
> b = {2}
> 
> **输出:**中位数为 2。
> 
> **解释:**
> 合并后的向量= {1，2，4}
> 所以，中位数是 2。
> 
> **输入:** a = {1，2}
> b = {3，5}
> 
> **产量:**中位数为 2.50000
> 
> **解释:**
> 合并后的向量= {1，2，3，5}
> 所以，中位数是(2 + 3) / 2 = 2.5。

**进场:**

1.  初始化向量 a。
2.  初始化向量 b。
3.  创建一个新的大小向量 **a + b** 。
4.  使用循环迭代第一个向量，并将数据存储到新创建的向量中，在迭代第一个向量后，类似地对第二个向量进行迭代。
5.  使用 [merge()](https://www.geeksforgeeks.org/merge-in-cpp-stl/) STL 函数将两个排序的向量合并到新创建的向量中。
6.  找到偶数和奇数尺寸的中间值并返回。

下面是上述方法的 C++实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the median
double findMedianSortedVectors(vector<int>& a,
                               vector<int>& b)
{
    // New Vector of size a + b
    vector<int> c(a.size() + b.size());
    int k = 0;
    double median = 0;
    int size_a = a.size();
    int size_b = b.size();
    for (int i = 0; i < size_a; i++) 
    {
        // Store data of first vector
        // in new vector
        c[k++] = a[i];
    }
    for (int i = 0; i < size_b; i++) 
    {
        // Store second vector in
        // vector c
        c[k++] = b[i];
    }

    merge(a.begin(), a.end(),
          b.begin(), b.end(), c.begin());

    // Merge the both sorted vectors
    int n = c.size();
    if (n % 2 == 0) 
    {
        // Calculate median for even 
        // size vector
        median = c[(n / 2) - 1] + c[n / 2];
        median = median / 2;
    }
    else 
    { 
        // Calculate median for odd 
        // size vector 
        median = c[(n - 1) / 2];
    }
    return median;
}

// Driver code
int main()
{
    vector<int> v1;
    vector<int> v2;

    // Initialize first vector
    v1.push_back(1);
    v1.push_back(4);

    // Initialize second vector
    v2.push_back(2);

    // Invoke function to calculate
    // median
    double median_vectors = 
    findMedianSortedVectors(v1, v2);

    // Print median value
    cout << median_vectors << endl;
    return 0;
}
```

**Output**

```
2
```

**复杂度:**

**时间复杂度:** O(m + n)至于合并两个向量 O(m + n)需要时间。
**空间复杂度:** O(1)因为不需要额外空间。