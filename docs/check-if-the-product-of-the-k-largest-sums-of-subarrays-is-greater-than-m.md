# 检查子阵的 K 个最大和的乘积是否大于 M

> 原文:[https://www . geeksforgeeks . org/check-如果 k 个最大子阵之和的乘积大于 m/](https://www.geeksforgeeks.org/check-if-the-product-of-the-k-largest-sums-of-subarrays-is-greater-than-m/)

给定一个由 **N** 整数和两个整数 **M** 和 **K** 组成的数组 **arr[]** 。任务是检查相邻子阵列的 **K** 最大和的乘积是否大于 **M** 。

**示例:**

> **输入:** arr[] = {10，-4，-2，7}，M = 659，K = 3
> **输出:**是
> 子阵列
> 的 3 个最大连续和是子阵列{10，-4，-2，7}、{10}和{7}
> 即 11，10 和 7，乘积是 11 * 10 * 7 = 770
> ，大于 659。
> 
> **输入:** arr[] = {4，-3，8}，M = 100，K = 6
> T3】输出:否

一种**蛮力方法**是将相邻子阵列的所有和存储在某个其他阵列中，并对其进行排序，然后计算 K 个最大和的乘积，并检查该值是否大于 m。但是，如果阵列的大小太大，连续子阵列的数量将增加，因此辅助阵列将占用更多的空间。

更好的方法是将数组的前缀和存储在数组本身中。那么子阵列 **arr[i…j]** 的和可以计算为**arr[j]–arr[I–1]**。现在为了存储 **K** 最大和连续子阵列，使用最小堆(优先级队列)，其中一次只存储 K 个最大和。此后，对于每隔一个元素，检查该元素是否大于最小堆的顶部元素。如果是，则该元素将被插入到最小堆中，顶部元素将从最小堆中弹出。最后，计算最小堆中所有元素的乘积，检查它是否大于 **M** 。

下面是上述方法的实现:

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true is the product
// of the maximum K subarrays sums of
// arr[] is greater than M
bool checkKSum(int arr[], int n, int k, int M)
{
    // Update the array to store the prefix sum
    for (int i = 1; i < n; i++)
        arr[i] = arr[i - 1] + arr[i];

    // Min-heap
    priority_queue<int, vector<int>, greater<int> > Q;

    // Starting index of the subarray
    for (int i = 0; i < n; i++) {

        // Ending index of the subarray
        for (int j = i; j < n; j++) {

            // To store the sum of the
            // subarray arr[i...j]
            int sum = (i == 0) ? arr[j] : arr[j] - arr[i - 1];

            // If the queue has less then k elements
            // then simply push it
            if (Q.size() < k)
                Q.push(sum);

            else {

                // If the min heap has equal exactly k
                // elements then check if the current
                // sum is greater than the smallest
                // of the current k sums stored
                if (Q.top() < sum) {
                    Q.pop();
                    Q.push(sum);
                }
            }
        }
    }

    // Calculate the product of
    // the k largest sum
    long product = 1;
    while (!Q.empty()) {
        product *= Q.top();
        Q.pop();
    }

    // If the product is greater than M
    if (product > M)
        return true;

    return false;
}

// Driver code
int main()
{
    int a[] = { 10, -4, -2, 7 };
    int n = sizeof(a) / sizeof(a[0]);
    int k = 3, M = 659;

    if (checkKSum(a, n, k, M))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

**Output:**

```
Yes

```