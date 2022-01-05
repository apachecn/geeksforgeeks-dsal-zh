# 检查一个大数是否能被 11 整除

> 原文:[https://www . geesforgeks . org/check-大数-整除-11-not/](https://www.geeksforgeeks.org/check-large-number-divisible-11-not/)

给定一个数，任务是检查这个数是否能被 11 整除。输入的数字可能很大，即使我们使用 long long int 也可能无法存储。
示例:

```
Input : n = 76945
Output : Yes

Input  : n = 1234567589333892
Output : Yes

Input  : n = 363588395960667043875487
Output : No
```

因为输入的数字可能非常大，所以我们不能用 n % 11 来检查一个数字是否能被 11 整除，尤其是在像 C/C++这样的语言中。这个想法基于以下事实。
如果后面两个的**差能被 11 整除，则一个数能被 11 整除。** 

1.  奇数位的位数总和。
2.  偶数位置的位数总和。

**插图:**

```
For example, let us consider 76945 
Sum of digits at odd places  : 7 + 9 + 5
Sum of digits at even places : 6 + 4 
Difference of two sums = 21 - 10 = 11
Since difference is divisible by 11, the
number 7945 is divisible by 11.
```

**这是如何工作的？**

```
Let us consider 7694, we can write it as
7694 = 7*1000 + 6*100 + 9*10 + 4

The proof is based on below observation:
Remainder of 10i divided by 11 is 1 if i is even
Remainder of 10i divided by 11 is -1 if i is odd

So the powers of 10 only result in values either 1 
or -1\. 

Remainder of "7*1000 + 6*100 + 9*10 + 4"
divided by 11 can be written as : 
7*(-1) + 6*1 + 9*(-1) + 4*1

The above expression is basically difference 
between sum of even digits and odd digits.
```

以下是上述事实的实现:

## C++

```
// C++ program to find if a number is divisible by
// 11 or not
#include<bits/stdc++.h>
using namespace std;

// Function to find that number divisible by 11 or not
int check(string str)
{
    int n = str.length();

    // Compute sum of even and odd digit
    // sums
    int oddDigSum = 0, evenDigSum = 0;
    for (int i=0; i<n; i++)
    {
        // When i is even, position of digit is odd
        if (i%2 == 0)
            oddDigSum += (str[i]-'0');
        else
            evenDigSum += (str[i]-'0');
    }

    // Check its difference is divisible by 11 or not
    return ((oddDigSum - evenDigSum) % 11 == 0);
}

// Driver code
int main()
{
    string str = "76945";
    check(str)?  cout << "Yes" : cout << "No ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if a number is
// divisible by 11 or not
class IsDivisible
{
    // Function to find that number divisible by 11 or not
    static boolean check(String str)
    {
        int n = str.length();

        // Compute sum of even and odd digit
        // sums
        int oddDigSum = 0, evenDigSum = 0;
        for (int i=0; i<n; i++)
        {
            // When i is even, position of digit is odd
            if (i%2 == 0)
                oddDigSum += (str.charAt(i)-'0');
            else
                evenDigSum += (str.charAt(i)-'0');
        }

        // Check its difference is divisible by 11 or not
        return ((oddDigSum - evenDigSum) % 11 == 0);
    }

    // main function
    public static void main (String[] args)
    {
        String str = "76945";
        if(check(str))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python 3 code program to find if a number
# is divisible by 11 or not

# Function to find that number divisible by
#  11 or not
def check(st) :
    n = len(st)

    # Compute sum of even and odd digit
    # sums
    oddDigSum = 0
    evenDigSum = 0
    for i in range(0,n) :
        # When i is even, position of digit is odd
        if (i % 2 == 0) :
            oddDigSum = oddDigSum + ((int)(st[i]))
        else:
            evenDigSum = evenDigSum + ((int)(st[i]))

    # Check its difference is divisible by 11 or not
    return ((oddDigSum - evenDigSum) % 11 == 0)

# Driver code
st = "76945"
if(check(st)) :
    print( "Yes")
else :
    print("No ")

# This code is contributed by Nikita tiwari.
```

## C#

```
// C# program to find if a number is
// divisible by 11 or not
using System;

class GFG
{
    // Function to find that number
    // divisible by 11 or not
    static bool check(string str)
    {
        int n = str.Length;

        // Compute sum of even and odd digit
        // sums
        int oddDigSum = 0, evenDigSum = 0;

        for (int i = 0; i < n; i++)
        {
            // When i is even, position of
            // digit is odd
            if (i % 2 == 0)
                oddDigSum += (str[i] - '0');
            else
                evenDigSum += (str[i] - '0');
        }

        // Check its difference is
        // divisible by 11 or not
        return ((oddDigSum - evenDigSum)
                                % 11 == 0);
    }

    // main function
    public static void Main ()
    {
        String str = "76945";

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
// 11 or not

// Function to find that number
// divisible by 11 or not
function check($str)
{
    $n = strlen($str);

    // Compute sum of even
    // and odd digit sums
    $oddDigSum = 0; $evenDigSum = 0;
    for ($i = 0; $i < $n; $i++)
    {

        // When i is even, position
        // of digit is odd
        if ($i % 2 == 0)
            $oddDigSum += ($str[$i] - '0');
        else
            $evenDigSum += ($str[$i] - '0');
    }

    // Check its difference
    // is divisible by 11 or not
    return (($oddDigSum - $evenDigSum)
                            % 11 == 0);
}

// Driver code
$str = "76945";
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
    // divisible by 11 or not
    function check(str)
    {
        let n = str.length;

        // Compute sum of even and odd digit
        // sums
        let oddDigSum = 0, evenDigSum = 0;

        for (let i = 0; i < n; i++)
        {

            // When i is even, position of
            // digit is odd
            if (i % 2 == 0)
                oddDigSum += (str[i] - '0');
            else
                evenDigSum += (str[i] - '0');
        }

        // Check its difference is
        // divisible by 11 or not
        return ((oddDigSum - evenDigSum)
                                % 11 == 0);
    }

// Driver Code
    let str = "76945";
    if(check(str))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by chinmoy1997pal.
</script>
```

输出:

```
Yes
```

本文由 [**丹麦语 _RAZA**](https://www.facebook.com/danish.raza.98096721) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。