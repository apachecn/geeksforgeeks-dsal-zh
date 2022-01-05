# 求给定规则生成的矩阵元素之和

> 原文:[https://www . geeksforgeeks . org/find-由给定规则生成的矩阵元素之和/](https://www.geeksforgeeks.org/find-the-sum-of-elements-of-the-matrix-generated-by-the-given-rules/)

给定三个整数 **A** 、 **B** 和 **R** ，任务是找出由给定规则生成的矩阵的所有元素的和:

1.  第一行将包含单个元素 **A** ，其余元素为 **0** 。
2.  下一行将包含**两个元素**，全部为 **(A + B)** ，其余为 **0s** 。
3.  第三行将包含 **(A + B + B)** 三次，其余为 **0s** 以此类推。
4.  矩阵将只包含 R 行。

**比如**如果 **A = 5** 、 **B = 3** 和 **R = 3** 那么矩阵就是:
5 0 0
8 8 0
11 11 11
**例:**

> **输入:** A = 5，B = 3，R = 3
> **输出:**54
> 5+8+8+11+11 = 54
> **输入:** A = 7，B = 56，R = 1
> **输出:** 7

**方法:**初始化**总和= 0** 并且对于每个 **1 ≤ i ≤ R** 更新**总和=总和+ (i * A)** 。每次迭代更新后 **A = A + B** 。打印最后的总和。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the required sum
int sum(int A, int B, int R)
{

    // To store the sum
    int sum = 0;

    // For every row
    for (int i = 1; i <= R; i++) {

        // Update the sum as A appears i number
        // of times in the current row
        sum = sum + (i * A);

        // Update A for the next row
        A = A + B;
    }

    // Return the sum
    return sum;
}

// Driver code
int main()
{

    int A = 5, B = 3, R = 3;
    cout << sum(A, B, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA implementation of the approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{

// Function to return the required sum
static int sum(int A, int B, int R)
{

    // To store the sum
    int sum = 0;

    // For every row
    for (int i = 1; i <= R; i++)
    {

        // Update the sum as A appears i number
        // of times in the current row
        sum = sum + (i * A);

        // Update A for the next row
        A = A + B;
    }

    // Return the sum
    return sum;
}

// Driver code
public static void main (String[] args)
              throws java.lang.Exception
{
    int A = 5, B = 3, R = 3;

    System.out.print(sum(A, B, R));
}
}

// This code is contributed by nidhiva
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the required ssum
def Sum(A, B, R):

    # To store the ssum
    ssum = 0

    # For every row
    for i in range(1, R + 1):

        # Update the ssum as A appears i number
        # of times in the current row
        ssum = ssum + (i * A)

        # Update A for the next row
        A = A + B

    # Return the ssum
    return ssum

# Driver code
A, B, R = 5, 3, 3
print(Sum(A, B, R))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the required sum
static int sum(int A, int B, int R)
{

    // To store the sum
    int sum = 0;

    // For every row
    for (int i = 1; i <= R; i++)
    {

        // Update the sum as A appears i number
        // of times in the current row
        sum = sum + (i * A);

        // Update A for the next row
        A = A + B;
    }

    // Return the sum
    return sum;
}

// Driver code
public static void Main ()
{
    int A = 5, B = 3, R = 3;

    Console.Write(sum(A, B, R));
}
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>
// JAVA SCRIPT  implementation of the approach
// Function to return the required sum
function sum( A,  B,  R)
{

    // To store the sum
    let sum = 0;

    // For every row
    for (let i = 1; i <= R; i++)
    {

        // Update the sum as A appears i number
        // of times in the current row
        sum = sum + (i * A);

        // Update A for the next row
        A = A + B;
    }

    // Return the sum
    return sum;
}

// Driver code

    let A = 5, B = 3, R = 3;

    document.write(sum(A, B, R));

//contributed by bobby

</script>
```

**Output:** 

```
54
```

**时间复杂度:** O(R)

**辅助空间:** O(1)