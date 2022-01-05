# 找到与给定分数最接近的分数，该分数具有最小绝对差

> 原文:[https://www . geesforgeks . org/find-与给定分数最接近的分数-具有最小绝对差/](https://www.geeksforgeeks.org/find-the-closest-fraction-to-given-fraction-having-minimum-absolute-difference/)

给定三个整数 **x** ， **y** ，以及 **n，**任务就是找到这样一对整数 **a，b**T8】(1<= b<= n；0 < = a) 值**| x/y–a/b |**尽可能最小，其中|x|代表 x 的绝对值。

**示例:**

> **输入:** x = 3，y = 7，n = 6
> **输出:** 2/5
> **解释:** a=2 和 b=5 和 b < =6 然后 3/7–2/5 = 1/35，这是可能的最小差值
> 
> **输入:** x = 12，y = 37，n = 5
> T3】输出: 1/3

**方法:**迭代分母。让分母为 **i** 。那么就需要选择这样一个分子 **d** 使得**| x/y–d/I |**最小。 **d = (x*i)/y** 是个不错的选择。还要检查 **d+1** 。在将答案从 **A/B** 更新为 **d/i 时，**检查**x/y–d/I<x/y-A/B**或**(B * x-y * A)*(I * y)>(I * x-y * d)*(B * y)。**按照以下步骤解决问题:

*   将变量 **A** 和 **B** 初始化为 **-1** 存储答案。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**，并执行以下步骤:
    *   将变量 **d** 初始化为 **(i*x)/y** 作为最接近的分子。
    *   如果 **d** 大于等于 **0** 且 **A** 等于 **-1** 或**ABS(B * x–y * A)* ABS(I * y)**大于**ABS(I * x–y * d)* ABS(B * y)，**则将 **A** 的值设置为 **d** 和 **B**
    *   将 **d** 的值增加 **1。**
    *   如果 **d** 大于等于 **0** 且 **A** 等于 **-1** 或**ABS(B * x–y * A)* ABS(I * y)**大于**ABS(I * x–y * d)* ABS(B * y)，**则将 **A** 的值设置为 **d** 和 **B**
*   执行上述步骤后，打印 **A/B** 的值作为答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the absolute
// value of x
long long ABS(long long x) { return max(x, -x); }

// Function to find the fraction with
// minimum absolute difference
void findFraction(long long x, long long y, long long n)
{

    // Initialize the answer variables
    long long A = -1, B = -1;

    // Iterate over the range
    for (long long i = 1; i <= n; i++) {

        // Nearest fraction
        long long d = (i * x) / y;

        // x/y - d/i < x/y -A/B
        //(B*x-y*A) * (i*y) > (i*x-y*d) * (B*y)
        if (d >= 0
            && (A == -1
                || ABS(B * x - y * A) * ABS(i * y)
                       > ABS(i * x - y * d) * ABS(B * y)))
            A = d, B = i;

        // Check for d+1
        d++;
        if (d >= 0
            && (A == -1
                || ABS(B * x - y * A) * ABS(i * y)
                       > ABS(i * x - y * d) * ABS(B * y)))
            A = d, B = i;
    }

    // Print the answer
    cout << A << "/" << B << endl;
}

// Driver Code
int main()
{

    long long x = 3, y = 7, n = 6;

    findFraction(x, y, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.io.*;
class GFG
{

    // Function to find the absolute
    // value of x
    static long ABS(long x) { return Math.max(x, -x); }

    // Function to find the fraction with
    // minimum absolute difference
    static void findFraction(long x, long y, long n)
    {

        // Initialize the answer variables
        long A = -1, B = -1;

        // Iterate over the range
        for (long i = 1; i <= n; i++) {

            // Nearest fraction
            long d = (i * x) / y;

            // x/y - d/i < x/y -A/B
            //(B*x-y*A) * (i*y) > (i*x-y*d) * (B*y)
            if (d >= 0
                && (A == -1
                    || ABS(B * x - y * A) * ABS(i * y)
                           > ABS(i * x - y * d)
                                 * ABS(B * y)))
                A = d;
            B = i;

            // Check for d+1
            d++;
            if (d >= 0
                && (A == -1
                    || ABS(B * x - y * A) * ABS(i * y)
                           > ABS(i * x - y * d)
                                 * ABS(B * y)))
                A = d;
            B = i;
        }
        A--;
        B--;

        // Print the answer
        System.out.println(A + "/" + B);
    }

    // Driver Code
    public static void main(String[] args)
    {

        long x = 3;
        long y = 7;
        long n = 6;

        findFraction(x, y, n);
    }
}

// This code is contributed by lokeshpotta.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the absolute
# value of x
def ABS(x):

    return max(x, -x)

# Function to find the fraction with
# minimum absolute difference
def findFraction(x, y, n):

    # Initialize the answer variables
    A = -1
    B = -1

    # Iterate over the range
    for i in range(1, n + 1):

        # Nearest fraction
        d = (i * x) // y

        # x/y - d/i < x/y -A/B
        # (B*x-y*A) * (i*y) > (i*x-y*d) * (B*y)
        if (d >= 0 and (A == -1 or
           ABS(B * x - y * A) * ABS(i * y) >
           ABS(i * x - y * d) * ABS(B * y))):
            A = d
            B = i

        # Check for d+1
        d += 1
        if (d >= 0 and (A == -1 or
           ABS(B * x - y * A) * ABS(i * y) >
           ABS(i * x - y * d) * ABS(B * y))):
            A = d
            B = i

    # Print the answer
    print(str(A) + "/" + str(B))

# Driver Code
if __name__ == '__main__':

    x = 3
    y = 7
    n = 6

    findFraction(x, y, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# code for the above approach
using System;

public class GFG{

    // Function to find the absolute
    // value of x
    static long ABS(long x) { return Math.Max(x, -x); }

    // Function to find the fraction with
    // minimum absolute difference
    static void findFraction(long x, long y, long n)
    {

        // Initialize the answer variables
        long A = -1, B = -1;

        // Iterate over the range
        for (long i = 1; i <= n; i++) {

            // Nearest fraction
            long d = (i * x) / y;

            // x/y - d/i < x/y -A/B
            //(B*x-y*A) * (i*y) > (i*x-y*d) * (B*y)
            if (d >= 0
                && (A == -1
                    || ABS(B * x - y * A) * ABS(i * y)
                           > ABS(i * x - y * d)
                                 * ABS(B * y)))
                A = d;
            B = i;

            // Check for d+1
            d++;
            if (d >= 0
                && (A == -1
                    || ABS(B * x - y * A) * ABS(i * y)
                           > ABS(i * x - y * d)
                                 * ABS(B * y)))
                A = d;
            B = i;
        }
        A--;
        B--;

        // Print the answer
        Console.Write(A + "/" + B);
    }

    // Driver Code
    static public void Main (){

        long x = 3;
        long y = 7;
        long n = 6;

        findFraction(x, y, n);
    }
}

// This code is contributed by shubhamsingh10.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the absolute
// value of x
function ABS(x)
{
    return Math.max(x, -x);
}

// Function to find the fraction with
// minimum absolute difference
function findFraction(x, y, n)
{

    // Initialize the answer variables
    let A = -1, B = -1;

    // Iterate over the range
    for(let i = 1; i <= n; i++)
    {

        // Nearest fraction
        let d = Math.floor((i * x) / y);

        // x/y - d/i < x/y -A/B
        //(B*x-y*A) * (i*y) > (i*x-y*d) * (B*y)
        if (d >= 0 && (A == -1 || ABS(B * x - y * A) *
            ABS(i * y) > ABS(i * x - y * d) * ABS(B * y)))
            A = d;

        B = i;

        // Check for d+1
        d++;
        if (d >= 0 && (A == -1 || ABS(B * x - y * A) *
            ABS(i * y) > ABS(i * x - y * d) * ABS(B * y)))
            A = d;

        B = i;
    }
    A--;
    B--;

    // Print the answer
    document.write(A + "/" + B);
}

// Driver code
let x = 3;
let y = 7;
let n = 6;

findFraction(x, y, n);

// This code is contributed by sanjoy_62

</script>
```

**Output**

```
2/5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)