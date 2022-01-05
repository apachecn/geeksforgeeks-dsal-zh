# 给定和的长度为 K 的唯一子序列

> 原文:[https://www . geeksforgeeks . org/unique-sequence-of-length-k-with-given-sum/](https://www.geeksforgeeks.org/unique-subsequences-of-length-k-with-given-sum/)

给定一个由 **N** 个整数和两个数字 **K** 和 **S** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是打印长度为 **K** 的所有子序列，其和为 **S** 。
**举例:**

> **输入:** N = 5，K = 3，S = 20，arr[] = {4，6，8，2，12}
> **输出:**
> {6，2，12}
> **解释:**
> 只有一个大小为 3 且和为 20 的子序列是可能的，即{6，2，12}，和为 6 + 2 + 12 = 20
> **输入:** N = 10 5，7}
> **输出:**
> {10，1，2，5，7}
> {4，8，1，5，7}
> {4，8，10，1，2}
> {4，6，12，1，2}
> {4，6，8，2，5}
> {2，10，1，5，7}
> {2，8，12，1，2}

**方法:**思路是用[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)打印给定和的所有子序列 **S** 。以下是步骤:

*   迭代数组 **arr[]** 的所有值，并执行以下操作:
    1.  如果我们在结果子序列中包含当前元素，那么将 **K** 和当前元素的上述值减为总和 **S** 。
    2.  递归地从元素的下一个索引迭代到数组的末尾，以找到结果子序列。
    3.  如果 **K 是 0** ， **S 是 0** ，那么我们得到长度为 **K** 的结果子序列之一，并对 **S** 求和，打印这个子序列，并对下一个结果子序列进行回溯。
    4.  如果我们不包含当前元素，那么通过排除当前元素并对数组中的其余元素重复上述过程来找到结果子序列。
