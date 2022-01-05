# 检查一个大数是否可除以 15

> 原文:[https://www . geesforgeks . org/check-大数-可除性-15/](https://www.geeksforgeeks.org/check-large-number-divisibility-15/)

给定一个非常大的数字。用 15 检查它的可除性。
**例:**

```
Input: 31
Output: No

Input : num = "156457463274623847239840239
               402394085458848462385346236
               482374823647643742374523747
               264723762374620"
Output: Yes
Given number is divisible by 15
```

如果一个数[能被 5](https://www.geeksforgeeks.org/check-large-number-divisible-5-not/) 整除(如果最后一个数字是 5 或 0)，那么这个数就能被 15 整除，如果数字的和能被 3 整除，那么这个数就是[能被 3 整除](https://www.geeksforgeeks.org/check-large-number-divisible-3-not/)。
这里，用[累加](https://www.geeksforgeeks.org/numeric-header-in-c-stl-set-1-accumulate-and-partial_sum/)功能把所有数字加起来。

## C++

```
// CPP program to check if a large
// number is divisible by 15
#include <bits/stdc++.h>

using namespace std;

// function to check if a large number
// is divisible by 15
bool isDivisible(string s)
{
    // length of string
    int n = s.length();

    // check divisibility by 5
    if (s[n - 1] != '5' and s[n - 1] != '0')
        return false;

    // Sum of digits
    int sum = accumulate(begin(s), end(s), 0) - '0' * n;

    // if divisible by 3
    return (sum % 3 == 0);
}

// driver program
int main()
{
    string s = "15645746327462384723984023940239";
    isDivisible(s)? cout << "Yes\n": cout << "No\n";
    string s1 = "15645746327462384723984023940235";
    isDivisible(s1)? cout << "Yes\n": cout << "No\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a large
// number is divisible by 15
import java.util.*;

class GFG
{

// function to check if a large
// number is divisible by 15
public static boolean isDivisible(String S)
{
    // length of string
    int n = S.length();

    // check divisibility by 5
    if (S.charAt(n - 1) != '5' &&
        S.charAt(n - 1) != '0')
        return false;

    // Sum of digits
    int sum = 0;
    for(int i = 0; i < S.length(); i++)
        sum += (int)S.charAt(i);

        // if divisible by 3
        if(sum % 3 == 0)
            return true;
        else
            return false;
}

// Driver code
public static void main (String[] args)
{
    String S = "15645746327462384723984023940239";
    if(isDivisible(S) == true)
        System.out.println("Yes");
    else
        System.out.println("No");

    String S1 = "15645746327462384723984023940235";
    if(isDivisible(S1) == true)
        System.out.println("Yes");
    else
        System.out.println("No");
    }
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 蟒蛇 3

```
# Python3 program to check if
# a large number is
# divisible by 15

# to find sum
def accumulate(s):
    acc = 0;
    for i in range(len(s)):
        acc += ord(s[i]) - 48;
    return acc;

# function to check
# if a large number
# is divisible by 15
def isDivisible(s):
    # length of string
    n = len(s);

    # check divisibility by 5
    if (s[n - 1] != '5' and s[n - 1] != '0'):
        return False;

    # Sum of digits
    sum = accumulate(s);

    # if divisible by 3
    return (sum % 3 == 0);

# Driver Code
s = "15645746327462384723984023940239";
if isDivisible(s):
    print("Yes");
else:
    print("No");

s = "15645746327462384723984023940235";
if isDivisible(s):
    print("Yes");
else:
    print("No");

# This code is contributed by mits
```

## C#

```
// C# program to check if a large
// number is divisible by 15
using System;

class GFG
{
// function to check if a large
// number is divisible by 15
public static bool isDivisible(String S)
{
    // length of string
    int n = S.Length;

    // check divisibility by 5
    if (S[n - 1] != '5' &&
        S[n - 1] != '0')
        return false;

    // Sum of digits
    int sum = 0;
    for(int i = 0; i < S.Length; i++)
        sum += (int)S[i];

        // if divisible by 3
        if(sum % 3 == 0)
            return true;
        else
            return false;
}

// Driver code
public static void Main()
{
    String S = "15645746327462384723984023940239";
    if(isDivisible(S) == true)
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");

    String S1 = "15645746327462384723984023940235";
    if(isDivisible(S1) == true)
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
    }
}

// This code is contributed
// by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if
// a large number is
// divisible by 15

// to find sum
function accumulate($s)
{
    $acc = 0;
    for($i = 0;
        $i < strlen($s); $i++)
    {
        $acc += $s[$i] - '0';
    }
    return $acc;
}

// function to check
// if a large number
// is divisible by 15
function isDivisible($s)
{
    // length of string
    $n = strlen($s);

    // check divisibility by 5
    if ($s[$n - 1] != '5' &&
        $s[$n - 1] != '0')
        return false;

    // Sum of digits
    $sum = accumulate($s);

    // if divisible by 3
    return ($sum % 3 == 0);
}

// Driver Code
$s = "15645746327462384723984023940239";
isDivisible($s) ?
print("Yes\n") : print("No\n");

$s = "15645746327462384723984023940235";
isDivisible($s) ?
print("Yes\n") : print("No\n");

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to check if
// a large number is
// divisible by 15
// to find sum

function accumulate(s)
{
    let acc = 0;
    for(let i = 0;
        i < s.length; i++)
    {
        acc += s[i] - '0';
    }
    return acc;
}

// function to check
// if a large number
// is divisible by 15
function isDivisible(s)
{

    // length of string
    let n = s.length;

    // check divisibility by 5
    if (s[n - 1] != '5' &&
        s[n - 1] != '0')
        return false;

    // Sum of digits
    let sum = accumulate(s);

    // if divisible by 3
    return (sum % 3 == 0);
}

// Driver Code
let s = "15645746327462384723984023940239";
isDivisible(s) ?
document.write("Yes<br>") : document.write("No<br>");

s = "15645746327462384723984023940235";
isDivisible(s) ?
document.write("Yes<br>") : document.write("No<br>");

// This code is contributed by _saurabh_jaiswal
</script>
```

**输出:**

```
No
Yes
```

**时间复杂度:** O(位数)
本文由 [**奋斗者**](https://www.facebook.com/raja.vikramaditya.7) 投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。