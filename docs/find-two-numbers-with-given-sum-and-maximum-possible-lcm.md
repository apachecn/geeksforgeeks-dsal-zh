# 找出两个给定总和和最大可能 LCM 的数字

> 原文:[https://www . geesforgeks . org/find-两个数同给定和最大可能 lcm/](https://www.geeksforgeeks.org/find-two-numbers-with-given-sum-and-maximum-possible-lcm/)

给定一个整数 **X** ，任务是找出两个整数 **A** 和 **B** ，使得这两个数之和为 **X** ，且 **A** 和 **B** 的 [LCM](https://www.geeksforgeeks.org/lcm-gq/) 最大。

**示例:**

> **输入:** X = 15
> **输出:** 7 8
> **说明:**
> 7 + 8 = 15，LCM(7，8) = 56 是最大可能。
> 
> **输入:** X = 30
> **输出:** 13 17
> **说明:**
> 13 + 17 = 30，LCM(13，17) = 221 是最大可能。

**天真法:**最简单的方法是用[两个指针](https://www.geeksforgeeks.org/two-pointers-technique/)找到给定和 **X** 和最大可能 *LCM* 的整数对 **A** 和 **B** 。以下是步骤:

*   将 **A** 和 **B** 分别初始化为 *1* 和**X**–*1*。
*   运行一个循环，同时， **A** 小于等于 **B** 。
*   每次迭代计算 **A** 和 **B、**的 *LCM* ，然后将 **A** 增加 *1* ，将 **B** 减少 *1* 。
*   打印最大 *LCM 对应的 **A** 和 **B** 。*

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效方法:**优化上述幼稚方法的思路是使用一些数学观察。两个同素整数的 *LCM* 等于两个整数的乘积。因此，问题可以简化为求两个同素整数 **A** 和 **B** ，使得 **A+B** = **X** 和 **A×B** 最大。以下是步骤:

*   如果 **X** 是奇数，那么**A =***T5【楼层(X/2)***B =*****楼层(X/2) + 1*** 。
*   否则，如果 **X** 是偶数，那么
    *   如果*楼层( **X** /2)* 为偶数，那么 **A =** ***楼层(X/2)–1***和 **B =** ***楼层(X/2) + 1** 。*
    *   *否则，如果楼层( **X** /2)* 为奇数，则 **A =** ***楼层(X/2)–2***和 **B =** ***楼层(X/2) + 2** 。*

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that print two numbers with
// the sum X and maximum possible LCM
void maxLCMWithGivenSum(int X)
{
    // variables to store the result
    int A, B;

    // If X is odd
    if (X & 1) {
        A = X / 2;
        B = X / 2 + 1;
    }

    // If X is even
    else {

        // If floor(X/2) is even
        if ((X / 2) % 2 == 0) {
            A = X / 2 - 1;
            B = X / 2 + 1;
        }

        // If floor(X/2) is odd
        else {
            A = X / 2 - 2;
            B = X / 2 + 2;
        }
    }

    // Print the result
    cout << A << " " << B << endl;
}

// Driver Code
int main()
{
    // Given Number
    int X = 30;

    // Function call
    maxLCMWithGivenSum(X);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.util.*;

class GFG{

// Function that print two numbers with
// the sum X and maximum possible LCM
static void maxLCMWithGivenSum(int X)
{

    // Variables to store the result
    int A, B;

    // If X is odd
    if ((X & 1) == 1)
    {
        A = X / 2;
        B = X / 2 + 1;
    }

    // If X is even
    else
    {

        // If floor(X/2) is even
        if ((X / 2) % 2 == 0)
        {
            A = X / 2 - 1;
            B = X / 2 + 1;
        }

        // If floor(X/2) is odd
        else
        {
            A = X / 2 - 2;
            B = X / 2 + 2;
        }
    }

    // Print the result
    System.out.println(A + " " + B);
}

// Driver code
public static void main(String[] args)
{

    // Given number
    int X = 30;

    // Function call
    maxLCMWithGivenSum(X);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that print two numbers with
# the sum X and maximum possible LCM
def maxLCMWithGivenSum(X):

    # If X is odd
    if X % 2 != 0:
        A = X / 2
        B = X / 2 + 1

    # If X is even
    else:

        # If floor(X/2) is even
        if (X / 2) % 2 == 0:
            A = X / 2 - 1
            B = X / 2 + 1

        # If floor(X/2) is odd
        else:
            A = X / 2 - 2
            B = X / 2 + 2

    # Print the result
    print(int(A), int(B), end = " ")

# Driver Code
if __name__ == '__main__':

    # Given Number
    X = 30

    # Function call
    maxLCMWithGivenSum(X)

# This code is contributed by virusbuddah_
```

## C#

```
// C# program of the above approach
using System;
class GFG{

// Function that print two numbers with
// the sum X and maximum possible LCM
static void maxLCMWithGivenSum(int X)
{

    // Variables to store the result
    int A, B;

    // If X is odd
    if ((X & 1) == 1)
    {
        A = X / 2;
        B = X / 2 + 1;
    }

    // If X is even
    else
    {

        // If floor(X/2) is even
        if ((X / 2) % 2 == 0)
        {
            A = X / 2 - 1;
            B = X / 2 + 1;
        }

        // If floor(X/2) is odd
        else
        {
            A = X / 2 - 2;
            B = X / 2 + 2;
        }
    }

    // Print the result
    Console.WriteLine(A + " " + B);
}

// Driver code
public static void Main(String[] args)
{

    // Given number
    int X = 30;

    // Function call
    maxLCMWithGivenSum(X);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program of the above approach

// Function that print two numbers with
// the sum X and maximum possible LCM
function maxLCMWithGivenSum(X)
{
    // variables to store the result
    let A, B;

    // If X is odd
    if (X & 1) {
        A = X / 2;
        B = X / 2 + 1;
    }

    // If X is even
    else {

        // If floor(X/2) is even
        if ((X / 2) % 2 == 0) {
            A = X / 2 - 1;
            B = X / 2 + 1;
        }

        // If floor(X/2) is odd
        else {
            A = X / 2 - 2;
            B = X / 2 + 2;
        }
    }

    // Print the result
    document.write(A + " " + B + "<br>");
}

// Driver Code

    // Given Number
    let X = 30;

    // Function call
    maxLCMWithGivenSum(X);

// This code is contributed by Manoj

</script>
```

**Output:** 

```
13 17
```

**时间复杂度:***O(1)*
T5】辅助空间: *O(1)*