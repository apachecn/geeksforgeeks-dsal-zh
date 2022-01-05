# 检查一个大数是否能被 13 整除

> 原文:[https://www . geesforgeks . org/check-大数-整除-13-not/](https://www.geeksforgeeks.org/check-large-number-divisible-13-not/)

给定一个大数，任务是检查数是否能被 13 整除。

**示例:**

```
Input :  637
Output : 637 is divisible by 13.

Input :  920
Output : 920 is not divisible by 13.

Input  : 83959092724
Output : 83959092724 is divisible by 13.
```

如果给定的数 **num** 很小，我们通过做 num % 13，检查结果是否为 0，就可以很容易地发现它是否能被 13 整除。但是非常大的数字呢？让我们讨论一下大数。

下面是一些关于 13 整除性的有趣事实。

*   一个数可以被 13 整除，如果从右到左三个块的交替和(交替加减)可以被 13 整除。例如，2911285 可以被 13 整除，因为大小为 3 的块的交替和是 2–911+285 =-650，它可以被 13 整除。
*   一个数可以被 13 整除当且仅当最后一位数字乘以 4 得到的数也可以被 13 整除。
    例如，考虑 2353。应用上述规则，我们得到 235 + 3*4 = 247。我们再次应用规则，得到，24 + 7*4 = 52。因为 52 可以被 13 整除，所以给定的数可以被 13 整除。

下面是基于上述第一个事实的实现(寻找大小为 3 的块的交替和)

## C++

```
// CPP program to check
// whether a number is
// divisible by 13 or not.
#include <iostream>
using namespace std;

// Returns true if number
// is divisible by 13 else
// returns false
bool checkDivisibility(string num)
{
    int length = num.size();
    if (length == 1 && num[0] == '0')
        return true;

    // Append required 0s .
    // at the beginning.
    if (length % 3 == 1)
    {
        // Same as strcat(num, "00");
        // in c.
        num +="00";
        length += 2;
    }
    else if (length % 3 == 2)
    {
        // Same as strcat(num, "0");
        // in c.
        num += "0";
        length += 1;
    }

    // Alternatively add/subtract
    // digits in group of three
    // to result.
    int sum = 0, p = 1;
    for (int i = length - 1; i >= 0; i--)
    {
        // Store group of three
        // numbers in group variable.
        int group = 0;
        group += num[i--] - '0';
        group += (num[i--] - '0') * 10;
        group += (num[i] - '0') * 100;

        sum = sum + group * p;

        // Generate alternate series
        // of plus and minus
        p *= (-1);
    }
    sum = abs(sum);
    return (sum % 13 == 0);
}

// Driver code
int main()
{
    string number = "83959092724";
    if (checkDivisibility(number))
        cout << number << " is divisible by 13.";
    else
        cout << number << " is not divisible by 13.";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check
// whether a number is
// divisible by 13 or not.

class GFG
{

// Returns true if number
// is divisible by 13 else
// returns false
static boolean checkDivisibility(String num)
{
    int length = num.length();
    if (length == 1 &&
        num.charAt(0) == '0')
        return true;

    // Append required 0s .
    // at the beginning.
    if (length % 3 == 1)
    {
        // Same as strcat(num, "00");
        // in c.
        num +="00";
        length += 2;
    }
    else if (length % 3 == 2)
    {
        // Same as strcat(num, "0");
        // in c.
        num += "0";
        length += 1;
    }

    // Alternatively add/subtract
    // digits in group of three
    // to result.
    int sum = 0, p = 1;
    for (int i = length - 1; i >= 0; i--)
    {
        // Store group of three
        // numbers in group variable.
        int group = 0;
        group += num.charAt(i--) - '0';
        group += (num.charAt(i--) - '0') * 10;
        group += (num.charAt(i) - '0') * 100;

        sum = sum + group * p;

        // Generate alternate series
        // of plus and minus
        p *= (-1);
    }
    sum = Math.abs(sum);
    return (sum % 13 == 0);
}

// Driver code
public static void main(String[] args)
{
    String number = "83959092724";

    if (checkDivisibility(number))
            System.out.println(number +
                       " is divisible by 13.");
        else
            System.out.println(number +
                       " is not divisible by 13.");
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python 3 program to check whether a
# number is divisible by 13 or not

# Returns true if number is divisible
# by 13 else returns false
def checkDivisibility( num):
    length = len(num)
    if (length == 1 and num[0] == '0'):
        return True

    # Append required 0s at the beginning.
    if (length % 3 == 1):

        # Same as strcat(num, "00");
        # in c.
        num = str(num) + "00"
        length += 2

    elif (length % 3 == 2):

        # Same as strcat(num, "0");
        # in c.
        num = str(num) + "0"
        length += 1

    # Alternatively add/subtract digits 
    # in group of three to result.
    sum = 0
    p = 1
    for i in range(length - 1, -1 , -1) :

        # Store group of three
        # numbers in group variable.
        group = 0
        group += ord(num[i]) - ord('0')
        i -= 1
        group += (ord(num[i]) - ord('0')) * 10
        i -= 1
        group += (ord(num[i]) - ord('0')) * 100

        sum = sum + group * p

        # Generate alternate series
        # of plus and minus
        p *= (-1)
    sum = abs(sum)
    return (sum % 13 == 0)

# Driver code
if __name__ == "__main__":
    number = "83959092724"
    if (checkDivisibility(number)):
        print( number , "is divisible by 13.")
    else:
        print( number ,"is not divisible by 13.")

# This code is contributed by ChitraNayal
```

## C#

```
// C# program to check
// whether a number is
// divisible by 13 or not.
using System;

class GFG {

    // Returns true if number
    // is divisible by 13 else
    // returns false
    static bool checkDivisibility(string num)
    {
        int length = num.Length;
        if (length == 1 && num[0] == '0')
            return true;

        // Append required 0s .
        // at the beginning.
        if (length % 3 == 1)
        {
            // Same as strcat(num, "00");
            // in c.
            num +="00";
            length += 2;
        }
        else if (length % 3 == 2)
        {
            // Same as strcat(num, "0");
            // in c.
            num += "0";
            length += 1;
        }

        // Alternatively add/subtract
        // digits in group of three
        // to result.
        int sum = 0, p = 1;
        for (int i = length - 1; i >= 0; i--)
        {
            // Store group of three
            // numbers in group variable.
            int group = 0;
            group += num[i--] - '0';
            group += (num[i--] - '0') * 10;
            group += (num[i] - '0') * 100;

            sum = sum + group * p;

            // Generate alternate series
            // of plus and minus
            p *= (-1);
        }
        sum = Math.Abs(sum);
        return (sum % 13 == 0);
    }

    // Driver code
    static void Main()
    {
        string number = "83959092724";

        if (checkDivisibility(number))
                Console.Write( number +
                    " is divisible by 13.");
            else
                Console.Write( number +
                  " is not divisible by 13.");
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check
// whether a number is
// divisible by 13 or not.

// Returns true if number
// is divisible by 13 else
// returns false
function checkDivisibility($num)
{
    $length = strlen($num);
    if ($length == 1 &&
        $num[0] == '0')
        return true;

    // Append required 0s
    // at the beginning.
    if ($length % 3 == 1)
    {
        // Same as strcat(num, "00");
        // in c.
        $num += "00";
        $length += 2;
    }
    else if ($length % 3 == 2)
    {
        // Same as strcat(num, "0");
        // in c.
        $num += "0";
        $length += 1;
    }

    // Alternatively add/subtract
    // digits in group of three
    // to result.
    $sum = 0; $p = 1;
    for ($i = $length - 1; $i >= 0; $i--)
    {
        // Store group of three
        // numbers in group variable.
        $group = 0;
        $group += $num[$i--] - '0';
        $group += ($num[$i--] - '0') * 10;
        $group += ($num[$i] - '0') * 100;

        $sum = $sum + $group * $p;

        // Generate alternate series 
        // of plus and minus
        $p *= (-1);
    }

    $sum = abs($sum);
    return ($sum % 13 == 0);
}

// Driver code
$number = "83959092724";
if (checkDivisibility($number))
    echo($number . " is divisible by 13.");
else
    echo($number . " is not divisible by 13.");

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// Javascript program to check
// whether a number is
// divisible by 13 or not.

// Returns true if number
// is divisible by 13 else
// returns false
function checkDivisibility(num)
{
    let length = num.length;
    if (length == 1 &&
        num[0] == '0')
        return true;

    // Append required 0s
    // at the beginning.
    if (length % 3 == 1)
    {
        // Same as strcat(num, "00");
        // in c.
        num += "00";
        length += 2;
    }
    else if (length % 3 == 2)
    {
        // Same as strcat(num, "0");
        // in c.
        num += "0";
        length += 1;
    }

    // Alternatively add/subtract
    // digits in group of three
    // to result.
    let sum = 0; p = 1;
    for (let i = length - 1; i >= 0; i--)
    {
        // Store group of three
        // numbers in group variable.
        group = 0;
        group += num[i--] - '0';
        group += (num[i--] - '0') * 10;
        group += (num[i] - '0') * 100;

        sum = sum + group * p;

        // Generate alternate series
        // of plus and minus
        p *= (-1);
    }

    sum = Math.abs(sum);
    return (sum % 13 == 0);
}

// Driver code
let number = "83959092724";
if (checkDivisibility(number))
    document.write(number + " is divisible by 13.");
else
    document.write(number + " is not divisible by 13.");

// This code is contributed by _saurabh_jaiswal.
</script>
```

**输出:**

```
83959092724 is divisible by 13.
```