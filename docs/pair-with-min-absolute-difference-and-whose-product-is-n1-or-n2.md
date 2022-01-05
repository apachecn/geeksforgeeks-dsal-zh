# 最小绝对差配对，乘积为 N+1 或 N+2

> 原文:[https://www . geesforgeks . org/pair-with-min-绝对差-and-谁的产品是-n1-或-n2/](https://www.geeksforgeeks.org/pair-with-min-absolute-difference-and-whose-product-is-n1-or-n2/)

给定一个整数 **N** ，任务是找到一对乘积为 **N + 1** 或 **N + 2** 且对的绝对差最小的对。

**示例:**

> **输入:** N = 8
> **输出:** 3，3
> **解释:** 3 * 3 = 8 + 1
> **输入:** N = 123
> **输出:** 5，25
> **解释:** 5 * 25 = 123 + 2

**方法:**思想是用一个循环变量 I 从 sqrt(N+2)到 1 迭代一个循环，并检查以下条件:

*   如果 **(n + 1) % i = 0** ，那么我们将打印该对 **(i，(n + 1) / i)** 。
*   如果 **(n + 2) % i = 0** ，那么我们将打印该对 **(i，(n + 2) / i)** 。
*   打印的第一对将是绝对差异最小的一对。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print pair (a, b)
// such that a*b=N+1 or N+2
void closestDivisors(int n)
{
    // Loop to iterate over the
    // desired possible values
    for (int i = sqrt(n + 2);
         i > 0; i--) {

        // Check for condition 1
        if ((n + 1) % i == 0) {
            cout << i << ", "
                 << (n + 1) / i;
            break;
        }

        // Check for condition 2
        if ((n + 2) % i == 0) {
            cout << i << ", "
                 << (n + 2) / i;
            break;
        }
    }
}

// Driver Code
int main()
{
    // Given Number
    int N = 123;

    // Function Call
    closestDivisors(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to print pair (a, b)
// such that a*b=N+1 or N+2
static void closestDivisors(int n)
{
    // Loop to iterate over the
    // desired possible values
    for (int i = (int)Math.sqrt(n + 2); i > 0; i--)
    {

        // Check for condition 1
        if ((n + 1) % i == 0)
        {
           System.out.print(i +  ", " +
                           (n + 1) / i);
            break;
        }

        // Check for condition 2
        if ((n + 2) % i == 0)
        {
            System.out.print(i + ", " +
                            (n + 2) / i);
            break;
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    // Given Number
    int N = 123;

    // Function Call
    closestDivisors(N);
}
}

// This code is contributed by rock_cool
```

## 计算机编程语言

```
# Python3 program for the above approach
from math import sqrt, ceil, floor

# Function to prpair (a, b)
# such that a*b=N+1 or N+2
def closestDivisors(n):

    # Loop to iterate over the
    # desired possible values
    for i in range(ceil(sqrt(n + 2)), -1, -1):

        # Check for condition 1
        if ((n + 1) % i == 0):
            print(i, ",", (n + 1) // i)
            break

        # Check for condition 2
        if ((n + 2) % i == 0):
            print(i, ",", (n + 2) // i)
            break

# Driver Code
if __name__ == '__main__':

    # Given Number
    N = 123

    # Function Call
    closestDivisors(N)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to print pair (a, b)
// such that a*b=N+1 or N+2
static void closestDivisors(int n)
{
    // Loop to iterate over the
    // desired possible values
    for (int i = (int)Math.Sqrt(n + 2); i > 0; i--)
    {

        // Check for condition 1
        if ((n + 1) % i == 0)
        {
           Console.Write(i +  ", " +
                           (n + 1) / i);
            break;
        }

        // Check for condition 2
        if ((n + 2) % i == 0)
        {
            Console.Write(i + ", " +
                         (n + 2) / i);
            break;
        }
    }
}

// Driver Code
public static void Main(string[] args)
{
    // Given Number
    int N = 123;

    // Function Call
    closestDivisors(N);
}
}

// This code is contributed by Ritik Bansal
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to print pair (a, b)
// such that a*b=N+1 or N+2
function closestDivisors(n)
{
    // Loop to iterate over the
    // desired possible values
    for (var i = parseInt(Math.sqrt(n + 2));
         i > 0; i--) {

        // Check for condition 1
        if ((n + 1) % i == 0) {

            document.write(i+", "+parseInt((n + 1) / i));
            break;
        }

        // Check for condition 2
        if ((n + 2) % i == 0) {
            document.write(i+", "+parseInt((n + 2) / i));
            break;
        }
    }
}

// Driver Code

// Given Number
N = 123;

// Function Call
closestDivisors(N);

</script>
```

**Output:** 

```
5, 25
```

**时间复杂度:***O(sqrt(N))*
T5】辅助空间: *O(1)*