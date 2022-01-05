# 计算与倒数之差为 k 的乘积的数

> 原文:[https://www . geeksforgeeks . org/counting-numbers-谁的反向差异是 k 的乘积/](https://www.geeksforgeeks.org/counting-numbers-whose-difference-from-reverse-is-a-product-of-k/)

给定两个数字 l 和 r。计算 l 和 r 之间的总数，当从它们各自的倒数中减去时，差就是 k 的乘积。
**例:**

```
Input : 20 23 6
Output : 2
20 and 22 are the two numbers.
|20-2| = 18 which is a product of 6
|22-22| = 0 which is a product of 6

Input : 35 45 5
Output : 2
38 and 44 are the two numbers.
|38-83| = 45 which is a product of 5
|44-44| = 0 which is a product of 5
```

**方法:**对于给定范围内的每个数字，检查该数字与其反向数字之间的差值是否可被 k 整除，如果是，则递增计数。

## C++

```
// C++ program to Count the numbers
// within a given range in which when
// you subtract a number from its
// reverse, the difference is a product
// of k
#include <iostream>
using namespace std;

bool isRevDiffDivisible(int x, int k)
{
    // function to check if the number
    // and its reverse have their
    // absolute difference divisible by k
    int n = x;
    int m = 0;
    int flag;
    while (x > 0)
    {  
        // reverse the number
        m = m * 10 + x % 10;
        x /= 10;
    }

    return (abs(n - m) % k == 0);
}

int countNumbers(int l, int r, int k)
{
    int count = 0;
    for (int i = l; i <= r; i++)   
        if (isRevDiffDivisible(i, k))       
            ++count;
    return count;
}

// Driver code
int main()
{
    int l = 20, r = 23, k = 6;
    cout << countNumbers(l, r, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Count the
// numbers within a given range
// in which when you subtract
// a number from its reverse,
// the difference is a product of k
import java.io.*;
import java.math.*;

class GFG {

    static boolean isRevDiffDivisible(int x, int k)
    {
        // function to check if the number
        // and its reverse have their
        // absolute difference divisible by k
        int n = x;
        int m = 0;
        int flag;
        while (x > 0)
        {
            // reverse the number
            m = m * 10 + x % 10;
            x /= 10;
        }

        return (Math.abs(n - m) % k == 0);
    }

    static int countNumbers(int l, int r, int k)
    {
        int count = 0;
        for (int i = l; i <= r; i++)
            if (isRevDiffDivisible(i, k))    
                ++count;
        return count;
    }

    // Driver code
    public static void main(String args[])
    {
        int l = 35, r = 45, k = 5;
        System.out.println(countNumbers(l, r, k));
    }
}

// This code is contributed
// by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python 3 program to Count the numbers
# within a given range in which when you
# subtract a number from its reverse,
# the difference is a product of k

def isRevDiffDivisible(x, k) :
    # function to check if the number
    # and its reverse have their
    # absolute difference divisible by k
    n = x; m = 0
    while (x > 0) :

        # Reverse the number
        m = m * 10 + x % 10
        x = x // 10

    return (abs(n - m) % k == 0)

def countNumbers(l, r, k) :
    count = 0
    for i in range(l, r + 1) :

        if (isRevDiffDivisible(i, k)) :
            count = count + 1

    return count

# Driver code
l = 20; r = 23; k = 6
print(countNumbers(l, r, k))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to Count the
// numbers within a given range
// in which when you subtract
// a number from its reverse,
// the difference is a product of k
using System;

class GFG {

    static bool isRevDiffDivisible(int x, int k)
    {
        // function to check if the number
        // and its reverse have their
        // absolute difference divisible by k
        int n = x;
        int m = 0;

        // int flag;
        while (x > 0)
        {
            // reverse the number
            m = m * 10 + x % 10;
            x /= 10;
        }

        return (Math.Abs(n - m) % k == 0);
    }

    static int countNumbers(int l, int r, int k)
    {
        int count = 0;

        for (int i = l; i <= r; i++)
            if (isRevDiffDivisible(i, k))
                ++count;
        return count;
    }

    // Driver code
    public static void Main()
    {
        int l = 35, r = 45, k = 5;
        Console.WriteLine(countNumbers(l, r, k));
    }
}

// This code is contributed
// by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Count the
// numbers within a given
// range in which when you
// subtract a number from
// its reverse, the difference
// is a product of k
function isRevDiffDivisible($x, $k)
{
    // function to check if
    // the number and its
    // reverse have their
    // absolute difference
    // divisible by k
    $n = $x;
    $m = 0;
    $flag;
    while ($x > 0)
    {
        // reverse the number
        $m = $m * 10 + $x % 10;
        $x = (int)$x / 10;
    }

    return (abs($n - $m) %
                $k == 0);
}

function countNumbers($l, $r, $k)
{
    $count = 0;
    for ($i = $l; $i <= $r; $i++)
        if (isRevDiffDivisible($i, $k))
            ++$count;
    return $count;
}

// Driver code
$l = 20; $r = 23; $k = 6;
echo countNumbers($l, $r, $k);

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>
// javascript program to Count the
// numbers within a given range
// in which when you subtract
// a number from its reverse,
// the difference is a product of k

function isRevDiffDivisible(x , k)
{
    // function to check if the number
    // and its reverse have their
    // absolute difference divisible by k
    var n = x;
    var m = 0;
    var flag;
    while (x > 0)
    {
        // reverse the number
        m = m * 10 + x % 10;
        x = parseInt(x/10);
    }

    return (Math.abs(n - m) % k == 0);
}

function countNumbers(l , r , k)
{
    var count = 0;
    for (i = l; i <= r; i++)
        if (isRevDiffDivisible(i, k))    
            count++;
    return count;
}

// Driver code

var l = 35, r = 45, k = 5;
document.write(countNumbers(l, r, k));

// This code contributed by Princi Singh

</script>
```

**输出:**

```
2
```