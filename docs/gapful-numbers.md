# 目瞪口呆的数字

> 原文:[https://www.geeksforgeeks.org/gapful-numbers/](https://www.geeksforgeeks.org/gapful-numbers/)

**间隙数**是一个至少有 3 位数字的数 **N** ，这样它可以被它的第一个和最后一个数字的连接整除。
很少有空白的数字是:

> 100、105、108、110、120、121、130、132、135、140……

### 检查 N 是否为空白数

给定一个整数 **N** ，任务是检查 **N** 是否为间隙数。如果 **N** 是空白号码，则打印**“是”**否则打印**“否”**。
**举例:**

> **输入:** N = 108
> **输出:**是
> **说明:**
> 108 可被 18 整除
> **输入:** N = 112
> **输出:**否

**方法:**思路是用给定数字的首末数字创建一个数字(比如 **num** ，检查 **N** 是否可以被 **num** 整除。如果 **N** 可以被 **num** 整除，那么它就是一个间隙数，打印**“是”**，否则打印**“否”**。
以下是上述方法的实施:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Find the first digit
int firstDigit(int n)
{
    // Find total number of digits - 1
    int digits = (int)log10(n);

    // Find first digit
    n = (int)(n / pow(10, digits));

    // Return first digit
    return n;
}

// Find the last digit
int lastDigit(int n)
{
    // return the last digit
    return (n % 10);
}

// A function to check Gapful numbers
bool isGapful(int n)
{
    int first_dig = firstDigit(n);
    int last_dig = lastDigit(n);

    int concatenation = first_dig * 10
                        + last_dig;

    // Return true if n is gapful number
    return (n % concatenation == 0);
}

// Driver Code
int main()
{
    // Given Number
    int n = 108;

    // Function Call
    if (isGapful(n))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Find the first digit
static int firstDigit(int n)
{

    // Find total number of digits - 1
    int digits = (int)(Math.log(n) /
                       Math.log(10));

    // Find first digit
    n = (int)(n / Math.pow(10, digits));

    // Return first digit
    return n;
}

// Find the last digit
static int lastDigit(int n)
{

    // Return the last digit
    return (n % 10);
}

// A function to check Gapful numbers
static boolean isGapful(int n)
{
    int first_dig = firstDigit(n);
    int last_dig = lastDigit(n);

    int concatenation = first_dig * 10 +
                        last_dig;

    // Return true if n is gapful number
    return (n % concatenation == 0);
}

// Driver code
public static void main(String[] args)
{

    // Given number
    int n = 108;

    // Function call
    if (isGapful(n))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Pratima Pandey
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Find the first digit
def firstDigit(n):

    # Find total number of digits - 1
    digits = math.log10(n)

    # Find first digit
    n = (n / math.pow(10, digits))

    # Return first digit
    return n

# Find the last digit
def lastDigit(n):

    # return the last digit
    return (n % 10)

# A function to check Gapful numbers
def isGapful(n):

    concatenation = (firstDigit(n) * 10) +\
                     lastDigit(n)

    # Return true if n is gapful number
    return (n % concatenation)

# Driver Code
if __name__=='__main__':

    # Given Number
    n = 108

    # Function Call
    if (isGapful(n)):
        print("Yes")
    else:
        print("No")

# This code is contributed by Ritik Bansal
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Find the first digit
static int firstDigit(int n)
{

    // Find total number of digits - 1
    int digits = (int)(Math.Log(n) /
                       Math.Log(10));

    // Find first digit
    n = (int)(n / Math.Pow(10, digits));

    // Return first digit
    return n;
}

// Find the last digit
static int lastDigit(int n)
{

    // Return the last digit
    return (n % 10);
}

// A function to check Gapful numbers
static bool isGapful(int n)
{
    int first_dig = firstDigit(n);
    int last_dig = lastDigit(n);

    int concatenation = first_dig * 10 +
                        last_dig;

    // Return true if n is gapful number
    return (n % concatenation == 0);
}

// Driver code
public static void Main()
{

    // Given number
    int n = 108;

    // Function call
    if (isGapful(n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// Javascript program for the above approach

    // Find the first digit
    function firstDigit( n)
    {

        // Find total number of digits - 1
        let digits = parseInt( (Math.log(n) / Math.log(10)));

        // Find first digit
        n = parseInt( (n / Math.pow(10, digits)));

        // Return first digit
        return n;
    }

    // Find the last digit
    function lastDigit( n)
    {

        // Return the last digit
        return (n % 10);
    }

    // A function to check Gapful numbers
    function isGapful( n)
    {
        let first_dig = firstDigit(n);
        let last_dig = lastDigit(n);

        let concatenation = first_dig * 10 + last_dig;

        // Return true if n is gapful number
        return (n % concatenation == 0);
    }

    // Driver code

    // Given number
    let n = 108;

    // Function call
    if (isGapful(n))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***O(1)*
T5】参考:[https://oeis.org/A108343](https://oeis.org/A108343)