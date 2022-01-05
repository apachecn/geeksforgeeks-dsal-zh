# 重新排列两个给定的数组，以最大化相同索引元素的总和

> 原文:[https://www . geeksforgeeks . org/重排-两个给定数组-最大化相同索引元素的和/](https://www.geeksforgeeks.org/rearrange-two-given-arrays-to-maximize-sum-of-same-indexed-elements/)

给定两个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **A[]** 和 **B[]** ，任务是通过重新排列数组元素找到[ABS(A[I]–B[I])](https://www.geeksforgeeks.org/abs-labs-llabs-functions-cc/)的最大可能和。

**示例:**

> **输入:** A[] = {1，2，3，4，5}，B[] = {1，2，3，4，5}
> **输出:** 12
> **解释:**
> A[]可能的重排之一是{5，4，3，2，1}。
> B[]可能的重排之一是{1，2，3，4，4}。
> 因此，ABS(A[I]–B[I])的所有可能值之和= { ABS(5–1)+ABS(4–2)+ABS(3–3)+ABS(2–4)+ABS(1–5)} = 12
> 
> **输入:** A[] = {1，2，2，4，5}，B[] = {5，5，6，6}
> **输出:** 13
> **解释:**
> A[]可能的重排之一是{5，4，2，2，1}。
> B[]可能的重排之一是{5，5，5，6，6}。
> 因此，ABS(A[I]–B[I])的所有可能值之和= { ABS(5–5)+ABS(4–5)+ABS(2–5)+ABS(2–6)+ABS(1–6)} = 13

**方法:**按照以下步骤解决问题:

*   [按升序](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/)对数组 **A[]** 进行排序。
*   [按降序排列数组**B[]**](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
*   [遍历两个数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并打印[ABS(A[I]–B[I])](https://www.geeksforgeeks.org/abs-labs-llabs-functions-cc/)所有可能值的总和。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum possible sum
// by rearranging the given array elements
int MaxRearrngeSum(int A[], int B[], int N)
{

    // Sort the array A[]
    // in ascending order
    sort(A, A + N);

    // Sort the array B[]
    // in descending order
    sort(B, B + N,
            greater<int>());

    // Stores maximum possible sum
    // by rearranging array elements        
    int maxSum = 0;

    // Traverse both the arrays
    for (int i = 0; i < N; i++) {

        // Update maxSum
        maxSum += abs(A[i] - B[i]);
    }

    return maxSum;

}

// Driver Code
int main()

{

    int A[] = { 1, 2, 2, 4, 5 };
    int B[] = { 5, 5, 5, 6, 6 };

    int N = sizeof(A) / sizeof(A[0]);

    cout<< MaxRearrngeSum(A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.lang.Math;
import java.util.Arrays;
import java.util.Collections;

class GFG{

// Function to find the maximum possible sum
// by rearranging the given array elements
static int MaxRearrngeSum(Integer A[],
                          Integer B[],
                          int N)
{

    // Sort the array A[]
    // in ascending order
    Arrays.sort(A);

    // Sort the array B[]
    // in descending order
    Arrays.sort(B, Collections.reverseOrder());

    // Stores maximum possible sum
    // by rearranging array elements         
    int maxSum = 0;

    // Traverse both the arrays
    for(int i = 0; i < N; i++)
    {
        // Update maxSum
        maxSum += Math.abs(A[i] - B[i]);
    }
    return maxSum;
}

// Driver code
public static void main (String[] args)
{
    Integer A[] = { 1, 2, 2, 4, 5 };
    Integer B[] = { 5, 5, 5, 6, 6 };

    int N = A.length;

    System.out.println(MaxRearrngeSum(A, B, N));
}
}

// This code is contributed by ujjwalgoel1103
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the maximum possible sum
# by rearranging the given array elements
def MaxRearrngeSum(A, B, N):

    # Sort the array A[]
    # in ascending order
    A.sort()

    # Sort the array B[]
    # in descending order
    B.sort(reverse = True)

    # Stores maximum possible sum
    # by rearranging array elements
    maxSum = 0

    # Traverse both the arrays
    for i in range(N):

        # Update maxSum
        maxSum += abs(A[i] - B[i])

    return maxSum

# Driver Code
if __name__ == "__main__":

    A = [ 1, 2, 2, 4, 5 ]
    B = [ 5, 5, 5, 6, 6 ]

    N = len(A)

    print(MaxRearrngeSum(A, B, N))

# This code is contributed by chitranayal
```

## C#

```
// Java program to implement
// the above approach
using System;

class GFG{

// Function to find the maximum possible sum
// by rearranging the given array elements
static int MaxRearrngeSum(int []A, int []B, int N)
{

    // Sort the array A[]
    // in ascending order
    Array.Sort(A);

    // Sort the array B[]
    // in descending order
    Array.Sort(B);
    Array.Reverse(B);

    // Stores maximum possible sum
    // by rearranging array elements         
    int maxSum = 0;

    // Traverse both the arrays
    for(int i = 0; i < N; i++)
    {

        // Update maxSum
        maxSum += Math.Abs(A[i] - B[i]);
    }
    return maxSum;
}

// Driver code
public static void Main()
{
    int []A = { 1, 2, 2, 4, 5 };
    int []B = { 5, 5, 5, 6, 6 };

    int N = A.Length;

    Console.WriteLine(MaxRearrngeSum(A, B, N));
}
}

// This code is contributed by ipg2016107
```

## java 描述语言

```
<script>
// javascript program for the
// above approach

// Function to find the maximum possible sum
// by rearranging the given array elements
function MaxRearrngeSum(A, B, N)
{

    // Sort the array A[]
    // in ascending order
    A.sort();

    // Sort the array B[]
    // in descending order
    B.sort();
    B.reverse();

    // Stores maximum possible sum
    // by rearranging array elements        
    let maxSum = 0;

    // Traverse both the arrays
    for(let i = 0; i < N; i++)
    {
        // Update maxSum
        maxSum += Math.abs(A[i] - B[i]);
    }
    return maxSum;
}

// Driver Code

  let A = [ 1, 2, 2, 4, 5 ];
  let B = [ 5, 5, 5, 6, 6 ];

    let N = A.length;

    document.write(MaxRearrngeSum(A, B, N));

</script>
```

**Output:** 

```
13
```

***时间复杂度:** O(N * Log N)*
***辅助空间:** O(1)*