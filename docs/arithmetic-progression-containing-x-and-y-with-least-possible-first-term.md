# 包含 X 和 Y 的算术级数，第一项最少

> 原文:[https://www . geeksforgeeks . org/算术级数-包含-x-和-y-具有最少可能-第一项/](https://www.geeksforgeeks.org/arithmetic-progression-containing-x-and-y-with-least-possible-first-term/)

给定三个整数 **N** 、 **X** 和 **Y** ，任务是找到一个 **N** 长度[等差数列](https://www.geeksforgeeks.org/arithmetic-progression/)系列，其中第一项包含 **X** 和 **Y** 。

**示例:**

> **输入:** N = 5，X = 10，Y = 15
> **输出:** 5 10 15 20 25
> **解释:**
> AP 最不可能的第一项是 5。AP = 5 的共同区别
> 给定的 AP 包含 10 和 15。
> 
> **输入:** N = 10，X = 5，Y = 15
> **输出:** 1 3 5 7 9 11 13 15 17 19

**天真方法:**最简单的方法是迭代从 1 到 **abs(X-Y)** 的所有可能公共差的值，并检查是否存在第一项大于 0 且包含 **X** 和 **Y** 的 **N** 长度 AP。

***时间复杂度:**O(N * ABS(X-Y))*
***辅助空间:** O(1)*

**有效方法:**该方法基于这样的思想，即要将 X 和 Y 都包括在系列中，AP 的共同差异必须是 **abs(X-Y)** 的一个因素。以下是解决问题的步骤:

1.  从 **1** 迭代到 **sqrt(abs(X-Y))** ，只考虑那些共同的差异，它们是 **abs(X-Y)** 的因素。
2.  对于每一个可能的共同差异，说 **diff** ，其划分 **abs(X-Y)** ，使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)算法找到大于 0 的最小第一项。
3.  存储最小第一项和对应的公共差，打印 **N** 长度等差数列。

下面是上述方法的实现:

## C++

```
// C++ program for the approach
#include <bits/stdc++.h>
using namespace std;

// Function that finds the minimum
// positive first term including X with given
// common difference and the number of terms
int minFirstTerm(int X, int diff, int N)
{

    // Stores the first term
    int first_term;

    // Initialize the low and high
    int low = 0, high = N;

    // Perform binary search
    while (low <= high) {

        // Find the mid
        int mid = (low + high) / 2;

        // Check if first term is
        // greater than 0
        if (X - mid * diff > 0) {

            // Store the possible first term
            first_term = X - mid * diff;

            // Search between mid + 1 to high
            low = mid + 1;
        }
        else

            // Search between low to mid-1
            high = mid - 1;
    }

    // Return the minimum first term
    return first_term;
}

// Function that finds the Arithmetic
// Progression with minimum possible
// first term containing X and Y
void printAP(int N, int X, int Y)
{
    // Considering X to be
    // smaller than Y always
    if (X > Y)
        swap(X, Y);

    // Stores the max common difference
    int maxDiff = Y - X;

    // Stores the minimum first term
    // and the corresponding common
    // difference of the resultant AP
    int first_term = INT_MAX, diff;

    // Iterate over all the common difference
    for (int i = 1; i * i <= maxDiff; i++) {

        // Check if X and Y is included
        // for current common difference
        if (maxDiff % i == 0) {

            // Store the possible
            // common difference
            int diff1 = i;
            int diff2 = maxDiff / diff1;

            // Number of terms from
            // X to Y with diff1
            // common difference
            int terms1 = diff2 + 1;

            // Number of terms from
            // X to Y with diff2
            // common difference
            int terms2 = diff1 + 1;

            // Find the corresponding first
            // terms with diff1 and diff2
            int first_term1
                = minFirstTerm(X, diff1, N - terms1);
            int first_term2
                = minFirstTerm(X, diff2, N - terms2);

            // Store the minimum first term
            // and the corresponding
            // common difference
            if (first_term1 < first_term) {
                first_term = first_term1;
                diff = diff1;
            }
            if (first_term2 < first_term) {
                first_term = first_term2;
                diff = diff2;
            }
        }
    }

    // Print the resultant AP
    for (int i = 0; i < N; i++) {
        cout << first_term << " ";
        first_term += diff;
    }
}

// Driver Code
int main()
{
    // Given length of AP
    // and the two terms
    int N = 5, X = 10, Y = 15;

    // Function Call
    printAP(N, X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the approach
import java.util.*;

class GFG{

// Function that finds the minimum
// positive first term including X
// with given common difference and
// the number of terms
static int minFirstTerm(int X, int diff, int N)
{

    // Stores the first term
    int first_term = Integer.MAX_VALUE;

    // Initialize the low and high
    int low = 0, high = N;

    // Perform binary search
    while (low <= high)
    {

        // Find the mid
        int mid = (low + high) / 2;

        // Check if first term is
        // greater than 0
        if (X - mid * diff > 0)
        {

            // Store the possible first term
            first_term = X - mid * diff;

            // Search between mid + 1 to high
            low = mid + 1;
        }
        else

            // Search between low to mid-1
            high = mid - 1;
    }

    // Return the minimum first term
    return first_term;
}

// Function that finds the Arithmetic
// Progression with minimum possible
// first term containing X and Y
static void printAP(int N, int X, int Y)
{

    // Considering X to be
    // smaller than Y always
    if (X > Y)
    {
        X = X + Y;
        Y = X - Y;
        X = X - Y;
    }

    // Stores the max common difference
    int maxDiff = Y - X;

    // Stores the minimum first term
    // and the corresponding common
    // difference of the resultant AP
    int first_term = Integer.MAX_VALUE, diff = 0;

    // Iterate over all the common difference
    for(int i = 1; i * i <= maxDiff; i++)
    {

        // Check if X and Y is included
        // for current common difference
        if (maxDiff % i == 0)
        {

            // Store the possible
            // common difference
            int diff1 = i;
            int diff2 = maxDiff / diff1;

            // Number of terms from
            // X to Y with diff1
            // common difference
            int terms1 = diff2 + 1;

            // Number of terms from
            // X to Y with diff2
            // common difference
            int terms2 = diff1 + 1;

            // Find the corresponding first
            // terms with diff1 and diff2
            int first_term1 = minFirstTerm(X, diff1,
                                           N - terms1);
            int first_term2 = minFirstTerm(X, diff2,
                                           N - terms2);

            // Store the minimum first term
            // and the corresponding
            // common difference
            if (first_term1 < first_term)
            {
                first_term = first_term1;
                diff = diff1;
            }
            if (first_term2 < first_term)
            {
                first_term = first_term2;
                diff = diff2;
            }
        }
    }

    // Print the resultant AP
    for(int i = 0; i < N; i++)
    {
        System.out.print(first_term + " ");
        first_term += diff;
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given length of AP
    // and the two terms
    int N = 5, X = 10, Y = 15;

    // Function call
    printAP(N, X, Y);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the approach
import sys

# Function that finds the minimum
# positive first term including X with given
# common difference and the number of terms
def minFirstTerm(X, diff, N):

    # Stores the first term
    first_term_1 = sys.maxsize

    # Initialize the low and high
    low = 0
    high = N

    # Perform binary search
    while (low <= high):

        # Find the mid
        mid = (low + high) // 2

        # Check if first term is
        # greater than 0
        if (X - mid * diff > 0):

            # Store the possible first term
            first_term_1 = X - mid * diff

            # Search between mid + 1 to high
            low = mid + 1

        else:

            # Search between low to mid-1
            high = mid - 1

    # Return the minimum first term
    return first_term_1

# Function that finds the Arithmetic
# Progression with minimum possible
# first term containing X and Y
def printAP(N, X, Y):

    # Considering X to be
    # smaller than Y always
    if (X > Y):
        X = X + Y
        Y = X - Y
        X = X - Y

    # Stores the max common difference
    maxDiff = Y - X

    # Stores the minimum first term
    # and the corresponding common
    # difference of the resultant AP
    first_term = sys.maxsize
    diff = 0

    # Iterate over all the common difference
    for i in range(1, maxDiff + 1):
        if i * i > maxDiff:
            break

        # Check if X and Y is included
        # for current common difference
        if (maxDiff % i == 0):

            # Store the possible
            # common difference
            diff1 = i
            diff2 = maxDiff // diff1

            # Number of terms from
            # X to Y with diff1
            # common difference
            terms1 = diff2 + 1

            # Number of terms from
            # X to Y with diff2
            # common difference
            terms2 = diff1 + 1

            # Find the corresponding first
            # terms with diff1 and diff2
            first_term1 = minFirstTerm(X, diff1,
                                       N - terms1)
            first_term2 = minFirstTerm(X, diff2,
                                       N - terms2)

            # Store the minimum first term
            # and the corresponding
            # common difference
            if (first_term1 < first_term):
                first_term = first_term1
                diff = diff1

            if (first_term2 < first_term):
                first_term = first_term2
                diff = diff2

    # Print the resultant AP
    for i in range(N):
        print(first_term, end = " ")
        first_term += diff

# Driver Code
if __name__ == '__main__':

    # Given length of AP
    # and the two terms
    N = 5
    X = 10
    Y = 15

    # Function call
    printAP(N, X, Y)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the approach
using System;

class GFG{

// Function that finds the minimum
// positive first term including X
// with given common difference and
// the number of terms
static int minFirstTerm(int X, int diff,
                        int N)
{

    // Stores the first term
    int first_term = int.MaxValue;

    // Initialize the low and high
    int low = 0, high = N;

    // Perform binary search
    while (low <= high)
    {

        // Find the mid
        int mid = (low + high) / 2;

        // Check if first term is
        // greater than 0
        if (X - mid * diff > 0)
        {

            // Store the possible first term
            first_term = X - mid * diff;

            // Search between mid + 1 to high
            low = mid + 1;
        }
        else

            // Search between low to mid-1
            high = mid - 1;
    }

    // Return the minimum first term
    return first_term;
}

// Function that finds the Arithmetic
// Progression with minimum possible
// first term containing X and Y
static void printAP(int N, int X, int Y)
{

    // Considering X to be
    // smaller than Y always
    if (X > Y)
    {
        X = X + Y;
        Y = X - Y;
        X = X - Y;
    }

    // Stores the max common difference
    int maxDiff = Y - X;

    // Stores the minimum first term
    // and the corresponding common
    // difference of the resultant AP
    int first_term = int.MaxValue, diff = 0;

    // Iterate over all the common difference
    for(int i = 1; i * i <= maxDiff; i++)
    {

        // Check if X and Y is included
        // for current common difference
        if (maxDiff % i == 0)
        {

            // Store the possible
            // common difference
            int diff1 = i;
            int diff2 = maxDiff / diff1;

            // Number of terms from
            // X to Y with diff1
            // common difference
            int terms1 = diff2 + 1;

            // Number of terms from
            // X to Y with diff2
            // common difference
            int terms2 = diff1 + 1;

            // Find the corresponding first
            // terms with diff1 and diff2
            int first_term1 = minFirstTerm(X, diff1,
                                        N - terms1);
            int first_term2 = minFirstTerm(X, diff2,
                                        N - terms2);

            // Store the minimum first term
            // and the corresponding
            // common difference
            if (first_term1 < first_term)
            {
                first_term = first_term1;
                diff = diff1;
            }
            if (first_term2 < first_term)
            {
                first_term = first_term2;
                diff = diff2;
            }
        }
    }

    // Print the resultant AP
    for(int i = 0; i < N; i++)
    {
        Console.Write(first_term + " ");
        first_term += diff;
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given length of AP
    // and the two terms
    int N = 5, X = 10, Y = 15;

    // Function call
    printAP(N, X, Y);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function that finds the minimum
// positive first term including X
// with given common difference and
// the number of terms
function minFirstTerm(X, diff, N)
{

    // Stores the first term
    let first_term = Number.MAX_VALUE;

    // Initialize the low and high
    let low = 0, high = N;

    // Perform binary search
    while (low <= high)
    {

        // Find the mid
        let mid = Math.floor((low + high) / 2);

        // Check if first term is
        // greater than 0
        if (X - mid * diff > 0)
        {

            // Store the possible first term
            first_term = X - mid * diff;

            // Search between mid + 1 to high
            low = mid + 1;
        }
        else

            // Search between low to mid-1
            high = mid - 1;
    }

    // Return the minimum first term
    return first_term;
}

// Function that finds the Arithmetic
// Progression with minimum possible
// first term containing X and Y
function prletAP(N, X, Y)
{

    // Considering X to be
    // smaller than Y always
    if (X > Y)
    {
        X = X + Y;
        Y = X - Y;
        X = X - Y;
    }

    // Stores the max common difference
    let maxDiff = Y - X;

    // Stores the minimum first term
    // and the corresponding common
    // difference of the resultant AP
    let first_term = Number.MAX_VALUE, diff = 0;

    // Iterate over all the common difference
    for(let i = 1; i * i <= maxDiff; i++)
    {

        // Check if X and Y is included
        // for current common difference
        if (maxDiff % i == 0)
        {

            // Store the possible
            // common difference
            let diff1 = i;
            let diff2 = Math.floor(maxDiff / diff1);

            // Number of terms from
            // X to Y with diff1
            // common difference
            let terms1 = diff2 + 1;

            // Number of terms from
            // X to Y with diff2
            // common difference
            let terms2 = diff1 + 1;

            // Find the corresponding first
            // terms with diff1 and diff2
            let first_term1 = minFirstTerm(X, diff1,
                                           N - terms1);
            let first_term2 = minFirstTerm(X, diff2,
                                           N - terms2);

            // Store the minimum first term
            // and the corresponding
            // common difference
            if (first_term1 < first_term)
            {
                first_term = first_term1;
                diff = diff1;
            }
            if (first_term2 < first_term)
            {
                first_term = first_term2;
                diff = diff2;
            }
        }
    }

    // Prlet the resultant AP
    for(let i = 0; i < N; i++)
    {
        document.write(first_term + " ");
        first_term += diff;
    }
}

// Driver Code

        // Given length of AP
    // and the two terms
    let N = 5, X = 10, Y = 15;

    // Function call
    prletAP(N, X, Y);

// This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
5 10 15 20 25 
```

***时间复杂度:**O(sqrt(ABS(X-Y))* log(N))*
***辅助空间:** O(1)*