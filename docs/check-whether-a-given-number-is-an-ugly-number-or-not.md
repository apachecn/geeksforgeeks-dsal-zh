# 检查给定的数字是否是丑陋的数字

> 原文:[https://www . geesforgeks . org/check-给定的数字是不是一个丑陋的数字/](https://www.geeksforgeeks.org/check-whether-a-given-number-is-an-ugly-number-or-not/)

给定一个整数 **N** ，任务是找出给定的数字是不是丑数。

> [丑数](https://www.geeksforgeeks.org/ugly-numbers/)是指质因数只有 2、3 或 5 的数。

**示例:**

> **输入:** N = 14
> **输出:**否
> **说明:**
> 14 并不丑，因为它包含了另一个质因数 7。
> 
> **输入:** N = 6
> **输出:**是
> **说明:**
> 6 是一个丑陋的，因为它包括 2 和 3。

**方法:**思路是用[递归](https://www.geeksforgeeks.org/recursion/)解决这个问题，检查一个数是否能被 2、3 或 5 整除。如果是，然后除以那个数，递归地检查一个数是否是一个丑陋的数。如果在任何时候，没有这样的除数，那么返回假，否则返回真。

以下是上述方法的实现:

## C++

```
// C++ implementation to check
// if a number is an ugly
// number or not

#include <stdio.h>
#include <stdlib.h>

// Function to check if a number
// is an ugly number or not
int isUgly(int n)
{
    // Base Cases
    if (n == 1)
        return 1;
    if (n <= 0)
        return 0;

    // Condition to check if the
    // number is divided by 2, 3, or 5
    if (n % 2 == 0) {
        return (isUgly(n / 2));
    }
    if (n % 3 == 0) {
        return (isUgly(n / 3));
    }
    if (n % 5 == 0) {
        return (isUgly(n / 5));
    }

    // Otherwise return false
    return 0;
}
// Driver Code
int main()
{
    int no = isUgly(14);
    if (no == 1)
        printf("Yes");
    else
        printf("No");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to
// check if a number is ugly number
class GFG {

    // Function to check the ugly
    // number
    static int isUgly(int n)
    {
        // Base Cases
        if (n == 1)
            return 1;
        if (n <= 0)
            return 0;

        // Condition to check if
        // a number is divide by
        // 2, 3, or 5
        if (n % 2 == 0) {
            return (isUgly(n / 2));
        }
        if (n % 3 == 0) {
            return (isUgly(n / 3));
        }
        if (n % 5 == 0) {
            return (isUgly(n / 5));
        }
        return 0;
    }

    // Driver Code
    public static void main(String args[])
    {
        int no = isUgly(14);
        if (no == 1)
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python3 implementation to check
# if a number is an ugly number
# or not

# Function to check if a number
# is an ugly number or not
def isUgly(n):

    # Base Cases
    if (n == 1):
        return 1
    if (n <= 0):
        return 0

    # Condition to check if the
    # number is divided by 2, 3, or 5
    if (n % 2 == 0):
        return (isUgly(n // 2))

    if (n % 3 == 0):
        return (isUgly(n // 3))

    if (n % 5 == 0):
        return (isUgly(n // 5))

    # Otherwise return false
    return 0

# Driver Code
if __name__ == "__main__":

    no = isUgly(14)

    if (no == 1):
        print("Yes")
    else:
        print("No")

# This code is contributed by chitranayal
```

## C#

```
// C# implementation to check
// if a number is ugly number
using System;

class GFG{

// Function to check the ugly
// number
static int isUgly(int n)
{

    // Base Cases
    if (n == 1)
        return 1;
    if (n <= 0)
        return 0;

    // Condition to check if
    // a number is divide by
    // 2, 3, or 5
    if (n % 2 == 0)
    {
        return (isUgly(n / 2));
    }
    if (n % 3 == 0)
    {
        return (isUgly(n / 3));
    }
    if (n % 5 == 0)
    {
        return (isUgly(n / 5));
    }
    return 0;
}

// Driver Code
public static void Main(String []args)
{
    int no = isUgly(14);

    if (no == 1)
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript implementation to check
// if a number is an ugly
// number or not

// Function to check if a number
// is an ugly number or not
function isUgly(n)
{
    // Base Cases
    if (n == 1)
        return 1;
    if (n <= 0)
        return 0;

    // Condition to check if the
    // number is divided by 2, 3, or 5
    if (n % 2 == 0) {
        return (isUgly(n / 2));
    }
    if (n % 3 == 0) {
        return (isUgly(n / 3));
    }
    if (n % 5 == 0) {
        return (isUgly(n / 5));
    }

    // Otherwise return false
    return 0;
}
// Driver Code

    let no = isUgly(14);
    if (no == 1)
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
No
```