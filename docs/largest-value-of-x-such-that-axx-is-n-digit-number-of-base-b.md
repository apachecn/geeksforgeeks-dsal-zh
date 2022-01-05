# x 的最大值，使得 axx 为基数 b 的 N 位数

> 原文:[https://www . geesforgeks . org/最大值-x-so-axx-is-n 位数-base-b/](https://www.geeksforgeeks.org/largest-value-of-x-such-that-axx-is-n-digit-number-of-base-b/)

给定整数 **a** 、 **b** 、 **N** ，任务是找到最大的数 **x** ，使得![a*x^{x}    ](img/55cca891b992aa938afcd47eecd30a96.png "Rendered by QuickLaTeX.com")是基数 b 的 N 位数。

**示例:**

> **输入:** a = 2，b = 10，N = 2
> **输出:** 3
> **说明:**
> 此处 2 * 3 <sup>3</sup> = 54，其位数= 2，
> 但 2 * 4 <sup>4</sup> = 512，其位数= 3，不等于 N.
> 因此，x 的最大值为 2。
> 
> **输入:** a = 1，b = 2，N = 3
> **输出:** 2
> **解释:**
> 1 * 2 <sup>2</sup> = 4，二进制表示为 100，有 3 位数字。

**进场:**这个问题可以用[二分搜索法](http://www.geeksforgeeks.org/binary-search/)解决。

*   基数![b    ](img/56c19e62ea115719245402c109e4c477.png "Rendered by QuickLaTeX.com")中![ax^x    ](img/3c8ce68276091deedd2436f99bb88427.png "Rendered by QuickLaTeX.com")的位数为![\lceil\log_b{ax^x}\rceil  ](img/c6363d56e4a37a474fb9ce6b7ad19f47.png "Rendered by QuickLaTeX.com")。
*   二分搜索法用来寻找最大的![x    ](img/bd0dd68c093f19d4b996e479298a7648.png "Rendered by QuickLaTeX.com")，使得![b    ](img/56c19e62ea115719245402c109e4c477.png "Rendered by QuickLaTeX.com")中![ax^x    ](img/3c8ce68276091deedd2436f99bb88427.png "Rendered by QuickLaTeX.com")的位数正好是![n  ](img/31d70d7c99878a33c601d487c9b6eb43.png "Rendered by QuickLaTeX.com")。
*   在二分搜索法，我们会检查数字的个数![ax^x  ](img/0fed5701e032821eb493546b3b500d81.png "Rendered by QuickLaTeX.com")，其中![x = mid  ](img/80c1ebf49f30d4eb9ba65581399fb321.png "Rendered by QuickLaTeX.com")，并根据这个数字改变指针。
    T3】

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find log_b(a)
double log(int a, int b)
{
    return log10(a) / log10(b);
}

int get(int a, int b, int n)
{

    // Set two pointer for binary search
    int lo = 0, hi = 1e6;

    int ans = 0;

    while (lo <= hi) {
        int mid = (lo + hi) / 2;

        // Calculating number of digits
        // of a*mid^mid in base b
        int dig = ceil((mid * log(mid, b)
                        + log(a, b)));

        if (dig > n) {

            // If number of digits > n
            // we can simply ignore it
            // and decrease our pointer
            hi = mid - 1;
        }
        else {

            // if number of digits <= n,
            // we can go higher to
            // reach value exactly equal to n
            ans = mid;
            lo = mid + 1;
        }
    }

    // return the largest value of x
    return ans;
}

// Driver Code
int main()
{

    int a = 2, b = 2, n = 6;

    cout << get(a, b, n)
         << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG{

// Function to find log_b(a)
static int log(int a, int b)
{
    return (int)(Math.log10(a) /
                 Math.log10(b));
}

static int get(int a, int b, int n)
{

    // Set two pointer for binary search
    int lo = 0, hi = (int) 1e6;

    int ans = 0;

    while (lo <= hi)
    {
        int mid = (lo + hi) / 2;

        // Calculating number of digits
        // of a*mid^mid in base b
        int dig = (int) Math.ceil((mid * log(mid, b) +
                                         log(a, b)));

        if (dig > n)
        {

            // If number of digits > n
            // we can simply ignore it
            // and decrease our pointer
            hi = mid - 1;
        }
        else
        {

            // If number of digits <= n,
            // we can go higher to reach
            // value exactly equal to n
            ans = mid;
            lo = mid + 1;
        }
    }

    // Return the largest value of x
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int a = 2, b = 2, n = 6;

    System.out.print(get(a, b, n) + "\n");
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

from math import log10,ceil,log

# Function to find log_b(a)
def log1(a,b):
    return log10(a)//log10(b)

def get(a,b,n):
    # Set two pointer for binary search
    lo = 0
    hi = 1e6

    ans = 0

    while (lo <= hi):
        mid = (lo + hi) // 2

        # Calculating number of digits
        # of a*mid^mid in base b
        dig = ceil((mid * log(mid, b) + log(a, b)))

        if (dig > n):
            # If number of digits > n
            # we can simply ignore it
            # and decrease our pointer
            hi = mid - 1

        else:
            # if number of digits <= n,
            # we can go higher to
            # reach value exactly equal to n
            ans = mid
            lo = mid + 1

    # return the largest value of x
    return ans

# Driver Code
if __name__ == '__main__':
    a = 2
    b = 2
    n = 6

    print(int(get(a, b, n)))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;
class GFG{

// Function to find log_b(a)
static int log(int a, int b)
{
    return (int)(Math.Log10(a) /
                 Math.Log10(b));
}

static int get(int a, int b, int n)
{

    // Set two pointer for binary search
    int lo = 0, hi = (int) 1e6;

    int ans = 0;

    while (lo <= hi)
    {
        int mid = (lo + hi) / 2;

        // Calculating number of digits
        // of a*mid^mid in base b
        int dig = (int)Math.Ceiling((double)(mid *
                                         log(mid, b) +
                                         log(a, b)));

        if (dig > n)
        {

            // If number of digits > n
            // we can simply ignore it
            // and decrease our pointer
            hi = mid - 1;
        }
        else
        {

            // If number of digits <= n,
            // we can go higher to reach
            // value exactly equal to n
            ans = mid;
            lo = mid + 1;
        }
    }

    // Return the largest value of x
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int a = 2, b = 2, n = 6;

    Console.Write(get(a, b, n) + "\n");
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find log_b(a)
function log(a, b)
{
    return (Math.log10(a) /
                 Math.log10(b));
}

function get(a, b, n)
{

    // Set two pointer for binary search
    let lo = 0, hi = 1e6;

    let ans = 0;

    while (lo <= hi)
    {
        let mid = Math.floor((lo + hi) / 2);

        // Calculating number of digits
        // of a*mid^mid in base b
        let dig =  Math.ceil((mid * log(mid, b) +
                                         log(a, b)));

        if (dig > n)
        {

            // If number of digits > n
            // we can simply ignore it
            // and decrease our pointer
            hi = mid - 1;
        }
        else
        {

            // If number of digits <= n,
            // we can go higher to reach
            // value exactly equal to n
            ans = mid;
            lo = mid + 1;
        }
    }

    // Return the largest value of x
    return ans;
}
// Driver Code

    let a = 2, b = 2, n = 6;

    document.write(get(a, b, n) + "\n");

</script>
```

**Output:** 

```
3
```