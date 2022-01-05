# 两个给定数组中最接近 K 的子集的和

> 原文:[https://www . geeksforgeeks . org/两个给定数组中最接近 k 的子集之和/](https://www.geeksforgeeks.org/sum-of-subsets-nearest-to-k-possible-from-two-given-arrays/)

给定两个分别由 **N** 和 **M** 整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**和**B【】**，以及一个整数 **K** ，任务是通过从数组**A【】**中精确选择一个元素，从数组**B【】****中最多选择两次**元素，找到最接近 **K** 的和。

**示例:**

> **输入:** A[] = {1，7}，B[] = {3，4}，K = 10
> **输出:** 10
> **说明:**
> 选择 A[0]和 A[1] = 3 + 7 = 10 得到的和，和 K = 10 的值最接近。
> 
> **输入:** A[] = {2，3}，B[] = {4，5，30}，K = 18
> **输出:** 17

**方法:**给定的问题可以通过使用[递归](https://www.geeksforgeeks.org/tail-recursion/)来解决，对于每个数组元素**A【I】**，通过找到具有最接近于**(K–A【I】)**的和的数组子集**B【】**的元素的[和。按照以下步骤解决问题:](https://www.geeksforgeeks.org/subset-sum-problem-dp-25/)

*   初始化两个变量，说 **mini** 为 [**INT_MAX**](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) 和 **ans** 为 [**INT_MAX**](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) 存储最小绝对差和最接近 **K** 的值。
*   定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)，比如**find close(arr，I，currSum)** 来寻找最接近 **K** 的数组的子集-和，其中 **i** 是数组中的索引 **B[]** ， **currSum** 存储子集的和。
    *   如果 **i** 的值至少为**M**，则从函数返回。
    *   如果**(currSum–K)**的绝对值小于 **mini** ，则更新 **mini** 的值为**ABS(currSum–K)**，更新 **ans** 的值为 **currSum** 。
    *   如果**(currSum–K)**的绝对值等于 **mini** ，则更新 **ans** 的值为 **ans** 和 **currSum** 的最小值。
    *   调用除元素 **B[i]** 之外的递归函数作为**find close(I+1，currSum)** 。
    *   调用包含元素 **B[i]** 的递归函数一次，作为**find close(I+1，currSum + B[i])** 。
    *   调用包含元素 **B[i]** 的递归函数两次，作为**find close(I+1，currSum + 2*B[i])** 。
*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **A[]** ，对于每个元素调用函数**find close(0，A[i])** 。
*   完成上述步骤后，打印**和**的值作为结果总和。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach

#include <bits/stdc++.h>
using namespace std;

// Stores the sum closest to K
int ans = INT_MAX;

// Stores the minimum absolute difference
int mini = INT_MAX;

// Function to choose the elements
// from the array B[]
void findClosestTarget(int i, int curr,
                       int B[], int M,
                       int K)
{

    // If absolute difference is less
    // then minimum value
    if (abs(curr - K) < mini) {

        // Update the minimum value
        mini = abs(curr - K);

        // Update the value of ans
        ans = curr;
    }

    // If absolute difference between
    // curr and K is equal to minimum
    if (abs(curr - K) == mini) {

        // Update the value of ans
        ans = min(ans, curr);
    }

    // If i is greater than M - 1
    if (i >= M)
        return;

    // Includes the element B[i] once
    findClosestTarget(i + 1, curr + B[i],
                      B, M, K);

    // Includes the element B[i] twice
    findClosestTarget(i + 1, curr + 2 * B[i],
                      B, M, K);

    // Excludes the element B[i]
    findClosestTarget(i + 1, curr, B, M, K);
}

// Function to find a subset sum
// whose sum is closest to K
int findClosest(int A[], int B[],
                int N, int M, int K)
{
    // Traverse the array A[]
    for (int i = 0; i < N; i++) {

        // Function Call
        findClosestTarget(0, A[i], B,
                          M, K);
    }

    // Return the ans
    return ans;
}

// Driver Code
int main()
{
    // Input
    int A[] = { 2, 3 };
    int B[] = { 4, 5, 30 };
    int N = sizeof(A) / sizeof(A[0]);
    int M = sizeof(B) / sizeof(B[0]);
    int K = 18;

    // Function Call
    cout << findClosest(A, B, N, M, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Stores the sum closest to K
    static int ans = Integer.MAX_VALUE;

    // Stores the minimum absolute difference
    static int mini = Integer.MAX_VALUE;

    // Function to choose the elements
    // from the array B[]
    static void findClosestTarget(int i, int curr, int B[],
                                  int M, int K)
    {

        // If absolute difference is less
        // then minimum value
        if (Math.abs(curr - K) < mini) {

            // Update the minimum value
            mini = Math.abs(curr - K);

            // Update the value of ans
            ans = curr;
        }

        // If absolute difference between
        // curr and K is equal to minimum
        if (Math.abs(curr - K) == mini) {

            // Update the value of ans
            ans = Math.min(ans, curr);
        }

        // If i is greater than M - 1
        if (i >= M)
            return;

        // Includes the element B[i] once
        findClosestTarget(i + 1, curr + B[i], B, M, K);

        // Includes the element B[i] twice
        findClosestTarget(i + 1, curr + 2 * B[i], B, M, K);

        // Excludes the element B[i]
        findClosestTarget(i + 1, curr, B, M, K);
    }

    // Function to find a subset sum
    // whose sum is closest to K
    static int findClosest(int A[], int B[], int N, int M,
                           int K)
    {
        // Traverse the array A[]
        for (int i = 0; i < N; i++) {

            // Function Call
            findClosestTarget(0, A[i], B, M, K);
        }

        // Return the ans
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Input
        int A[] = { 2, 3 };
        int B[] = { 4, 5, 30 };
        int N = A.length;
        int M = B.length;
        int K = 18;

        // Function Call
        System.out.print(findClosest(A, B, N, M, K));
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program of the above approach

# Stores the sum closest to K
ans = 10**8

# Stores the minimum absolute difference
mini = 10**8

# Function to choose the elements
# from the array B[]
def findClosestTarget(i, curr, B, M, K):
    global ans, mini

    # If absolute difference is less
    # then minimum value
    if (abs(curr - K) < mini):

        # Update the minimum value
        mini = abs(curr - K)

        # Update the value of ans
        ans = curr

    # If absolute difference between
    # curr and K is equal to minimum
    if (abs(curr - K) == mini):

        # Update the value of ans
        ans = min(ans, curr)

    # If i is greater than M - 1
    if (i >= M):
        return

    # Includes the element B[i] once
    findClosestTarget(i + 1, curr + B[i], B, M, K)

    # Includes the element B[i] twice
    findClosestTarget(i + 1, curr + 2 * B[i], B, M, K)

    # Excludes the element B[i]
    findClosestTarget(i + 1, curr, B, M, K)

# Function to find a subset sum
# whose sum is closest to K
def findClosest(A, B, N, M, K):

    # Traverse the array A[]
    for i in range(N):

        # Function Call
        findClosestTarget(0, A[i], B, M, K)

    # Return the ans
    return ans

# Driver Code
if __name__ == '__main__':

    # Input
    A = [2, 3]
    B = [4, 5, 30]
    N = len(A)
    M = len(B)
    K = 18

    # Function Call
    print (findClosest(A, B, N, M, K))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program of the above approach
using System;
class GFG
{

    // Stores the sum closest to K
    static int ans = Int32.MaxValue;

    // Stores the minimum absolute difference
    static int mini = Int32.MaxValue;

    // Function to choose the elements
    // from the array B[]
    static void findClosestTarget(int i, int curr, int[] B,
                                  int M, int K)
    {

        // If absolute difference is less
        // then minimum value
        if (Math.Abs(curr - K) < mini) {

            // Update the minimum value
            mini = Math.Abs(curr - K);

            // Update the value of ans
            ans = curr;
        }

        // If absolute difference between
        // curr and K is equal to minimum
        if (Math.Abs(curr - K) == mini) {

            // Update the value of ans
            ans = Math.Min(ans, curr);
        }

        // If i is greater than M - 1
        if (i >= M)
            return;

        // Includes the element B[i] once
        findClosestTarget(i + 1, curr + B[i], B, M, K);

        // Includes the element B[i] twice
        findClosestTarget(i + 1, curr + 2 * B[i], B, M, K);

        // Excludes the element B[i]
        findClosestTarget(i + 1, curr, B, M, K);
    }

    // Function to find a subset sum
    // whose sum is closest to K
    static int findClosest(int[] A, int[] B, int N, int M,
                           int K)
    {

        // Traverse the array A[]
        for (int i = 0; i < N; i++) {

            // Function Call
            findClosestTarget(0, A[i], B, M, K);
        }

        // Return the ans
        return ans;
    }

    // Driver Code
    public static void Main()
    {
        // Input
        int[] A = { 2, 3 };
        int[] B = { 4, 5, 30 };
        int N = A.Length;
        int M = B.Length;
        int K = 18;

        // Function Call
        Console.WriteLine(findClosest(A, B, N, M, K));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // Javascript program for the above approach

        // Stores the sum closest to K
        let ans = Number.MAX_SAFE_INTEGER

        // Stores the minimum absolute difference
        let mini = Number.MAX_SAFE_INTEGER

        // Function to choose the elements
        // from the array B[]
        function findClosestTarget(i, curr, B,
            M, K) {

            // If absolute difference is less
            // then minimum value
            if (Math.abs(curr - K) < mini) {
                // Update the minimum value
                mini = Math.abs(curr - K);

                // Update the value of ans
                ans = curr;
            }

            // If absolute difference between
            // curr and K is equal to minimum
            if (Math.abs(curr - K) == mini) {

                // Update the value of ans
                ans = Math.min(ans, curr);
            }

            // If i is greater than M - 1
            if (i >= M)
                return;

            // Includes the element B[i] once
            findClosestTarget(i + 1, curr + B[i], B, M, K);

            // Includes the element B[i] twice
            findClosestTarget(i + 1, curr + 2 * B[i], B, M, K);

            // Excludes the element B[i]
            findClosestTarget(i + 1, curr, B, M, K);
        }

        // Function to find a subset sum
        // whose sum is closest to K
        function findClosest(A, B, N, M, K) {
            // Traverse the array A[]
            for (let i = 0; i < N; i++) {

                // Function Call
                findClosestTarget(0, A[i], B, M, K);
            }

            // Return the ans
            return ans;
        }

        // Driver Code
        // Input
        let A = [2, 3];
        let B = [4, 5, 30];
        let N = A.length;
        let M = B.length;
        let K = 18;

        // Function Call
        document.write(findClosest(A, B, N, M, K));

        //This code is contributed by Hritik.
    </script>
```

**Output:** 

```
17
```

***时间复杂度:**O(N * 3<sup>M</sup>)*
***辅助空间:** O(1)*