# 重新排列一个数组，使相似的索引元素不同于另一个数组

> 原文:[https://www . geeksforgeeks . org/重排数组以使相似的索引元素不同于另一个数组/](https://www.geeksforgeeks.org/rearrange-an-array-to-make-similar-indexed-elements-different-from-that-of-another-array/)

给定由 **N** 个不同整数组成的两个排序后的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **A[]** 和 **B[]** ，任务是重新排列数组 **B[]** 的元素，使得对于每个 **i <sup>第</sup>个**索引，**A【I】**不等于**B【I】**。如果存在多个这样的排列，请打印其中任何一个。如果没有这样的排列，打印 **-1** 。

**示例:**

> **输入:** A[] = {2，4，5，8}，B[] = {2，4，5，8}
> **输出:** 4 2 8 5
> **说明:**
> 满足要求条件的可能排列为{4，2，8，5}、{8，5，4，2}和{8，5，4，2}。
> 
> **输入:** A[] = {1，3，4，5}，B[] = {2，4，6，7}
> **输出:** 7 6 2 4

**天真方法:**最简单的方法是找到数组 **B[]** 的所有[可能的排列](https://www.geeksforgeeks.org/iterative-approach-to-print-all-permutations-of-an-array/)，并打印其中的任何排列，使得对于每个**I<sup>th</sup>T9】索引， **A[i])** 不等于 **B[i]** 。**

***时间复杂度:** O(N*N！)*
***辅助空间:** O(N)*

**高效法:**对上述方法进行优化，思路是利用两个数组均由 **N** 个不同元素按升序组成的条件，使用[贪婪法](https://www.geeksforgeeks.org/greedy-algorithms/)找到数组 **B[]** 所需的排列。按照以下步骤解决问题:

*   [反转给定的阵列](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/) **B[]** 。
*   如果 **N** 为**1****A[0]= B[0]**，则打印 **-1** 。
*   否则，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，检查**A【I】**是否等于**B【I】**。
*   如果 **A[i]** 等于 **B[i]** ，将 **B[i]** 换成 **B[i+1]** 并断开回路。
*   完成上述步骤后，打印数组 **B[]** 。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the arrangement
// of array B[] such that element at
// each index of A[] and B[] are not equal
void RearrangeB(int A[], vector<int> B, int n)
{

    // Print not possible, if arrays
    // only have single equal element
    if (n == 1 && A[0] == B[0])
    {
        cout << "-1" << endl;
        return;
    }

    // Reverse array B
    for(int i = 0; i < n / 2; i++)
    {
        int t = B[i];
        B[i] = B[n - i - 1];
        B[n - i - 1] = t;
    }

    // Traverse over arrays to check
    // if there is any index where
    // A[i] and B[i] are equal
    for(int i = 0; i < n - 1; i++)
    {

        // Swap B[i] with B[i - 1]
        if (B[i] == A[i])
        {
            int t = B[i + 1];
            B[i + 1] = B[i];
            B[i] = t;

            // Break the loop
            break;
        }
    }

    // Print required arrangement
    // of array B
    for(int k : B)
        cout << k << " ";
}

// Driver Code
int main()
{

    // Given arrays A[] and B[]
    int A[] = { 2, 4, 5, 8 };
    vector<int> B = { 2, 4, 5, 8 };

    // Length of array A[]
    int n = sizeof(A) / sizeof(A[0]);

    // Function call
    RearrangeB(A, B, n);
}

// This code is contributed by sanjoy_62
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;
import java.lang.*;

class GFG {

    // Function to find the arrangement
    // of array B[] such that element at
    // each index of A[] and B[] are not equal
    static void RearrangeB(int[] A, int[] B)
    {
        // Length of array
        int n = A.length;

        // Print not possible, if arrays
        // only have single equal element
        if (n == 1 && A[0] == B[0]) {
            System.out.println("-1");
            return;
        }

        // Reverse array B
        for (int i = 0; i < n / 2; i++) {
            int t = B[i];
            B[i] = B[n - i - 1];
            B[n - i - 1] = t;
        }

        // Traverse over arrays to check
        // if there is any index where
        // A[i] and B[i] are equal
        for (int i = 0; i < n - 1; i++) {

            // Swap B[i] with B[i - 1]
            if (B[i] == A[i]) {
                int t = B[i + 1];
                B[i + 1] = B[i];
                B[i] = t;

                // Break the loop
                break;
            }
        }

        // Print required arrangement
        // of array B
        for (int k : B)
            System.out.print(k + " ");
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given arrays A[] and B[]
        int[] A = { 2, 4, 5, 8 };
        int[] B = { 2, 4, 5, 8 };

        // Function Call
        RearrangeB(A, B);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the arrangement
# of array B[] such that element at
# each index of A[] and B[] are not equal
def RearrangeB(A, B):

    # Length of array
    n = len(A)

    # Print not possible, if arrays
    # only have single equal element
    if (n == 1 and A[0] == B[0]):
        print(-1)
        return

    # Reverse array B
    for i in range(n // 2):
        t = B[i]
        B[i] = B[n - i - 1]
        B[n - i - 1] = t

    # Traverse over arrays to check
    # if there is any index where
    # A[i] and B[i] are equal
    for i in range(n - 1):

        # Swap B[i] with B[i - 1]
        if (B[i] == A[i]):
            B[i], B[i - 1] = B[i - 1], B[i]
            break

    # Print required arrangement
    # of array B
    for k in B:
        print(k, end = " ")

# Driver Code

# Given arrays A[] and B[]
A = [ 2, 4, 5, 8 ]
B = [ 2, 4, 5, 8 ]

# Function call
RearrangeB(A, B)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to find the arrangement
// of array []B such that element at
// each index of []A and []B
// are not equal
static void RearrangeB(int[] A,
                       int[] B)
{
  // Length of array
  int n = A.Length;

  // Print not possible, if arrays
  // only have single equal element
  if (n == 1 && A[0] == B[0])
  {
    Console.WriteLine("-1");
    return;
  }

  // Reverse array B
  for (int i = 0; i < n / 2; i++)
  {
    int t = B[i];
    B[i] = B[n - i - 1];
    B[n - i - 1] = t;
  }

  // Traverse over arrays to check
  // if there is any index where
  // A[i] and B[i] are equal
  for (int i = 0; i < n - 1; i++)
  {
    // Swap B[i] with B[i - 1]
    if (B[i] == A[i])
    {
      int t = B[i + 1];
      B[i + 1] = B[i];
      B[i] = t;

      // Break the loop
      break;
    }
  }

  // Print required arrangement
  // of array B
  foreach (int k in B)
    Console.Write(k + " ");
}

// Driver Code
public static void Main(String[] args)
{
  // Given arrays []A and []B
  int[] A = {2, 4, 5, 8};
  int[] B = {2, 4, 5, 8};

  // Function Call
  RearrangeB(A, B);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program for the
// above approach

    // Function to find the arrangement
    // of array B[] such that element at
    // each index of A[] and B[] are not equal
    function RearrangeB( A, B)
    {
        // Length of array
        let n = A.length;

        // Print not possible, if arrays
        // only have single equal element
        if (n == 1 && A[0] == B[0]) {
            document.write("-1");
            return;
        }

        // Reverse array B
        for (let i = 0; i < n / 2; i++) {
            let t = B[i];
            B[i] = B[n - i - 1];
            B[n - i - 1] = t;
        }

        // Traverse over arrays to check
        // if there is any index where
        // A[i] and B[i] are equal
        for (let i = 0; i < n - 1; i++) {

            // Swap B[i] with B[i - 1]
            if (B[i] == A[i]) {
                let t = B[i + 1];
                B[i + 1] = B[i];
                B[i] = t;

                // Break the loop
                break;
            }
        }

        // Print required arrangement
        // of array B
        for (let k in B)
            document.write(B[k] + " ");
    }

// Driver Code

     // Given arrays A[] and B[]
        let A = [ 2, 4, 5, 8 ];
        let B = [ 2, 4, 5, 8 ];

        // Function Call
        RearrangeB(A, B);

        // This code is contributed by avijitmondal1998.
</script>
```

**Output:** 

```
8 5 4 2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)