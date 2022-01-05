# 打印给定范围内所有回文的程序

> 原文:[https://www . geesforgeks . org/program-print-回文-给定-range/](https://www.geeksforgeeks.org/program-print-palindromes-given-range/)

给定一个数字范围，打印给定范围内的所有回文。例如，如果给定的范围是{10，115}，那么输出应该是{11，22，33，44，55，66，77，88，99，101，111}
我们可以运行一个从最小值到最大值的循环，并检查每个数字的回文。如果数字是回文，我们可以简单地打印出来。

## C++

```
#include<iostream>
using namespace std;

// A function to check if n is palindrome
int isPalindrome(int n)
{
    // Find reverse of n
    int rev = 0;
    for (int i = n; i > 0; i /= 10)
        rev = rev*10 + i%10;

    // If n and rev are same, then n is palindrome
    return (n==rev);
}

// prints palindrome between min and max
void countPal(int min, int max)
{
    for (int i = min; i <= max; i++)
        if (isPalindrome(i))
          cout << i << " ";
}

// Driver program to test above function
int main()
{
    countPal(100, 2000);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print all
// palindromes in a given range

class GFG
{

    // A function to check
    // if n is palindrome
    static int isPalindrome(int n)
    {

        // Find reverse of n
        int rev = 0;
        for (int i = n; i > 0; i /= 10)
            rev = rev * 10 + i % 10;

        // If n and rev are same,
        // then n is palindrome
        return(n == rev) ? 1 : 0;
    }

    // prints palindrome between
    // min and max
    static void countPal(int min, int max)
    {
        for (int i = min; i <= max; i++)
            if (isPalindrome(i)==1)
                System.out.print(i + " ");
    }

    // Driver Code
    public static void main(String args[])
    {
        countPal(100, 2000);
    }
}

// This code is contributed by Taritra Saha.
```

## 蟒蛇 3

```
# Python3 implementation of above idea

# A function to check if n is palindrome
def isPalindrome(n: int) -> bool:

    # Find reverse of n
    rev = 0
    i = n
    while i > 0:
        rev = rev * 10 + i % 10
        i //= 10

    # If n and rev are same,
    # then n is palindrome
    return (n == rev)

# prints palindrome between min and max
def countPal(minn: int, maxx: int) -> None:
    for i in range(minn, maxx + 1):
        if isPalindrome(i):
            print(i, end = " ")

# Driver Code
if __name__ == "__main__":
    countPal(100, 2000)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# Program to print all
// palindromes in a given range
using System;

class GFG
{

// A function to check
// if n is palindrome
public static int isPalindrome(int n)
{

    // Find reverse of n
    int rev = 0;
    for (int i = n; i > 0; i /= 10)
    {
        rev = rev * 10 + i % 10;
    }

    // If n and rev are same,
    // then n is palindrome
    return (n == rev) ? 1 : 0;
}

// prints palindrome between
// min and max
public static void countPal(int min,
                            int max)
{
    for (int i = min; i <= max; i++)
    {
        if (isPalindrome(i) == 1)
        {
            Console.Write(i + " ");
        }
    }
}

// Driver Code
public static void Main(string[] args)
{
    countPal(100, 2000);
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
// A function to check if n is palindrome
function isPalindrome(n)
{
    // Find reverse of n
    var rev = 0;
    for (var i = n; Math.trunc(i) > 0; i /= 10)
    {
        rev = ((rev*10) + (Math.trunc(i)%10));

        }

    // If n and rev are same, then n is palindrome
    return (n==rev);
}

// prints palindrome between min and max
function countPal(min,  max)
{
    for (var i = min; i <=max; i++)
    {
        if(isPalindrome(i))
        document.write(i+" " );
       }
}

// Driver program to test above function

    countPal(100, 2000);
</script>
```

**输出:**

```
101 111 121 131 141 151 161 171 181 191 202 212
222 232 242 252 262 272 282 292 303 313 323 333
343 353 363 373 383 393 404 414 424 434 444 454
464 474 484 494 505 515 525 535 545 555 565 575
585 595 606 616 626 636 646 656 666 676 686 696
707 717 727 737 747 757 767 777 787 797 808 818
828 838 848 858 868 878 888 898 909 919 929 939
949 959 969 979 989 999 1001 1111 1221 1331 1441
1551 1661 1771 1881 1991 
```

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息