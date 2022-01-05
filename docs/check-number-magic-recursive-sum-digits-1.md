# 检查一个数字是否为幻数(数字的递归和为 1)

> 原文:[https://www . geesforgeks . org/check-number-magic-recursive-sum-digits-1/](https://www.geeksforgeeks.org/check-number-magic-recursive-sum-digits-1/)

如果一个数的位数总和是通过每次相加后的位数总和递归计算出来的，那么这个数被称为幻数。如果一位数是 1，那么这个数字就是一个神奇的数字。

**例如-**
号= 50113
=>5+0+1+1+3 = 10
=>1+0 = 1
这是一个**幻数**

**例如-**
号= 1234
=>1+2+3+4 = 10
=>1+0 = 1
这是一个**幻数**

**示例:**

```
 Input : 1234
Output : Magic Number

Input  : 12345
Output : Not a magic Number
```

这种方法使用暴力。该函数不断增加数字，直到达到一位数的总和。为了理解我如何计算一位数的总和，请查看本页- [查找一个数字的位数总和，直到总和变成一位数](https://www.geeksforgeeks.org/finding-sum-of-digits-of-a-number-until-sum-becomes-single-digit/)

## C++

```
// CPP program to check if a number is Magic
// number.
#include<iostream>
using namespace std;

bool isMagic(int n)
{
    int sum = 0;

    // Note that the loop continues
    // if n is 0 and sum is non-zero.
    // It stops when n becomes 0 and
    // sum becomes single digit.
    while (n > 0 || sum > 9)
    {
        if (n == 0)
        {
            n = sum;
            sum = 0;
        }
        sum += n % 10;
        n /= 10;
    }

    // Return true if sum becomes 1.
    return (sum == 1);
}

// Driver code
int main()
{
    int n = 1234;
    if (isMagic(n))
        cout << "Magic Number";
    else
        cout << "Not a magic Number";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if
// a number is Magic number.
class GFG
{
   public static boolean isMagic(int n)
   {
       int sum = 0;

       // Note that the loop continues
       // if n is 0 and sum is non-zero.
       // It stops when n becomes 0 and
       // sum becomes single digit.
       while (n > 0 || sum > 9)
       {
           if (n == 0)
           {
               n = sum;
               sum = 0;
           }
           sum += n % 10;
           n /= 10;
       }

       // Return true if sum becomes 1.
       return (sum == 1);
   }

   // Driver code
   public static void main(String args[])
    {
     int n = 1234;
     if (isMagic(n))
        System.out.println("Magic Number");

     else
        System.out.println("Not a magic Number");
    }
}

// This code is contributed by Anshika Goyal.
```

## 蟒蛇 3

```
# Python3 program to check
# if a number is Magic
# number.

def isMagic(n):
    sum = 0;

    # Note that the loop
    # continues if n is 0
    # and sum is non-zero.
    # It stops when n becomes
    # 0 and sum becomes single
    # digit.
    while (n > 0 or sum > 9):
        if (n == 0):
            n = sum;
            sum = 0;
        sum = sum + n % 10;
        n = int(n / 10);

    # Return true if
    # sum becomes 1.
    return True if (sum == 1) else False;

# Driver code
n = 1234;
if (isMagic(n)):
    print("Magic Number");
else:
    print("Not a magic Number");

# This code is contributed
# by mits.
```

## C#

```
// C# program to check if
// a number is Magic number.
using System;

class GFG
{
    public static bool isMagic(int n)
    {
        int sum = 0;

        // Note that the loop continues
        // if n is 0 and sum is non-zero.
        // It stops when n becomes 0 and
        // sum becomes single digit.
        while (n > 0 || sum > 9)
        {
            if (n == 0)
            {
                n = sum;
                sum = 0;
            }
            sum += n % 10;
            n /= 10;
        }

        // Return true if sum becomes 1.
        return (sum == 1);
    }

    // Driver code
    public static void Main()
    {
        int n = 1234;
        if (isMagic(n))
            Console.WriteLine("Magic Number");

        else
            Console.WriteLine("Not a magic Number");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if
// a number is Magic number.
function isMagic($n)
{
    $sum = 0;

    // Note that the loop
    // continues if n is 0
    // and sum is non-zero.
    // It stops when n becomes
    // 0 and sum becomes single
    // digit.
    while ($n > 0 || $sum > 9)
    {
        if ($n == 0)
        {
            $n = $sum;
            $sum = 0;
        }
        $sum += $n % 10;
        $n /= 10;
    }

    // Return true if
    // sum becomes 1.
    return ($sum == 1);
}

// Driver code
$n = 1234;
if (isMagic($n))
    echo"Magic Number";
else
    echo "Not a magic Number";

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to check if
// a number is Magic number.
function isMagic( n)
   {
       var sum = 0;

       // Note that the loop continues
       // if n is 0 and sum is non-zero.
       // It stops when n becomes 0 and
       // sum becomes single digit.
       while (n > 0 || sum > 9)
       {
           if (n = 0)
           {
               n = sum;
               sum = 0;
           }
           sum += n % 10;
           n /= 10;
       }

       // Return true if sum becomes 1.
       return (sum = 1);
   }

   // Driver code
    var n = 1234;
    if (isMagic(n))
    document.write("Magic Number");

    else
        document.write("Not a magic Number");

// This code is contributed by shivanisinghss2110

</script>
```

**Output:** 

```
Magic Number
```

**高效进场(捷径):**还有一个验证幻数的捷径方法。该函数将确定输入除以 9 的余数是否为 1。如果是 1，那么这个数就是一个幻数。9 的可除性规则说，如果一个数的总和也能被 9 整除，那么这个数就能被 9 整除。因此，如果一个数能被 9 整除，那么，递归地，所有的数字和也能被 9 整除。最后的数字总和总是 9。原数增加 1 会使最终值增加 1，使其为 10，最终和为 1，从而验证其为幻数。

## C++

```
// C++ program to check
// Whether the number is Magic or not.
#include <iostream>
using namespace std;

int main() {
    // Accepting sample input
    int x = 1234;

    // Condition to check Magic number
    if(x%9==1)
        cout << ("Magic Number");
    else
        cout << ("Not a Magic Number");    

    return 0;
}
```

## C

```
// C program to check
// Whether the number is Magic or not.
#include <stdio.h>

int main() {

    // Accepting sample input
    int x = 1234;

    // Condition to check Magic number
    if(x%9==1)
        printf("Magic Number");
    else
        printf("Not a Magic Number");      

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check
// Whether the number is Magic or not.
class GFG{

public static void main(String[] args)
{

    // Accepting sample input
    int x = 1234;

    // Condition to check Magic number
    if (x % 9 == 1)
        System.out.printf("Magic Number");
    else
        System.out.printf("Not a Magic Number");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to check
# Whether the number is Magic or not.

# Accepting sample input
x = 1234

# Condition to check Magic number
if (x % 9 == 1):
    print("Magic Number")
else:
    print("Not a Magic Number")

# This code is contributed by kirti
```

## C#

```
// C# program to check
// Whether the number is Magic or not.
using System;
using System.Collections.Generic;

class GFG{

public static void Main(String[] args)
{

    // Accepting sample input
    int x = 1234;

    // Condition to check Magic number
    if (x % 9 == 1)
        Console.Write("Magic Number");
    else
        Console.Write("Not a Magic Number");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program to check
// Whether the number is Magic or not.

// Accepting sample input
var x = 1234;

// Condition to check Magic number
if (x % 9 == 1)
    document.write("Magic Number");
else
    document.write("Not a Magic Number");

// This code is contributed by shivanisinghss2110

</script>
```

**Output:** 

```
Magic Number
```

本文由 **Ayush Saxena** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。