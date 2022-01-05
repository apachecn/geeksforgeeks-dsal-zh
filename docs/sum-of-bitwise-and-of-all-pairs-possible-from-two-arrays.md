# 两个数组中所有可能的对的按位“与”的和

> 原文:[https://www . geeksforgeeks . org/两个数组中所有可能的对的按位求和/](https://www.geeksforgeeks.org/sum-of-bitwise-and-of-all-pairs-possible-from-two-arrays/)

给定两个大小分别为 **N** 和 **M** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **A[]** 和 **B[]** ，任务是从这两个数组中找到所有可能的无序对 **(A[i]，B[j])的[位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)之和。**

**示例:**

> **输入:** A[] = {1，2}，B[] = {3，4 }
> T3】输出: 3
> **解释:**
> 所有可能对的按位 AND 为
> 1&3 = 1
> 1&4 = 0
> 2&3 = 2
> 2&4 = 0
> 因此，所有可能对的按位 AND 之和为=(1+0+1)
> 
> **输入:** A[] = {4，6，0，0，3，3}，B[] = {0，5，6，5，0，3}
> **输出:** 42

**方法:**为了解决这个问题，思路是[遍历两个数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[从给定的两个数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中生成所有可能的对，并不断添加它们各自的**位与** s。最后，打印从两个给定数组中获得的所有可能对 **(A[i]，B[j])** 的[和。](https://www.geeksforgeeks.org/calculate-sum-of-bitwise-and-of-all-pairs/)

按照以下步骤解决问题:

*   初始化一个变量，比如说**对和**来存储所有可能对的**位和**的和。
*   遍历两个数组，并从给定的两个数组中生成所有可能的对。
*   最后，计算两个数组中所有可能对的**位“与”**之和，并打印总和。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of
// AND of all possible pair
int sumOfAnd(int A[], int B[],
                int N, int M)
{

    // Stores sum of bitwise AND
    // of  all possible pair
    int pairsAndSum = 0;

    // Traverse the array A[]
    for (int i = 0; i < N; i++) {

       // Traverse the array B[]
        for (int j = 0; j < M;
                           j++) {

            // Update pairsAndSum
            pairsAndSum +=
                   (A[i] & B[j]);
        }
    }

    return pairsAndSum;
}

// Driver Code
int main()
{

    int A[] = { 4, 6, 0, 0, 3, 3 };
    int B[] = { 0, 5, 6, 5, 0, 3 };

    int N = sizeof(A) / sizeof(A[0]);

    int M = sizeof(B) / sizeof(B[0]);

    cout << sumOfAnd(A, B, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG{

// Function to find the sum of
// AND of all possible pair
static int sumOfAnd(int A[], int B[],
                    int N, int M)
{
  // Stores sum of bitwise AND
  // of  all possible pair
  int pairsAndSum = 0;

  // Traverse the array A[]
  for (int i = 0; i < N; i++)
  {
    // Traverse the array B[]
    for (int j = 0; j < M; j++)
    {
      // Update pairsAndSum
      pairsAndSum += (A[i] & B[j]);
    }
  }

  return pairsAndSum;
}

// Driver Code
public static void main(String[] args)
{
  int A[] = {4, 6, 0, 0, 3, 3};
  int B[] = {0, 5, 6, 5, 0, 3};
  int N = A.length;
  int M = B.length;
  System.out.print(sumOfAnd(A, B,
                            N, M));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the sum of
# AND of all possible pair
def sumOfAnd(A, B, N, M):

    # Stores sum of bitwise AND
    # of all possible pair
    pairsAndSum = 0

    # Traverse the array A
    for i in range(N):

        # Traverse the array B
        for j in range(M):

            # Update pairsAndSum
            pairsAndSum += (A[i] & B[j])

    return pairsAndSum

# Driver Code
if __name__ == '__main__':

    A = [ 4, 6, 0, 0, 3, 3 ]
    B = [ 0, 5, 6, 5, 0, 3 ]

    N = len(A)
    M = len(B)

    print(sumOfAnd(A, B, N, M))

# This code is contributed by Amit Katiyar
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

// Function to find the sum of
// AND of all possible pair
static int sumOfAnd(int []A, int []B,
                    int N, int M)
{
  // Stores sum of bitwise AND
  // of  all possible pair
  int pairsAndSum = 0;

  // Traverse the array []A
  for (int i = 0; i < N; i++)
  {
    // Traverse the array []B
    for (int j = 0; j < M; j++)
    {
      // Update pairsAndSum
      pairsAndSum += (A[i] & B[j]);
    }
  }

  return pairsAndSum;
}

// Driver Code
public static void Main(String[] args)
{
  int []A = {4, 6, 0, 0, 3, 3};
  int []B = {0, 5, 6, 5, 0, 3};
  int N = A.Length;
  int M = B.Length;
  Console.Write(sumOfAnd(A, B,
                            N, M));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function to find the sum of
// AND of all possible pair
function sumOfAnd(A, B, N, M)
{

    // Stores sum of bitwise AND
    // of all possible pair
    var pairsAndSum = 0;

    // Traverse the array A[]
    for (var i = 0; i < N; i++) {

    // Traverse the array B[]
        for (var j = 0; j < M;
                        j++) {

            // Update pairsAndSum
            pairsAndSum +=
                (A[i] & B[j]);
        }
    }

    return pairsAndSum;
}

// Driver Code
var A = [ 4, 6, 0, 0, 3, 3 ];
var B = [ 0, 5, 6, 5, 0, 3 ];
var N = A.length;
var M = B.length;

document.write(sumOfAnd(A, B, N, M));

</script>
```

**Output:** 

```
42
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*