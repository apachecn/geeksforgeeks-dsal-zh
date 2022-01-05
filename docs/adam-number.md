# 亚当号

> 原文:[https://www.geeksforgeeks.org/adam-number/](https://www.geeksforgeeks.org/adam-number/)

给定一个数字 n，写一个程序检查给定的数字是否是亚当数。
亚当数是反转时的数，数的平方和反转数的平方应该是相互反转的数。多达 1000 个 Adam 数字是:0、1、2、3、11、12、13、21、22、31、101、102、103、111、112、113、121、122、201、202、211、212、221、301、311。

**例:**

```
Input : 12
Output : Adam Number
Explanation: 
Square of 12 = 144
Reverse of 12 = 21
Square of 21 = 441
Now Square of 12 and square of reverse of 12 are 
reverse of each other. Therefore 12 is Adam number.

Input : 14
Output : Not a Adam Number
```

**寻找亚当号的步骤:**

```
Step 1:  Find square of number. 
Step 2:  Find reverse of number.
Step 3:  Find square of number in Step 2.
Step 4:  Find reverse of number in Step 3.
Step 5:  Find whether number obtained in Step 4 and Step 1 are equal or not.
```

## C++

```
// CPP program to check Adam Number
#include <bits/stdc++.h>
using namespace std;

// To reverse Digits of numbers
int reverseDigits(int num)
{
    int rev = 0;
    while (num > 0)
    {
        rev = rev * 10 + num % 10;
        num /= 10;
    }
    return rev;
}

// To square number
int square(int num)
{
    return (num * num);
}

// To check Adam Number
bool checkAdamNumber(int num)
{
    // Square first number and square
    // reverse digits of second number
    int a = square(num);
    int b = square(reverseDigits(num));

    // If reverse of b equals a then given
    // number is Adam number
    if (a == reverseDigits(b))
    return true;
    return false;       
}

// Driver program to test above functions
int main()
{
    int num = 12;

    if (checkAdamNumber(num))
    cout << "Adam Number";
    else
    cout << "Not a Adam Number";   

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check Adam Number
public class Main {
    // To reverse Digits of numbers
    static int reverseDigits(int num)
    {
        int rev = 0;
        while (num > 0)
        {
            rev = rev * 10 + num % 10;
            num /= 10;
        }
        return rev;
    }

    // To square number
    static int square(int num)
    {
        return (num * num);
    }

    // To check Adam Number
    static boolean checkAdamNumber(int num)
    {
        // Square first number and square
        // reverse digits of second number
        int a = square(num);
        int b = square(reverseDigits(num));

        // If reverse of b equals a then given
        // number is Adam number
        if (a == reverseDigits(b))
        return true;
        return false;       
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {
        int num = 12;

        if (checkAdamNumber(num))
        System.out.println("Adam Number");
        else
        System.out.println("Not a Adam Number");   
    }

}
```

## 计算机编程语言

```
# Python program to check Adam Number
# To reverse Digits of numbers
def reverseDigits(num) :
    rev = 0
    while (num > 0) :
        rev = rev * 10 + num % 10
        num /= 10

    return rev

# To square number
def square(num) :
    return (num * num)

# To check Adam Number
def checkAdamNumber(num) :

    # Square first number and square
    # reverse digits of second number
    a = square(num)
    b = square(reverseDigits(num))

    # If reverse of b equals a then given
    # number is Adam number
    if (a == reverseDigits(b)) :
        return True
    else :
        return False

# Driver program to test above functions
num = 13
if (checkAdamNumber(num)) :
    print "Adam Number"
else :
    print "Not a Adam Number"

# This code is contributed by Nikita Tiwari
```

## C#

```
// C# Program to Check Adam Number
using System;

public class main {

    // To reverse Digits of numbers
    static int reverseDigits(int num)
    {
        int rev = 0;
        while (num > 0)
        {
            rev = rev * 10 + num % 10;
            num /= 10;
        }
        return rev;
    }

    // To square number
    static int square(int num)
    {
        return (num * num);
    }

    // To check Adam Number
    static bool checkAdamNumber(int num)
    {
        // Square first number and square
        // reverse digits of second number
        int a = square(num);
        int b = square(reverseDigits(num));

        // If reverse of b equals a then
        // given number is Adam number
        if (a == reverseDigits(b))
        return true;
        return false;
    }

    // Driver Code
    public static void Main(String []args)
    {
        int num = 12;

        if (checkAdamNumber(num))
        Console.WriteLine("Adam Number");
        else
        Console.WriteLine("Not a Adam Number");
    }

}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check Adam Number

// To reverse Digits of numbers
function reverseDigits($num)
{
    $rev = 0;
    while ($num > 0)
    {
        $rev = $rev * 10 + $num % 10;
        $num = (int) $num / 10;
    }
    return $rev;
}

// To square number
function square($num)
{
    return ($num * $num);
}

// To check Adam Number
function checkAdamNumber($num)
{
    // Square first number and square
    // reverse digits of second number
    $a = square($num);
    $b = square(reverseDigits($num));

    // If reverse of b equals a then
    // given number is Adam number
    if ($a == reverseDigits($b))
    return 0;
    return -1;
}

// Driver Code
$num = 12;

if (checkAdamNumber($num))
echo "Adam Number";
else
echo "Not a Adam Number";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
    // Javascript Program to Check Adam Number

    // To reverse Digits of numbers
    function reverseDigits(num)
    {
        let rev = 0;
        while (num > 0)
        {
            rev = rev * 10 + num % 10;
            num = parseInt(num / 10, 10);
        }
        return rev;
    }

    // To square number
    function square(num)
    {
        return (num * num);
    }

    // To check Adam Number
    function checkAdamNumber(num)
    {
        // Square first number and square
        // reverse digits of second number
        let a = square(num);
        let b = square(reverseDigits(num));

        // If reverse of b equals a then
        // given number is Adam number
        if (a == reverseDigits(b))
        return true;
        return false;
    }

    let num = 12;

    if (checkAdamNumber(num))
      document.write("Adam Number");
    else
      document.write("Not a Adam Number");

</script>
```

**输出:**

```
Adam Number
```

本文由**核素**投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。