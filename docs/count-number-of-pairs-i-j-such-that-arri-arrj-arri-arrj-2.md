# 计算对(I，j)的数量，使得 arr[i] * arr[j] = arr[i] + arr[j]

> 原文:[https://www . geesforgeks . org/count-对数-I-j-so-arri-arrj-arri-arrj-2/](https://www.geeksforgeeks.org/count-number-of-pairs-i-j-such-that-arri-arrj-arri-arrj-2/)

给定长度为 N 的数组 arr[]，计算对(I，j)的数量，使得**arr[I]* arr[j]= arr[I]+arr[j]**和 **0 < = i < j < = N** 。另外，数组的元素可以是任何正整数，包括零。

**示例:**

```
Input : arr[] = {2, 0, 3, 2, 0} 
Output : 2

Input : arr[] = {1, 2, 3, 4}
Output : 0

```

**简单解:**
我们可以生成数组中所有可能的对，并对满足给定条件的对进行计数。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to count pairs (i, j)
// such that arr[i] * arr[j] = arr[i] + arr[j]

#include <bits/stdc++.h>
using namespace std;

// Function to return the count of pairs(i, j)
// such that arr[i] * arr[j] = arr[i] + arr[j]
long countPairs(int arr[], int n)
{
    long count = 0;

    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {

            // Increment count if condition satisfy
            if (arr[i] * arr[j] == arr[i] + arr[j])
                count++;
        }
    }

    // Return count of pairs
    return count;
}

// Driver code
int main()
{

    int arr[] = { 2, 0, 3, 2, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Get and print count of pairs
    cout << countPairs(arr, n);

    return 0;
}
```