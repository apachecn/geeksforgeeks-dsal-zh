# 检查一个大数是否能被 8 整除

> 原文:[https://www . geesforgeks . org/check-大数-整除-8-not/](https://www.geeksforgeeks.org/check-large-number-divisible-8-not/)

给定一个数，任务是检查一个数是否能被 8 整除。输入的数字可能很大，即使我们使用 long long int 也可能无法存储。
示例:

```
Input  : n = 1128
Output : Yes

Input : n = 1124
Output : No

Input  : n = 363588395960667043875487
Output : No
```

因为输入的数字可能非常大，所以我们不能用 n % 8 来检查一个数字是否能被 8 整除，尤其是在像 C/C++这样的语言中。这个想法基于以下事实。

> 如果一个数的最后三位数字组成的数能被 8 整除，那么这个数就能被 8 整除。

**插图:**

```
For example, let us consider 76952 
Number formed by last three digits = 952
Since 952 is divisible by 8, answer is YES.
```

**这是如何工作的？**

```
Let us consider 76952, we can write it as
76942 = 7*10000 + 6*1000 + 9*100 + 5*10 + 2

The proof is based on below observation:
Remainder of 10i divided by 8 is 0 if i greater 
than or equal to three. Note than 10000, 
1000,... etc lead to remainder 0 when divided by 8.

So remainder of "7*10000 + 6*1000 + 9*100 + 
5*10 + 2" divided by 8 is equivalent to remainder 
of following : 
0 + 0 + 9*100 + 5*10 + 2 = 52
Therefore we can say that the whole number is 
divisible by 8 if 952 is divisible by 8.
```

以下是上述事实的实现:

## C++

```
// C++ program to find if a number is divisible by
// 8 or not
#include<bits/stdc++.h>
using namespace std;

// Function to find that number divisible by
// 8 or not
bool check(string str)
{
    int n = str.length();

    // Empty string
    if (n == 0)
        return false;

    // If there is single digit
    if (n == 1)
        return ((str[0]-'0')%8 == 0);

    // If there is double digit
    if (n == 2)
        return (((str[n-2]-'0')*10 + (str[n-1]-'0'))%8 == 0);

    // If number formed by last three digits is
    // divisible by 8.
    int last = str[n-1] - '0';
    int second_last = str[n-2] - '0';
    int third_last = str[n-3] - '0';

    return ((third_last*100 + second_last*10 + last) % 8 == 0);
}

// Driver code
int main()
{
    string str = "76952";
    check(str)?  cout << "Yes" : cout << "No ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if a number is
// divisible by 8 or not
class IsDivisible
{
    // Function to find that number divisible by
    // 8 or not
    static boolean check(String str)
    {
        int n = str.length();

        // Empty string
        if (n == 0)
            return false;

        // If there is single digit
        if (n == 1)
            return ((str.charAt(0)-'0')%8 == 0);

        // If there is double digit
        if (n == 2)
            return (((str.charAt(n-2)-'0')*10 + (str.charAt(n-1)-'0'))%8 == 0);

        // If number formed by last three digits is
        // divisible by 8.
        int last = str.charAt(n-1) - '0';
        int second_last = str.charAt(n-2) - '0';
        int third_last = str.charAt(n-3) - '0';

        return ((third_last*100 + second_last*10 + last) % 8 == 0);
    }

    // main function
    public static void main (String[] args)
    {
        String str = "76952";
        if(check(str))
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
# by 8 or not

# Function to find that
# number divisible by 8
# or not
def check(st) :
    n = len(st)

    # Empty string
    if (n == 0) :
        return False

    # If there is single digit
    if (n == 1) :
        return ((int)(st[0]) % 8 == 0)

    # If there is double digit
    if (n == 2) :
        return ((int)(st[n - 2]) * 10 +
          ((int)(str[n - 1]) % 8 == 0))

    # If number formed by last
    # three digits is divisible
    # by 8.
    last = (int)(st[n - 1])
    second_last = (int)(st[n - 2])
    third_last = (int)(st[n - 3])

    return ((third_last*100 + second_last*10 +
                               last) % 8 == 0)

# Driver code
st = "76952"

if(check(st)) :
    print("Yes")
else :
    print("No ")

# This code is contributed by Nikita tiwari
```

## C#

```
// C# program to find if a number
// is divisible by 8 or not
using System;

class IsDivisible
{
    // Function to find that number
    // divisible by 8 or not
    static bool check(String str)
    {
        int n = str.Length;

        // Empty string
        if (n == 0)
            return false;

        // If there is single digit
        if (n == 1)
            return ((str[0] - '0') %8  == 0);

        // If there is double digit
        if (n == 2)
            return (((str[n - 2] - '0') * 10 +
            (str[n - 1] - '0')) % 8 == 0);

        // If number formed by last three
        // digits is divisible by 8
        int last = str[n - 1] - '0';
        int second_last = str[n - 2] - '0';
        int third_last = str[n - 3] - '0';

        return ((third_last * 100 + second_last 
                        * 10 + last) % 8 == 0);
    }

    // Driver Code
    public static void Main ()
    {
        String str = "76952";
        if(check(str))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This Code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if a number
// is divisible by 8 or not

// Function to find that number
// divisible by 8 or not
function check($str)
{
    $n = strlen($str);

    // Empty string
    if ($n == 0)
        return false;

    // If there is single digit
    if ($n == 1)
        return (($str[0] - '0') %
                          8 == 0);

    // If there is double digit
    if ($n == 2)
        return ((($str[$n - 2] - '0') *
               10 + ($str[$n - 1] - '0'))
                                % 8 == 0);

    // If number formed by last three
    // digits is divisible by 8.
    $last = $str[$n - 1] - '0';
    $second_last = $str[$n - 2] - '0';
    $third_last = $str[$n - 3] - '0';

    return (($third_last * 100 +
             $second_last * 10 +
             $last) % 8 == 0);
}

// Driver code
$str = "76952";
$x = check($str)? "Yes" : "No ";
echo($x);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to find that number 
    // divisible by 8 or not
    function check(str)
    {
        let n = str.length;

        // Empty string
        if (n == 0)
            return false;

        // If there is single digit
        if (n == 1)
            return ((str[0] - '0') %8  == 0);

        // If there is double digit
        if (n == 2)
            return (((str[n - 2] - '0') * 10 + 
            (str[n - 1] - '0')) % 8 == 0);

        // If number formed by last three 
        // digits is divisible by 8
        let last = str[n - 1] - '0';
        let second_last = str[n - 2] - '0';
        let third_last = str[n - 3] - '0';

        return ((third_last * 100 + second_last  
                        * 10 + last) % 8 == 0);
    }

// Driver Code

     let str = "76952";
     if(check(str))
        document.write("Yes");
     else
         document.write("No");

// This code is contributed by splevel62.
</script>
```

输出:

```
Yes
```

本文由 [**丹麦语 _RAZA**](https://www.facebook.com/danish.raza.98096721) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。