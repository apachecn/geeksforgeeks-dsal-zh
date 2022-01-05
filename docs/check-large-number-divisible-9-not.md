# 检查一个大数是否能被 9 整除

> 原文:[https://www . geesforgeks . org/check-大数-整除-9-not/](https://www.geeksforgeeks.org/check-large-number-divisible-9-not/)

给定一个数，任务是找出这个数是否能被 9 整除。输入的数字可能很大，即使我们使用 long long int 也可能无法存储。

示例:

```
Input  : n = 69354
Output : Yes

Input  : n = 234567876799333
Output : No

Input  : n = 3635883959606670431112222
Output : No
```

因为输入的数字可能非常大，所以我们不能用 n % 9 来检查一个数字是否能被 9 整除，尤其是在像 C/C++这样的语言中。这个想法基于以下事实。

```
A number is divisible by 9 if sum of its digits is divisible by 9.
```

插图:

```
For example n = 9432
Sum of digits = 9 + 4 + 3 + 2
             = 18
Since sum is divisible by 9,
answer is Yes.
```

**这是如何工作的？**

```
Let us consider 1332, we can write it as
1332 = 1*1000 + 3*100 + 3*10 + 2

The proof is based on below observation:
Remainder of 10i divided by 9 is 1
So powers of 10 only results in remainder 1 
when divided by 9.

Remainder of "1*1000 + 3*100 + 3*10 + 2"
divided by 9 can be written as : 
1*1 + 3*1 + 3*1 + 2 = 9
The above expression is basically sum of
all digits.

Since 9 is divisible by 9, answer is yes.
```

以下是上述想法的实现。

## C++

```
// C++ program to find if a number is divisible by
// 9 or not
#include<bits/stdc++.h>
using namespace std;

// Function to find that number divisible by 9 or not
int check(string str)
{
    // Compute sum of digits
    int n = str.length();
    int digitSum = 0;
    for (int i=0; i<n; i++)
        digitSum += (str[i]-'0');

    // Check if sum of digits is divisible by 9.
    return (digitSum % 9 == 0);
}

// Driver code
int main()
{
    string str = "99333";
    check(str)?  cout << "Yes" : cout << "No ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if a number is
// divisible by 9 or not
class IsDivisible
{
    // Function to find that number
    // is divisible by 9 or not
    static boolean check(String str)
    {
        // Compute sum of digits
        int n = str.length();
        int digitSum = 0;
        for (int i=0; i<n; i++)
            digitSum += (str.charAt(i)-'0');

        // Check if sum of digits is divisible by 9.
        return (digitSum % 9 == 0);
    }

    // main function
    public static void main (String[] args)
    {
        String str = "99333";
        if(check(str))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python 3 program to
# find if a number is
# divisible by
# 9 or not

# Function to find that
# number divisible by 9
# or not
def check(st) :

    # Compute sum of digits
    n = len(st)
    digitSum = 0

    for i in range(0,n) :
        digitSum = digitSum + (int)(st[i])

    # Check if sum of digits
    # is divisible by 9.
    return (digitSum % 9 == 0)

# Driver code
st = "99333"

if(check(st)) :
    print("Yes")
else :
    print("No")

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find if a number is
// divisible by 9 or not.
using System;

class GFG {

    // Function to find that number
    // is divisible by 9 or not
    static bool check(String str)
    {

        // Compute sum of digits
        int n = str.Length;
        int digitSum = 0;
        for (int i = 0; i < n; i++)
            digitSum += (str[i] - '0');

        // Check if sum of digits is
        // divisible by 9.
        return (digitSum % 9 == 0);
    }

    // main function
    public static void Main ()
    {
        String str = "99333";
        if(check(str))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is Contributed by
// nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if a number
// is divisible by 9 or not

// Function to find that
// number divisible by 9 or not
function check($str)
{

    // Compute sum of digits
    $n = strlen($str);
    $digitSum = 0;
    for ($i = 0; $i < $n; $i++)
        $digitSum += ($str[$i] - '0');

    // Check if sum of digits
    // is divisible by 9.
    return ($digitSum % 9 == 0);
}

// Driver code
$str = "99333";
$x = check($str) ? "Yes" : "No ";
echo($x);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find if a number
// is divisible by 9 or not

// Function to find that
// number divisible by 9 or not
function check(str)
{

    // Compute sum of digits
    let n = str.length;
    let digitSum = 0;

    for(let i = 0; i < n; i++)
        digitSum += (str[i] - '0');

    // Check if sum of digits
    // is divisible by 9.
    return (digitSum % 9 == 0);
}

// Driver code
let str = "99333";
let x = check(str) ? "Yes" : "No ";

document.write(x);

// This code is contributed by _saurabh_jaiswal.

</script>
```

**输出:**

```
Yes
```

本文由 [**丹麦语 _RAZA**](https://www.facebook.com/danish.raza.98096721) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。