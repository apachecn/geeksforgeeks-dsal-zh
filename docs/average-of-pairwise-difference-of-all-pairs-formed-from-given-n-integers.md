# 由给定的 N 个整数形成的所有对的成对差的平均值

> 原文:[https://www . geeksforgeeks . org/由给定 n 个整数形成的所有成对差的平均值/](https://www.geeksforgeeks.org/average-of-pairwise-difference-of-all-pairs-formed-from-given-n-integers/)

给定一个包含 **N** 个整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是计算由给定的 **N** 个整数形成的两个元素对之间的差的**平均值**。

**示例:**

> **输入:** arr[] = {-1，3，-5，4}
> **输出:** 5.166667
> **解释:**给定数组中有 6 个可能的点对，成对差为:diff(-1，3) = 4，diff(-1，-5) = 4，diff(-1，4) = 5，diff(3，-5) = 8，diff(3，4) = 1，diff(-5，4) = 9。因此，平均成对差值为(4 + 4 + 5 + 8 + 1 + 9)/6 = 31/6 = 5.166667。
> 
> **输入:** arr[] = { -1，2，-3，7，-6 }
> 输出: 6.2

**进场:**这个问题可以用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)和[前缀求和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)的方法解决。如果[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**中的点按排序顺序排列，那么 i <sup>第</sup>个点到所有更大点的距离之和可以计算为:**(arr[I+1]–arr[I])+(arr[I+2]–arr[I])……+(arr[N-1]–arr[I])**=>**(arr[I+1]+arr[I+2]……利用这一观察，可以使用以下步骤来解决给定的问题:**

*   最初[按照非递减顺序对数组](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/) **arr[]** 进行排序。
*   创建一个[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) **前置[]** 的数组 **arr[]** 。
*   遍历每个索引 **i** 并将**(pre[N–1]–pre[I])–arr[I]*(N–1–I)**添加到变量 **ans** 中。
*   要求的答案是 **ans /配对数** = > **ans / (N*(N-1)/2)** 。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find average distance
// between given points on a line
long double averageDistance(
  vector<int> arr, int N)
{
    // Sorting the array arr[]
    sort(arr.begin(), arr.end());

    // Stores the prefix sum
    // array of arr[]
    int pre[N] = { 0 };
    pre[0] = arr[0];

    // Loop to calculate prefix sum
    for (int i = 1; i < N; i++) {
        pre[i] = pre[i - 1] + arr[i];
    }

    // Initialising the answer variable
    long double ans = 0;

    // Loop to iterate through arr[]
    for (int i = 0; i < N - 1; i++) {

        // Adding summation of all
        // distances from ith point
        ans += (pre[N - 1] - pre[i])
          - arr[i] * (N - 1 - i);
    }

    // Return Average
    return ans / ((N * (N - 1)) / 2);
}

// Driver Code
int main()
{
    vector<int> arr = { -1, 3, -5, 4 };
    cout << averageDistance(arr, arr.size());

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.util.*;
class GFG {

    // Function to find average distance
    // between given points on a line
    static double averageDistance(int[] arr, int N)
    {
        // Sorting the array arr[]
        Arrays.sort(arr);

        // Stores the prefix sum
        // array of arr[]
        int[] pre = new int[N];
        pre[0] = arr[0];

        // Loop to calculate prefix sum
        for (int i = 1; i < N; i++) {
            pre[i] = pre[i - 1] + arr[i];
        }

        // Initialising the answer variable
        double ans = 0;

        // Loop to iterate through arr[]
        for (int i = 0; i < N - 1; i++) {

            // Adding summation of all
            // distances from ith point
            ans += (pre[N - 1] - pre[i])
                   - arr[i] * (N - 1 - i);
        }

        // Return Average
        ans = (ans / ((N * (N - 1)) / 2));
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { -1, 3, -5, 4 };

        System.out.print(String.format(
            "%.5f", averageDistance(arr, arr.length)));
    }
}

// This code is contributed by ukasp.
```

## 蟒蛇 3

```
# Python3 program for above approach

# Function to find average distance
# between given points on a line
def averageDistance(arr, N):

    # Sorting the array arr[]
    arr.sort()

    # Stores the prefix sum
    # array of arr[]
    pre = [0 for _ in range(N)]
    pre[0] = arr[0]

    # Loop to calculate prefix sum
    for i in range(1, N):
        pre[i] = pre[i - 1] + arr[i]

    # Initialising the answer variable
    ans = 0

    # Loop to iterate through arr[]
    for i in range(0, N - 1):

        # Adding summation of all
        # distances from ith point
        ans += ((pre[N - 1] - pre[i]) -
               (arr[i] * (N - 1 - i)))

    # Return Average
    return ans / ((N * (N - 1)) / 2)

# Driver Code
if __name__ == "__main__":

    arr = [ -1, 3, -5, 4 ]

    print(averageDistance(arr, len(arr)))

# This code is contributed by rakeshsahni
```

## C#

```
// C# implementation for the above approach
using System;
class GFG
{

// Function to find average distance
// between given points on a line
static double averageDistance(
  int []arr, int N)
{
    // Sorting the array arr[]
    Array.Sort(arr);

    // Stores the prefix sum
    // array of arr[]
    int []pre = new int[N];
    pre[0] = arr[0];

    // Loop to calculate prefix sum
    for (int i = 1; i < N; i++) {
        pre[i] = pre[i - 1] + arr[i];
    }

    // Initialising the answer variable
    double ans = 0;

    // Loop to iterate through arr[]
    for (int i = 0; i < N - 1; i++) {

        // Adding summation of all
        // distances from ith point
        ans += (pre[N - 1] - pre[i])
          - arr[i] * (N - 1 - i);
    }

    // Return Average
    ans  = Math.Round((ans / ((N * (N - 1)) / 2)), 5);
    return ans;
}

// Driver Code
public static void Main()
{
    int []arr = { -1, 3, -5, 4 };

    Console.Write(averageDistance(arr, arr.Length));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

      // JavaScript Program to implement
      // the above approach

      // Function to find average distance
      // between given points on a line
      function averageDistance(
          arr, N)
      {

          // Sorting the array arr[]
          arr.sort(function (a, b) { return a - b })

          // Stores the prefix sum
          // array of arr[]
          let pre = new Array(N).fill(0);
          pre[0] = arr[0];

          // Loop to calculate prefix sum
          for (let i = 1; i < N; i++) {
              pre[i] = pre[i - 1] + arr[i];
          }

          // Initialising the answer variable
          let ans = 0;

          // Loop to iterate through arr[]
          for (let i = 0; i < N - 1; i++) {

              // Adding summation of all
              // distances from ith point
              ans += (pre[N - 1] - pre[i])
                  - arr[i] * (N - 1 - i);
          }

          // Return Average
          return ans / ((N * (N - 1)) / 2);
      }

      // Driver Code
      let arr = [-1, 3, -5, 4];
      document.write(averageDistance(arr, arr.length).toPrecision(6));

  // This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
5.16667
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*