# 使一个数组的所有元素成为另一个数组的倍数所需的最小前缀增量

> 原文:[https://www . geeksforgeeks . org/最小前缀增量-要求将数组中的所有元素设为另一个数组的倍数/](https://www.geeksforgeeks.org/minimum-prefix-increments-required-to-make-all-elements-of-an-array-multiples-of-another-array/)

给定两个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **A[]** 和 **B[]** ，任务是通过将前缀子数组增加 **1** 来找到使 **A[i]** 成为 **B[i]** 的倍数所需的最小操作数。

**示例:**

> **输入:** A[ ] = {3，2，9}，B[ ] = {5，7，4}，N = 3
> **输出:** 7
> **解释:**
> 递增{A[0]}两次将 A[ ]修改为{ **5** ，2，9}
> 递增子阵列{A[0]，A[1]两次将 A[]修改为{ **7，4，** 9
> 
> **输入:** A[ ] = {3，4，5，2，5，5，9}，B[ ] = {1，1，9，6，3，8，7}，N = 7
> T3】输出: 22

**方法:**使用[贪婪技术](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。为了使运算次数最少，思路是寻找 **A[i]** 的最近最小的大于或等于元素，它是 **B[i]** 的倍数:

1.  [遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T3【A】从结束到这个开始。
2.  求的最近倍数与 **B[]** 的对应元素之间的最小差 **K** 。
3.  由于 **K** 等于在 **i <sup>第</sup>T10】元素处运算的次数，因此所有元素的值从 **0 <sup>第</sup>T16】索引到 **(i-1) <sup>第</sup>** 索引将增加 **K.******
4.  现在维护一个变量**进位**，它将存储累积增量，因此如果 **i <sup>th</sup>** 元素递增 **K** 次，那么将 **K** 加到**进位**上。
5.  **的值携带**变量将被用来到找到**(I-1)<sup>的新值 **A[]的第**</sup>** 元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum count of operations
// required to make A[i] multiple of B[i] by
// incrementing prefix subarray
int MinimumMoves(int A[], int B[], int N)
{

    // Stores  minimum count of operations
    // required to make A[i] multiple of B[i]
    // by  incrementing prefix subarray
    int totalOperations = 0;

    // Stores the carry
    int carry = 0;

    // Stores minimum difference of
    // correspoinding element in
    // prefix subarray
    int K = 0;

    // Traverse the array
    for (int i = N - 1; i >= 0; i--) {

        // Stores the closest greater or equal number
        // to A[i] which is a multiple of B[i]
        int nearestMultiple = ceil((double)(A[i] + carry)
                                   / (double)(B[i]))
                              * B[i];

        // Stores minimum difference
        K = nearestMultiple - (A[i] + carry);

        // Update totalOperations
        totalOperations += K;

        // Update carry
        carry += K;
    }

    return totalOperations;
}

// Driver Code
int main()
{

    // Input arrays A[] and B[]
    int A[] = { 3, 4, 5, 2, 5, 5, 9 };
    int B[] = { 1, 1, 9, 6, 3, 8, 7 };

    // Length of arrays
    int N = sizeof(A) / sizeof(A[0]);

    cout << MinimumMoves(A, B, N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find minimum count of operations
// required to make A[i] multiple of B[i] by
// incrementing prefix subarray
static int MinimumMoves(int A[], int B[], int N)
{

    // Stores  minimum count of operations
    // required to make A[i] multiple of B[i]
    // by  incrementing prefix subarray
    int totalOperations = 0;

    // Stores the carry
    int carry = 0;

    // Stores minimum difference of
    // correspoinding element in
    // prefix subarray
    int K = 0;

    // Traverse the array
    for (int i = N - 1; i >= 0; i--)
    {

        // Stores the closest greater or equal number
        // to A[i] which is a multiple of B[i]
        int nearestMultiple = (int) (Math.ceil((double)(A[i] + carry)
                                   / (double)(B[i]))
                              * B[i]);

        // Stores minimum difference
        K = nearestMultiple - (A[i] + carry);

        // Update totalOperations
        totalOperations += K;

        // Update carry
        carry += K;
    }
    return totalOperations;
}

// Driver Code
public static void main(String[] args)
{

    // Input arrays A[] and B[]
    int A[] = { 3, 4, 5, 2, 5, 5, 9 };
    int B[] = { 1, 1, 9, 6, 3, 8, 7 };

    // Length of arrays
    int N = A.length;
    System.out.print(MinimumMoves(A, B, N) +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import ceil,floor

# Function to find minimum count of operations
# required to make A[i] multiple of B[i] by
# incrementing prefix subarray
def MinimumMoves(A, B, N):

    # Stores  minimum count of operations
    # required to make A[i] multiple of B[i]
    # by  incrementing prefix subarray
    totalOperations = 0

    # Stores the carry
    carry = 0

    # Stores minimum difference of
    # correspoinding element in
    # prefix subarray
    K = 0

    # Traverse the array
    for i in range(N - 1, -1, -1):

        # Stores the closest greater or equal number
        # to A[i] which is a multiple of B[i]
        nearestMultiple = ceil((A[i] + carry)/ B[i])* B[i]

        # Stores minimum difference
        K = nearestMultiple - (A[i] + carry)

        # Update totalOperations
        totalOperations += K

        # Update carry
        carry += K
    return totalOperations

# Driver Code
if __name__ == '__main__':

    # Input arrays A[] and B[]
    A = [3, 4, 5, 2, 5, 5, 9]
    B = [1, 1, 9, 6, 3, 8, 7]

    # Length of arrays
    N = len(A)
    print (MinimumMoves(A, B, N))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find minimum count of operations
// required to make A[i] multiple of B[i] by
// incrementing prefix subarray
static int MinimumMoves(int[] A, int[] B, int N)
{

    // Stores  minimum count of operations
    // required to make A[i] multiple of B[i]
    // by  incrementing prefix subarray
    int totalOperations = 0;

    // Stores the carry
    int carry = 0;

    // Stores minimum difference of
    // correspoinding element in
    // prefix subarray
    int K = 0;

    // Traverse the array
    for (int i = N - 1; i >= 0; i--)
    {

        // Stores the closest greater or equal number
        // to A[i] which is a multiple of B[i]
        int nearestMultiple = (int) (Math.Ceiling((double)(A[i] + carry)
                                   / (double)(B[i]))
                              * B[i]);

        // Stores minimum difference
        K = nearestMultiple - (A[i] + carry);

        // Update totalOperations
        totalOperations += K;

        // Update carry
        carry += K;
    }
    return totalOperations;
}

// Driver Code
public static void Main(string[] args)
{
    // Input arrays A[] and B[]
    int[] A = { 3, 4, 5, 2, 5, 5, 9 };
    int[] B = { 1, 1, 9, 6, 3, 8, 7 };

    // Length of arrays
    int N = A.Length;
    Console.Write(MinimumMoves(A, B, N) +"\n");
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
// javascript program of the above approach

// Function to find minimum count of operations
// required to make A[i] multiple of B[i] by
// incrementing prefix subarray
function MinimumMoves(A, B, N)
{

    // Stores  minimum count of operations
    // required to make A[i] multiple of B[i]
    // by  incrementing prefix subarray
    let totalOperations = 0;

    // Stores the carry
    let carry = 0;

    // Stores minimum difference of
    // correspoinding element in
    // prefix subarray
    let K = 0;

    // Traverse the array
    for (let i = N - 1; i >= 0; i--)
    {

        // Stores the closest greater or equal number
        // to A[i] which is a multiple of B[i]
        let nearestMultiple =  (Math.ceil((A[i] + carry)
                                   / (B[i]))
                              * B[i]);

        // Stores minimum difference
        K = nearestMultiple - (A[i] + carry);

        // Update totalOperations
        totalOperations += K;

        // Update carry
        carry += K;
    }
    return totalOperations;
}

    // Driver Code

    // Input arrays A[] and B[]
    let A = [ 3, 4, 5, 2, 5, 5, 9 ];
    let B = [ 1, 1, 9, 6, 3, 8, 7 ];

    // Length of arrays
    let N = A.length;
    document.write(MinimumMoves(A, B, N) + "<br/>");

</script>
```

**Output:** 

```
22
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)