*   步骤 3 中的结果数组将给出所有可能的长度子序列 **K** 加上给定的和 **S** 。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find all the subsequences
// of a given length and having sum S
void comb(int* arr, int len, int r,
          int ipos, int* op, int opos,
          int sum)
{

    // Termination condition
    if (opos == r) {

        int sum2 = 0;
        for (int i = 0; i < opos; i++) {

            // Add value to sum
            sum2 = sum2 + op[i];
        }

        // Check if the resultant sum
        // equals to target sum
        if (sum == sum2) {

            // If true
            for (int i = 0; i < opos; i++)

                // Print resultant array
                cout << op[i] << ", ";

            cout << endl;
        }

        // End this recursion stack
        return;
    }
    if (ipos < len) {

        // Check all the combinations
        // using backtracking
        comb(arr, len, r, ipos + 1,
             op, opos, sum);

        op[opos] = arr[ipos];

        // Check all the combinations
        // using backtracking
        comb(arr, len, r, ipos + 1,
             op, opos + 1, sum);
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 4, 6, 8, 2, 12 };
    int K = 3;
    int S = 20;

    int N = sizeof(arr) / sizeof(arr[0]);

    // To store the subsequence
    int op[N] = { 0 };

    // Function Call
    comb(arr, N, K, 0, op, 0, S);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find all the subsequences
// of a given length and having sum S
static void comb(int []arr, int len, int r,
                 int ipos, int[] op, int opos,
                 int sum)
{

    // Termination condition
    if (opos == r)
    {
        int sum2 = 0;
        for(int i = 0; i < opos; i++)
        {

           // Add value to sum
           sum2 = sum2 + op[i];
        }

        // Check if the resultant sum
        // equals to target sum
        if (sum == sum2)
        {

            // If true
            for(int i = 0; i < opos; i++)

               // Print resultant array
               System.out.print(op[i] + ", ");

            System.out.println();
        }

        // End this recursion stack
        return;
    }
    if (ipos < len)
    {

        // Check all the combinations
        // using backtracking
        comb(arr, len, r, ipos + 1,
             op, opos, sum);

        op[opos] = arr[ipos];

        // Check all the combinations
        // using backtracking
        comb(arr, len, r, ipos + 1,
             op, opos + 1, sum);
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 4, 6, 8, 2, 12 };
    int K = 3;
    int S = 20;

    int N = arr.length;

    // To store the subsequence
    int op[] = new int[N];

    // Function Call
    comb(arr, N, K, 0, op, 0, S);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find all the subsequences
# of a given length and having sum S
def comb(arr, Len, r, ipos, op, opos, Sum):

    # Termination condition
    if (opos == r):

        sum2 = 0
        for i in range(opos):

            # Add value to sum
            sum2 = sum2 + op[i]

        # Check if the resultant sum
        # equals to target sum
        if (Sum == sum2):

            # If true
            for i in range(opos):

                # Print resultant array
                print(op[i], end = ", ")

            print()

        # End this recursion stack
        return

    if (ipos < Len):

        # Check all the combinations
        # using backtracking
        comb(arr, Len, r, ipos + 1,
             op, opos, Sum)

        op[opos] = arr[ipos]

        # Check all the combinations
        # using backtracking
        comb(arr, Len, r, ipos + 1, op,
                          opos + 1, Sum)

# Driver code
if __name__ == '__main__':

    # Given array
    arr = [ 4, 6, 8, 2, 12 ]
    K = 3
    S = 20
    N = len(arr)

    # To store the subsequence
    op = [0] * N

    # Function call
    comb(arr, N, K, 0, op, 0, S)

# This code is contributed by himanshu77
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find all the subsequences
// of a given length and having sum S
static void comb(int []arr, int len, int r,
                 int ipos, int[] op, int opos,
                 int sum)
{

    // Termination condition
    if (opos == r)
    {
        int sum2 = 0;
        for(int i = 0; i < opos; i++)
        {

           // Add value to sum
           sum2 = sum2 + op[i];
        }

        // Check if the resultant sum
        // equals to target sum
        if (sum == sum2)
        {

            // If true
            for(int i = 0; i < opos; i++)

               // Print resultant array
               Console.Write(op[i] + ", ");
            Console.WriteLine();
        }

        // End this recursion stack
        return;
    }
    if (ipos < len)
    {

        // Check all the combinations
        // using backtracking
        comb(arr, len, r, ipos + 1,
             op, opos, sum);

        op[opos] = arr[ipos];

        // Check all the combinations
        // using backtracking
        comb(arr, len, r, ipos + 1,
             op, opos + 1, sum);
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 4, 6, 8, 2, 12 };
    int K = 3;
    int S = 20;

    int N = arr.Length;

    // To store the subsequence
    int []op = new int[N];

    // Function call
    comb(arr, N, K, 0, op, 0, S);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find all the subsequences
// of a given length and having sum S
function comb(arr, len, r,
                 ipos, op, opos,
                 sum)
{

    // Termination condition
    if (opos == r)
    {
        let sum2 = 0;
        for(let i = 0; i < opos; i++)
        {

           // Add value to sum
           sum2 = sum2 + op[i];
        }

        // Check if the resultant sum
        // equals to target sum
        if (sum == sum2)
        {

            // If true
            for(let i = 0; i < opos; i++)

               // Prlet resultant array
               document.write(op[i] + ", ");

            document.write();
        }

        // End this recursion stack
        return;
    }
    if (ipos < len)
    {

        // Check all the combinations
        // using backtracking
        comb(arr, len, r, ipos + 1,
             op, opos, sum);

        op[opos] = arr[ipos];

        // Check all the combinations
        // using backtracking
        comb(arr, len, r, ipos + 1,
             op, opos + 1, sum);
    }
}

// Driver Code

    // Given array
    let arr = [ 4, 6, 8, 2, 12 ];
    let K = 3;
    let S = 20;

    let N = arr.length;

    // To store the subsequence
    let op = Array.from({length: N}, (_, i) => 0);

    // Function Call
    comb(arr, N, K, 0, op, 0, S);

// This code is contributed by sanjoy_62.
</script>
```

**输出:**

```
6, 2, 12, 
```

**时间复杂度:** *O(2^N * K)*
***辅助空间** : O(N)*