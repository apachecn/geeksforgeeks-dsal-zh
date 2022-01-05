# 求给定和的子阵，常数空间允许有负数

> 原文:[https://www . geeksforgeeks . org/find-subarray-带给定负数的和-允许在常数空间中/](https://www.geeksforgeeks.org/find-subarray-with-given-sum-with-negatives-allowed-in-constant-space/)

给定一个未排序的整数数组，找到一个与给定数字相加的子数组。如果给定数量的总和超过一个子阵列，打印其中任何一个。

**示例**:

```
Input: arr[] = {1, 4, 20, 3, 10, 5}, sum = 33
Output: Sum found between indexes 2 and 4

Input: arr[] = {10, 2, -2, -20, 10}, sum = -10
Output: Sum found between indexes 0 to 3

Input: arr[] = {-10, 0, 2, -2, -20, 10}, sum = 20
Output: No subarray with given sum exists.
```

我们已经讨论了一种方法，使用哈希法
在包含正负元素的数组中找到给定和的子数组。在本文中，讨论了一种不使用任何额外空间的方法。
想法是将数组修改为只包含正元素:

*   找到数组中最小的负元素，并将数组中的每个值增加找到的最小负元素的绝对值。

我们可能会注意到，在进行上述修改后，每个子阵列的总和也将增加:

```
(number of elements in the subarray) * (absolute value of min element)
```

对输入数组进行上述修改后，任务简化为*查找给定的只有正数的数组中是否有任何子数组具有新的目标和*。这可以在 O(N)时间和恒定空间中使用滑动窗口技术来完成。
每次向窗口添加元素时，用最小元素的绝对值增加目标和，类似地，当从当前窗口移除元素时，用最小元素的绝对值减少目标和，这样对于每个长度的子阵列，比如 K，更新的目标和将是:

```
targetSum = sum + K*abs(minimum element)
```

以下是相同的方法:

*   将变量 curr_sum 初始化为第一个元素。
*   变量 curr_sum 表示当前子阵列的总和。
*   从第二个元素开始，将所有元素逐个添加到 curr_sum 中，并继续按 abs(最小元素)递增目标和。
*   如果 curr_sum 等于目标总和，则打印解决方案。
*   如果 curr_sum 超过总和，则删除尾随元素，同时减少 curr_sum 大于总和，并继续按 abs(最小元素)减少目标总和。

下面是上述方法的实现:

## C++

```
// C++ program to check if subarray with sum
// exists when negative elements are also present
#include <bits/stdc++.h>
using namespace std;

// Function to check if subarray with sum
// exists when negative elements are also present
void subArraySum(int arr[], int n, int sum)
{
    int minEle = INT_MAX;

    // Find minimum element in the array
    for (int i = 0; i < n; i++)
        minEle = min(arr[i], minEle);

    // Initialize curr_sum as value of first element
    // and starting point as 0
    int curr_sum = arr[0] + abs(minEle), start = 0, i;

    // Starting window length will be 1,
    // For generating new target sum,
    // add abs(minEle) to sum only 1 time
    int targetSum = sum;

    // Add elements one by one to curr_sum
    // and if the curr_sum exceeds the
    // updated sum, then remove starting element
    for (i = 1; i <= n; i++) {

        // If curr_sum exceeds the sum,
        // then remove the starting elements
        while (curr_sum - (i - start) * abs(minEle) > targetSum && start < i) {
            curr_sum = curr_sum - arr[start] - abs(minEle);
            start++;
        }

        // If curr_sum becomes equal to sum, then return true
        if (curr_sum - (i - start) * abs(minEle) == targetSum) {
            cout << "Sum found between indexes " << start << " and " << i - 1;
            return;
        }

        // Add this element to curr_sum
        if (i < n) {
            curr_sum = curr_sum + arr[i] + abs(minEle);
        }
    }

    // If we reach here, then no subarray
    cout << "No subarray found";
}

// Driver Code
int main()
{
    int arr[] = { 10, -12, 2, -2, -20, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);

    int sum = -10;

    subArraySum(arr, n, sum);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if subarray with sum
// exists when negative elements are also present
class GFG
{

    // Function to check if subarray with sum
    // exists when negative elements are also present
    static void subArraySum(int arr[], int n, int sum)
    {
        int minEle = Integer.MAX_VALUE;

        // Find minimum element in the array
        for (int i = 0; i < n; i++)
            minEle = Math.min(arr[i], minEle);

        // Initialize curr_sum as value of
        // first element and starting point as 0
        int curr_sum = arr[0] + Math.abs(minEle);
        int start = 0, i;

        // Starting window length will be 1,
        // For generating new target sum,
        // add abs(minEle) to sum only 1 time
        int targetSum = sum;

        // Add elements one by one to curr_sum
        // and if the curr_sum exceeds the
        // updated sum, then remove starting element
        for (i = 1; i <= n; i++)
        {

            // If curr_sum exceeds the sum,
            // then remove the starting elements
            while (curr_sum - (i - start) *
                   Math.abs(minEle) > targetSum &&
                                      start < i)
            {
                curr_sum = curr_sum - arr[start] -
                           Math.abs(minEle);
                start++;
            }

            // If curr_sum becomes equal to sum,
            // then return true
            if (curr_sum - (i - start) *
                Math.abs(minEle) == targetSum)
            {
                System.out.println("Sum found between indexes " +
                                      start + " and " + (i - 1));
                return;
            }

            // Add this element to curr_sum
            if (i < n)
            {
                curr_sum = curr_sum + arr[i] +
                             Math.abs(minEle);
            }
        }

        // If we reach here, then no subarray
        System.out.println("No subarray found");
    }

    // Driver Code
    public static void main (String[] args)
    {
        int arr[] = { 10, -12, 2, -2, -20, 10 };
        int n = arr.length;

        int sum = -10;

        subArraySum(arr, n, sum);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to check if subarray with summ
# exists when negative elements are also present

# Function to check if subarray with summ
# exists when negative elements are also present
def subArraySum(arr, n, summ):
    minEle = 10**9

    # Find minimum element in the array
    for i in range(n):
        minEle = min(arr[i], minEle)

    # Initialize curr_summ as value of
    # first element and starting poas 0
    curr_summ = arr[0] + abs(minEle)
    start = 0

    # Starting window length will be 1,
    # For generating new target summ,
    # add abs(minEle) to summ only 1 time
    targetSum = summ

    # Add elements one by one to curr_summ
    # and if the curr_summ exceeds the
    # updated summ, then remove starting element
    for i in range(1, n + 1):

        # If curr_summ exceeds the summ,
        # then remove the starting elements
        while (curr_summ - (i - start) * abs(minEle) >
                       targetSum and start < i):
            curr_summ = curr_summ - arr[start] - abs(minEle)
            start += 1

        # If curr_summ becomes equal to summ,
        # then return true
        if (curr_summ - (i - start) *
            abs(minEle) == targetSum):
            print("Sum found between indexes",
                          start, "and", i - 1)
            return

        # Add this element to curr_summ
        if (i < n):
            curr_summ = curr_summ + arr[i] + abs(minEle)

    # If we reach here, then no subarray
    print("No subarray found")

# Driver Code
arr = [10, -12, 2, -2, -20, 10]
n = len(arr)

summ = -10

subArraySum(arr, n, summ)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to check if subarray
// with sum exists when negative
// elements are also present
using System;

class GFG
{

    // Function to check if subarray
    // with sum exists when negative
    // elements are also present
    static void subArraySum(int []arr,
                            int n, int sum)
    {
        int minEle = int.MaxValue;
        int i;

        // Find minimum element in the array
        for (i = 0; i < n; i++)
            minEle = Math.Min(arr[i], minEle);

        // Initialize curr_sum as value of
        // first element and starting point as 0
        int curr_sum = arr[0] + Math.Abs(minEle);
        int start = 0;

        // Starting window length will be 1,
        // For generating new target sum,
        // add abs(minEle) to sum only 1 time
        int targetSum = sum;

        // Add elements one by one to curr_sum
        // and if the curr_sum exceeds the
        // updated sum, then remove starting element
        for (i = 1; i <= n; i++)
        {

            // If curr_sum exceeds the sum,
            // then remove the starting elements
            while (curr_sum - (i - start) *
                   Math.Abs(minEle) > targetSum &&
                                      start < i)
            {
                curr_sum = curr_sum - arr[start] -
                           Math.Abs(minEle);
                start++;
            }

            // If curr_sum becomes equal to sum,
            // then return true
            if (curr_sum - (i - start) *
                Math.Abs(minEle) == targetSum)
            {
                Console.Write("Sum found between indexes " +
                                 start + " and " + (i - 1));
                return;
            }

            // Add this element to curr_sum
            if (i < n)
            {
                curr_sum = curr_sum + arr[i] +
                             Math.Abs(minEle);
            }
        }

        // If we reach here, then no subarray
        Console.Write("No subarray found");
    }

    // Driver Code
    static public void Main ()
    {
        int []arr = { 10, -12, 2, -2, -20, 10 };
        int n = arr.Length;

        int sum = -10;

        subArraySum(arr, n, sum);
    }
}

// This code is contributed by ajit
```

## java 描述语言

```
<script>
// Java Script program to check if subarray with sum
// exists when negative elements are also present

// Function to check if subarray with sum
// exists when negative elements are also present
function subArraySum(arr,n,sum)
{
    let minEle = Number.MAX_VALUE;

    // Find minimum element in the array
    for (let i = 0; i < n; i++)
        minEle = Math.min(arr[i], minEle);

    // Initialize curr_sum as value of
    // first element and starting point as 0
    let curr_sum = arr[0] + Math.abs(minEle);
    let start = 0, i;

    // Starting window length will be 1,
    // For generating new target sum,
    // add abs(minEle) to sum only 1 time
    let targetSum = sum;

    // Add elements one by one to curr_sum
    // and if the curr_sum exceeds the
    // updated sum, then remove starting element
    for (i = 1; i <= n; i++)
    {

        // If curr_sum exceeds the sum,
        // then remove the starting elements
        while (curr_sum - (i - start) *
            Math.abs(minEle) > targetSum &&
                                    start < i)
        {
            curr_sum = curr_sum - arr[start] -
                    Math.abs(minEle);
            start++;
        }

        // If curr_sum becomes equal to sum,
        // then return true
        if (curr_sum - (i - start) *
                Math.abs(minEle) == targetSum)
        {
            document.write("Sum found between indexes " +
                                    start + " and " + (i - 1));
            return;
        }

        // Add this element to curr_sum
        if (i < n)
        {
            curr_sum = curr_sum + arr[i] +
                            Math.abs(minEle);
        }
    }

    // If we reach here, then no subarray
    document.write("No subarray found");
}

// Driver Code

    let arr = [ 10, -12, 2, -2, -20, 10 ];
    let n = arr.length;

    let sum = -10;

    subArraySum(arr, n, sum);

// This code is contributed by sravan kumar
</script>
```

**Output:** 

```
Sum found between indexes 1 and 2
```