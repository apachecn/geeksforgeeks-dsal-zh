# 检查一个大数是否能被 4 整除

> 原文:[https://www . geesforgeks . org/check-大数-整除-4-not/](https://www.geeksforgeeks.org/check-large-number-divisible-4-not/)

给定一个数，任务是检查一个数是否能被 4 整除。输入的数字可能很大，即使我们使用 long long int 也可能无法存储。

**示例:**

```
Input : n = 1124
Output : Yes

Input  : n = 1234567589333862
Output : No

Input  : n = 363588395960667043875487
Output : No

```

因为输入的数字可能非常大，所以我们不能用 n % 4 来检查一个数字是否能被 4 整除，尤其是在像 C/C++这样的语言中。这个想法基于以下事实。

> 如果一个数的最后两位数组成的数能被 4 整除，这个数就能被 4 整除。

插图:

```
For example, let us consider 76952 
Number formed by last two digits = 52
Since 52 is divisible by 4, answer is YES.

```

**这是如何工作的？**

```
Let us consider 76952, we can write it as
76942 = 7*10000 + 6*1000 + 9*100 + 5*10 + 2

The proof is based on below observation:
Remainder of 10i divided by 4 is 0 if i greater 
than or equal to two. Note than 100, 1000,
... etc lead to remainder 0 when divided by 4.

So remainder of "7*10000 + 6*1000 + 9*100 + 
5*10 + 2" divided by 4 is equivalent to remainder 
of following : 
0 + 0 + 0 + 5*10 + 2 = 52
Therefore we can say that the whole number is 
divisible by 4 if 52 is divisible by 4.

```

以下是上述想法的实现:

## C++

```
// C++ program to find if a number is divisible by
// 4 or not
#include <bits/stdc++.h>
using namespace std;

// Function to find that number divisible by
// 4 or not
bool check(string str)
{
    int n = str.length();

    // Empty string
    if (n == 0)
        return false;

    // If there is single digit
    if (n == 1)
        return ((str[0] - '0') % 4 == 0);

    // If number formed by last two digits is
    // divisible by 4.
    int last = str[n - 1] - '0';
    int second_last = str[n - 2] - '0';
    return ((second_last * 10 + last) % 4 == 0);
}

// Driver code
int main()
{
    string str = "76952";

    // Function call
    check(str) ? cout << "Yes" : cout << "No ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if a number is
// divisible by 4 or not
class IsDivisible
{
    // Function to find that number
    // is divisible by 4 or not
    static boolean check(String str)
    {
        int n = str.length();

        // Empty string
        if (n == 0)
            return false;

        // If there is single digit
        if (n == 1)
            return ((str.charAt(0) - '0') % 4 == 0);

        // If number formed by last two digits is
        // divisible by 4.
        int last = str.charAt(n - 1) - '0';
        int second_last = str.charAt(n - 2) - '0';
        return ((second_last * 10 + last) % 4 == 0);
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "76952";

        // Function call
        if (check(str))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find
# if a number is divisible
# by 4 or not

# Function to find that
# number divisible by
# 4 or not

def check(st):
    n = len(st)

    # Empty string
    if (n == 0):
        return False

    # If there is single
    # digit
    if (n == 1):
        return ((st[0] - '0') % 4 == 0)

    # If number formed by
    # last two digits is
    # divisible by 4.
    last = (int)(st[n - 1])
    second_last = (int)(st[n - 2])

    return ((second_last * 10 + last) % 4 == 0)

# Driver code
st = "76952"

# Function call
if(check(st)):
    print("Yes")
else:
    print("No ")

# This code is contributed by Nikita tiwari
```

## C#

```
// C# program to find if a number is
// divisible by 4 or not
using System;

class GFG
{
    // Function to find that number
    // is divisible by 4 or not
    static bool check(String str)
    {
        int n = str.Length;

        // Empty string
        if (n == 0)
            return false;

        // If there is single digit
        if (n == 1)
            return ((str[0] - '0') % 4 == 0);

        // If number formed by last two
        // digits is divisible by 4.
        int last = str[n - 1] - '0';
        int second_last = str[n - 2] - '0';

        return ((second_last * 10 + last) % 4 == 0);
    }

    // Driver code
    public static void Main()
    {
        String str = "76952";

        // Function call
        if (check(str))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is Contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if a
// number is divisible by
// 4 or not

// Function to find that
// number divisible by
// 4 or not
function check($str)
{
    $n = strlen($str);

    // Empty string
    if ($n == 0)
        return false;

    // If there is single digit
    if ($n == 1)
        return (($str[0] - '0') % 4 == 0);

    // If number formed by
    // last two digits is
    // divisible by 4.
    $last = $str[$n - 1] - '0';
    $second_last = $str[$n - 2] - '0';
    return (($second_last * 10 + $last) % 4 == 0);
}

// Driver code
$str = "76952";

// Function call
$x = check($str)? "Yes" : "No";
echo($x);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
//Javascript program to check whether a string is divisible by 4 or not

// function to check the divisibility
function check(str)
{ 
      // checking the length for future reference
      var n = str.length;

      // if it is empty then directly returning false
      if( n == 0)
      {        
           return false;
      }

      if( n == 1)
      {
           return ((str[0] -'0') % 4 == 0);
      }
      var lastNumber = str[n-1] -'0';
      var lastSecondNUmber = str[n-2] -'0';
      return ((lastSecondNUmber * 10  + lastNumber) % 4 == 0);   
}

// Driver code
var str="76952";

//checking the value by passing it into the function
// Function call
if(check(str)){
  console.log("Yes");
}
else{
  console.log("No");
}
```

**Output**

```
Yes
```

本文由 [**丹麦语 _RAZA**](https://www.facebook.com/danish.raza.98096721) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。