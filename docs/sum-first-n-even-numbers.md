# 前 n 个偶数之和

> 原文:[https://www.geeksforgeeks.org/sum-first-n-even-numbers/](https://www.geeksforgeeks.org/sum-first-n-even-numbers/)

给定一个数字 **n** 。问题是找到第一个 **n** 个偶数的和。
**例:**

```
Input : n = 4
Output : 20
Sum of first 4 even numbers
= (2 + 4 + 6 + 8) = 20 

Input : n = 20
Output : 420
```

**天真的方法:**迭代第一个 **n** 个偶数并相加。

## C++

```
// C++ implementation to find sum of
// first n even numbers
#include <bits/stdc++.h>

using namespace std;

// function to find sum of
// first n even numbers
int evenSum(int n)
{
    int curr = 2, sum = 0;

    // sum of first n even numbers
    for (int i = 1; i <= n; i++) {
        sum += curr;

        // next even number
        curr += 2;
    }

    // required sum
    return sum;
}

// Driver program to test above
int main()
{
    int n = 20;
    cout << "Sum of first " << n
         << " Even numbers is: " << evenSum(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find sum
// of first n even numbers
import java.util.*;
import java.lang.*;

public class GfG{

    // function to find sum of
    // first n even numbers
    static int evenSum(int n)
    {
        int curr = 2, sum = 0;

        // sum of first n even numbers
        for (int i = 1; i <= n; i++) {
            sum += curr;

            // next even number
            curr += 2;
        }

        // required sum
        return sum;    
    }

    // driver function
    public static void main(String argc[])
    {
        int n = 20;
        System.out.println("Sum of first " + n +
                          " Even numbers is: " +
                          evenSum(n));
    }

}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 implementation to find sum of
# first n even numbers

# function to find sum of
# first n even numbers
def evensum(n):
    curr = 2
    sum = 0
    i = 1

    # sum of first n even numbers
    while i <= n:
        sum += curr

        # next even number
        curr += 2
        i = i + 1
    return sum

# Driver Code
n = 20
print("sum of first ", n, "even number is: ",
      evensum(n))

# This article is contributed by rishabh_jain
```

## C#

```
// C# implementation to find sum
// of first n even numbers
using System;

public class GfG {

    // function to find sum of
    // first n even numbers
    static int evenSum(int n)
    {
        int curr = 2, sum = 0;

        // sum of first n even numbers
        for (int i = 1; i <= n; i++) {
            sum += curr;

            // next even number
            curr += 2;
        }

        // required sum
        return sum;
    }

    // driver function
    public static void Main()
    {
        int n = 20;

        Console.WriteLine("Sum of first " + n
         + " Even numbers is: " + evenSum(n));
    }
}

// This code is contributed by vt-m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find sum of
// first n even numbers

// function to find sum of
// first n even numbers
function evenSum($n)
{
    $curr = 2;
    $sum = 0;

    // sum of first n even numbers
    for ($i = 1; $i <= $n; $i++) {
        $sum += $curr;

        // next even number
        $curr += 2;
    }

    // required sum
    return $sum;
}

// Driver program to test above

    $n = 20;
    echo "Sum of first ".$n." Even numbers is: ".evenSum($n);

// this code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript implementation to find sum of
// first n even numbers

    // function to find sum of
    // first n even numbers
    function evenSum(n)
    {
        let curr = 2, sum = 0;

        // sum of first n even numbers
        for (let i = 1; i <= n; i++) {
            sum += curr;

            // next even number
            curr += 2;
        }

        // required sum
        return sum;
    }

    // Driver program to test above

    let n = 20;
    document.write("Sum of first " + n +
    " Even numbers is: " + evenSum(n));

//This code is contributed by Surbhi Tyagi

</script>
```

**Output**

```
Sum of first 20 Even numbers is: 420
```