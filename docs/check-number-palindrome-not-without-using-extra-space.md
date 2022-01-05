# 不使用任何多余的空格来检查一个数字是不是回文

> 原文:[https://www . geeksforgeeks . org/check-number-回文-非不使用-extra-space/](https://www.geeksforgeeks.org/check-number-palindrome-not-without-using-extra-space/)

给定一个数字“n”，我们的目标是在不使用任何额外空间的情况下找出它是否是回文。我们不能复制一份新的号码。
**例:**

```
Input  : 2332
Output : Yes it is Palindrome.
Explanation:
original number = 2332
reversed number = 2332
Both are same hence the number is palindrome.

Input :1111
Output :Yes it is Palindrome.

Input : 1234
Output : No not Palindrome.
```

一个递归的解决方案将在下面的文章中讨论。
[检查一个数字是否是回文](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome/)
在这篇文章中讨论了一个不同的解决方案。
1)我们可以比较第一个数字和最后一个数字，然后我们重复这个过程。
2)对于第一个数字，我们需要数字的顺序。比方说，12321。把这个除以 10000 会得到领先的 1。尾部的 1 可以通过取 10 的 mod 来检索。
3)现在，把这个减少到 232。

```
(12321 % 10000)/10 = (2321)/10 = 232 
```

4)现在，10000 需要减少 100 倍。
以下是上述算法的实现:

## C++

```
// C++ program to find number is palindrome
// or not without using any extra space
#include <bits/stdc++.h>
using namespace std;
bool isPalindrome(int);

bool isPalindrome(int n)
{  
    // Find the appropriate divisor
    // to extract the leading digit
    int divisor = 1;
    while (n / divisor >= 10)
        divisor *= 10;

    while (n != 0)
    {
        int leading = n / divisor;
        int trailing = n % 10;

        // If first and last digit
        // not same return false
        if (leading != trailing) 
            return false;

        // Removing the leading and trailing
        // digit from number
        n = (n % divisor) / 10;

        // Reducing divisor by a factor
        // of 2 as 2 digits are dropped
        divisor = divisor / 100;
    }
    return true;
}

// Driver code
int main()
{
    isPalindrome(1001) ? cout << "Yes, it is Palindrome" :
    cout << "No, not Palindrome";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number is palindrome
// or not without using any extra space
public class GFG
{     
    static boolean isPalindrome(int n)
    {  
        // Find the appropriate divisor
        // to extract the leading digit
        int divisor = 1;
        while (n / divisor >= 10)
            divisor *= 10;

        while (n != 0)
        {
            int leading = n / divisor;
            int trailing = n % 10;

            // If first and last digit
            // not same return false
            if (leading != trailing) 
                return false;

            // Removing the leading and trailing
            // digit from number
            n = (n % divisor) / 10;

            // Reducing divisor by a factor
            // of 2 as 2 digits are dropped
            divisor = divisor / 100;
        }
        return true;
    }

    // Driver code
    public static void main(String args[])
    {
        if(isPalindrome(1001))
            System.out.println("Yes, it is Palindrome");
        else
            System.out.println("No, not Palindrome");
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python program to find number
# is palindrome or not without
# using any extra space

# Function to check if given number
# is palindrome or not without
# using the extra space
def isPalindrome(n):

    # Find the appropriate divisor
    # to extract the leading digit
    divisor = 1
    while (n / divisor >= 10):
        divisor *= 10

    while (n != 0):

        leading = n // divisor
        trailing = n % 10

        # If first and last digit
        # not same return false
        if (leading != trailing):
            return False

        # Removing the leading and
        # trailing digit from number
        n = (n % divisor)//10

        # Reducing divisor by a factor
        # of 2 as 2 digits are dropped
        divisor = divisor/100

    return True

# Driver code
if(isPalindrome(1001)):
    print('Yes, it is palindrome')
else:
    print('No, not palindrome')

# This code is contributed by Danish Raza
```

## C#

```
// C# program to find number
// is palindrome or not without
// using any extra space
using System;

class GFG
{
    static bool isPalindrome(int n)
    {
        // Find the appropriate
        // divisor to extract
        // the leading digit
        int divisor = 1;
        while (n / divisor >= 10)
            divisor *= 10;

        while (n != 0)
        {
            int leading = n / divisor;
            int trailing = n % 10;

            // If first and last digit
            // not same return false
            if (leading != trailing)
                return false;

            // Removing the leading and
            // trailing digit from number
            n = (n % divisor) / 10;

            // Reducing divisor by
            // a factor of 2 as 2
            // digits are dropped
            divisor = divisor / 100;
        }
        return true;
    }

    // Driver code
    static public void Main ()
    {
        if(isPalindrome(1001))
            Console.WriteLine("Yes, it " +
                         "is Palindrome");
        else
            Console.WriteLine("No, not " +
                            "Palindrome");
    }
}

// This code is contributed by m_kit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// number is palindrome
// or not without using
// any extra space

function isPalindrome($n)
{
    // Find the appropriate divisor
    // to extract the leading digit
    $divisor = 1;
    while ($n / $divisor >= 10)
        $divisor *= 10;

    while ($n != 0)
    {
        $leading = floor($n / $divisor);
        $trailing = $n % 10;

        // If first and last digit
        // not same return false
        if ($leading != $trailing)
            return false;

        // Removing the leading and
        // trailing digit from number
        $n = ($n % $divisor) / 10;

        // Reducing divisor by a
        // factor of 2 as 2 digits
        // are dropped
        $divisor = $divisor / 100;
    }
    return true;
}

// Driver code
if(isPalindrome(1001) == true)
echo "Yes, it is Palindrome" ;
else

echo "No, not Palindrome";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// javascript program to find number is palindrome
// or not without using any extra space

    function isPalindrome(n) {
        // Find the appropriate divisor
        // to extract the leading digit
        var divisor = 1;
        while (parseInt(n / divisor) >= 10)
            divisor *= 10;

        while (n != 0) {
            var leading = parseInt(n / divisor);
            var trailing = n % 10;

            // If first and last digit
            // not same return false
            if (leading != trailing)
                return false;

            // Removing the leading and trailing
            // digit from number
            n = parseInt((n % divisor) / 10);

            // Reducing divisor by a factor
            // of 2 as 2 digits are dropped
            divisor = divisor / 100;
        }
        return true;
    }

    // Driver code

        if (isPalindrome(1001))
            document.write("Yes, it is Palindrome");
        else
            document.write("No, not Palindrome");

// This code is contributed by todaysgaurav
</script>
```

**输出:**

```
Yes, it is Palindrome
```

本文由**阿比吉特·尚赫达尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。