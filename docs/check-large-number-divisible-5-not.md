# 检查一个大数是否能被 5 整除

> 原文:[https://www . geesforgeks . org/check-大数-整除-5-not/](https://www.geeksforgeeks.org/check-large-number-divisible-5-not/)

给定一个数，任务是检查数是否能被 5 整除。输入的数字可能很大，即使我们使用 long long int 也可能无法存储。

示例:

```
Input  : n = 56945255
Output : Yes

Input  : n = 1234567589333150
Output : Yes

Input  : n = 3635883959606670431112222
Output : No
```

因为输入的数字可能非常大，所以我们不能用 n % 5 来检查一个数字是否能被 5 整除，尤其是在像 C/C++这样的语言中。这个想法基于以下事实。

```
   A number is divisible by 5 if its  
   digits last digit will be 0 or 5 .
```

插图:

```
For example, let us consider 769555 
Number formed by last digit is = 5
Since 5 is divisible by 5 , answer is YES.
```

**这是如何工作的？**

```
Let us consider 5335, we can write it as
5335 = 5*1000 + 3*100 + 3*10 + 5

The proof is based on below observation:
Remainder of 10i divided by 5 is 0 if i greater 
than or equal to one. Note than 10, 100, 1000,
... etc lead to remainder 0 when divided by 5.

So remainder of " 5*1000 + 3*100 + 
3*10 + 5" divided by 5 is equivalent to remainder 
of following : 
0 + 0 + 0 + 5 = 5

Since 5 is divisible by 5, answer is yes.
```

以下是上述想法的实现。

## C++

```
// C++ program to find if a number is
// divisible by 5 or not
#include<bits/stdc++.h>
using namespace std;

// Function to find that number divisible
// by 5 or not. The function assumes that
// string length is at least one.
bool isDivisibleBy5(string str)
{
    int n = str.length();

    return ( ((str[n-1]-'0') == 0) ||
             ((str[n-1]-'0') == 5));
}

// Driver code
int main()
{
    string str = "76955";
    isDivisibleBy5(str)?  cout << "Yes" :
                          cout << "No ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if a number is
// divisible by 5 or not
class IsDivisible
{
    // Function to find that number divisible
    // by 5 or not. The function assumes that
    // string length is at least one.
    static boolean isDivisibleBy5(String str)
    {
        int n = str.length();

        return ( ((str.charAt(n-1)-'0') == 0) ||
                 ((str.charAt(n-1)-'0') == 5));
    }

    // main function
    public static void main (String[] args)
    {
        String str = "76955";
        if(isDivisibleBy5(str))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 计算机编程语言

```
# Python program to find if a number is
# divisible by 5 or not

# Function to find that number divisible
# by 5 or not. The function assumes that
# string length is at least one.
def isDivisibleBy5(st) :
    n = len(st)
    return ( (st[n-1] == '0') or
           (st[n-1] == '5'))

# Driver code
st = "76955"
if isDivisibleBy5(st) :
    print "Yes"
else :
    print "No "

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find if a number is
// C# program to find if a number
// is divisible by 5 or not.
using System;

class IsDivisible
{
    // Function to find that number divisible
    // by 5 or not. The function assumes that
    // string length is at least one.
    static bool isDivisibleBy5(String str)
    {
        int n = str.Length;

        return (((str[n - 1] - '0') == 0) ||
                ((str[n - 1] - '0') == 5));
    }

    // Driver Code
    public static void Main ()
    {
        String str = "76955";
        if(isDivisibleBy5(str))
        Console.Write("Yes");
        else
        Console.Write("No");
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if a number
// is divisible by 5 or not

// Function to find that number divisible
// by 5 or not. The function assumes that
// string length is at least one.
function isDivisibleBy5($str)
{
    $n = strlen($str);

    return ( (($str[$n-1]-'0') == 0) ||
            (($str[$n-1]-'0') == 5));
}

// Driver code
$str = "76955";
$x = isDivisibleBy5($str) ? "Yes" : "No";
echo($x);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find if a number
// is divisible by 5 or not

// Function to find that number divisible
// by 5 or not. The function assumes that
// string length is at least one.
function  isDivisibleBy5(str)
{
    n = str.length;

    return (((str[n - 1] - '0') == 0) ||
            ((str[n - 1] - '0') == 5));
}

// Driver Code
var str = "76955";
var x = isDivisibleBy5(str) ? "Yes" : "No";

document.write(x);

// This code is contributed by bunnyram19

</script>
```

输出:

```
Yes
```

本文由 [**丹麦语 _RAZA**](https://www.facebook.com/danish.raza.98096721) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。