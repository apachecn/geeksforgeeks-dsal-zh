# 找到给定 LCM 的数组子集

> 原文:[https://www . geeksforgeeks . org/find-带有给定 lcm 的数组子集/](https://www.geeksforgeeks.org/find-the-subset-of-array-with-given-lcm/)

给定一个由 **N** 个正整数和一个正整数 **X** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是[找到给定数组](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)的子集，该子集的[最低公倍数(LCM)](https://www.geeksforgeeks.org/program-to-find-lcm-of-two-numbers/) 为 **X** 。如果不存在任何子集，则打印**-1”**。

**示例:**

> **输入:** arr[ ] = {2，4，3，5}，X = 20
> **输出:** {4，5}
> **解释:**
> 考虑子集{4，5}，这个子集的 LCM 为 20(= X)。因此，打印此子集。
> 
> **输入:** arr[ ] = {2，3，4，5}，X = 18
> **输出:** -1

**天真方法:**解决给定问题最简单的方法是[找到给定数组](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)的所有可能子集，如果存在 LCM 为 **X** 的子集，则打印该子集。否则，打印**-1”**。

***时间复杂度:**O(N *(log N)* 2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过使用以下事实进行优化:如果数组元素不是 **X** 的除数，则该元素不能包含在子集内，因为 [LCM](https://www.geeksforgeeks.org/lcm-gq/) 永远不会是 **X** 。按照以下步骤解决问题:

*   初始化一个变量，比如说 **LCM** 为 **1** ，存储结果子集的 LCM。
*   [初始化一个向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/)，比如**子集[]** 来存储结果子集中包含的数组元素。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:
    *   如果当前元素是 **X** 的[除数](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)，则推子集内的元素，取值为 **LCM** 的 LCM。
    *   否则， [**继续迭代**](https://www.geeksforgeeks.org/continue-statement-cpp/) 。
*   完成上述步骤后，如果值 **LCM** 为 **X** ，则[打印数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/) **子集[**作为结果子集。否则，打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the LCM of two
// numbers P and Q
int LCM(int P, int Q)
{
    // Return the value of LCM
    return ((P * Q) / __gcd(P, Q));
}

// Function to find the subset with
// LCM as X
int subsetArrayWithLCM_X(int A[], int N,
                         int X)
{
    // Stores LCM of resultant subset
    int lcm = 1;

    // Stores elements of subset
    vector<int> subset;

    // Traverse the array A[]
    for (int i = 0; i < N; i++) {

        // Check if the current element
        // is a divisor of X
        if (X % A[i] == 0) {

            // Inserting it into subset
            subset.push_back(A[i]);

            // Update the lcm
            lcm = LCM(lcm, A[i]);
        }
    }

    // Check if the final LCM is
    // not equal to X
    if (X != lcm) {
        cout << "-1";
        return 0;
    }

    // Otherwise, print the subset
    for (int i = 0; i < subset.size(); i++) {
        cout << subset[i] << ' ';
    }

    return 0;
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 4, 5 };
    int X = 20;
    int N = sizeof(arr) / sizeof(arr[0]);
    subsetArrayWithLCM_X(arr, N, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to find the LCM of two
    // numbers P and Q
    static int LCM(int P, int Q)
    {

        // Return the value of LCM
        return ((P * Q) / __gcd(P, Q));
    }

    // Function to find the subset with
    // LCM as X
    static int subsetArrayWithLCM_X(int A[], int N, int X)
    {

        // Stores LCM of resultant subset
        int lcm = 1;

        // Stores elements of subset
        Vector<Integer> subset = new Vector<Integer>();

        // Traverse the array A[]
        for (int i = 0; i < N; i++) {

            // Check if the current element
            // is a divisor of X
            if (X % A[i] == 0) {

                // Inserting it into subset
                subset.add(A[i]);

                // Update the lcm
                lcm = LCM(lcm, A[i]);
            }
        }

        // Check if the final LCM is
        // not equal to X
        if (X != lcm) {
            System.out.print("-1");
            return 0;
        }

        // Otherwise, print the subset
        for (int i = 0; i < subset.size(); i++) {
            System.out.print(subset.get(i) + " ");
        }

        return 0;

    }

    static int __gcd(int a, int b) {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Driver Code
    public static void main(String[] args) {
        int arr[] = { 2, 3, 4, 5 };
        int X = 20;
        int N = arr.length;
        subsetArrayWithLCM_X(arr, N, X);

    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program for the above approach
from math import gcd

# Function to find the LCM of two
# numbers P and Q
def LCM(P, Q):

    # Return the value of LCM
    return ((P * Q) // gcd(P, Q))

# Function to find the subset with
# LCM as X
def subsetArrayWithLCM_X(A, N, X):

    # Stores LCM of resultant subset
    lcm = 1

    # Stores elements of subset
    subset = []

    # Traverse the array A[]
    for i in range(N):

        # Check if the current element
        # is a divisor of X
        if (X % A[i] == 0):

            # Inserting it into subset
            subset.append(A[i])

            # Update the lcm
            lcm = LCM(lcm, A[i])

    # Check if the final LCM is
    # not equal to X
    if (X != lcm):
        print("-1")
        return 0

    # Otherwise, print the subset
    for i in range(len(subset)):
        print(subset[i],end = ' ')

    return 0

# Driver Code
if __name__ == '__main__':
    arr = [2, 3, 4, 5]
    X = 20
    N = len(arr)
    subsetArrayWithLCM_X(arr, N, X)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG {

    // Function to find the LCM of two
    // numbers P and Q
    static int LCM(int P, int Q)
    {

        // Return the value of LCM
        return ((P * Q) / __gcd(P, Q));
    }

    // Function to find the subset with
    // LCM as X
    static int subsetArrayWithLCM_X(int []A, int N, int X)
    {

        // Stores LCM of resultant subset
        int lcm = 1;

        // Stores elements of subset
        List<int> subset = new List<int>();

        // Traverse the array []A
        for (int i = 0; i < N; i++) {

            // Check if the current element
            // is a divisor of X
            if (X % A[i] == 0) {

                // Inserting it into subset
                subset.Add(A[i]);

                // Update the lcm
                lcm = LCM(lcm, A[i]);
            }
        }

        // Check if the readonly LCM is
        // not equal to X
        if (X != lcm) {
            Console.Write("-1");
            return 0;
        }

        // Otherwise, print the subset
        for (int i = 0; i < subset.Count; i++) {
            Console.Write(subset[i] + " ");
        }

        return 0;

    }

    static int __gcd(int a, int b) {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Driver Code
    public static void Main(String[] args) {
        int []arr = { 2, 3, 4, 5 };
        int X = 20;
        int N = arr.Length;
        subsetArrayWithLCM_X(arr, N, X);

    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the LCM of two
// numbers P and Q
function gcd(a, b)
{

    // Everything divides 0
    if (a == 0)
        return b;
    if (b == 0)
        return a;

    // Base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcd(a - b, b);

    return gcd(a, b - a);
}

// Function to find the LCM of two
// numbers P and Q
function LCM(P, Q)
{

    // Return the value of LCM
    return ((P * Q) / gcd(P, Q));
}

// Function to find the subset with
// LCM as X
function subsetArrayWithLCM_X(A, N, X)
{

    // Stores LCM of resultant subset
    let lcm = 1;

    // Stores elements of subset
    let subset = [];

    // Traverse the array A[]
    for(let i = 0; i < N; i++)
    {

        // Check if the current element
        // is a divisor of X
        if (X % A[i] == 0)
        {

            // Inserting it into subset
            subset.push(A[i]);

            // Update the lcm
            lcm = LCM(lcm, A[i]);
        }
    }

    // Check if the final LCM is
    // not equal to X
    if (X != lcm)
    {
        document.write("-1");
        return 0;
    }

    // Otherwise, print the subset
    for(let i = 0; i < subset.length; i++)
    {
        document.write(subset[i] + ' ');
    }
    return 0;
}

// Driver Code
let arr = [ 2, 3, 4, 5 ];
let X = 20;
let N = arr.length;

subsetArrayWithLCM_X(arr, N, X);

// This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
2 4 5
```

***时间复杂度:** O(N*log M)，其中 M 为* [*阵的最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*
***辅助空间:** O(N)*