# 递归程序检查数字是否回文

> 原文:[https://www . geesforgeks . org/递归程序检查数字是不是回文/](https://www.geeksforgeeks.org/recursive-program-to-check-if-number-is-palindrome-or-not/)

给定一个数字，任务是编写一个递归函数，检查给定的数字是否是回文。
**例:**

```
Input : 121
Output : yes

Input : 532
Output : no
```

编写函数的方法是递归调用函数，直到数字从后面完全遍历完。根据在[这个](https://www.geeksforgeeks.org/write-a-c-program-to-reverse-digits-of-a-number/)帖子中得到的公式，使用一个 temp 变量来存储数字的倒数。在参数中传递 temp 变量，一旦达到 n==0 的基本情况，返回存储一个数字的倒数的 temp。
以下是上述办法的实施情况:

## C++

```
// Recursive C++ program to check if the
// number is palindrome or not
#include <bits/stdc++.h>
using namespace std;

// recursive function that returns the reverse of digits
int rev(int n, int temp)
{
    // base case
    if (n == 0)
        return temp;

    // stores the reverse of a number
    temp = (temp * 10) + (n % 10);

    return rev(n / 10, temp);
}

// Driver Code
int main()
{

    int n = 121;

    int temp = rev(n, 0);

    if (temp == n)
        cout << "yes" << endl;
    else
        cout << "no" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program to
// check if the number is
// palindrome or not
import java.io.*;

class GFG
{

// recursive function that
// returns the reverse of digits
static int rev(int n, int temp)
{
    // base case
    if (n == 0)
        return temp;

    // stores the reverse
    // of a number
    temp = (temp * 10) + (n % 10);

    return rev(n / 10, temp);
}

// Driver Code
public static void main (String[] args)
{
    int n = 121;
    int temp = rev(n, 0);

    if (temp == n)
        System.out.println("yes");
    else
        System.out.println("no" );
}
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Recursive Python3 program to check
# if the number is palindrome or not

# Recursive function that returns
# the reverse of digits
def rev(n, temp):

    # base case
    if (n == 0):
        return temp;

    # stores the reverse of a number
    temp = (temp * 10) + (n % 10);

    return rev(n / 10, temp);

# Driver Code
n = 121;
temp = rev(n, 0);

if (temp != n):
    print("yes");
else:
    print("no");

# This code is contributed
# by mits
```

## C#

```
// Recursive C# program to
// check if the number is
// palindrome or not
using System;

class GFG
{

// recursive function
// that returns the
// reverse of digits
static int rev(int n,
               int temp)
{
    // base case
    if (n == 0)
        return temp;

    // stores the reverse
    // of a number
    temp = (temp * 10) +
               (n % 10);

    return rev(n / 10, temp);
}

// Driver Code
public static void Main ()
{
    int n = 121;
    int temp = rev(n, 0);

    if (temp == n)
        Console.WriteLine("yes");
    else
        Console.WriteLine("no" );
}
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Recursive PHP program to check
// if the number is palindrome or not

// Recursive function that returns
// the reverse of digits
function rev($n, $temp)
{
    // base case
    if ($n == 0)
        return $temp;

    // stores the reverse of a number
    $temp = ($temp * 10) + ($n % 10);

    return rev($n / 10, $temp);
}

// Driver Code
$n = 121;
$temp = rev($n, 0);

if ($temp != $n)
    echo "yes";
else
    echo "no";

// This code is contributed
// by Sach_Code
?>
```

## java 描述语言

```
<script>

// Recursive Javascript program to check if the
// number is palindrome or not

// recursive function that returns the reverse of digits
function rev(n, temp)
{
    // base case
    if (n == 0)
        return temp;

    // stores the reverse of a number
    temp = (temp * 10) + (n % 10);

    return rev(Math.floor(n / 10), temp);
}

// Driver Code

    let n = 121;

    let temp = rev(n, 0);

    if (temp == n)
        document.write("yes" + "<br>");
    else
        document.write("no" + "<br>");

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
yes
```