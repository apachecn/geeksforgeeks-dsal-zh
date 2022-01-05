# a 中的第 K 位数字升至 b 的幂

> 原文:[https://www.geeksforgeeks.org/k-th-digit-raised-power-b/](https://www.geeksforgeeks.org/k-th-digit-raised-power-b/)

给定三个数字 a、b 和 k，从右侧找到 a <sup>b</sup> 中的第 k 个数字
示例:

```
Input : a = 3, b = 3, 
        k = 1
Output : 7
Explanation
3^3 = 27 for k = 1\. First digit is 7 in 27

Input : a = 5, b = 2, 
        k = 2
Output : 2
Explanation
5^2 = 25 for k = 2\. First digit is 2 in 25
```

**方法**
1)计算 a^b
2)迭代去除最后一个数字，直到第 k 个数字不满足

## C++

```
// CPP program for finding k-th digit in a^b
#include <bits/stdc++.h>
using namespace std;

// To compute k-th digit in a^b
int kthdigit(int a, int b, int k)
{
    // computing a^b
    int p = pow(a, b);

    int count = 0;
    while (p > 0 && count < k) {

        // getting last digit
        int rem = p % 10;

        // increasing count by 1
        count++;

        // if current number is required digit
        if (count == k)
            return rem;

        // remove last digit
        p = p / 10;
    }

    return 0;
}

// Driver code
int main()
{
    int a = 5, b = 2;
    int k = 1;
    cout << kthdigit(a, b, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for finding k-th digit in a^b
import java.util.*;
import java.lang.*;

public class GfG {
    // To compute k-th digit in a^b
    public static int kthdigit(int a, int b, int k)
    {
        // Computing a^b
        int p = (int)Math.pow(a, b);

        int count = 0;
        while (p > 0 && count < k) {

            // Getting last digit
            int rem = p % 10;

            // Increasing count by 1
            count++;

            // If current number is required digit
            if (count == k)
                return rem;

            // Remove last digit
            p = p / 10;
        }

        return 0;
    }

    // Driver Code
    public static void main(String argc[]) {
        int a = 5, b = 2;
        int k = 1;
        System.out.println(kthdigit(a, b, k));
    }

}

// This code is contributed by Sagar Shukla.
```

## 蟒蛇 3

```
# Python3 code to compute k-th
# digit in a^b
def kthdigit(a, b, k):

    # computing a^b in python
    p = a ** b
    count = 0

    while (p > 0 and count < k):

        # getting last digit
        rem = p % 10

        # increasing count by 1
        count = count + 1

        # if current number is
        # required digit
        if (count == k):
            return rem

        # remove last digit
        p = p / 10;

# driver code   
a = 5
b = 2
k = 1
ans = kthdigit(a, b, k)
print (ans)

# This code is contributed by Saloni Gupta
```

## C#

```
// C# program for finding k-th digit in a^b
using System;

public class GfG {

    // To compute k-th digit in a^b
    public static int kthdigit(int a, int b, int k)
    {
        // Computing a^b
        int p = (int)Math.Pow(a, b);

        int count = 0;
        while (p > 0 && count < k) {

            // Getting last digit
            int rem = p % 10;

            // Increasing count by 1
            count++;

            // If current number is required digit
            if (count == k)
                return rem;

            // Remove last digit
            p = p / 10;
        }

        return 0;
    }

    // Driver Code
    public static void Main() {
        int a = 5, b = 2;
        int k = 1;
        Console.WriteLine(kthdigit(a, b, k));
    }

}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for finding
// k-th digit in a^b

// To compute k-th
// digit in a^b
function kthdigit($a, $b, $k)
{

    // computing a^b
    $p = pow($a, $b);

    $count = 0;
    while ($p > 0 and $count < $k)
    {

        // getting last digit
        $rem = $p % 10;

        // increasing count by 1
        $count++;

        // if current number is
        // required digit
        if ($count == $k)
            return $rem;

        // remove last digit
        $p = $p / 10;
    }

    return 0;
}

    // Driver Code
    $a = 5;
    $b = 2;
    $k = 1;
    echo kthdigit($a, $b, $k);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program for finding k-th digit in a^b

// To compute k-th digit in a^b
    function kthdigit(a, b, k)
    {
        // Computing a^b
        let p = Math.pow(a, b);

        let count = 0;
        while (p > 0 && count < k) {

            // Getting last digit
            let rem = p % 10;

            // Increasing count by 1
            count++;

            // If current number is required digit
            if (count == k)
                return rem;

            // Remove last digit
            p = p / 10;
        }

        return 0;
    }

// Driver code

        let a = 5, b = 2;
        let k = 1;
        document.write(kthdigit(a, b, k));  

</script>
```

**输出:**

```
5
```

**如何避免溢出？**
我们可以在模下找到[的力量 10sup > k 避免溢出。求模下的幂之后，我们需要返回幂的第一个数字。](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)