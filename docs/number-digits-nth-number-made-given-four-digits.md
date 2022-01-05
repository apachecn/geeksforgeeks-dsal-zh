# 由给定的四位数字组成的第 n 个数字中的位数

> 原文:[https://www . geesforgeks . org/number-digits-n-number-make-given-四位数/](https://www.geeksforgeeks.org/number-digits-nth-number-made-given-four-digits/)

找出第 n 个数字中的位数，该数字是用 6、1、4 和 9 作为升序中的唯一数字构造的。
通过仅使用 6、1、4 和 9 作为升序数字构建的前几个数字将是:1、6、4、
9、11、14、16、19、41、44、46、49、61、64、66、69、91、94、96、99、111、114、116、119 等等。

**示例:**

```
Input : 6
Output : 2
6th digit of the series is 14 which has 2 digits.

Input : 21
Output : 3
21st digit of the series is 111 which has 3 digits.
```

**简单法:**这是蛮力法。
1。将一个数字初始化为 1，将一个计数器初始化为 0。
2。检查初始化的数字是否只有 6、1、4 或 9 个数字。
3。如果它只有提到的数字，那么增加计数器 1。
4。增加数字并重复以上步骤，直到计数器小于 n。
**注意:**n 的值可能很大，因此这种方法不能工作，因为它没有时间效率。

**有效方法:**你可以计算出在 O (1)时间内 k 个数字的个数，它们总是 4 的幂，例如数列中 1 个数字的个数是 4，数列中 2 个数字的个数是 16，等等。

1.  计算所有随后的 k 位数，并不断将它们相加。
2.  当总和大于或等于 n 时中断循环。
3.  保留一个计数器来记录位数。
4.  循环中断时计数器的值将指示答案。

下面是上述方法的实现:

## C++

```
// C++ program to count number of digits
// in n-th number made of given four digits.
#include <bits/stdc++.h>
using namespace std;

// Efficient function to calculate number
// of digits in the nth number constructed
// by using 6, 1, 4 and 9 as digits in the
// ascending order.
int number_of_digits(int n)
{
    int i, res, sum = 0;

    // Number of digits increase after
    // every i-th number where i increases in
    // powers of 4.
    for (i = 4, res = 1;; i *= 4, res++) {
        sum += i;
        if (sum >= n)
            break;       
    }
    return res;
}

// Driver code
int main()
{
    int n = 21;
    cout << number_of_digits(n) << endl;
    return 0;
}
//Thic code is contributed by Mayank Tyagi
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count
// number of digits in
// n-th number made of
// given four digits.
import java.io.*;

class GFG {

    // Efficient function to
    // calculate number of digits
    // in the nth number constructed
    // by using 6, 1, 4 and 9 as
    // digits in the ascending order.
    static int number_of_digits(int n)
    {
        int i;
        int res;
        int sum = 0;

        // Number of digits increase
        // after every i-th number
        // where i increases in powers of 4.
        for (i = 4, res = 1;; i *= 4, res++) {
            sum += i;
            if (sum >= n)
                break;
        }
        return res;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 21;
        System.out.println(number_of_digits(n));
    }
}

// This code is contributed
// by akt_mit
```

## 蟒蛇 3

```
# Python3 program to count number of
# digits in n-th number made of given
# four digits.

# Efficient function to calculate number
# of digits in the nth number constructed
# by using 6, 1, 4 and 9 as digits in the
# ascending order.

def number_of_digits(n):

    i = 4
    res = 1
    sum = 0

    # Number of digits increase after
    # every i-th number where i increases
    # in powers of 4.
    while(True):
        i *= 4
        res += 1
        sum += i
        if(sum >= n):
            break
    return res

# Driver Code
n = 21
print(number_of_digits(n))

# This code is contributed by mits
```

## C#

```
// C#  program to count
// number of digits in
// n-th number made of
// given four digits.

using System;

public class GFG {

    // Efficient function to
    // calculate number of digits
    // in the nth number constructed
    // by using 6, 1, 4 and 9 as
    // digits in the ascending order.
    static int number_of_digits(int n)
    {
        int i;
        int res;
        int sum = 0;

        // Number of digits increase
        // after every i-th number
        // where i increases in powers of 4.
        for (i = 4, res = 1;; i *= 4, res++) {
            sum += i;
            if (sum >= n)
                break;
        }
        return res;
    }

    // Driver Code

    static public void Main()
    {

        int n = 21;
        Console.WriteLine(number_of_digits(n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number
// of digits in n-th number
// made of given four digits.

// Efficient function to
// calculate number of digits
// in the nth number constructed
// by using 6, 1, 4 and 9 as
// digits in the ascending order.
function number_of_digits($n)
{
    $i; $res; $sum = 0;

    // Number of digits increase
    // after every i-th number
    // where i increases in
    // powers of 4.
    for ($i = 4, $res = 1;;
         $i *= 4, $res++)
    {
        $sum += $i;
        if ($sum >= $n)
            break;
    }
    return $res;
}

// Driver Code
$n = 21;
echo number_of_digits($n),"\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to count number of digits
// in n-th number made of given four digits.

// Efficient function to calculate number
// of digits in the nth number constructed
// by using 6, 1, 4 and 9 as digits in the
// ascending order.
function number_of_digits(n)
{
    let i, res, sum = 0;

    // Number of digits increase after
    // every i-th number where i increases in
    // powers of 4.
    for(i = 4, res = 1;; i *= 4, res++)
    {
        sum += i;

        if (sum >= n)
            break;   
    }
    return res;
}

// Driver code
let n = 21;

document.write(number_of_digits(n) + "<br>");

// This code is contributed by Manoj.

</script>
```

**Output**

```
3
```

**注意:**由于 n 可能真的很大，我们使用了 boost 库，要了解更多关于 boost 库的信息，请阅读本文:[高级 C++与 boost 库](https://www.geeksforgeeks.org/advanced-c-boost-library/)