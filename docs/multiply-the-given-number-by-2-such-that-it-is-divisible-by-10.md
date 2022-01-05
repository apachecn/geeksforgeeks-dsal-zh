# 将给定的数乘以 2，使其可被 10 整除

> 原文:[https://www . geesforgeks . org/给定数字乘以 2，这样它就可以被 10 整除/](https://www.geeksforgeeks.org/multiply-the-given-number-by-2-such-that-it-is-divisible-by-10/)

给定一个数字，唯一允许的操作是将该数字乘以 2。计算最小运算数，使该数可被 10 整除。
**注:**如果无法转换，则打印-1。
**示例:**

> **输入:** 10
> **输出:** 0
> 由于给定的数本身可以被 10 整除，
> 的答案是 0。
> **输入:** 1
> **输出:** -1
> 由于通过乘以 2，给定的编号不能被
> 转换成可被 10 整除的数字，
> 因此答案是-1。

**方法:**任何给定的数只有在最后一位数字为 0 时才能被 10 整除。对于这个问题，提取输入数字的最后一位数字，并通过以下方式进行检查:
1)如果最后一位数字是 0，那么它已经可以被 10 整除，因此最小步数是 0。
2)如果最后一位数字是 5，那么将其乘以 2 一次将使其可被 10 整除，因此最小步数是 1。
3)如果最后一个数字是偶数或奇数(除了 0 和 5)，那么将其乘以 2 的任何次数都只会产生偶数，因此我们永远无法使其被 10 整除。因此步数为-1。

## C++

```
// C++ code for finding
// number of operations
#include <bits/stdc++.h>
using namespace std;

int multiplyBy2(int n)
{
    int rem, value;

    // Find the last digit or remainder
    rem = n % 10;
    switch (rem) {

    // If the last digit is 0
    case 0:
        value = 0;
        break;

    // If the last digit is 5
    case 5:
        value = 1;
        break;

    // If last digit is other
    // than 0 and 5.
    default:
        value = -1;
    }

    return value;
}

// Driver code
int main()
{

    int n = 28;
    cout << multiplyBy2(n) << endl;

    n = 255;
    cout << multiplyBy2(n) << endl;

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA code for finding
// number of operations
import java.io.*;

class GFG
{
    static int multiplyBy2(int n)
{
    int rem, value;

    // Find the last digit
    // or remainder
    rem = n % 10;
    switch (rem)
    {

    // If the last digit is 0
    case 0:
        value = 0;
        break;

    // If the last digit is 5
    case 5:
        value = 1;
        break;

    // If last digit is other
    // than 0 and 5.
    default:
        value = -1;
    }

    return value;
}

// Driver code
public static void main (String[] args)
{
    int n = 28;
    System.out.println(multiplyBy2(n));

    n = 255;
    System.out.println(multiplyBy2(n));
}
}

// This code is contributed
// by shiv_bhakt.
```

## 蟒蛇 3

```
# Python3 code for finding number
# of operations
def dig(argu):
    switcher = {
        0: 0,
        5: 1,
    }
    return switcher.get(argu, -1)

def multiplyBy2(n):

    # Find the last digit or remainder
    rem = n % 10;
    return dig(rem);

# Driver code
n = 28;
print(multiplyBy2(n));

n = 255;
print(multiplyBy2(n));

# This code is contributed by mits
```

## C#

```
// C# code for finding
// number of operations
using System;

class GFG
{
    static int multiplyBy2(int n)
    {
    int rem, value;

    // Find the last digit
    // or remainder
    rem = n % 10;
    switch (rem)
    {

    // If the last
    // digit is 0
    case 0:
        value = 0;
        break;

    // If the last
    // digit is 5
    case 5:
        value = 1;
        break;

    // If last digit is
    // other than 0 and 5.
    default:
        value = -1;
        break;
    }

    return value;
}

// Driver code
public static void Main ()
{
    int n = 28;
    Console.WriteLine(multiplyBy2(n));

    n = 255;
    Console.WriteLine(multiplyBy2(n));
}
}

// This code is contributed
// by shiv_bhakt.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP  code for finding
// number of operations

function  multiplyBy2($n)
{
     $rem;
     $value;

    // Find the last digit or remainder
    $rem = $n % 10;
    switch ($rem) {

    // If the last digit is 0
    case 0:
        $value = 0;
        break;

    // If the last digit is 5
    case 5:
        $value = 1;
        break;

    // If last digit is other
    // than 0 and 5.
    default:
        $value = -1;
    }

    return $value;
}

// Driver code
    $n = 28;
    echo  multiplyBy2($n),"\n";

    $n = 255;
        echo  multiplyBy2($n),"\n";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// Javascript code for finding
// number of operations

    function multiplyBy2(n)
    {
        var rem, value;

        // Find the last digit
        // or remainder
        rem = n % 10;
        switch (rem) {

        // If the last digit is 0
        case 0:
            value = 0;
            break;

        // If the last digit is 5
        case 5:
            value = 1;
            break;

        // If last digit is other
        // than 0 and 5.
        default:
            value = -1;
        }

        return value;
    }

    // Driver code

        var n = 28;
        document.write(multiplyBy2(n)+"<br/>");

        n = 255;
        document.write(multiplyBy2(n));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
-1
1
```