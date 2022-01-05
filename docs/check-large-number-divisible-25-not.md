# 检查一个大数是否能被 25 整除

> 原文:[https://www . geesforgeks . org/check-大数-整除-25-not/](https://www.geeksforgeeks.org/check-large-number-divisible-25-not/)

给定一个数字，任务是检查这个数字是否能被 25 整除。输入的数字可能很大，即使我们使用 long long int 也可能无法存储。

示例:

```
Input  : n = 56945250
Output : Yes

Input  : n = 1234567589333100
Output : Yes

Input  : n = 3635883959606670431112222
Output : No
```

因为输入的数字可能非常大，所以我们不能用 n % 25 来检查一个数字是否能被 25 整除，尤其是在像 C/C++这样的语言中。这个想法基于以下事实。

```
A number is divisible by 25 if its digits 
last two digits will be 0  or divisible by 25 .
```

插图:

```
For example, let us consider 769575 
Number formed by last two digits is = 75
Since 75 is divisible by 25 , answer is YES.
```

```
Let us consider 5325, we can write it as
5325 = 5*1000 + 3*100 + 2*10 + 5

The proof is based on below observation:
Remainder of 10i divided by 25 is 0 if i greater 
than or equal to two. Note than 100, 1000,
... etc lead to remainder 0 when divided by 25.

So remainder of " 5*1000 + 3*100 + 2*10 + 5" 
divided by 25 is equivalent to remainder 
of following : 
0 + 0 + 20 + 5 = 25

Since 25 is divisible by 25, answer is yes.
```

## C++

```
// C++ program to find if a number is
// divisible by 25 or not
#include<bits/stdc++.h>
using namespace std;

// Function to find that number divisible
// by 25 or not.
bool isDivisibleBy25(string str)
{
    // If length of string is single digit then
    // it's not divisible by 25
    int n = str.length();
    if (n == 1)
        return false;

    return ( (str[n-1]-'0' == 0  &&
              str[n-2]-'0' == 0) ||
   ((str[n-2]-'0')*10 + (str[n-1]-'0'))%25 == 0 );
}

// Driver code
int main()
{
    string str = "76955";
    isDivisibleBy25(str)?  cout << "Yes" :
                           cout << "No ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if a number is
// divisible by 25 or not
class IsDivisible
{
    // Function to find that number divisible
    // by 25 or not.
    static boolean isDivisibleBy25(String str)
    {
        // If length of string is single digit then
        // it's not divisible by 25
        int n = str.length();
        if (n == 1)
            return false;

        return ( (str.charAt(n-1)-'0' == 0  &&
                  str.charAt(n-2)-'0' == 0) ||
        ((str.charAt(n-2)-'0')*10 + (str.charAt(n-1)-'0'))%25 == 0 );
    }

    // main function
    public static void main (String[] args)
    {
        String str = "76955";
        if(isDivisibleBy25(str))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find if
# a number is divisible by 25
# or not

# Function to find that
# number divisible by 25 or not.
def isDivisibleBy25(st) :

    # If length of string is
    # single digit then it's
    # not divisible by 25
    n = len(st)
    if (n == 1) :
        return False

    return ((int)(st[n-1]) == 0 and ((int)(st[n-2])== 0) or
           ((int)(st[n-2])*10 + (int)(st[n-1])%25 == 0))

# Driver code
st = "76955"
if(isDivisibleBy25(st)) :
    print("Yes")
else :
    print("No")

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find if a number
// is divisible by 25 or not
using System;

class IsDivisible
{
    // Function to find that number
    // divisible by 25 or not.
    static bool isDivisibleBy25(String str)
    {
        // If length of string is single digit then
        // then it's not divisible by 25
        int n = str.Length;
        if (n == 1)
            return false;

        return ((str[n - 1] - '0' == 0 &&
                 str[n - 2] - '0' == 0) ||
                ((str[n - 2] - '0') * 10 +
                 (str[n - 1] - '0')) % 25 == 0);
    }

    // Driver Code
    public static void Main ()
    {
        String str = "76955";
        if(isDivisibleBy25(str))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by Nitin Mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if a number
// is divisible by 25 or not

// Function to find that number
//  divisible by 25 or not.
function isDivisibleBy25($str)
{

    // If length of string
    // is single digit then
    // it's not divisible by 25
    $n = strlen($str);
    if ($n == 1)
        return false;

    return ( ($str[$n - 1] -'0' == 0 &&
              $str[$n - 2] -'0' == 0) ||
            (($str[$n - 2] -'0') * 10 +
             ($str[$n - 1] - '0')) % 25 == 0 );
}

// Driver code
$str = "76955";
$x = isDivisibleBy25($str) ? "Yes" : "No ";
echo($x);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find if a number
// is divisible by 25 or not

// Function to find that number
// divisible by 25 or not
function isDivisibleBy25(str)
{

    // If length of string
    // is single digit then
    // it's not divisible by 25
    n = str.length;

    if (n == 1)
        return false;

    return ((str[n - 1] -'0' == 0 &&
             str[n - 2] -'0' == 0) ||
           ((str[n - 2] -'0') * 10 +
            (str[n - 1] - '0')) % 25 == 0);
}

// Driver Code
var str = "76955";
var x = isDivisibleBy25(str) ? "Yes" : "No";

document.write (x);

// This code is contributed by bunnyram19

</script>
```

输出:

```
No
```

本文由**丹麦语 _RAZA** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。