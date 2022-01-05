# 检查 N 是否包含基 B 中作为 K 的所有数字

> 原文:[https://www . geesforgeks . org/check-if-n-contains-all-digits-as-k-in-base-b/](https://www.geeksforgeeks.org/check-if-n-contains-all-digits-as-k-in-base-b/)

给定三个数字 **N** 、 **K** 和 **B** ，任务是检查 **N** 是否只包含 **K** 作为基数 **B** 中的数字。

**示例:**

> **输入:** N = 13，B = 3，K = 1
> **输出:**是
> **说明:**
> 13 的基数 3 是 111，其中包含了所有的 1(K)。
> 
> **输入:** N = 5，B = 2，K = 1
> **输出:**否
> **说明:**
> 5 基数 2 是 101，不包含全部的(K)。

**天真方法:**一个简单的解决方法是[将给定的数字 **N** 转换为基数**B**T7】并逐一检查其所有数字是否为 **K** 。
***时间复杂度:** O(D)，其中 D 为数字 N 中的位数*
***辅助空间:** O(1)*](https://www.geeksforgeeks.org/convert-base-decimal-vice-versa/)

**高效逼近:**问题中的关键观察是任何一个在基数 **B** 中所有数字都为 **K** 的数字都可以表示为:

> ![K*B^0 + K*B^1 + K*B^2+...K*B^{\log_b N + 1} = N  ](img/8cd85bc8b3123d0f86cb805722d0a3e1.png "Rendered by QuickLaTeX.com")

这些项采用[几何级数](https://www.geeksforgeeks.org/geometric-progression/)的形式，第一项为 K，公比为 b

宝洁系列之和:

> ![\frac{a * (1 - r^{N})}{(1-r)}  ](img/7eedeb97f81f0d67afd289a0024faf5b.png "Rendered by QuickLaTeX.com")

因此，所有数字都为 K 的基数 B 中的数字是:

> ![\frac{K * (1-B^{log_bN + 1})}{(1-B)}  ](img/82cdef5a767a99dbfa780ac5c2f461bd.png "Rendered by QuickLaTeX.com")

因此，只需检查这个**和是否等于 N** 。如果相等，则打印**“是”**，否则打印**“否”**。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to print the number of digits
int findNumberOfDigits(int n, int base)
{

    // Calculate log using base change
    // property and then take its floor
    // and then add 1
    int dig = (floor(log(n) / log(base)) + 1);

    // Return the output
    return (dig);
}

// Function that returns true if n contains
// all one's in base b
int isAllKs(int n, int b, int k)
{
    int len = findNumberOfDigits(n, b);

    // Calculate the sum
    int sum = k * (1 - pow(b, len)) /
                  (1 - b);
    if(sum == n)
    {
        return(sum);
    }
}

// Driver code
int main()
{

    // Given number N
    int N = 13;

    // Given base B
    int B = 3;

    // Given digit K
    int K = 1;

    // Function call
    if (isAllKs(N, B, K))
    {
        cout << "Yes";
    }
    else
    {
        cout << "No";
    }
}

// This code is contributed by vikas_g
```

## C

```
// C implementation of the approach
#include <stdio.h>
#include <math.h>

// Function to print the number of digits
int findNumberOfDigits(int n, int base)
{

    // Calculate log using base change
    // property and then take its floor
    // and then add 1
    int dig = (floor(log(n) / log(base)) + 1);

    // Return the output
    return (dig);
}

// Function that returns true if n contains
// all one's in base b
int isAllKs(int n, int b, int k)
{
    int len = findNumberOfDigits(n, b);

    // Calculate the sum
    int sum = k * (1 - pow(b, len)) /
                  (1 - b);
    if(sum == n)
    {
        return(sum);
    }
}

// Driver code
int main(void)
{

    // Given number N
    int N = 13;

    // Given base B
    int B = 3;

    // Given digit K
    int K = 1;

    // Function call
    if (isAllKs(N, B, K))
    {
        printf("Yes");
    }
    else
    {
        printf("No");
    }
    return 0;
}

// This code is contributed by vikas_g
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class GFG{

// Function to print the number of digits
static int findNumberOfDigits(int n, int base)
{

    // Calculate log using base change
    // property and then take its floor
    // and then add 1
    int dig = ((int)Math.floor(Math.log(n) /
                    Math.log(base)) + 1);

    // Return the output
    return dig;
}

// Function that returns true if n contains
// all one's in base b
static boolean isAllKs(int n, int b, int k)
{
    int len = findNumberOfDigits(n, b);

    // Calculate the sum
    int sum = k * (1 - (int)Math.pow(b, len)) /
                  (1 - b);

    return sum == n;
}

// Driver code
public static void main(String[] args)
{

    // Given number N
    int N = 13;

    // Given base B
    int B = 3;

    // Given digit K
    int K = 1;

    // Function call
    if (isAllKs(N, B, K))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to print the number of digits
def findNumberOfDigits(n, base):

    # Calculate log using base change
    # property and then take its floor
    # and then add 1
    dig = (math.floor(math.log(n) /
                      math.log(base)) + 1)

    # Return the output
    return dig

# Function that returns true if n contains
# all one's in base b
def isAllKs(n, b, k):

    len = findNumberOfDigits(n, b)

    # Calculate the sum
    sum = k * (1 - pow(b, len)) / (1 - b)

    return sum == N

# Driver code

# Given number N
N = 13

# Given base B
B = 3

# Given digit K
K = 1

# Function call
if (isAllKs(N, B, K)):
    print("Yes")
else:
    print("No")
```

## C#

```
// C# implementation of above approach
using System;

class GFG{

// Function to print the number of digits
static int findNumberOfDigits(int n, int bas)
{

    // Calculate log using base change
    // property and then take its floor
    // and then add 1
    int dig = ((int)Math.Floor(Math.Log(n) /
                               Math.Log(bas)) + 1);

    // Return the output
    return dig;
}

// Function that returns true if n contains
// all one's in base b
static bool isAllKs(int n, int b, int k)
{
    int len = findNumberOfDigits(n, b);

    // Calculate the sum
    int sum = k * (1 - (int)Math.Pow(b, len)) /
                  (1 - b);

    return sum == n;
}

// Driver code
public static void Main()
{

    // Given number N
    int N = 13;

    // Given base B
    int B = 3;

    // Given digit K
    int K = 1;

    // Function call
    if (isAllKs(N, B, K))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by vikas_g
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to print the number of digits
function findNumberOfDigits(n, base)
{

    // Calculate log using base change
    // property and then take its floor
    // and then add 1
    var dig = (Math.floor(Math.log(n) / Math.log(base)) + 1);

    // Return the output
    return (dig);
}

// Function that returns true if n contains
// all one's in base b
function isAllKs(n, b, k)
{
    var len = findNumberOfDigits(n, b);

    // Calculate the sum
    var sum = k * (1 - Math.pow(b, len)) /
                  (1 - b);
    if(sum == n)
    {
        return(sum);
    }
}

// Driver code
// Given number N
var N = 13;

// Given base B
var B = 3;

// Given digit K
var K = 1;

// Function call
if (isAllKs(N, B, K))
{
    document.write( "Yes");
}
else
{
    document.write("No");
}

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** *O(log(D))，其中 D 为数字 N 中的位数*
**辅助空间:** *O(1)*