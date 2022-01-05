# 通过重新排列第二个数组

，将两个数组的相同索引元素之和减少到小于 K

> 原文:[https://www . geeksforgeeks . org/通过重新排列第二个数组将两个数组的相同索引元素之和减少到小于 k/](https://www.geeksforgeeks.org/reduce-sum-of-same-indexed-elements-of-two-arrays-to-less-than-k-by-rearranging-the-second-array/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr1[]** 和 **arr2[]** ，大小均为 **N** 和一个整数 **X** ，任务是在重新排列第二个数组后，检查两个数组在相应索引处的相同索引元素的和是否最多可为**。如果可能，则打印**“是”**否则打印**“否”**。**

**示例:**

> **输入:** arr1[] = {1，2，3}，arr2[] = {1，1，2}，X = 4
> **输出:**是
> **解释:**
> 将数组 B[]重新排列为{1，2，1}。现在对应的指标之和为:
> A[0]+B[0]= 1+1 = 2≤4
> A[1]+B[1]= 2+2 = 4≤4
> A[2]+B[2]= 3+1 = 4≤4
> 
> **输入:** arr1[] = {1，2，3，4}，arr2[] = {1，2，3，4}，X = 4
> **输出:**否
> **说明:**数组 B[]不可能重新排列，使得条件 A[i] + B[i] < = X 满足。

**天真方法:**最简单的方法是[生成数组 **B[]** 的所有可能排列](https://www.geeksforgeeks.org/all-permutations-of-an-array-using-stl-in-c/)，如果有任何排列满足给定条件，则打印**是**。否则，打印**否**。

***时间复杂度:** O(N！)*
***辅助空间:** O(1)*

**高效途径:**优化上述途径，思路是使用[排序](https://www.geeksforgeeks.org/sorting-algorithms/)。按照以下步骤解决问题:

*   [将数组 **arr1[]** 按升序排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)和 **arr2[]** 按降序排序。
*   现在，[同时遍历两个数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，如果存在任何一对使得 **arr1[i]** 和 **arr2[]** 之和超过 **X** ，则打印**“否”**。否则，打印**“是”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if elements
// of B[] can be rearranged
// such that A[i] + B[i] <= X
void rearrange(int A[], int B[],
               int N, int X)
{
    // Checks the given condition
    bool flag = true;

    // Sort A[] in ascending order
    sort(A, A + N);

    // Sort B[] in descending order
    sort(B, B + N, greater<int>());

    // Traverse the arrays A[] and B[]
    for (int i = 0; i < N; i++) {

        // If A[i] + B[i] exceeds X
        if (A[i] + B[i] > X) {

            // Rearrangement not possible,
            // set flag to false
            flag = false;
            break;
        }
    }

    // If flag is true
    if (flag)
        cout << "Yes";

    // Otherwise
    else
        cout << "No";
}

// Driver Code
int main()
{
    int A[] = { 1, 2, 3 };
    int B[] = { 1, 1, 2 };
    int X = 4;
    int N = sizeof(A) / sizeof(A[0]);

    // Function Call
    rearrange(A, B, N, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Function to check if elements
  // of B[] can be rearranged
  // such that A[i] + B[i] <= X
  static void rearrange(int A[], int B[],
                        int N, int X)
  {

    // Checks the given condition
    boolean flag = true;

    // Sort A[] in ascending order
    Arrays.sort(A);

    // Sort B[] in descending order
    Arrays.sort(B);

    // Traverse the arrays A[] and B[]
    for (int i = 0; i < N; i++)
    {

      // If A[i] + B[i] exceeds X
      if (A[i] + B[N - 1 - i] > X)
      {

        // Rearrangement not possible,
        // set flag to false
        flag = false;
        break;
      }
    }

    // If flag is true
    if (flag == true)
      System.out.print("Yes");

    // Otherwise
    else
      System.out.print("No");
  }

  // Driver Code
  public static void main (String[] args)
  {
    int A[] = { 1, 2, 3 };
    int B[] = { 1, 1, 2 };
    int X = 4;
    int N = A.length;

    // Function Call
    rearrange(A, B, N, X);
  }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if elements
# of B can be rearranged
# such that A[i] + B[i] <= X
def rearrange(A, B, N, X):

    # Checks the given condition
    flag = True

    # Sort A in ascending order
    A = sorted(A)

    # Sort B in descending order
    B = sorted(B)[::-1]

    # Traverse the arrays A and B
    for i in range(N):

        # If A[i] + B[i] exceeds X
        if (A[i] + B[i] > X):

            # Rearrangement not possible,
            # set flag to false
            flag = False
            break

    # If flag is true
    if (flag):
        print("Yes")

    # Otherwise
    else:
        print("No")

# Driver Code
if __name__ == '__main__':
    A = [ 1, 2, 3 ]
    B = [ 1, 1, 2 ]
    X = 4
    N = len(A)

    # Function Call
    rearrange(A, B, N, X)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to check if elements
  // of B[] can be rearranged
  // such that A[i] + B[i] <= X
  static void rearrange(int[] A, int[] B,
                        int N, int X)
  {

    // Checks the given condition
    bool flag = true;

    // Sort A[] in ascending order
    Array.Sort(A);

    // Sort B[] in descending order
    Array.Sort(B);

    // Traverse the arrays A[] and B[]
    for (int i = 0; i < N; i++)
    {

      // If A[i] + B[i] exceeds X
      if (A[i] + B[N - 1 - i] > X)
      {

        // Rearrangement not possible,
        // set flag to false
        flag = false;
        break;
      }
    }

    // If flag is true
    if (flag == true)
      Console.WriteLine("Yes");

    // Otherwise
    else
      Console.WriteLine("No");
  }

  // Driver Code
  public static void Main()
  {
    int []A = { 1, 2, 3 };
    int []B = { 1, 1, 2 };
    int X = 4;
    int N = A.Length;

    // Function Call
    rearrange(A, B, N, X);
  }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// Javascript program of the above approach

// Function to check if elements
// of B[] can be rearranged
// such that A[i] + B[i] <= X
function rearrange(A, B, N, X)
{

    // Checks the given condition
    let flag = true;

    // Sort A[] in ascending order
    A.sort();

    // Sort B[] in descending order
    B.sort();

    // Traverse the arrays A[] and B[]
    for(let i = 0; i < N; i++)
    {

        // If A[i] + B[i] exceeds X
        if (A[i] + B[N - 1 - i] > X)
        {

            // Rearrangement not possible,
            // set flag to false
            flag = false;
            break;
        }
    }

    // If flag is true
    if (flag == true)
        document.write("Yes");

    // Otherwise
    else
        document.write("No");
}

// Driver Code
let A = [ 1, 2, 3 ];
let B = [ 1, 1, 2 ];
let X = 4;
let N = A.length;

// Function Call
rearrange(A, B, N, X);

// This code is contributed by avijitmondal1998

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*