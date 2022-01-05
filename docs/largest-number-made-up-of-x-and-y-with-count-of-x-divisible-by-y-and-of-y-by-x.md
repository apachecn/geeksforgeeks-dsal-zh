# 由 X 和 Y 组成的最大数，其中 X 的计数可被 Y 整除，Y 的计数可被 X 整除

> 原文:[https://www . geeksforgeeks . org/x 和 y 的最大组合数 x 的计数可被 y 整除，y 的计数可被 x 整除/](https://www.geeksforgeeks.org/largest-number-made-up-of-x-and-y-with-count-of-x-divisible-by-y-and-of-y-by-x/)

给定三个整数 **X** 、 **Y** 和 **N** ，任务是找到长度 **N** 的最大可能数，该最大可能数仅由 **X** 和 **Y** 作为其数字组成，因此其中的 **X** 的计数可被 **Y** 整除，反之亦然。如果无法形成这样的编号，打印 **-1** 。
**例:**

> **输入:** N = 3，X = 5，Y = 3
> **输出:** 555
> **说明:**
> 5 的计数= 3，可被 3 整除
> 3 的计数= 0
> **输入:** N = 4，X = 7，Y = 5
> **输出:** -1

**进场:**
按照以下步骤解决问题:

*   将 **X** 和 **Y** 中较大的一个视为 **X** ，较小的一个视为 **Y** 。
*   由于编号需要达到 **N** 的长度，请执行以下两个步骤，直到 N ≤ 0:
    *   如果 N 能被 Y 整除，在答案上追加 X，N 次，把 N 减为零。
    *   否则，将 N 减 X，并在答案中追加 Y，X 倍。
*   完成上述步骤后，如果 N <0, then a number of required type is not possible. Print **-1** 。
*   否则，打印答案。

以下是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to generate and return
// the largest number
void largestNumber(int n, int X, int Y)
{
    int maxm = max(X, Y);

    // Store the smaller in Y
    Y = X + Y - maxm;

    // Store the larger in X
    X = maxm;

    // Stores respective counts
    int Xs = 0;
    int Ys = 0;

    while (n > 0) {

        // If N is divisible by Y
        if (n % Y == 0) {

            // Append X, N times to
            // the answer
            Xs += n;

            // Reduce N to zero
            n = 0;
        }
        else {

            // Reduce N by X
            n -= X;

            // Append Y, X times
            // to the answer
            Ys += X;
        }
    }

    // If number can be formed
    if (n == 0) {
        while (Xs-- > 0)
            cout << X;

        while (Ys-- > 0)
            cout << Y;
    }

    // Otherwise
    else
        cout << "-1";
}

// Driver Code
int main()
{
    int n = 19, X = 7, Y = 5;
    largestNumber(n, X, Y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the
// above approach
import java.util.*;

class GFG{

// Function to generate and return
// the largest number
public static void largestNumber(int n, int X,
                                        int Y)
{
    int maxm = Math.max(X, Y);

    // Store the smaller in Y
    Y = X + Y - maxm;

    // Store the larger in X
    X = maxm;

    // Stores respective counts
    int Xs = 0;
    int Ys = 0;

    while (n > 0)
    {

        // If N is divisible by Y
        if (n % Y == 0)
        {

            // Append X, N times to
            // the answer
            Xs += n;

            // Reduce N to zero
            n = 0;
        }
        else
        {
            // Reduce N by X
            n -= X;

            // Append Y, X times
            // to the answer
            Ys += X;
        }
    }

    // If number can be formed
    if (n == 0)
    {
        while (Xs-- > 0)
            System.out.print(X);

        while (Ys-- > 0)
            System.out.print(Y);
    }

    // Otherwise
    else
        System.out.print("-1");
}

// Driver code
public static void main (String[] args)
{
    int n = 19, X = 7, Y = 5;

    largestNumber(n, X, Y);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to generate and return
# the largest number
def largestNumber(n, X, Y):

    maxm = max(X, Y)

    # Store the smaller in Y
    Y = X + Y - maxm

    # Store the larger in X
    X = maxm

    # Stores respective counts
    Xs = 0
    Ys = 0

    while (n > 0):

        # If N is divisible by Y
        if (n % Y == 0):

            # Append X, N times to
            # the answer
            Xs += n

            # Reduce N to zero
            n = 0

        else:

            # Reduce N by x
            n -= X

            # Append Y, X times to
            # the answer
            Ys += X

    # If number can be formed
    if (n == 0):

        while (Xs > 0):
            Xs -= 1
            print(X, end = '')

        while (Ys > 0):
            Ys -= 1
            print(Y, end = '')

    # Otherwise
    else:
        print("-1")

# Driver code
n = 19
X = 7
Y = 5

largestNumber(n, X, Y)

# This code is contributed by himanshu77
```

## C#

```
// C# program to implement the
// above approach
using System;
class GFG{

// Function to generate and return
// the largest number
public static void largestNumber(int n, int X,
                                        int Y)
{
    int maxm = Math.Max(X, Y);

    // Store the smaller in Y
    Y = X + Y - maxm;

    // Store the larger in X
    X = maxm;

    // Stores respective counts
    int Xs = 0;
    int Ys = 0;

    while (n > 0)
    {

        // If N is divisible by Y
        if (n % Y == 0)
        {

            // Append X, N times to
            // the answer
            Xs += n;

            // Reduce N to zero
            n = 0;
        }
        else
        {
            // Reduce N by X
            n -= X;

            // Append Y, X times
            // to the answer
            Ys += X;
        }
    }

    // If number can be formed
    if (n == 0)
    {
        while (Xs-- > 0)
            Console.Write(X);

        while (Ys-- > 0)
            Console.Write(Y);
    }

    // Otherwise
    else
        Console.Write("-1");
}

// Driver code
public static void Main (String[] args)
{
    int n = 19, X = 7, Y = 5;

    largestNumber(n, X, Y);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// Javascript program to implement the
// above approach

// Function to generate and return
// the largest number
function largestNumber(n, X, Y)
{
    let maxm = Math.max(X, Y);

    // Store the smaller in Y
    Y = X + Y - maxm;

    // Store the larger in X
    X = maxm;

    // Stores respective counts
    let Xs = 0;
    let Ys = 0;

    while (n > 0)
    {

        // If N is divisible by Y
        if (n % Y == 0)
        {

            // Append X, N times to
            // the answer
            Xs += n;

            // Reduce N to zero
            n = 0;
        }
        else
        {
            // Reduce N by X
            n -= X;

            // Append Y, X times
            // to the answer
            Ys += X;
        }
    }

    // If number can be formed
    if (n == 0)
    {
        while (Xs-- > 0)
            document.write(X);

        while (Ys-- > 0)
            document.write(Y);
    }

    // Otherwise
    else
        document.write("-1");
}

// Driver Code

    let n = 19, X = 7, Y = 5;

    largestNumber(n, X, Y);

 // This code is contributed by splevel62.
</script>
```

**Output:** 

```
7777755555555555555
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*