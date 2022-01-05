# 检查一个号码是否乱码

> 原文:[https://www . geesforgeks . org/check-a-number-jumbed-or-not/](https://www.geeksforgeeks.org/check-if-a-number-is-jumbled-or-not/)

写一个程序来检查给定的整数是否混乱。如果一个数字的每一个数字与其相邻的数字相差最大值 1，则称这个数字是混杂的。
**例:**

```
Input : 6765
Output : True
All neighbour digits differ by atmost 1.

Input : 1223
Output : True

Input : 1235
Output : False
```

要发现一个数字是否乱码，我们只需要检查一个数字是否有差大于 1 的邻居
。如果找到了这样的数字，这个数字就不乱了。
以下是上述思路的实现:

## C++

```
// CPP code to check if a
// number is jumbled or not
#include <bits/stdc++.h>
using namespace std;

// Function to check if a
// number is jumbled or not
bool checkJumbled(int num)
{
    // Single digit number
    if (num / 10 == 0)
        return true;

    // Checking every digit
    // through a loop
    while (num != 0)
    {

        // All digits were checked
        if (num / 10 == 0)
            return true;

        // Digit at index i
        int digit1 = num % 10;

        // Digit at index i-1
        int digit2 = (num / 10) % 10;

        // If difference is
        // greater than 1
        if (abs(digit2 - digit1) > 1)
            return false;

        num = num / 10;
    }

    // Number checked
    return true;
}

// Driver code
int main()
{

    //-1234 to be checked
    int num = -1234;

    if (checkJumbled(num))
        cout << "True \n";
    else
        cout << "False \n";

    // 287 to be checked
    num = -1247;

    if (checkJumbled(num))
        cout << "True \n";
    else
        cout << "False \n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check if a
// number is jumbled or not
import java.io.*;

class GFG
{

    // Function to check if a
    // number is jumbled or not
    static boolean checkJumbled(int num)
    {
        // Single digit number
        if (num / 10 == 0)
            return true;

        // Checking every digit
        // through a loop
        while (num != 0)
        {

            // All digits were checked
            if (num / 10 == 0)
                return true;

            // Digit at index i
            int digit1 = num % 10;

            // Digit at index i-1
            int digit2 = (num / 10) % 10;

            // If difference is
            // greater than 1
            if (Math.abs(digit2 - digit1) > 1)
                return false;

            num = num / 10;
        }

        // Number checked
        return true;
    }

    // Driver code
    public static void main (String[]args)
    {
        //-1234 to be checked
        int num = -1234;

        if (checkJumbled(num))
            System.out.println("True ");
        else
            System.out.println("False ");

        // 287 to be checked
        num = -1247;

        if (checkJumbled(num))
            System.out.println("True ");

        else
            System.out.println("False ");

    }
}

// This code is contributed by vt_m.
```

## 计算机编程语言

```
# Python code to check if
# a number is jumbled or not

# Function to check if a
# number is jumbled or not
def checkJumbled(num):

    # Single digit number
    if (num / 10 == 0):
        return True

    # Checking every digit
    # through a loop
    while (num != 0):

        # All digits were checked
        if (num / 10 == 0):
            return True

        # Digit at index i
        digit1 = num % 10

        # Digit at index i-1
        digit2 = (num / 10) % 10

        # If difference is
        # greater than 1
        if (abs(digit2 - digit1) > 1):
            return False

        num = num / 10

    # Number checked
    return True

# Driver code

# -1234 to be checked
num = -1234
if (checkJumbled(abs(num))):
    print "True "
else:
    print "False"

# -1247 to be checked
num = -1247
if (checkJumbled(abs(num))):
    print "True "
else:
    print "False"

# This code is contributed
# by Sachin Bisht
```

## C#

```
// C# code to check if a number
// is jumbled or not
using System;

class GFG
{

    // Function to check if a
    // number is jumbled or not
    static bool checkJumbled(int num)
    {

        // Single digit number
        if (num / 10 == 0)
            return true;

        // Checking every digit
        // through a loop
        while (num != 0)
        {

            // All digits were checked
            if (num / 10 == 0)
                return true;

            // Digit at index i
            int digit1 = num % 10;

            // Digit at index i-1
            int digit2 = (num / 10) % 10;

            // If difference is
            // greater than 1
            if (Math.Abs(digit2 - digit1) > 1)
                return false;

            num = num / 10;
        }

        // Number checked
        return true;
    }

    // Driver code
    public static void Main ()
    {
        //-1234 to be checked
        int num = -1234;

        if (checkJumbled(num))
            Console.WriteLine("True ");
        else
            Console.WriteLine("False ");

        // 287 to be checked
        num = -1247;

        if (checkJumbled(num))
            Console.WriteLine("True");

        else
            Console.WriteLine("False");

    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to check if a
// number is jumbled or not

// Function to check if a
// number is jumbled or not
function checkJumbled($num)
{
    // Single digit number
    if ($num / 10 == 0)
        return true;

    // Checking every digit
    // through a loop
    while ($num != 0)
    {

        // All digits were checked
        if ($num / 10 == 0)
            return true;

        // Digit at index i
        $digit1 = $num % 10;

        // Digit at index i-1
        $digit2 = ($num / 10) % 10;

        // If difference is
        // greater than 1
        if (abs($digit2 - $digit1) > 1)
            return false;

        $num = $num / 10;
    }

    // Number checked
    return true;
}

// Driver code

//-1234 to be checked
$num = -1234;

if (checkJumbled($num))
    echo "True \n";
else
    echo "False \n";

// 287 to be checked
$num = -1247;

if (checkJumbled($num))
    echo "True \n";
else
    echo "False \n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript code to check if a number is jumbled or not

    // Function to check if a
    // number is jumbled or not
    function checkJumbled(num)
    {

        // Single digit number
        if (parseInt(num / 10, 10) == 0)
            return true;

        // Checking every digit
        // through a loop
        while (num != 0)
        {

            // All digits were checked
            if (parseInt(num / 10, 10) == 0)
                return true;

            // Digit at index i
            let digit1 = num % 10;

            // Digit at index i-1
            let digit2 = parseInt(num / 10, 10) % 10;

            // If difference is
            // greater than 1
            if (Math.abs(digit2 - digit1) > 1)
                return false;

            num = parseInt(num / 10, 10);
        }

        // Number checked
        return true;
    }

    //-1234 to be checked
    let num = -1234;

    if (checkJumbled(num))
      document.write("True " + "</br>");
    else
      document.write("False " + "</br>");

    // 287 to be checked
    num = -1247;

    if (checkJumbled(num))
      document.write("True " + "</br>");

    else
      document.write("False " + "</br>");

    // This code is contributed by rameshtravel07.
</script>
```

**输出:**

```
True
False
```

**相关文章:**
[步数](https://www.geeksforgeeks.org/stepping-numbers/)
本文由**罗希特·塔普利亚尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。