# 将数组分割成最大和最小元素之间最多相差 K 个的最小数量的子集

> 原文:[https://www . geeksforgeeks . org/将数组拆分成最小数量的子集-最多有最大和最小元素之差-k/](https://www.geeksforgeeks.org/split-array-into-minimum-number-of-subsets-having-difference-between-maximum-and-minimum-element-at-most-k/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】【】**，任务是找到集合的最小数量，数组元素可以被划分成使得每个集合的最大和最小元素之间的差最多为**K**。

**示例:**

> **输入:** arr[] = {1，2，3，4，5}，K = 2
> **输出:** 2
> **解释:**
> 给定数组可以分为最大值和最小值之差为 3–1 = 2 的两组{1，2，3}和最大值和最小值之差为 5–4 = 1 的{4，5}。
> 
> **输入:** arr[] = {5，2，9，7，3，2，4，6，14，10}，K = 3
> **输出:** 4

**方法:**给定的问题可以通过[对给定的数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行排序并找到最小数量的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)来解决，数组元素可以被打破，使得最大和最小元素**之间的差最多为 K** 。按照以下步骤解决给定的问题:

*   [按照非递减顺序](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/)对给定数组 **arr[]** 进行排序。
*   初始化两个迭代器**开始**和**结束**为 **0** 代表每个集合的开始和结束。
*   初始化一个变量，比如说**设置计数**为 **1** ，它存储数组元素分解为子数组的最小次数。
*   重复一个循环，直到**结束**的值小于 **N** ，并执行以下步骤:
    1.  如果**arr[end]–arr[begin]<= K**的值，则增加 **end** 的值。
    2.  否则，用 **1** 增加**集合计数**的值，并更新代表新集合的**开始**到**结束**的值。
*   完成以上步骤后，打印**设置计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of sets the array can be divided such
// that for each set max-min <= K
int minSetCount(int arr[], int N, int K)
{
    // Sort the input array
    sort(arr, arr + N);

    // Stores the count of set required
    int setCount = 1;

    // Stores the beginning and ending
    // of the current set
    int begin = 0, end = 0;

    // Loop to iterate over the array
    while (end < N) {

        // If arr[end] can be included
        // in the current set else
        // begin a new set
        if (arr[end] - arr[begin] <= K) {
            end++;
        }
        else {
            // Increment the set count
            setCount++;
            begin = end;
        }
    }

    // Return answer
    return setCount;
}

// Driver Code
int main()
{
    int arr[] = { 5, 2, 9, 7, 3, 2, 4, 6, 14, 10 };
    int N = sizeof(arr) / sizeof(int);
    int K = 3;
    cout << minSetCount(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG {

    // Function to find the minimum number
    // of sets the array can be divided such
    // that for each set max-min <= K
    static int minSetCount(int[] arr, int N, int K)
    {
        // Sort the input array
        Arrays.sort(arr);

        // Stores the count of set required
        int setCount = 1;

        // Stores the beginning and ending
        // of the current set
        int begin = 0, end = 0;

        // Loop to iterate over the array
        while (end < N) {

            // If arr[end] can be included
            // in the current set else
            // begin a new set
            if (arr[end] - arr[begin] <= K) {
                end++;
            }
            else {
                // Increment the set count
                setCount++;
                begin = end;
            }
        }

        // Return answer
        return setCount;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 5, 2, 9, 7, 3, 2, 4, 6, 14, 10 };
        int N = arr.length;
        int K = 3;
        System.out.print(minSetCount(arr, N, K));
    }
}

// This code is contributed by subham348.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the minimum number
# of sets the array can be divided such
# that for each set max-min <= K
def minSetCount(arr, N, K):
    # Sort the input array
    arr.sort()

    # Stores the count of set required
    setCount = 1

    # Stores the beginning and ending
    # of the current set
    begin = 0
    end = 0

    # Loop to iterate over the array
    while (end < N):

        # If arr[end] can be included
        # in the current set else
        # begin a new set
        if (arr[end] - arr[begin] <= K):
            end += 1
        else:
            # Increment the set count
            setCount += 1
            begin = end

    # Return answer
    return setCount

# Driver Code
if __name__ == '__main__':
    arr = [5, 2, 9, 7, 3, 2, 4, 6, 14, 10]
    N = len(arr)
    K = 3
    print(minSetCount(arr, N, K))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

    // Function to find the minimum number
    // of sets the array can be divided such
    // that for each set max-min <= K
    static int minSetCount(int[] arr, int N, int K)
    {

        // Sort the input array
        Array.Sort(arr);

        // Stores the count of set required
        int setCount = 1;

        // Stores the beginning and ending
        // of the current set
        int begin = 0, end = 0;

        // Loop to iterate over the array
        while (end < N) {

            // If arr[end] can be included
            // in the current set else
            // begin a new set
            if (arr[end] - arr[begin] <= K) {
                end++;
            }
            else {
                // Increment the set count
                setCount++;
                begin = end;
            }
        }

        // Return answer
        return setCount;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[] arr = { 5, 2, 9, 7, 3, 2, 4, 6, 14, 10 };
        int N = arr.Length;
        int K = 3;
        Console.WriteLine(minSetCount(arr, N, K));
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the minimum number
        // of sets the array can be divided such
        // that for each set max-min <= K
        function minSetCount(arr, N, K) {
            // Sort the input array
            arr.sort(function (a, b) { return a - b })

            // Stores the count of set required
            let setCount = 1;

            // Stores the beginning and ending
            // of the current set
            let begin = 0, end = 0;

            // Loop to iterate over the array
            while (end < N) {

                // If arr[end] can be included
                // in the current set else
                // begin a new set
                if (arr[end] - arr[begin] <= K) {
                    end++;
                }
                else {
                    // Increment the set count
                    setCount++;
                    begin = end;
                }
            }

            // Return answer
            return setCount;
        }

        // Driver Code
        let arr = [5, 2, 9, 7, 3, 2, 4, 6, 14, 10];
        let N = arr.length;
        let K = 3;
        document.write(minSetCount(arr, N, K));

// This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*