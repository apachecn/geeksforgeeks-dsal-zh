# 求两个同素整数，第一个除 A，第二个除 B

> 原文:[https://www . geeksforgeeks . org/find-two-co-prime-integers-so-第一除 a 和第二除 b/](https://www.geeksforgeeks.org/find-two-co-prime-integers-such-that-the-first-divides-a-and-the-second-divides-b/)

给定两个整数 **A** 和 **B** ，任务是找到两个同质数 **C1** 和 **C2** ，使得 **C1** 除 **A** 和 **C2** 除 **B** 。
**举例:**

> **输入:** A = 12，B = 16
> T3】输出:3 4
> 12% 3 = 0
> 16% 4 = 0
> gcd(3，4)= 1
> T9】输入: A = 542，B = 762
> **输出:** 271 381

**天真方法:**一个简单的解决方案是存储 **A** 和 **B** 的所有除数，然后成对迭代 **A** 和 **B** 的所有除数，以找到共素的元素对。
**有效途径:**如果整数 **d** 除以 **gcd(a，b)** ，则 **gcd(a / d，b / d) = gcd(a，b) / d** 。更正式地说，如果 **num = gcd(a，b)** ，那么 **gcd(a / num，b / num) = 1** 即 **(a / num)** 和 **(b / num)** 是相对同素的。
所以为了找到需要的数字，找到 **gcd(a，b)** 存储在变量 **gcd** 中。现在需要的数字是 **(a / gcd)** 和 **(b / gcd)** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the required numbers
void findNumbers(int a, int b)
{

    // GCD of the given numbers
    int gcd = __gcd(a, b);

    // Printing the required numbers
    cout << (a / gcd) << " " << (b / gcd);
}

// Driver code
int main()
{
    int a = 12, b = 16;

    findNumbers(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.math.*;

class GFG
{
    public static int findGCD(int a, int b)
    {
        if(b == 0)
            return a;
        else
            return findGCD(b, a % b);
    }

    // Function to find the required numbers
    static void findNumbers(int a, int b)
    {

        // GCD of the given numbers
        int gcd = findGCD(a, b);

        // Printing the required numbers
        System.out.println((a / gcd) + " " +
                           (b / gcd));

    }

    // Driver code
    public static void main(String[] args)
    {
        int a = 12, b = 16;

        findNumbers(a, b);
    }
}

// This code is contributed by Naman_Garg
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# import gcd function from math module
from math import gcd

# Function to find the required numbers
def findNumbers(a, b) :

    # GCD of the given numbers
    __gcd = gcd(a, b);

    # Printing the required numbers
    print((a // __gcd), (b // __gcd));

# Driver code
if __name__ == "__main__" :

    a = 12; b = 16;

    findNumbers(a, b);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    public static int findGCD(int a, int b)
    {
        if(b == 0)
            return a;
        else
            return findGCD(b, a % b);
    }

    // Function to find the required numbers
    static void findNumbers(int a, int b)
    {

        // GCD of the given numbers
        int gcd = findGCD(a, b);

        // Printing the required numbers
        Console.Write((a / gcd) + " " +
                      (b / gcd));

    }

    // Driver code
    static public void Main ()
    {
        int a = 12, b = 16;

        findNumbers(a, b);
    }
}

// This code is contributed by ajit
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

function findGCD(a, b)
{
    if (b == 0)
        return a;
    else
        return findGCD(b, a % b);
}

// Function to find the required numbers
function findNumbers(a, b)
{

    // GCD of the given numbers
    var gcd = findGCD(a, b);

    // Printing the required numbers
    document.write((a / gcd) + " " +
                   (b / gcd));
}

// Driver Code
var a = 12, b = 16;

findNumbers(a, b);

// This code is contributed by Khushboogoyal499

</script>
```

**Output:** 

```
3 4
```