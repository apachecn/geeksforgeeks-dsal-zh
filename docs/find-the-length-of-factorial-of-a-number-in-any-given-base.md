# 求任意给定基数上一个数的阶乘长度

> 原文:[https://www . geeksforgeeks . org/find-任意给定基数的阶乘长度/](https://www.geeksforgeeks.org/find-the-length-of-factorial-of-a-number-in-any-given-base/)

给定一个整数 **n** 和基数 **B** ，任务是找到 **n 的长度！**在基地 **B** 。
**举例:**

> **输入:** n = 4，b = 10
> T3】输出:2
> T6】说明: 4！= 24，因此位数为 2
> **输入:** n = 4，b = 16
> **输出:** 2
> **解释:** 4！= 18 为基数 16，因此位数为 2

**方法:**
为了解决这个问题，我们使用了卡门涅斯基公式，该公式近似于阶乘
中的位数

```
f(x) =    log10( ((n/e)^n) * sqrt(2*pi*n))
```

从 n 到基数 b 的位数由**logb(n)= log10(n)/log10(b)**给出。因此，利用对数的性质，基 b 中阶乘的位数可以通过
得到

```
f(x) = ( n* log10(( n/ e)) + log10(2*pi*n)/2  ) / log10(b)
```

这种方法可以处理 32 位整数甚至更大的输入！
下面代码是上面思路的实现:

## C++

```
// A optimised program to find the
// number of digits in a factorial in base b
#include <bits/stdc++.h>
using namespace std;

// Returns the number of digits present
// in n! in base b Since the result can be large
// long long is used as return type
long long findDigits(int n, int b)
{
    // factorial of -ve number
    // doesn't exists
    if (n < 0)
        return 0;

    // base case
    if (n <= 1)
        return 1;

    // Use Kamenetsky formula to calculate
    // the number of digits
    double x = ((n * log10(n / M_E) +
                log10(2 * M_PI * n) /
                2.0)) / (log10(b));

    return floor(x) + 1;
}

// Driver Code
int main()
{
    //calling findDigits(Number, Base)
    cout << findDigits(4, 16) << endl;
    cout << findDigits(5, 8) << endl;
    cout << findDigits(12, 16) << endl;
    cout << findDigits(19, 13) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A optimised program to find the
// number of digits in a factorial in base b
class GFG{

// Returns the number of digits present
// in n! in base b Since the result can be large
// long is used as return type
static long findDigits(int n, int b)
{
    // factorial of -ve number
    // doesn't exists
    if (n < 0)
        return 0;

    // base case
    if (n <= 1)
        return 1;
    double M_PI = 3.141592;
    double M_E = 2.7182;

    // Use Kamenetsky formula to calculate
    // the number of digits
    double x = ((n * Math.log10(n / M_E) +
            Math.log10(2 * M_PI * n) /
                2.0)) / (Math.log10(b));

    return (long) (Math.floor(x) + 1);
}

// Driver Code
public static void main(String[] args)
{
    //calling findDigits(Number, Base)
    System.out.print(findDigits(4, 16) +"\n");
    System.out.print(findDigits(5, 8) +"\n");
    System.out.print(findDigits(12, 16) +"\n");
    System.out.print(findDigits(19, 13) +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
from math import log10,floor

# A optimised program to find the
# number of digits in a factorial in base b

# Returns the number of digits present
# in n! in base b Since the result can be large
# long long is used as return type
def findDigits(n, b):

    # factorial of -ve number
    # doesn't exists
    if (n < 0):
        return 0

    M_PI = 3.141592
    M_E = 2.7182

    # base case
    if (n <= 1):
        return 1

    # Use Kamenetsky formula to calculate
    # the number of digits
    x = ((n * log10(n / M_E) + log10(2 * M_PI * n) / 2.0)) / (log10(b))

    return floor(x) + 1

# Driver Code
if __name__ == '__main__':

    #calling findDigits(Number, Base)
    print(findDigits(4, 16))
    print(findDigits(5, 8))
    print(findDigits(12, 16))
    print(findDigits(19, 13))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// A optimised C# program to find the
// number of digits in a factorial in base b
using System;

class GFG{

    // Returns the number of digits present
    // in n! in base b Since the result can be large
    // long is used as return type
    static long findDigits(int n, int b)
    {
        // factorial of -ve number
        // doesn't exists
        if (n < 0)
            return 0;

        // base case
        if (n <= 1)
            return 1;
        double M_PI = 3.141592;
        double M_E = 2.7182;

        // Use Kamenetsky formula to calculate
        // the number of digits
        double x = ((n * Math.Log10(n / M_E) +
                Math.Log10(2 * M_PI * n) /
                    2.0)) / (Math.Log10(b));

        return (long) (Math.Floor(x) + 1);
    }

    // Driver Code
    public static void Main(string[] args)
    {
        // calling findDigits(Number, Base)
        Console.WriteLine(findDigits(4, 16));
        Console.WriteLine(findDigits(5, 8));
        Console.WriteLine(findDigits(12, 16));
        Console.WriteLine(findDigits(19, 13));
    }
}

// This code is contributed by Yash_R
```

## java 描述语言

```
<script>

// A optimised program to find the
// number of digits in a factorial in base b

// Returns the number of digits present
// in n! in base b Since the result can be large
// long long is used as return type
function findDigits(n, b)
{

    // factorial of -ve number
    // doesn't exists
    if (n < 0)
        return 0;

    // base case
    if (n <= 1)
        return 1;

    var M_PI = 3.141592;
    var M_E = 2.7182;

    // Use Kamenetsky formula to calculate
    // the number of digits
    var x = ((n * Math.log10(n / M_E) +
                Math.log10(2 * M_PI * n) /
                    2.0)) / (Math.log10(b));

    return Math.floor(x) + 1;
}

// Driver Code
// calling findDigits(Number, Base)
document.write(findDigits(4, 16) + "<br>");
document.write( findDigits(5, 8) + "<br>");
document.write( findDigits(12, 16) + "<br>");
document.write( findDigits(19, 13) + "<br>");

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
2
3
8
16
```

**参考:**T2oeis.org