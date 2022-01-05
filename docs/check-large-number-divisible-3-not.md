# 检查一个大数是否能被 3 整除

> 原文:[https://www . geesforgeks . org/check-大数-整除-3-not/](https://www.geeksforgeeks.org/check-large-number-divisible-3-not/)

给定一个数，任务是我们用 3 除这个数。输入的数字可能很大，即使我们使用 long long int 也可能无法存储。
示例:

```
Input  : n = 769452
Output : Yes

Input  : n = 123456758933312
Output : No

Input  : n = 3635883959606670431112222
Output : Yes
```

因为输入的数字可能非常大，所以我们不能用 n % 3 来检查一个数字是否能被 3 整除，尤其是在像 C/C++这样的语言中。这个想法基于以下事实。

> 如果一个数的总和能被 3 整除，这个数就能被 3 整除。

**插图:**

```
For example n = 1332
Sum of digits = 1 + 3 + 3 + 2
             = 9
Since sum is divisible by 3,
answer is Yes.
```

**这是如何工作的？**

```
Let us consider 1332, we can write it as
1332 = 1*1000 + 3*100 + 3*10 + 2

The proof is based on below observation:
Remainder of 10i divided by 3 is 1
So powers of 10 only result in value 1.

Remainder of "1*1000 + 3*100 + 3*10 + 2"
divided by 3 can be written as : 
1*1 + 3*1 + 3*1 + 2 = 9
The above expression is basically sum of
all digits.

Since 9 is divisible by 3, answer is yes.
```

以下是上述事实的实现:

## C++

```
// C++ program to find if a number is divisible by
// 3 or not
#include<bits/stdc++.h>
using namespace std;

// Function to find that number divisible by 3 or not
int check(string str)
{
    // Compute sum of digits
    int n = str.length();
    int digitSum = 0;
    for (int i=0; i<n; i++)
        digitSum += (str[i]-'0');

    // Check if sum of digits is divisible by 3.
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
// divisible by 3 or not
class IsDivisible
{
    // Function to find that number
    // divisible by 3 or not
    static boolean check(String str)
    {
        // Compute sum of digits
        int n = str.length();
        int digitSum = 0;
        for (int i=0; i<n; i++)
            digitSum += (str.charAt(i)-'0');

        // Check if sum of digits is
        // divisible by 3.
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

## 计算机编程语言

```
# Python program to find if a number is
# divisible by 3 or not

# Function to find that number
# divisible by 3 or not
def check(num) :

    # Compute sum of digits
    digitSum = 0
    while num > 0 :
        rem = num % 10
        digitSum = digitSum + rem
        num = num / 10

    # Check if sum of digits is
    # divisible by 3.
    return (digitSum % 3 == 0)

# main function
num = 1332
if(check(num)) :
    print "Yes"
else :
    print "No"

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find if a number is
// divisible by 3 or not
using System;

class GFG
{
    // Function to find that number
    // divisible by 3 or not
    static bool check(string str)
    {
        // Compute sum of digits
        int n = str.Length;
        int digitSum = 0;

        for (int i = 0; i < n; i++)
            digitSum += (str[i] - '0');

        // Check if sum of digits is
        // divisible by 3.
        return (digitSum % 3 == 0);
    }

    // main function
    public static void Main ()
    {
        string str = "1332";

        if(check(str))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if a
// number is divisible by
// 3 or not

// Function to find that
// number divisible by 3 or not
function check($str)
{

    // Compute sum of digits
    $n = strlen($str);
    $digitSum = 0;
    for ($i = 0; $i < $n; $i++)
        $digitSum += ($str[$i] - '0');

    // Check if sum of digits
    // is divisible by 3.
    return ($digitSum % 3 == 0);
}

// Driver code
$str = "1332";
$x = check($str) ? "Yes" : "No ";
echo($x);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// Javascript program to find if a
// number is divisible by
// 3 or not

// Function to find that
// number divisible by 3 or not
function check(str)
{

    // Compute sum of digits
    let n = str.length;
    let digitSum = 0;
    for (let i = 0; i < n; i++)
        digitSum += (str[i] - '0');

    // Check if sum of digits
    // is divisible by 3.
    return (digitSum % 3 == 0);
}

// Driver code
let str = "1332";
let x = check(str) ? "Yes" : "No ";
document.write(x);

// This code is contributed by _saurabh_jaiswal.
</script>
```

输出:

```
Yes
```

本文由 [**丹麦语 _RAZA**](https://www.facebook.com/danish.raza.98096721) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。