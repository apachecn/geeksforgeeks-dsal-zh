# 求 K 的最小值，使指数中的元素之和最大化，指数是 K 的倍数

> 原文:[https://www . geeksforgeeks . org/find-最小 k 值-最大化 k 倍数指数上的元素总和/](https://www.geeksforgeeks.org/find-minimum-value-of-k-to-maximise-sum-of-elements-on-indices-that-are-multiples-of-k/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到 **K** 的最小值，使得指数上的元素之和是 **K** 的倍数是最大可能的。

**示例:**

> **输入:** arr[] = {-3，4}
> **输出:** 2
> **解释:**对于给定的数组，它取 K = 1 的值，那么 K 的倍数为{1，2}，其和为 arr[1] + arr[2] = -3 + 4 = 1。对于 K = 2，K 的有效倍数为 2，因此总和为 arr[2] = 4，这是最大可能值。因此，K = 2 是一个有效答案。
> 
> **输入:** arr[] = {-1，-2，-3 }
> T3】输出: 2

**方法:**给定的问题可以用类似于厄拉多塞的[筛的方法来解决。其思想是通过迭代 **K** 的每个倍数来计算**【1，N】**范围内 **K** 的所有可能值的总和，就像在筛子中标记非素元素时所做的那样。给出最大和的 **K** 的值就是需要的答案。](http://www.geeksforgeeks.org/sieve-of-eratosthenes/)

下面是上述方法的实现:

## C++

```
// C++ Program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum K such that
// the sum of elements on indices that
// are multiples of K is maximum possible
int maxSum(int arr[], int N)
{
    // Stores the maximum sum and
    // respective K value
    int maxSum = INT_MIN, ans = -1;

    // Loop to iterate over all
    // value of K in range [1, N]
    for (int K = 1; K <= N; K++) {
        int sum = 0;

        // Iterating over all
        // multiples of K
        for (int i = K; i <= N; i += K) {
            sum += arr[i - 1];
        }

        // Update Maximum Sum
        if (sum > maxSum) {
            maxSum = sum;
            ans = K;
        }
    }

    // Return Answer
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { -1, -2, -3 };
    int N = sizeof(arr) / sizeof(int);

    cout << maxSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find minimum K such that
// the sum of elements on indices that
// are multiples of K is maximum possible
static int maxSum(int arr[], int N)
{

    // Stores the maximum sum and
    // respective K value
    int maxSum = Integer.MIN_VALUE, ans = -1;

    // Loop to iterate over all
    // value of K in range [1, N]
    for(int K = 1; K <= N; K++)
    {
        int sum = 0;

        // Iterating over all
        // multiples of K
        for(int i = K; i <= N; i += K)
        {
            sum += arr[i - 1];
        }

        // Update Maximum Sum
        if (sum > maxSum)
        {
            maxSum = sum;
            ans = K;
        }
    }

    // Return Answer
    return ans;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { -1, -2, -3 };
    int N = arr.length;

    System.out.println(maxSum(arr, N));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
      // JavaScript code for the above approach

      // Function to find minimum K such that
      // the sum of elements on indices that
      // are multiples of K is maximum possible
      function maxSum(arr, N) {
          // Stores the maximum sum and
          // respective K value
          let maxSum = -999999;
          let ans = -1;

          // Loop to iterate over all
          // value of K in range [1, N]
          for (let K = 1; K <= N; K++) {
              let sum = 0;

              // Iterating over all
              // multiples of K
              for (let i = K; i <= N; i += K) {
                  sum = sum + arr[i - 1];
              }

              // Update Maximum Sum
              if (sum > maxSum) {
                  maxSum = sum;
                  ans = K;
              }
          }

          // Return Answer
          return ans;
      }

      // Driver Code

      let arr = [-1, -2, -3];
      let N = arr.length;

      document.write(maxSum(arr, N));

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
2
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*