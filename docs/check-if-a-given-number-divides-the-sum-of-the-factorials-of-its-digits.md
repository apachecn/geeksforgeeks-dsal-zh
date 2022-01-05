# 检查给定的数字是否除以其数字的阶乘之和

> 原文:[https://www . geeksforgeeks . org/check-if-a-给定数字除以其位数的阶乘之和/](https://www.geeksforgeeks.org/check-if-a-given-number-divides-the-sum-of-the-factorials-of-its-digits/)

给定一个整数 **N** ，任务是检查 **N** 是否除以其位数的阶乘之和。

**示例:**

> **输入:**N = 19
> T3】输出:是
> 1！+ 9!= 1 + 362880 = 362881，可被 19 整除。
> 
> **输入:**N = 20
> T3】输出:否
> 0！+ 2!= 1 + 4 = 5，不能被 20 整除。

**方法:**首先，将从 **0** 到 **9** 的所有数字的阶乘存储在一个数组中。并且，对于给定的数字 **N** 检查它是否除以其数字的阶乘之和。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if n divides
// the sum of the factorials of its digits
bool isPossible(int n)
{

    // To store factorials of digits
    int fac[10];
    fac[0] = fac[1] = 1;

    for (int i = 2; i < 10; i++)
        fac[i] = fac[i - 1] * i;

    // To store sum of the factorials
    // of the digits
    int sum = 0;

    // Store copy of the given number
    int x = n;

    // Store sum of the factorials
    // of the digits
    while (x) {
        sum += fac[x % 10];
        x /= 10;
    }

    // If it is divisible
    if (sum % n == 0)
        return true;

    return false;
}

// Driver code
int main()
{
    int n = 19;

    if (isPossible(n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function that returns true if n divides
    // the sum of the factorials of its digits
    static boolean isPossible(int n)
    {

        // To store factorials of digits
        int fac[] = new int[10];
        fac[0] = fac[1] = 1;

        for (int i = 2; i < 10; i++)
            fac[i] = fac[i - 1] * i;

        // To store sum of the factorials
        // of the digits
        int sum = 0;

        // Store copy of the given number
        int x = n;

        // Store sum of the factorials
        // of the digits
        while (x != 0)
        {
            sum += fac[x % 10];
            x /= 10;
        }

        // If it is divisible
        if (sum % n == 0)
            return true;

        return false;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 19;

        if (isPossible(n))
            System.out.println("Yes");
        else
            System.out.println("No");

    }
}

// This code is contributed by Ryuga
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function that returns true if n divides
# the sum of the factorials of its digits
def isPossible(n):

    # To store factorials of digits
    fac = [0 for i in range(10)]
    fac[0] = 1
    fac[1] = 1

    for i in range(2, 10, 1):
        fac[i] = fac[i - 1] * i

    # To store sum of the factorials
    # of the digits
    sum = 0

    # Store copy of the given number
    x = n

    # Store sum of the factorials
    # of the digits
    while (x):
        sum += fac[x % 10]
        x = int(x / 10)

    # If it is divisible
    if (sum % n == 0):
        return True

    return False

# Driver code
if __name__ == '__main__':
    n = 19

    if (isPossible(n)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

    // Function that returns true if n divides
    // the sum of the factorials of its digits
    static bool isPossible(int n)
    {

        // To store factorials of digits
        int[] fac = new int[10];
        fac[0] = fac[1] = 1;

        for (int i = 2; i < 10; i++)
            fac[i] = fac[i - 1] * i;

        // To store sum of the factorials
        // of the digits
        int sum = 0;

        // Store copy of the given number
        int x = n;

        // Store sum of the factorials
        // of the digits
        while (x != 0)
        {
            sum += fac[x % 10];
            x /= 10;
        }

        // If it is divisible
        if (sum % n == 0)
            return true;

        return false;
    }

    // Driver code
    public static void Main ()
    {
        int n = 19;

        if (isPossible(n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Code_Mech.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if n divides
// the sum of the factorials of its digits
function isPossible($n)
{

    // To store factorials of digits
    $fac = array();
    $fac[0] = $fac[1] = 1;

    for ($i = 2; $i < 10; $i++)
        $fac[$i] = $fac[$i - 1] * $i;

    // To store sum of the factorials
    // of the digits
    $sum = 0;

    // Store copy of the given number
    $x = $n;

    // Store sum of the factorials
    // of the digits
    while ($x)
    {
        $sum += $fac[$x % 10];
        $x /= 10;
    }

    // If it is divisible
    if ($sum % $n == 0)
        return true;

    return false;
}

// Driver code
$n = 19;

if (isPossible($n))
    echo "Yes";
else
    echo "No";

// This code is contributed by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function that returns true if n divides
// the sum of the factorials of its digits
function isPossible(n)
{

    // To store factorials of digits
    var fac = new Array(10);
    fac[0] = fac[1] = 1;

    for(var i = 2; i < 10; i++)
        fac[i] = fac[i - 1] * i;

    // To store sum of the factorials
    // of the digits
    var sum = 0;

    // Store copy of the given number
    var x = n;

    // Store sum of the factorials
    // of the digits
    while (x != 0)
    {
        sum += fac[x % 10];
        x = parseInt(x / 10);
    }

    // If it is divisible
    if (sum % n == 0)
        return true;

    return false;
}

// Driver Code
var n = 19;

if (isPossible(n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by Khushboogoyal499

</script>
```

**Output:** 

```
Yes
```