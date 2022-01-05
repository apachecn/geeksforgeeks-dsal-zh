# 检查两个给定数字重复加减是否能得到 N

> 原文:[https://www . geeksforgeeks . org/check-if-n-n-可以通过对两个给定的数字进行重复加法或减法来获得/](https://www.geeksforgeeks.org/check-if-n-can-be-obtained-by-repetitive-addition-or-subtraction-of-two-given-numbers/)

给定三个正整数 **N** 、 **A、**和 **B、**，任务是检查通过多次加减 **A** 和 **B** 是否可以得到 **N** 。

**示例:**

> **输入:** N = 11，A = 2，B = 5
> **输出:** YES
> **说明:**11 = 5+5+5–2-2
> 
> **输入:** N = 11，A = 2，B = 4
> **输出:**否
> **说明:**仅从 2 和 4 不可能得到 11。

**方法:**
按照以下步骤解决问题:

*   任务是检查是否可以多次加减 **A** 和 **B** ，得到 **N** 作为最终结果。
*   因此，就线性方程而言，可以写成:
    T1】Ax+By = N，
    其中 **x** 和 **y** 代表 **A** 和 **B** 相加或相减的次数。负 **x** 代表 **A** 减去 **x** 次，同样负 **y** 代表 **B** 减去 **y** 次
*   现在，目标是找到上述方程的积分解。在这里，使用 [**扩展欧几里德算法**](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/) 是非常有效的，该算法认为当且仅当 **N % gcd(a，b)** 为 0 时解才存在。

下面是上述方法的实现:

## C++

```
// C++ Program to check if
// a number can be obtained
// by repetitive addition
// or subtraction of two numbers

#include <bits/stdc++.h>
using namespace std;

// Function to check and return if
// it is possible to obtain N by
// repetitive addition or subtraction
// of A and B
bool isPossible(int N, int a, int b)
{
    // Calculate GCD of A and B
    int g = __gcd(a, b);

    // Condition to check
    // if N can be obtained
    if (N % g == 0)
        return true;
    else
        return false;
}

// Driver Code
int main()
{
    int N = 11, a = 2;
    int b = 5;

    if (isPossible(N, a, b))
        cout << "YES";
    else
        cout << "NO";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if
// a number can be obtained
// by repetitive addition
// or subtraction of two numbers
class GFG{

// Recursive function to return
// gcd of a and b
public static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to check and return if
// it is possible to obtain N by
// repetitive addition or subtraction
// of A and B
public static boolean isPossible(int N, int a,
                                 int b)
{

    // Calculate GCD of A and B
    int g = gcd(a, b);

    // Condition to check
    // if N can be obtained
    if (N % g == 0)
        return true;
    else
        return false;
}

// Driver code
public static void main(String[] args)
{
    int N = 11, a = 2;
    int b = 5;

    if (isPossible(N, a, b))
        System.out.print("YES");
    else
        System.out.print("NO");
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to check if
# a number can be obtained
# by repetitive addition
# or subtraction of two numbers

# Recursive function to return
# gcd of a and b
def gcd(a, b):

    if (b == 0):
        return a
    return gcd(b, a % b)

# Function to check and return if
# it is possible to obtain N by
# repetitive addition or subtraction
# of A and B
def isPossible(N, a, b):

    # Calculate GCD of A and B
    g = gcd(a, b)

    # Condition to check
    # if N can be obtained
    if (N % g == 0):
        return True
    else:
        return False

# Driver code
N = 11
a = 2
b = 5

if (isPossible(N, a, b) != False):
    print("YES")
else:
    print("NO")

# This code is contributed by code_hunt
```

## C#

```
// C# program to check if
// a number can be obtained
// by repetitive addition
// or subtraction of two numbers
using System;

class GFG{

// Recursive function to return
// gcd of a and b
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to check and return if
// it is possible to obtain N by
// repetitive addition or subtraction
// of A and B
static bool isPossible(int N, int a,
                              int b)
{

    // Calculate GCD of A and B
    int g = gcd(a, b);

    // Condition to check
    // if N can be obtained
    if (N % g == 0)
        return true;
    else
        return false;
}

// Driver code
public static void Main()
{
    int N = 11, a = 2;
    int b = 5;

    if (isPossible(N, a, b))
        Console.Write("YES");
    else
        Console.Write("NO");
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// Javascript program to check if
// a number can be obtained
// by repetitive addition
// or subtraction of two numbers

// Recursive function to return
// gcd of a and b
function gcd(a, b)
{
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// Function to check and return if
// it is possible to obtain N by
// repetitive addition or subtraction
// of A and B
function isPossible(N, a, b)
{

    // Calculate GCD of A and B
    var g = gcd(a, b);

    // Condition to check
    // if N can be obtained
    if (N % g == 0)
        return true;
    else
        return false;
}

// Driver code
var N = 11, a = 2;
var b = 5;

if (isPossible(N, a, b))
    document.write("YES");
else
    document.write("NO");  

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
YES
```

***时间复杂度:** O(log(min(A，B))*
***辅助空间:** O(1)*