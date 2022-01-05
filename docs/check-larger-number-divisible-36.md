# 检查是否有能被 36 整除的更大的数

> 原文:[https://www . geesforgeks . org/check-biger-number-除数-36/](https://www.geeksforgeeks.org/check-larger-number-divisible-36/)

给定一个数，检查给定的数是否能被 36 整除。该数字可能非常大，并且可能不适合任何数字(int、long int、float 等)。)数据类型。
示例:

```
Input : 72
Output : Yes

Input : 244
Output : No

Input : 11322134
Output : No

Input : 92567812197966231384
Output : Yes
```

如果一个数可以被 4 和 9 整除

1.  [如果一个数的最后 2 位数字组成的数可以被 4 整除](https://www.geeksforgeeks.org/check-large-number-divisible-4-not/)
2.  [如果一个数的位数之和可以被 9 整除](https://www.geeksforgeeks.org/check-large-number-divisible-9-not/)

以下是基于上述思想的实现。

## C++

```
// C++ implementation to check divisibility by 36
#include <bits/stdc++.h>
using namespace std;

// Function to check whether a number
// is divisible by 36 or not
string divisibleBy36(string num)
{
    int l = num.length();

    // null number cannot
    // be divisible by 36
    if (l == 0)
        return "No";

    // single digit number other than
    // 0 is not divisible by 36
    if (l == 1 && num[0] != '0')
        return "No";

    // number formed by the last 2 digits
    int two_digit_num = (num[l-2] - '0')*10 +
                        (num[l-1] - '0') ;

    // if number is not divisible by 4
    if (two_digit_num%4 != 0)
        return "No";

    // number is divisible by 4 calculate
    // sum of digits
    int sum = 0;
    for (int i=0; i<l; i++)
        sum += (num[i] - '0');

    // sum of digits is not divisible by 9
    if (sum%9 != 0)
        return "No";

    // number is divisible by 4 and 9
    // hence, number is divisible by 36
    return "Yes";
}

// Driver program
int main()
{
    string num = "92567812197966231384";
    cout << divisibleBy36(num);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if a number is
// divisible by 36 or not
class IsDivisible
{
    // Function to check whether a number
    // is divisible by 36 or not
    static boolean divisibleBy36(String num)
    {
        int l = num.length();

        // null number cannot
        // be divisible by 36
        if (l == 0)
            return false;

        // single digit number other than
        // 0 is not divisible by 36
        if (l == 1 && num.charAt(0) != '0')
            return false;

        // number formed by the last 2 digits
        int two_digit_num = (num.charAt(l-2) - '0')*10 +
                            (num.charAt(l-1) - '0') ;

        // if number is not divisible by 4
        if (two_digit_num%4 != 0)
            return false;

        // number is divisible by 4 calculate
        // sum of digits
        int sum = 0;
        for (int i=0; i<l; i++)
            sum += (num.charAt(i) - '0');

        // sum of digits is not divisible by 9
        if (sum%9 != 0)
            return false;

        // number is divisible by 4 and 9
        // hence, number is divisible by 36
        return true;
    }

    // main function
    public static void main (String[] args)
    {
        String num = "92567812197966231384";
        if(divisibleBy36(num))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation to
# check divisibility by 36

# Function to check whether a
# number is divisible by
# 36 or not
def divisibleBy36(num) :
    l = len(num)

    # null number cannot
    # be divisible by 36
    if (l == 0) :
        return ("No")

    # single digit number other
    # than 0 is not divisible
    # by 36
    if (l == 1 and num[0] != '0') :
        return ("No")

    # number formed by the
    # last 2 digits
    two_digit_num = (((int)(num[l - 2])) *
                    10 +(int)(num[l - 1]))

    # if number is not
    # divisible by 4
    if (two_digit_num%4 != 0) :
        return "No"

    # number is divisible
    # by 4 calculate sum
    # of digits
    sm = 0
    for i in range(0,l) :
        sm = sm + (int)(num[i])

    # sum of digits is not
    # divisible by 9
    if (sm%9 != 0) :
        return ("No")

    # Number is divisible
    # by 4 and 9 hence,
    # number is divisible
    # by 36
    return ("Yes")

# Driver program
num = "92567812197966231384"
print(divisibleBy36(num))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find if a number is
// divisible by 36 or not
using System;

class GFG {

    // Function to check whether
    // a number is divisible by
    // 36 or not
    static bool divisibleBy36(String num)
    {
        int l = num.Length;

        // null number cannot
        // be divisible by 36
        if (l == 0)
            return false;

        // single digit number other than
        // 0 is not divisible by 36
        if (l == 1 && num[0] != '0')
            return false;

        // number formed by the last
        // 2 digits
        int two_digit_num = (num[l-2] - '0') * 10
                             + (num[l-1] - '0') ;

        // if number is not divisible by 4
        if (two_digit_num % 4 != 0)
            return false;

        // number is divisible by 4 calculate
        // sum of digits
        int sum = 0;
        for (int i = 0; i < l; i++)
            sum += (num[i] - '0');

        // sum of digits is not divisible by 9
        if (sum % 9 != 0)
            return false;

        // number is divisible by 4 and 9
        // hence, number is divisible by 36
        return true;
    }

    // main function
    public static void Main ()
    {
        String num = "92567812197966231384";

        if(divisibleBy36(num))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by parashar.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to
// check divisibility by 36

// Function to check whether a number
// is divisible by 36 or not
function divisibleBy36($num)
{
    $l = strlen($num);

    // null number cannot
    // be divisible by 36
    if ($l == 0)
        return "No";

    // single digit number other than
    // 0 is not divisible by 36
    if ($l == 1 && $num[0] != '0')
        return "No";

    // number formed by the
    // last 2 digits
    $two_digit_num = ($num[$l - 2] - '0') * 10 +
                            ($num[$l - 1] - '0') ;

    // if number is not
    // divisible by 4
    if ($two_digit_num%4 != 0)
        return "No";

    // number is divisible by 4
    // calculate sum of digits
    $sum = 0;
    for ($i = 0; $i < $l; $i++)
        $sum += ($num[$i] - '0');

    // sum of digits is not
    // divisible by 9
    if ($sum % 9 != 0)
        return "No";

    // number is divisible by 4 and 9
    // hence, number is divisible by 36
    return "Yes";
}

// Driver Code
$num = "92567812197966231384";
echo(divisibleBy36($num));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// Javascript implementation to
// check divisibility by 36

// Function to check whether a number
// is divisible by 36 or not
function divisibleBy36(num)
{
    let l = num.length;

    // null number cannot
    // be divisible by 36
    if (l == 0)
        return "No";

    // single digit number other than
    // 0 is not divisible by 36
    if (l == 1 && num[0] != '0')
        return "No";

    // number formed by the
    // last 2 digits
    let two_digit_num = (num[l - 2] - '0') * 10 +
                            (num[l - 1] - '0') ;

    // if number is not
    // divisible by 4
    if (two_digit_num%4 != 0)
        return "No";

    // number is divisible by 4
    // calculate sum of digits
    let sum = 0;
    for (let i = 0; i < l; i++)
        sum += (num[i] - '0');

    // sum of digits is not
    // divisible by 9
    if (sum % 9 != 0)
        return "No";

    // number is divisible by 4 and 9
    // hence, number is divisible by 36
    return "Yes";
}

// Driver Code
let num = "92567812197966231384";
document.write(divisibleBy36(num));

// This code is contributed by _saurabh_jaiswal.
</script>
```

输出:

```
Yes
```

时间复杂度:O(n)
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。