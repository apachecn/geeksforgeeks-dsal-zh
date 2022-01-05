# 排序数组中所有可能的 K 长度子序列的中间值的最小和

> 原文:[https://www . geeksforgeeks . org/所有可能的 k 长度排序数组的子序列的最小中值之和/](https://www.geeksforgeeks.org/minimum-sum-of-medians-of-all-possible-k-length-subsequences-of-a-sorted-array/)

给定一个排序的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**由 **N** 个整数和一个正整数 **K** (使得 **N%K** 为 **0** )组成，任务是找到大小为 K**的所有可能子序列的[中值的最小和，使得每个元素只属于一个子序列。](https://www.geeksforgeeks.org/median-of-all-non-empty-subset-sums/)**

**示例:**

> **输入:** arr[] = {1，2，3，4，5，6}，K = 2
> **输出:** 6
> **解释:**
> 考虑大小为K 的子序列为{1，4}、{2，5}和{3，6}。
> 所有子序列的中值之和为(1 + 2 + 3) = 6，这是最小可能和。
> 
> **输入:** K = 3，arr[] = {3，11，12，22，33，35，38，67，69，71，94，99}，K = 3
> **输出:** 135

**天真方法:**给定的问题可以通过生成所有可能的 **K** 大小的排序子序列并打印所有这些子序列的中值作为结果来解决。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法也可以通过使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来构建所有子序列来优化。其思想是从数组的开始处选择 **K/2** 元素，从数组的结束处选择 **K/2** 元素，这样中间值总是出现在第一部分。按照以下步骤解决问题:

*   初始化一个变量，比如说 **res** ，它存储中间值的和。
*   初始化一个变量，说 **T** 为 **N/K** 存储所需的子序列数，说一个变量 **D** 为 **(K + 1)/2** 存储中间值之间的距离。
*   初始化一个变量，说 **i** 为**(D–1)**来存储第一个[中值](https://www.geeksforgeeks.org/array-data-structure/)的索引以添加到结果中。
*   [迭代至 **i < N** 和**T>0**T5】的值，执行以下步骤:](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)
    *   将**arr【I】**的值添加到变量 **res** 中。
    *   将 **i** 的值增加 **D** 得到下一个中位数的指数。
    *   将 **T** 的值减少 **1** 。
*   完成上述步骤后，打印 **res** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum sum of
// all the medians of the K sized sorted
// arrays formed from the given array
void sumOfMedians(int arr[], int N,
                  int K)
{
    // Stores the distance between
    // the medians
    int selectMedian = (K + 1) / 2;

    // Stores the number of subsequences
    // required
    int totalArrays = N / K;

    // Stores the resultant sum
    int minSum = 0;

    // Iterate from start and add
    // all the medians
    int i = selectMedian - 1;
    while (i < N and totalArrays != 0) {

        // Add the value of arr[i]
        // to the variable minsum
        minSum = minSum + arr[i];

        // Increment i by select the
        // median to get the next
        // median index
        i = i + selectMedian;

        // Decrement the value of
        // totalArrays by 1
        totalArrays--;
    }

    // Print the resultant minimum sum
    cout << minSum;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int N = sizeof(arr) / sizeof(int);
    int K = 2;
    sumOfMedians(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function to find the minimum sum of
    // all the medians of the K sized sorted
    // arrays formed from the given array
    static void sumOfMedians(int arr[], int N, int K)
    {
        // Stores the distance between
        // the medians
        int selectMedian = (K + 1) / 2;

        // Stores the number of subsequences
        // required
        int totalArrays = N / K;

        // Stores the resultant sum
        int minSum = 0;

        // Iterate from start and add
        // all the medians
        int i = selectMedian - 1;
        while (i < N && totalArrays != 0) {

            // Add the value of arr[i]
            // to the variable minsum
            minSum = minSum + arr[i];

            // Increment i by select the
            // median to get the next
            // median index
            i = i + selectMedian;

            // Decrement the value of
            // totalArrays by 1
            totalArrays--;
        }

        // Print the resultant minimum sum
        System.out.println(minSum);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 4, 5, 6 };
        int N = arr.length;
        int K = 2;
        sumOfMedians(arr, N, K);
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum sum of
# all the medians of the K sized sorted
# arrays formed from the given array
def sumOfMedians(arr, N, K):

    # Stores the distance between
    # the medians
    selectMedian = (K + 1) // 2

    # Stores the number of subsequences
    # required
    totalArrays = N // K

    # Stores the resultant sum
    minSum = 0

    # Iterate from start and add
    # all the medians
    i = selectMedian - 1

    while (i < N and totalArrays != 0):

        # Add the value of arr[i]
        # to the variable minsum
        minSum = minSum + arr[i]

        # Increment i by select the
        # median to get the next
        # median index
        i = i + selectMedian

        # Decrement the value of
        # totalArrays by 1
        totalArrays -= 1

     # Print the resultant minimum sum
    print(minSum)

 # Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 3, 4, 5, 6 ]
    N = len(arr)
    K = 2

    sumOfMedians(arr, N, K)

# This code is contributed by nirajgsuain5
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

    // Function to find the minimum sum of
    // all the medians of the K sized sorted
    // arrays formed from the given array
    static void sumOfMedians(int[] arr, int N, int K)
    {

        // Stores the distance between
        // the medians
        int selectMedian = (K + 1) / 2;

        // Stores the number of subsequences
        // required
        int totalArrays = N / K;

        // Stores the resultant sum
        int minSum = 0;

        // Iterate from start and add
        // all the medians
        int i = selectMedian - 1;
        while (i < N && totalArrays != 0) {

            // Add the value of arr[i]
            // to the variable minsum
            minSum = minSum + arr[i];

            // Increment i by select the
            // median to get the next
            // median index
            i = i + selectMedian;

            // Decrement the value of
            // totalArrays by 1
            totalArrays--;
        }

        // Print the resultant minimum sum
        Console.WriteLine(minSum);
    }

// Driver Code
public static void Main()
{
        int[] arr = { 1, 2, 3, 4, 5, 6 };
        int N = arr.Length;
        int K = 2;
        sumOfMedians(arr, N, K);

}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to find the minimum sum of
    // all the medians of the K sized sorted
    // arrays formed from the given array
    function sumOfMedians(arr, N, K)
    {
        // Stores the distance between
        // the medians
        let selectMedian = Math.floor((K + 1) / 2);

        // Stores the number of subsequences
        // required
        let totalArrays =  Math.floor(N / K);

        // Stores the resultant sum
        let minSum = 0;

        // Iterate from start and add
        // all the medians
        let i = selectMedian - 1;
        while (i < N && totalArrays != 0) {

            // Add the value of arr[i]
            // to the variable minsum
            minSum = minSum + arr[i];

            // Increment i by select the
            // median to get the next
            // median index
            i = i + selectMedian;

            // Decrement the value of
            // totalArrays by 1
            totalArrays--;
        }

        // Print the resultant minimum sum
       document.write(minSum);
    }

// Driver Code

        let arr = [ 1, 2, 3, 4, 5, 6 ];
        let N = arr.length;
        let K = 2;
        sumOfMedians(arr, N, K);   

</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)