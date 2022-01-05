# 计算给定范围内的数字，该范围可以表示为数字的总和乘以数字的幂

> 原文:[https://www . geeksforgeeks . org/count-numbers-from-a-给定范围-可以表示为位数总和-提高到位数的幂/](https://www.geeksforgeeks.org/count-numbers-from-a-given-range-that-can-be-expressed-as-sum-of-digits-raised-to-the-power-of-count-of-digits/)

给定一个由形式为 **{L，R}** 的查询组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，每个查询的任务是计算范围**【L，R】**中的数字，该范围可以表示为其数字的[和乘以数字](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)[的](https://www.geeksforgeeks.org/program-count-digits-integer-3-different-methods/)的幂。

**示例:**

> **输入:** arr[][] = {{8，11}}
> **输出:** 2
> **说明:**
> 从给定的范围[1，9]中，可以表示为其位数的和乘以位数的幂的数是:
> 
> 1.  8:位数总和= 8，位数计数= 1。因此，8 <sup>1</sup> 等于给定的数。
> 2.  9:位数总和= 9，位数计数= 1。因此，9 <sup>1</sup> 等于给定的数。
> 
> 因此，给定范围内此类数字的计数为 2。
> 
> **输入:** arr[][] = {{10，100}，{1，400}}
> **输出:** 0 11

**天真方法:**最简单的方法是对每个查询迭代 **arr[i][0]** 到 **arr[i][1]** 的范围，并打印这些数字的计数。

***时间复杂度:**O(Q *(R–L)* log<sub>10</sub>R，其中 R 和 L 表示最大范围的界限。*
***辅助空间:** O(1)*

**有效方法:**上述方法可以通过预先计算和存储所有数字来优化，无论它们是否可以表示为其数字的[和上升到数字](https://www.geeksforgeeks.org/finding-sum-of-digits-of-a-number-until-sum-becomes-single-digit/)的[计数的](https://www.geeksforgeeks.org/c-program-to-count-the-digits-of-a-number/)[次方](https://www.geeksforgeeks.org/power-function-cc/)。最后，高效地打印每个查询的计数。
按照以下步骤解决问题:

*   初始化一个辅助数组，比如说 **ans[]** ，在 ans[i]处存储，我是否可以表示为其数字的[和上升到](https://www.geeksforgeeks.org/finding-sum-of-digits-of-a-number-until-sum-becomes-single-digit/)[的](https://www.geeksforgeeks.org/c-program-to-count-the-digits-of-a-number/)[幂](https://www.geeksforgeeks.org/power-function-cc/)的数字之和。
*   迭代范围**【1，10<sup>6</sup>**并相应更新阵**ans【】**。
*   将数组 **ans[]** 转换为[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。
*   [遍历给定的查询数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr[]**，对于每个查询 **{arr[i][0]，arr[i][1]}** ，打印**的值(ans[arr[I][1]–ans[arr[I][1]–1])**作为数字的结果计数，该计数可以表示为其数字的总和乘以数字计数的幂。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

#define R 100005
int arr[R];

// Function to check if a number N can be
// expressed as sum of its digits raised
// to the power of the count of digits
bool canExpress(int N)
{
    int temp = N;

    // Stores the number of digits
    int n = 0;

    while (N != 0) {
        N /= 10;
        n++;
    }

    // Stores the resultant number
    N = temp;

    int sum = 0;

    while (N != 0) {
        sum += pow(N % 10, n);
        N /= 10;
    }

    // Return true if both the
    // numbers are same
    return (sum == temp);
}

// Function to precompute and store
// for all numbers whether they can
// be expressed
void precompute()
{
    // Mark all the index which
    // are plus perfect number
    for (int i = 1; i < R; i++) {

        // If true, then update the
        // value at this index
        if (canExpress(i)) {
            arr[i] = 1;
        }
    }

    // Compute prefix sum of the array
    for (int i = 1; i < R; i++) {
        arr[i] += arr[i - 1];
    }
}

// Function to count array elements that
// can be expressed as the sum of digits
// raised to the power of count of digits
void countNumbers(int queries[][2], int N)
{
    // Precompute the results
    precompute();

    // Traverse the queries
    for (int i = 0; i < N; i++) {

        int L1 = queries[i][0];
        int R1 = queries[i][1];

        // Print the resultant count
        cout << (arr[R1] - arr[L1 - 1])
             << ' ';
    }
}

// Driver Code
int main()
{
    int queries[][2] = {
        { 1, 400 },
        { 1, 9 }
    };
    int N = sizeof(queries)
            / sizeof(queries[0]);
    countNumbers(queries, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.io.*;

class GFG{

static int R = 100005;
static int[] arr = new int[R];

// Function to check if a number N can be
// expressed as sum of its digits raised
// to the power of the count of digits
public static boolean canExpress(int N)
{
    int temp = N;

    // Stores the number of digits
    int n = 0;

    while (N != 0)
    {
        N /= 10;
        n++;
    }

    // Stores the resultant number
    N = temp;

    int sum = 0;

    while (N != 0)
    {
        sum += ((int)Math.pow(N % 10, n));
        N /= 10;
    }

    // Return true if both the
    // numbers are same
      if (sum == temp)
      return true;

    return false;
}

// Function to precompute and store
// for all numbers whether they can
// be expressed
public static void precompute()
{

    // Mark all the index which
    // are plus perfect number
    for(int i = 1; i < R; i++)
    {

        // If true, then update the
        // value at this index
        if (canExpress(i))
        {
            arr[i] = 1;
        }
    }

    // Compute prefix sum of the array
    for(int i = 1; i < R; i++)
    {
        arr[i] += arr[i - 1];
    }
}

// Function to count array elements that
// can be expressed as the sum of digits
// raised to the power of count of digits
public static void countNumbers(int[][] queries, int N)
{

    // Precompute the results
    precompute();

    // Traverse the queries
    for(int i = 0; i < N; i++)
    {
        int L1 = queries[i][0];
        int R1 = queries[i][1];

        // Print the resultant count
       System.out.print((arr[R1] - arr[L1 - 1]) + " ");
    }
}

// Driver Code
 public static void main(String args[])
{
    int[][] queries = { { 1, 400 }, { 1, 9 } };
    int N = queries.length;

    // Function call
    countNumbers(queries, N);
}
}

// This code is contributed by zack_aayush
```

## 蟒蛇 3

```
# Python 3 program for the above approach
R = 100005
arr = [0 for i in range(R)]

# Function to check if a number N can be
# expressed as sum of its digits raised
# to the power of the count of digits
def canExpress(N):
    temp = N

    # Stores the number of digits
    n = 0
    while (N != 0):
        N //= 10
        n += 1

    # Stores the resultant number
    N = temp
    sum = 0
    while (N != 0):
        sum += pow(N % 10, n)
        N //= 10

    # Return true if both the
    # numbers are same
    return (sum == temp)

# Function to precompute and store
# for all numbers whether they can
# be expressed
def precompute():

    # Mark all the index which
    # are plus perfect number
    for i in range(1, R, 1):

        # If true, then update the
        # value at this index
        if(canExpress(i)):
            arr[i] = 1

    # Compute prefix sum of the array
    for i in range(1,R,1):
        arr[i] += arr[i - 1]

# Function to count array elements that
# can be expressed as the sum of digits
# raised to the power of count of digits
def countNumbers(queries, N):

    # Precompute the results
    precompute()

    # Traverse the queries
    for i in range(N):
        L1 = queries[i][0]
        R1 = queries[i][1]

        # Print the resultant count
        print((arr[R1] - arr[L1 - 1]),end = " ")

# Driver Code
if __name__ == '__main__':
    queries = [[1, 400],[1, 9]]
    N = len(queries)
    countNumbers(queries, N)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int R = 100005;
static int[] arr = new int[R];

// Function to check if a number N can be
// expressed as sum of its digits raised
// to the power of the count of digits
public static bool canExpress(int N)
{
    int temp = N;

    // Stores the number of digits
    int n = 0;

    while (N != 0)
    {
        N /= 10;
        n++;
    }

    // Stores the resultant number
    N = temp;

    int sum = 0;

    while (N != 0)
    {
        sum += ((int)Math.Pow(N % 10, n));
        N /= 10;
    }

    // Return true if both the
    // numbers are same
      if (sum == temp)
      return true;

    return false;
}

// Function to precompute and store
// for all numbers whether they can
// be expressed
public static void precompute()
{

    // Mark all the index which
    // are plus perfect number
    for(int i = 1; i < R; i++)
    {

        // If true, then update the
        // value at this index
        if (canExpress(i))
        {
            arr[i] = 1;
        }
    }

    // Compute prefix sum of the array
    for(int i = 1; i < R; i++)
    {
        arr[i] += arr[i - 1];
    }
}

// Function to count array elements that
// can be expressed as the sum of digits
// raised to the power of count of digits
public static void countNumbers(int[,] queries, int N)
{

    // Precompute the results
    precompute();

    // Traverse the queries
    for(int i = 0; i < N; i++)
    {
        int L1 = queries[i, 0];
        int R1 = queries[i, 1];

        // Print the resultant count
        Console.Write((arr[R1] - arr[L1 - 1]) + " ");
    }
}

// Driver Code
static public void Main()
{
    int[,] queries = { { 1, 400 }, { 1, 9 } };
    int N = queries.GetLength(0);

    // Function call
    countNumbers(queries, N);
}
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>
// javascript program for the above approach
    var R = 100005;
    var arr = Array(R).fill(0);

    // Function to check if a number N can be
    // expressed as sum of its digits raised
    // to the power of the count of digits
    function canExpress(N) {
        var temp = N;

        // Stores the number of digits
        var n = 0;

        while (N != 0) {
            N = parseInt(N/10);
            n++;
        }

        // Stores the resultant number
        N = temp;

        var sum = 0;

        while (N != 0) {
            sum += Math.pow(N % 10, n);
            N = parseInt(N/10);
        }

        // Return true if both the
        // numbers are same
        return (sum == temp);
    }

    // Function to precompute and store
    // for all numbers whether they can
    // be expressed
    function precompute() {

        // Mark all the index which
        // are plus perfect number
        for (var i = 1; i < R; i++) {

            // If true, then update the
            // value at this index
            if (canExpress(i)) {
                arr[i] = 1;
            }
        }

        // Compute prefix sum of the array
        for (var i = 1; i < R; i++) {
            arr[i] += arr[i - 1];
        }
    }

    // Function to count array elements that
    // can be expressed as the sum of digits
    // raised to the power of count of digits
    function countNumbers(queries , N) {
        // Precompute the results
        precompute();

        // Traverse the queries
        for (var i = 0; i < N; i++) {

            var L1 = queries[i][0];
            var R1 = queries[i][1];

            // Print the resultant count
            document.write((arr[R1] - arr[L1 - 1]) + " ");
        }
    }

    // Driver Code
    var queries = [ [ 1, 400 ], [ 1, 9 ] ];
    var N = queries.length;

    // function call
    countNumbers(queries, N);

// This code is contributed by Princi Singh
</script>
```

**Output:** 

```
12 9
```

***时间复杂度:**O(Q+10<sup>6</sup>)*
***辅助空间:** O(10 <sup>6</sup> )*