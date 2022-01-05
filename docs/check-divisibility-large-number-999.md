# 用 999 检查任意大数的可除性

> 原文:[https://www . geesforgeks . org/check-可分性-大数-999/](https://www.geeksforgeeks.org/check-divisibility-large-number-999/)

给你一个 n 位数的大数字，你必须检查它是否能被 999 整除，而不能用 999 除或求数字的模。
**例:**

```
Input : 235764 
Output : Yes

Input : 23576 
Output : No
```

由于输入的数字可能非常大，我们不能用 n % 999 来检查一个数字是否能被 999 整除，尤其是在像 C/C++这样的语言中。这个想法基于以下事实。

这些解决方案基于以下事实。

> 如果一个数的 3 位数组的和(如果需要的组是在开头加上 0 形成的)能被 999 整除，那么这个数就能被 999 整除。

**插图:**

```
Input : 235764 
Output : Yes
Explanation : Step I - read input : 235, 764
              Step II - 235 + 764 = 999
              As result is 999 then we can 
              conclude that it is divisible by 999.

Input : 1244633121
Output : Yes
Explanation : Step I - read input : 1, 244, 633, 121
              Step II - 001 + 244 + 633 + 121 = 999
              As result is 999 then we can conclude 
              that it is divisible by 999.

Input : 999999999
Output : Yes
Explanation : Step I - read input : 999, 999, 999
              Step II - 999 + 999 + 999 = 2997
              Step III - 997 + 002 = 999
              As result is 999 then we can conclude  
              that it is divisible by 999.
```

**这是如何工作的？**

```
Let us consider 235764, we can write it as
235764 = 2*105 + 3*104 + 5*103 + 
         7*102 + 6*10 + 4

The idea is based on below observation:
Remainder of 103 divided by 999 is 1
For i > 3, 10i % 999 = 10i-3 % 999 

Let us see how we use above fact.
Remainder of 2*105 + 3*104 + 5*103 + 
7*102 + 6*10 + 4
Remainder with 999 can be written as : 
2*100 + 3*10 + 5*1 + 7*100 + 6*10 + 4 
The above expression is basically sum of
groups of size 3.

Since the sum is divisible by 999, answer is yes.
```

一个简单而有效的方法是以字符串的形式输入(如果需要，通过在数字的左边添加 0，使其长度为 3*m)，然后您必须从右向左添加三个块中的数字，直到它成为 3 位数，如果结果是 999，我们可以说该数字可被 999 整除。
就像在“可除 9”的情况下，我们检查所有数字的和是否能被 9 整除一样，在可除 999 的情况下也是如此。我们从右到左对所有 3 位数组进行求和，检查最终结果是否为 999。

## C++

```
// CPP for divisibility of number by 999
#include<bits/stdc++.h>
using namespace std;

// function to check divisibility
bool isDivisible999(string num)
{
    int n = num.length();
    if (n == 0 && num[0] == '0')
       return true;

    // Append required 0s at the beginning.
    if (n % 3 == 1)
       num = "00" + num;
    if (n % 3 == 2)
       num = "0" + num;

    // add digits in group of three in gSum
    int gSum = 0;
    for (int i = 0; i<n; i++)
    {
        // group saves 3-digit group
        int group = 0;
        group += (num[i++] - '0') * 100;
        group += (num[i++] - '0') * 10;
        group += num[i] - '0';
        gSum += group;
    }

    // calculate result till 3 digit sum
    if (gSum > 1000)
    {
        num = to_string(gSum);
        n = num.length();
        gSum = isDivisible999(num);
    }
    return (gSum == 999);
}

// driver program
int main()
{
    string num = "1998";
    int n = num.length();
    if (isDivisible999(num))
        cout << "Divisible";
    else
        cout << "Not divisible";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java for divisibility of number by 999

class Test
{   
    // Method to check divisibility
    static boolean isDivisible999(String num)
    {
        int n = num.length();
        if (n == 0 && num.charAt(0) == '0')
           return true;

        // Append required 0s at the beginning.
        if (n % 3 == 1)
           num = "00" + num;
        if (n % 3 == 2)
           num = "0" + num;

        // add digits in group of three in gSum
        int gSum = 0;
        for (int i = 0; i<n; i++)
        {
            // group saves 3-digit group
            int group = 0;
            group += (num.charAt(i++) - '0') * 100;
            group += (num.charAt(i++) - '0') * 10;
            group += num.charAt(i) - '0';
            gSum += group;
        }

        // calculate result till 3 digit sum
        if (gSum > 1000)
        {
            num = Integer.toString(gSum);
            n = num.length();
            gSum = isDivisible999(num) ? 1 : 0;
        }
        return (gSum == 999);
    }

    // Driver method
    public static void main(String args[])
    {
        String num = "1998";

        System.out.println(isDivisible999(num) ? "Divisible" : "Not divisible");
    }
}
```

## 蟒蛇 3

```
# Python3 program for divisibility
# of number by 999

# function to check divisibility
def isDivisible999(num):
    n = len(num);
    if(n == 0 or num[0] == '0'):
        return true

    # Append required 0s at the beginning.
    if((n % 3) == 1):
        num = "00" + num
    if((n % 3) == 2):
        num = "0" + num

    # add digits in group of three in gSum    
    gSum = 0
    for i in range(0, n, 3):

        # group saves 3-digit group
        group = 0
        group += (ord(num[i]) - 48) * 100
        group += (ord(num[i + 1]) - 48) * 10
        group += (ord(num[i + 2]) - 48)
        gSum += group

    # calculate result till 3 digit sum    
    if(gSum > 1000):
        num = str(gSum)
        n = len(num)
        gSum = isDivisible999(num)
    return (gSum == 999)

# Driver code
if __name__=="__main__":
    num = "1998"
    n = len(num)
    if(isDivisible999(num)):
        print("Divisible")
    else:
        print("Not divisible")

# This code is contributed
# by Sairahul Jella
```

## C#

```
// C# code for divisibility of number by 999

using System;
class Test
{
    // Method to check divisibility
    static bool isDivisible999(String num)
    {
        int n = num.Length;
        if (n == 0 && num[0] == '0')
        return true;

        // Append required 0s at the beginning.
        if (n % 3 == 1)
        num = "00" + num;
        if (n % 3 == 2)
        num = "0" + num;

        // add digits in group of three in gSum
        int gSum = 0;
        for (int i = 0; i<n; i++)
        {
            // group saves 3-digit group
            int group = 0;
            group += (num[i++] - '0') * 100;
            group += (num[i++] - '0') * 10;
            group += num[i] - '0';
            gSum += group;
        }

        // calculate result till 3 digit sum
        if (gSum > 1000)
        {
            num = Convert.ToString(gSum);
            n = num.Length ;
            gSum = isDivisible999(num) ? 1 : 0;
        }
        return (gSum == 999);
    }

    // Driver method
    public static void Main()
    {
        String num = "1998";

        Console.WriteLine(isDivisible999(num) ? "Divisible" : "Not divisible");
    }
    // This code is contributed by Ryuga
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP for divisibility of number by 999

// function to check divisibility
function isDivisible999($num)
{
    $n = strlen($num);
    if ($n == 0 && $num[0] == '0')
    return true;

    // Append required 0s at the beginning.
    if ($n % 3 == 1)
        $num = "00" . $num;
    if ($n % 3 == 2)
        $num = "0" . $num;

    // add digits in group of three in gSum
    $gSum = 0;
    for ($i = 0; $i < $n; $i += 3)
    {
        // group saves 3-digit group
        $group = 0;
        $group += (ord($num[$i]) - 48) * 100;
        $group += (ord($num[$i + 1]) - 48) * 10;
        $group += (ord($num[$i + 2]) - 48);
        $gSum += $group;
    }

    // calculate result till 3 digit sum
    if ($gSum > 1000)
    {
        $num = strval($gSum);
        $n = strlen($num);
        $gSum = isDivisible999($num);
    }
    return ($gSum == 999);
}

// Driver Code
$num = "1998";
if (isDivisible999($num))
    echo "Divisible";
else
    echo "Not divisible";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript for divisibility of number by 999

// function to check divisibility
function isDivisible999(num)
{
    let n = num.length;
    if (n == 0 && num[0] == '0')
    return true;

    // Append required 0s at the beginning.
    if (n % 3 == 1)
        num = "00" + num;
    if (n % 3 == 2)
        num = "0" + num;

    // add digits in group of three in gSum
    let gSum = 0;
    for (let i = 0; i < n; i += 3)
    {
        // group saves 3-digit group
        group = 0;
        group += (num.charCodeAt(i) - 48) * 100;
        group += (num.charCodeAt(i + 1) - 48) * 10;
        group += (num.charCodeAt(i + 2) - 48);
        gSum += group;
    }

    // calculate result till 3 digit sum
    if (gSum > 1000)
    {
        num = String(gSum);
        n = strlen(num);
        gSum = isDivisible999(num);
    }
    return (gSum == 999);
}

// Driver Code
let num = "1998";
if (isDivisible999(num))
    document.write("Divisible");
else
    document.write("Not divisible");

// This code is contributed by _saurabh_jaiswal.
</script>
```

**输出:**

```
Divisible
```

[更多可分性算法](https://www.geeksforgeeks.org/tag/divisibility/)。
本文由 [**希瓦姆·普拉丹(anuj_charm)**](https://www.facebook.com/anuj.charm) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。