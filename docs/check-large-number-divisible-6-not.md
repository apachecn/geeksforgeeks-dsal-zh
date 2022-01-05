# 检查一个大数是否能被 6 整除

> 原文:[https://www . geesforgeks . org/check-大数-整除-6-not/](https://www.geeksforgeeks.org/check-large-number-divisible-6-not/)

给定一个数，任务是检查一个数是否能被 6 整除。输入的数字可能很大，即使我们使用 long long int 也可能无法存储。

示例:

```
Input  : n = 2112
Output : Yes

Input : n = 1124
Output : No

Input  : n = 363588395960667043875487
Output : No
```

因为输入的数字可能非常大，所以我们不能用 n % 6 来检查一个数字是否能被 6 整除，尤其是在像 C/C++这样的语言中。这个想法基于以下事实。

```
A number is divisible by 6 it's divisible by 2 and 3\. 
a)  A number is divisible by 2 if its last digit is divisible by 2.
b)  A number is divisible by 3 if sum of digits is divisible by 3.
```

下面是基于上述步骤的实现。

## C++

```
// C++ program to find if a number is divisible by
// 6 or not
#include<bits/stdc++.h>
using namespace std;

// Function to find that number divisible by 6 or not
bool check(string str)
{
    int n = str.length();

    // Return false if number is not divisible by 2.
    if ((str[n-1]-'0')%2 != 0)
       return false;

    // If we reach here, number is divisible by 2.
    // Now check for 3.

    // Compute sum of digits
    int digitSum = 0;
    for (int i=0; i<n; i++)
        digitSum += (str[i]-'0');

    // Check if sum of digits is divisible by 3
    return (digitSum % 3 == 0);
}

// Driver code
int main()
{
    string str = "1332";
    check(str)?  cout << "Yes" : cout << "No ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if a number is
// divisible by 6 or not
class IsDivisible
{
    // Function to find that number divisible by 6 or not
    static boolean check(String str)
    {
        int n = str.length();

        // Return false if number is not divisible by 2.
        if ((str.charAt(n-1) -'0')%2 != 0)
           return false;

        // If we reach here, number is divisible by 2.
        // Now check for 3.

        // Compute sum of digits
        int digitSum = 0;
        for (int i=0; i<n; i++)
            digitSum += (str.charAt(i)-'0');

        // Check if sum of digits is divisible by 3
        return (digitSum % 3 == 0);
    }

    // main function
    public static void main (String[] args)
    {
        String str = "1332";
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
# by 6 or not

# Function to find that number
# is divisible by 6 or not
def check(st) :
    n = len(st)

    # Return false if number
    # is not divisible by 2.
    if (((int)(st[n-1])%2) != 0) :
        return False

    # If we reach here, number
    # is divisible by 2\. Now
    # check for 3.

    # Compute sum of digits
    digitSum = 0
    for i in range(0, n) :
        digitSum = digitSum + (int)(st[i])

    # Check if sum of digits
    # is divisible by 3
    return (digitSum % 3 == 0)

# Driver code
st = "1332"
if(check(st)) :
    print("Yes")
else :
    print("No ")

# This article is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find if a number is
// divisible by 6 or not
using System;

class GFG {

    // Function to find that number
    // divisible by 6 or not
    static bool check(String str)
    {
        int n = str.Length;

        // Return false if number is
        // not divisible by 2.
        if ((str[n-1] -'0') % 2 != 0)
            return false;

        // If we reach here, number is
        // divisible by 2.
        // Now check for 3.

        // Compute sum of digits
        int digitSum = 0;
        for (int i = 0; i < n; i++)
            digitSum += (str[i] - '0');

        // Check if sum of digits is
        // divisible by 3
        return (digitSum % 3 == 0);
    }

    // main function
    public static void Main ()
    {
        String str = "1332";

        if(check(str))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by parashar.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if a
// number is divisible by
// 6 or not

// Function to find that number
// divisible by 6 or not
function check($str)
{
    $n = strlen($str);

    // Return false if number is
    // not divisible by 2.
    if (($str[$n - 1] - '0') % 2 != 0)
    return false;

    // If we reach here, number
    // is divisible by 2.
    // Now check for 3.
    // Compute sum of digits
    $digitSum = 0;
    for ($i = 0; $i < $n; $i++)
        $digitSum += ($str[$i] - '0');

    // Check if sum of digits
    // is divisible by 3
    return ($digitSum % 3 == 0);
}

    // Driver code
    $str = "1332";
    if(check($str))
        echo "Yes" ;
    else
        echo " No ";
    return 0;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to find that number
    // divisible by 6 or not
    function check(str)
    {
        let n = str.length;

        // Return false if number is
        // not divisible by 2.
        if ((str[n-1] -'0') % 2 != 0)
            return false;

        // If we reach here, number is
        // divisible by 2.
        // Now check for 3.

        // Compute sum of digits
        let digitSum = 0;
        for (let i = 0; i < n; i++)
            digitSum += (str[i] - '0');

        // Check if sum of digits is
        // divisible by 3
        return (digitSum % 3 == 0);
    }

// Driver Code
     let str = "1332";
     if(check(str))
        document.write("Yes");
     else
        document.write("No");

// This code is contributed by splevel62.
</script>
```

**输出:**

```
Yes
```

本文由 [**丹麦语 _RAZA**](https://www.facebook.com/danish.raza.98096721) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。