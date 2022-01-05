# 反转和添加功能

> 原文:[https://www.geeksforgeeks.org/reverse-and-add-function/](https://www.geeksforgeeks.org/reverse-and-add-function/)

**反转加功能**以一个数字开始，反转其数字，并将反转加到原来的数字上。如果总和不是回文，重复这个过程，直到它。

写一个程序，取数字并给出结果回文(如果有的话)。如果需要 1000 次以上的迭代(加法)或产生大于 4，294，967，295 的回文，假设给定数字不存在回文。

**示例:**

```
Input : 195
Output : 9339

Input : 265
Output: 45254

Input : 196
Output : No palindrome exist  
```

## C++

```
// C++ Program to implement reverse and add function
#include<bits/stdc++.h>
using namespace std;

/* Iterative function to reverse digits of num*/
long long reversDigits(long long num)
{
    long long rev_num = 0;
    while (num > 0)
    {
        rev_num = rev_num*10 + num%10;
        num = num/10;
    }
    return rev_num;
}

/* Function to check whether he number is palindrome or not */
bool isPalindrome(long long num)
{
    return (reversDigits(num) == num);
}

/* Reverse and Add Function */
void ReverseandAdd(long long num)
{
    long long rev_num=0;
    while (num <= 4294967295)
    {
        // Reversing the digits of the number
        rev_num = reversDigits(num);

        // Adding the reversed number with the original
        num = num + rev_num;

        // Checking whether the number is palindrome or not
        if (isPalindrome(num))
        {
            printf("%lld\n",num);
            break;
        }
        else if (num > 4294967295)
        {
            printf("No palindrome exist");
        }
    }
}

// Driver Program
int main()
{
    ReverseandAdd(195);
    ReverseandAdd(265);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement reverse and add function
public class ReverseAdd
{
    /* Iterative function to reverse digits of num*/
    long reversDigits(long num)
    {
        long rev_num = 0;
        while (num > 0)
        {
            rev_num = rev_num*10 + num%10;
            num = num/10;
        }
        return rev_num;
    }

    /* Function to check whether he number is
           palindrome or not */
    boolean isPalindrome(long num)
    {
        return (reversDigits(num) == num);
    }

    /* Reverse and Add Function */
    void ReverseandAdd(long num)
    {
        long rev_num = 0;
        while (num <= 4294967295l)
        {
            // Reversing the digits of the number
            rev_num = reversDigits(num);

            // Adding the reversed number with the original
            num = num + rev_num;

            // Checking whether the number is palindrome or not
            if(isPalindrome(num))
            {
                System.out.println(num);
                break;
            }
            else if (num > 4294967295l)
            {
                System.out.println("No palindrome exist");
            }
        }
    }

    // Main method
    public static void main(String[] args)
    {
        ReverseAdd ob = new ReverseAdd();
        ob.ReverseandAdd(195l);
        ob.ReverseandAdd(265l);

    }
}
```

## 计算机编程语言

```
#Python Program to implement reverse and add function

# Iterative function to reverse digits of num
def reversDigits(num):
    rev_num=0
    while (num > 0):
        rev_num = rev_num*10 + num%10
        num = num/10
    return rev_num

# Function to check whether the number is palindrome or not
def isPalindrome(num):
    return (reversDigits(num) == num)

# Reverse and Add Function
def ReverseandAdd(num):
    rev_num = 0
    while (num <= 4294967295):
        # Reversing the digits of the number
        rev_num = reversDigits(num)

        # Adding the reversed number with the original
        num = num + rev_num

        # Checking whether the number is palindrome or not
        if(isPalindrome(num)):
            print num
            break
        else:
            if (num > 4294967295):
                print "No palindrome exist"

# Driver Code
ReverseandAdd(195)
ReverseandAdd(265)
```

## C#

```
// C# Program to implement reverse and add function
using System;

class GFG
{
    /* Iterative function to reverse digits of num*/
    static long reversDigits(long num)
    {
        long rev_num = 0;
        while (num > 0)
        {
            rev_num = rev_num * 10 + num % 10;
            num = num / 10;
        }
        return rev_num;
    }

    /* Function to check whether he number is
        palindrome or not */
    static bool isPalindrome(long num)
    {
        return (reversDigits(num) == num);
    }

    /* Reverse and Add Function */
    static void ReverseandAdd(long num)
    {
        long rev_num = 0;
        while (num <= 4294967295)
        {
            // Reversing the digits of the number
            rev_num = reversDigits(num);

            // Adding the reversed number with the original
            num = num + rev_num;

            // Checking whether the number is palindrome or not
            if(isPalindrome(num))
            {
                Console.WriteLine(num);
                break;
            }
            else if (num > 4294967295)
            {
                Console.WriteLine("No palindrome exist");
            }
        }
    }

    // Driver code
    public static void Main()
    {
        ReverseandAdd(195);
        ReverseandAdd(265);
    }
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to implement reverse and add function

/* Iterative function to reverse digits of num*/
function reversDigits($num)
{
    $rev_num = 0;
    while ($num > 0)
    {
        $rev_num = $rev_num * 10 + $num % 10;
        $num = (int)($num / 10);
    }
    return $rev_num;
}

/* Function to check whether he number
   is palindrome or not */
function isPalindrome($num)
{
    return (reversDigits($num) == $num);
}

/* Reverse and Add Function */
function ReverseandAdd($num)
{
     $rev_num = 0;
    while ($num <= 4294967295)
    {
        // Reversing the digits of the number
        $rev_num = reversDigits($num);

        // Adding the reversed number with
        // the original
        $num = $num + $rev_num;

        // Checking whether the number is
        // palindrome or not
        if (isPalindrome($num))
        {
            print($num . "\n");
            break;
        }
        else if ($num > 4294967295)
        {
            print("No palindrome exist");
        }
    }
}

// Driver Code
ReverseandAdd(195);
ReverseandAdd(265);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

// Javascript program to implement
// reverse and add function

// Iterative function to reverse digits of num
function reversDigits(num)
{
    let rev_num = 0;
    while (num > 0)
    {
        rev_num = rev_num * 10 + num % 10;
        num = parseInt(num / 10, 10);
    }
    return rev_num;
}

// Function to check whether he number
// is palindrome or not
function isPalindrome(num)
{
    return(reversDigits(num) == num);
}

// Reverse and Add Function
function ReverseandAdd(num)
{
    let rev_num = 0;

    while (num <= 4294967295)
    {

        // Reversing the digits of the number
        rev_num = reversDigits(num);

        // Adding the reversed number
        // with the original
        num = num + rev_num;

        // Checking whether the number
        // is palindrome or not
        if (isPalindrome(num))
        {
            document.write(num + "</br>");
            break;
        }
        else if (num > 4294967295)
        {
            document.write("No palindrome exist" +
                           "</br>");
        }
    }
}

// Driver code
ReverseandAdd(195);
ReverseandAdd(265);

// This code is contributed by rameshtravel07 

</script>
```

**输出:**

```
9339
45254
```

**参考文献**:[https://app . assembly . com/spaces/AASU _ fall 2008 _ programming team/wiki](https://app.assembla.com/spaces/AASU_Fall2008_ProgrammingTeam/wiki)

本文由**拉胡尔·阿格沃尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。