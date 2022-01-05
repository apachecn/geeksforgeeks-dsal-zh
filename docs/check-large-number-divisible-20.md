# 检查一个大数是否能被 20 整除

> 原文:[https://www . geesforgeks . org/check-大数-整除-20/](https://www.geeksforgeeks.org/check-large-number-divisible-20/)

给定一个数字，任务是检查这个数字是否能被 20 整除。输入的数字可能很大，可能无法存储 long long int，而且可能非常大，所以我们使用字符串。
**例:**

```
Input : 7575680
Output : Yes

Input : 987985865687690
Output : No
```

如果一个数能被 5 和 4 整除，它就能被 20 整除。我们可以通过检查最后两位数是否能被 4 整除来检查一个数是否能被 4 整除。我们可以通过检查最后一个数字来[检查除以 5 的可分性。另外，如果一个数的最后一位是零，第二个最后一位是 2 的倍数，那么这个数可以被 20 整除。](https://www.geeksforgeeks.org/check-large-number-divisible-5-not/) 

## C++

```
// CPP program to check if a large number
// is divisible by 20.
#include <iostream>
using namespace std;

bool divisibleBy20(string num)
{
    // Get number with last two digits
    int lastTwoDigits = stoi(num.substr(num.length() - 2,
                            num.length() - 1));

    // Check if the number formed by last two
    // digits is divisible by 5 and 4.
    return ((lastTwoDigits % 5 == 0) &&
            (lastTwoDigits % 4 == 0));
}

int main()
{
    string num = "63284689320";
    if (divisibleBy20(num))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a large n
// number is divisible by 20.
import java.io.*;

class GFG {

    static Boolean divisibleBy20(String num)
    {
        // Get number with last two digits
        int lastTwoDigits = Integer.parseInt(num.substring(num.length() - 2,
                                                           num.length() ));

        // Check if the number formed by last two
        // digits is divisible by 5 and 4.
        return ((lastTwoDigits % 5 == 0) &&
                (lastTwoDigits % 4 == 0));
    }

    // Driver Program
    public static void main (String[] args)
    {
        String num = "63284689320";
        if (divisibleBy20(num) == true)
            System.out.println("Yes");
        else
            System.out.println("No");

    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python3 program to check if a large
# number is divisible by 20.
import math

def divisibleBy20(num):

    # Get number with last two digits
    lastTwoDigits = int(num[-2:])

    # Check if the number formed by last two
    # digits is divisible by 5 and 4.
    return ((lastTwoDigits % 5 == 0 and
             lastTwoDigits % 4 == 0))

# driver code
num = "63284689320"
if (divisibleBy20(num) == True):
    print("Yes")
else:
    print("No")

# This code is contributed by Gitanjali.
```

## C#

```
// C# program to check if a large
// 'n' number is divisible by 20.
using System;
using System.Text;

class GFG
{

static bool divisibleBy20(String num)
{
    // Get number with last two digits
    int lastTwoDigits = Int32.Parse(num.Substring(2));

    // Check if the number formed
    // by last two digits is
    // divisible by 5 and 4.
    return ((lastTwoDigits % 5 == 0) &&
            (lastTwoDigits % 4 == 0));
}

// Driver Code
static public void Main ()
{
    String num = "63284689320";
    if (divisibleBy20(num) == true)
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Raj
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check
// if a large number is
// divisible by 20.

function divisibleBy20($num)
{
    // Get number with
    // last two digits
    $lastTwoDigits = intval(substr($num,
                           (strlen($num) - 2), 2));

    // Check if the number
    // formed by last two
    // digits is divisible
    // by 5 and 4.
    return (($lastTwoDigits % 5 == 0) &&
            ($lastTwoDigits % 4 == 0));
}

// Driver Code
$num = "63284689320";
if (divisibleBy20($num))
    echo "Yes";
else
    echo "No";

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>
// Javascript program to check
// if a large number is
// divisible by 20.
function divisibleBy20(num)
{

    // Get number with
    // last two digits
    let lastTwoDigits = parseInt(num.slice(-2, num.length))
    console.log(num.slice(-2, 1))

    // Check if the number
    // formed by last two
    // digits is divisible
    // by 5 and 4.
    return ((lastTwoDigits % 5 == 0) &&
            (lastTwoDigits % 4 == 0))
}

// Driver Code
let num = "63284689320";
if (divisibleBy20(num))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
Yes
```