# 检查一个大数是否能被 16 整除

> 原文:[https://www . geesforgeks . org/check-大数-整除-16-not/](https://www.geeksforgeeks.org/check-large-number-divisible-16-not/)

给定一个数，任务是检查一个数是否能被 16 整除。输入的数字可能很大，即使我们使用 long long int 也可能无法存储。

**示例:**

```
Input  : n = 1128
Output : No

Input  : n = 11216
Output : Yes

Input  : n = 1124273542764284287
Output : No
```

因为输入的数字可能非常大，所以我们不能用 n % 16 来检查一个数字是否能被 16 整除，尤其是在像 C/C++这样的语言中。这个想法基于以下事实。

```
A number is divisible by 16 if number formed 
by last four digits of it is divisible by 16.
```

插图:

```
For example, let us consider 769616 
Number formed by last four digits = 9616
Since 9522 is divisible by 16, answer is YES.
```

**这是如何工作的？**

```
Let us consider 76952, we can write it as
76942 = 7*10000 + 6*1000 + 9*100 + 5*10 + 2

The proof is based on below observation:
Remainder of 10i divided by 16 is 0 if i greater 
than or equal to four. Note that 10000, 
100000,... etc lead to remainder 0 when divided by 16.

So remainder of "7*10000 + 6*1000 + 9*100 + 
5*10 + 2" divided by 16 is equivalent to remainder 
of following : 
0 + 6*1000 + 9*100 + 5*10 + 2 = 6952
Therefore we can say that the whole number is 
divisible by 16 if 6952 is divisible by 16.
```

## C++

```
// C++ program to find if a number
// is divisible by 16 or not
#include<bits/stdc++.h>
using namespace std;

// Function to find that
// number divisible by 16 or not
bool check(string str)
{
    int n = str.length();

    // Empty string
    if (n == 0 && n == 1)
        return false;

    // If there is double digit
    if (n == 2)
        return (((str[n-2]-'0')*10 +
                 (str[n-1]-'0'))%16 == 0);

    // If there is triple digit
    if(n == 3)
         return ( ((str[n-3]-'0')*100 +
                   (str[n-2]-'0')*10 +
                   (str[n-1]-'0'))%16 == 0);

    // If number formed by last four
    // digits is divisible by 16.
    int last = str[n-1] - '0';
    int second_last = str[n-2] - '0';
    int third_last = str[n-3] - '0';
    int fourth_last = str[n-4] - '0';
    return ((fourth_last*1000 + third_last*100 +
             second_last*10 + last) % 16 == 0);
}

// Driver code
int main()
{
    string str = "769528";
    check(str)?  cout << "Yes" : cout << "No ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if a number
// is divisible by 16 or not
import java.io.*;

class GFG {
    // Function to find that
    // number divisible by 16 or not
    static boolean check(String str)
    {
        int n = str.length();

        // Empty string
        if (n == 0 && n == 1)
            return false;

        // If there is double digit
        if (n == 2)
            return (((str.charAt(n-2)-'0')*10 +
                     (str.charAt(n-1)-'0'))%16 == 0);

        // If there is triple digit
        if(n == 3)
             return ( ((str.charAt(n-3)-'0')*100 +
                       (str.charAt(n-2)-'0')*10 +
                       (str.charAt(n-1)-'0'))%16 == 0);

        // If number formed by last
        // four digits is divisible by 16.
        int last = str.charAt(n-1) - '0';
        int second_last = str.charAt(n-2) - '0';
        int third_last = str.charAt(n-3) - '0';
        int fourth_last = str.charAt(n-4) - '0';
        return ((fourth_last*1000 + third_last*100
                + second_last*10 + last) % 16 == 0);
    }

    // Driver code
    public static void main(String args[])
    {
        String str = "769528";
        if(check(str))
            System.out.println("Yes");
        else
            System.out.println("No ");
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python 3 program to find
# if a number is divisible
# by 16 or not

# Function to find that
# number divisible by
# 16 or not
def check(st) :
    n = len(st)

    # Empty string
    if (n == 0 and n == 1) :
        return False

    # If there is double digit
    if (n == 2) :
        return ((int)(st[n-2])*10 +
                ((int)(st[n-1])%16 == 0))

    # If there is triple digit
    if(n == 3) :
        return ( ((int)(st[n-3])*100 +
                   (int)(st[n-2])*10 +
                   (int)(st[n-1]))%16 == 0)

    # If number formed by last
    # four digits is divisible
    # by 16.
    last = (int)(st[n-1])
    second_last = (int)(st[n-2])
    third_last = (int)(st[n-3])
    fourth_last = (int)(st[n-4])
    return ((fourth_last*1000 + third_last*100
            + second_last*10 + last) % 16 == 0)

# Driver code
st = "769528"
if(check(st)) :
    print("Yes")
else :
    print("No")

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find if a number
// is divisible by 16 or not
using System;

class GFG {

    // Function to find that number
    // divisible by 16 or not
    static bool check(String str)
    {
        int n = str.Length;

        // Empty string
        if (n == 0 && n == 1)
            return false;

        // If there is double digit
        if (n == 2)
            return (((str[n - 2] - '0') * 10 +
                (str[n - 1] - '0')) % 16 == 0);

        // If there is triple digit
        if(n == 3)
            return (((str[n - 3] - '0') * 100 +
                     (str[n - 2] - '0') * 10 +
                     (str[n - 1] - '0')) % 16 == 0);

        // If number formed by last
        // four digits is divisible by 16.
        int last = str[n - 1] - '0';
        int second_last = str[n - 2] - '0';
        int third_last = str[n - 3] - '0';
        int fourth_last = str[n - 4] - '0';
        return ((fourth_last * 1000 + third_last * 100
            + second_last * 10 + last) % 16 == 0);
    }

    // Driver code
    public static void Main()
    {
        String str = "769528";
        if(check(str))
            Console.Write("Yes");
        else
            Console.Write("No ");
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if a number
// is divisible by 16 or not

// Function to find that
// number divisible by 16 or not
function check($str)
{
    $n = strlen($str);

    // Empty string
    if ($n == 0 && $n == 1)
        return false;

    // If there is double digit
    if ($n == 2)
        return ((($str[$n - 2] - '0') * 10 +
                 ($str[$n - 1] - '0')) % 16 == 0);

    // If there is triple digit
    if($n == 3)
        return ((($str[$n -3] - '0') *
                  100 + ($str[$n - 2] -
                  '0') * 10 + ($str[$n -
                  1] - '0')) % 16 == 0);

    // If number formed by last four
    // digits is divisible by 16.
    $last = $str[$n - 1] - '0';
    $second_last = $str[$n - 2] - '0';
    $third_last = $str[$n - 3] - '0';
    $fourth_last = $str[$n - 4] - '0';
    return (($fourth_last * 1000 +
             $third_last * 100 +
             $second_last * 10 +
             $last) % 16 == 0);
}

// Driver code
$str = "769528";
$x = check($str) ? "Yes" : "No ";
echo($x);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find if a number
// is divisible by 16 or not

// Function to find that number
// divisible by 16 or not
function check(str)
{
    let n = str.length;

    // Empty string
    if (n == 0 && n == 1)
        return false;

    // If there is double digit
    if (n == 2)
        return (((str[n - 2] - '0') * 10 +
                 (str[n - 1] - '0')) % 16 == 0);

    // If there is triple digit
    if(n == 3)
        return (((str[n - 3] - '0') * 100 +
                 (str[n - 2] - '0') * 10 +
                 (str[n - 1] - '0')) % 16 == 0);

    // If number formed by last
    // four digits is divisible by 16.
    let last = str[n - 1] - '0';
    let second_last = str[n - 2] - '0';
    let third_last = str[n - 3] - '0';
    let fourth_last = str[n - 4] - '0';

    return ((fourth_last * 1000 + third_last * 100 +
             second_last * 10 + last) % 16 == 0);
}

// Driver code
let str = "769528";

if (check(str))
    document.write("Yes");
else
    document.write("No ");

// This code is contributed by decode2207

</script>
```

**输出:**

```
No
```

本文由**丹麦语 _ 拉扎**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。