# 检查给定的数字是否可以用任意基数的给定位数来表示

> 原文:[https://www . geesforgeks . org/check-if-给定数字-给定数字-任意基数无位数/](https://www.geeksforgeeks.org/check-if-a-given-number-can-be-represented-in-given-a-no-of-digits-in-any-base/)

给定一个数字和表示该数字的位数，找出给定的数字是否可以用从 2 到 32 的任意基数的给定位数来表示。
**例:**

```
Input: 8 4  
Output: Yes
Possible in base 2 as 8 in base 2 is 1000

Input: 8 2 
Output: Yes 
Possible in base 3 as 8 in base 3 is 22

Input: 8 3  
Output: No
Not possible in any base
```

**我们强烈建议您最小化浏览器，先自己尝试一下。**
思路是从 2 号基地开始到 32 号基地，逐个检查所有基地。我们如何检查给定的基数？以下是一些简单的步骤。
1)如果数字小于基数，数字为 1，则返回真。
2)否则如果数字大于 1 且数字大于基数，则通过做 num/base 从 num 中移除最后一个数字，减少数字的数量并重复出现。
3) Else 返回 false
下面是上述思路的实现。

## C++

```
// C++ program to check if a given number can be
// represented in given number of digits in any base
#include <iostream>
using namespace std;

// Returns true if 'num' can be represented using 'dig'
// digits in 'base'
bool checkUtil(int num, int dig, int base)
{
    // Base case
    if (dig==1 && num < base)
       return true;

    // If there are more than 1 digits left and number
    // is more than base, then remove last digit by doing
    // num/base, reduce the number of digits and recur
    if (dig > 1 && num >= base)
       return checkUtil(num/base, --dig, base);

    return false;
}

// return true of num can be represented in 'dig'
// digits in any base from 2 to 32
bool check(int num, int dig)
{
    // Check for all bases one by one
    for (int base=2; base<=32; base++)
       if (checkUtil(num, dig, base))
            return true;
    return false;
}

// Driver program
int main()
{
    int num = 8;
    int dig = 3;
    (check(num, dig))? cout << "Yes" : cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a
// given number can be represented
// in given number of digits in any base
class GFG
{
    // Returns true if 'num' can be
    // represented using 'dig' digits in 'base'
    static boolean checkUtil(int num, int dig, int base)
    {
        // Base case
        if (dig==1 && num < base)
        return true;

        // If there are more than 1 digits
        // left and number is more than base,
        // then remove last digit by doing num/base,
        //  reduce the number of digits and recur
        if (dig > 1 && num >= base)
        return checkUtil(num / base, --dig, base);

        return false;
    }

    // return true of num can be
    // represented in 'dig' digits
    // in any base from 2 to 32
    static boolean check(int num, int dig)
    {
        // Check for all bases one by one
        for (int base = 2; base <= 32; base++)
        if (checkUtil(num, dig, base))
                return true;
        return false;
    }

    // Driver code
    public static void main (String[] args)
    {
        int num = 8;
        int dig = 3;
        if(check(num, dig))
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to check
# if a given number can be
# represented in given number
# of digits in any base

# Returns true if 'num' can
# be represented using 'dig'
# digits in 'base'
def checkUtil(num,dig,base):

    # Base case
    if (dig==1 and num < base):
        return True

    # If there are more than 1
    # digits left and number
    # is more than base, then
    # remove last digit by doing
    # num/base, reduce the number
    # of digits and recur
    if (dig > 1 and num >= base):
        return checkUtil(num/base, --dig, base)

    return False

# return true of num can
# be represented in 'dig'
# digits in any base from 2 to 32
def check(num,dig):

    # Check for all bases one by one
    for base in range(2,33):

        if (checkUtil(num, dig, base)):
            return True
    return False

# driver code
num = 8
dig = 3
if(check(num, dig)==True):
    print("Yes")
else:
    print("No")

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to check if a given
// number can be represented in
// given number of digits in any base
using System;

class GFG {

    // Returns true if 'num' can be
    // represented using 'dig' digits
    // in 'base'
    static bool checkUtil(int num, int dig,
                          int i)
    {

        // Base case
        if (dig == 1 && num < i)
        return true;

        // If there are more than 1 digits
        // left and number is more than base,
        // then remove last digit by doing
        // num/base, reduce the number of
        // digits and recur
        if (dig > 1 && num >= i)
        return checkUtil((num / i), --dig, i);

        return false;
    }

    // return true of num can be
    // represented in 'dig' digits
    // in any base from 2 to 32
    static bool check(int num, int dig)
    {

        // Check for all bases one by one
        for (int i = 2; i <= 32; i++)
        if (checkUtil(num, dig, i))
                return true;
        return false;
    }

    // Driver code
    public static void Main()
    {
        int num = 8;
        int dig = 3;
        if(check(num, dig))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a given
// number can be represented in given
// number of digits in any base

// Returns true if 'num' can be
// represented using 'dig'
// digits in 'base'

function checkUtil($num, $dig, $base)
{
    // Base case
    if ($dig == 1 && $num < $base)
    return true;

    // If there are more than 1
    // digits left and number is
    // more than base, then remove
    // last digit by doing num/base,
    // reduce the number of digits and recur
    if ($dig > 1 && $num >= $base)
    return checkUtil($num / $base,
                   --$dig, $base);

    return false;
}

// return true of num can be
// represented in 'dig' digits
// in any base from 2 to 32
function check($num, $dig)
{
    // Check for all bases one by one
    for ($base = 2; $base <= 32; $base++)
    if (checkUtil($num, $dig, $base))
            return true;
    return false;
}

// Driver Code
$num = 8;
$dig = 3;
if (check($num, $dig) == true)
echo "Yes" ;
else
echo "No";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// javascript program to check if a
// given number can be represented
// in given number of digits in any base

    // Returns true if 'num' can be
    // represented using 'dig' digits in 'base'
    function checkUtil(num , dig , base)
    {
        // Base case
        if (dig == 1 && num < base)
            return true;

        // If there are more than 1 digits
        // left and number is more than base,
        // then remove last digit by doing num/base,
        // reduce the number of digits and recur
        if (dig > 1 && num >= base)
            return checkUtil(parseInt(num / base), --dig, base);

        return false;
    }

    // return true of num can be
    // represented in 'dig' digits
    // in any base from 2 to 32
    function check(num , dig) {
        // Check for all bases one by one
        for (base = 2; base <= 32; base++)
            if (checkUtil(num, dig, base))
                return true;
        return false;
    }

    // Driver code

        var num = 8;
        var dig = 3;
        if (check(num, dig))
            document.write("Yes");
        else
            document.write("No");

// This code contributed by Rajput-Ji

</script>
```

**输出:**

```
No
```

**时间复杂度:** O(32*32)

**辅助空间:** O(1)
本文由**mehbob Elahi**供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息