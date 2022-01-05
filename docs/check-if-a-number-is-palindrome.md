# 检查一个数字是否是回文

> 原文:[https://www . geesforgeks . org/check-if-a-number-is-回文/](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome/)

给定一个整数，写一个函数，如果给定的数字是回文，则返回 true，否则返回 false。比如 12321 是回文，1451 不是回文。

![](img/c731721083c87a35c6b927c4946c4b6a.png)

让给定的数为*数*。这个问题的一个简单方法是先[倒*num*T5 的位数，然后比较 *num* 和 *num* 的倒位数。如果两者相同，则返回真，否则返回假。](https://www.geeksforgeeks.org/write-a-c-program-to-reverse-digits-of-a-number/)

以下是一个有趣的方法，灵感来自[这篇](https://www.geeksforgeeks.org/function-to-check-if-a-singly-linked-list-is-palindrome/)帖子的方法 2。想法是创建一个 *num* 的副本，并通过引用递归传递该副本，通过值传递 *num* 。在递归调用中，沿着递归树向下移动时，将*数*除以 10。在递归树上向上移动时，将副本除以 10。当他们在一个所有子调用都结束的函数中相遇时， *num* 的最后一个数字将从开始的第一个数字开始，副本的最后一个数字将从结束的第一个数字开始。

## C++

```
// A recursive C++ program to check
// whether a given number
// is palindrome or not
#include <iostream>
using namespace std;

// A function that returns true only
// if num contains one
// digit
int oneDigit(int num)
{

    // Comparison operation is faster
    // than division
    // operation. So using following
    // instead of "return num
    // / 10 == 0;"
    return (num >= 0 && num < 10);
}

// A recursive function to find
// out whether num is
// palindrome or not. Initially, dupNum
// contains address of
// a copy of num.
bool isPalUtil(int num, int* dupNum)
{

    // Base case (needed for recursion
    // termination): This
    // statement mainly compares the
    // first digit with the
    // last digit
    if (oneDigit(num))
        return (num == (*dupNum) % 10);

    // This is the key line in this
    // method. Note that all
    // recursive calls have a separate
    // copy of num, but they
    // all share same copy of *dupNum.
    // We divide num while
    // moving up the recursion tree
    if (!isPalUtil(num / 10, dupNum))
        return false;

    // The following statements are
    // executed when we move up
    // the recursion call tree
    *dupNum /= 10;

    // At this point, if num%10 contains
    // i'th digit from
    // beginning, then (*dupNum)%10
    // contains i'th digit
    // from end
    return (num % 10 == (*dupNum) % 10);
}

// The main function that uses
// recursive function
// isPalUtil() to find out whether
// num is palindrome or not
int isPal(int num)
{

    // Check if num is negative,
    // make it positive
    if (num < 0)
        num = -num;

    // Create a separate copy of num,
    // so that modifications
    // made to address dupNum don't
    // change the input number.
    // *dupNum = num
    int* dupNum = new int(num);

    return isPalUtil(num, dupNum);
}

// Driver program to test
// above functions
int main()
{
    int n = 12321;
    isPal(n) ? cout <<"Yes\n":  cout <<"No" << endl;

    n = 12;
    isPal(n) ? cout <<"Yes\n": cout <<"No" << endl;

    n = 88;
    isPal(n) ? cout <<"Yes\n": cout <<"No" << endl;

    n = 8999;
    isPal(n) ? cout <<"Yes\n": cout <<"No";
    return 0;
}

// this code is contributed by shivanisinghss2110
```

## C

```
// A recursive C program to check
// whether a given number
// is palindrome or not
#include <stdio.h>

// A function that returns true only
// if num contains one
// digit
int oneDigit(int num)
{

    // Comparison operation is faster
    // than division
    // operation. So using following
    // instead of "return num
    // / 10 == 0;"
    return (num >= 0 && num < 10);
}

// A recursive function to find
// out whether num is
// palindrome or not. Initially, dupNum
// contains address of
// a copy of num.
bool isPalUtil(int num, int* dupNum)
{

    // Base case (needed for recursion
    // termination): This
    // statement mainly compares the
    // first digit with the
    // last digit
    if (oneDigit(num))
        return (num == (*dupNum) % 10);

    // This is the key line in this
    // method. Note that all
    // recursive calls have a separate
    // copy of num, but they
    // all share same copy of *dupNum.
    // We divide num while
    // moving up the recursion tree
    if (!isPalUtil(num / 10, dupNum))
        return false;

    // The following statements are
    // executed when we move up
    // the recursion call tree
    *dupNum /= 10;

    // At this point, if num%10 contains
    // i'th digit from
    // beginning, then (*dupNum)%10
    // contains i'th digit
    // from end
    return (num % 10 == (*dupNum) % 10);
}

// The main function that uses
// recursive function
// isPalUtil() to find out whether
// num is palindrome or not
int isPal(int num)
{

    // Check if num is negative,
    // make it positive
    if (num < 0)
        num = -num;

    // Create a separate copy of num,
    // so that modifications
    // made to address dupNum don't
    // change the input number.
    // *dupNum = num
    int* dupNum = new int(num);

    return isPalUtil(num, dupNum);
}

// Driver program to test
// above functions
int main()
{
    int n = 12321;
    isPal(n) ? printf("Yes\n") : printf("No\n");

    n = 12;
    isPal(n) ? printf("Yes\n") : printf("No\n");

    n = 88;
    isPal(n) ? printf("Yes\n") : printf("No\n");

    n = 8999;
    isPal(n) ? printf("Yes\n") : printf("No\n");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A recursive Java program to
// check whether a given number
// is palindrome or not
import java.io.*;
import java.util.*;

public class CheckPallindromNumberRecursion {

    // A function that returns true
    // only if num contains one digit
    public static int oneDigit(int num) {

        if ((num >= 0) && (num < 10))
            return 1;
        else
            return 0;
    }

    public static int isPalUtil
    (int num, int dupNum) throws Exception {

        // base condition to return once we
        // move past first digit
        if (num == 0) {
            return dupNum;
        } else {
            dupNum = isPalUtil(num / 10, dupNum);
        }

        // Check for equality of first digit of
        // num and dupNum
        if (num % 10 == dupNum % 10) {
            // if first digit values of num and
            // dupNum are equal divide dupNum
            // value by 10 to keep moving in sync
            // with num.
            return dupNum / 10;
        } else {
            // At position values are not
            // matching throw exception and exit.
            // no need to proceed further.
            throw new Exception();
        }

    }

    public static int isPal(int num)
    throws Exception {

        if (num < 0)
            num = (-num);

        int dupNum = (num);

        return isPalUtil(num, dupNum);
    }

    public static void main(String args[]) {

        int n = 1242;
        try {
            isPal(n);
            System.out.println("Yes");
        } catch (Exception e) {
            System.out.println("No");
        }
        n = 1231;
        try {
            isPal(n);
            System.out.println("Yes");
        } catch (Exception e) {
            System.out.println("No");
        }

        n = 12;
        try {
            isPal(n);
            System.out.println("Yes");
        } catch (Exception e) {
            System.out.println("No");
        }

        n = 88;
        try {
            isPal(n);
            System.out.println("Yes");
        } catch (Exception e) {
            System.out.println("No");
        }

        n = 8999;
        try {
            isPal(n);
            System.out.println("Yes");
        } catch (Exception e) {
            System.out.println("No");
        }
    }
}

// This code is contributed
// by Nasir J
```

## 蟒蛇 3

```
# A recursive Pyhton3 program to check
# whether a given number is palindrome or not

# A function that returns true
# only if num contains one digit
def oneDigit(num):

    # comparison operation is faster
    # than division operation. So
    # using following instead of
    # "return num / 10 == 0;"
    return ((num >= 0) and
            (num < 10))

# A recursive function to find
# out whether num is palindrome
# or not. Initially, dupNum
# contains address of a copy of num.
def isPalUtil(num, dupNum):

    # Base case (needed for recursion
    # termination): This statement
    # mainly compares the first digit
    # with the last digit
    if oneDigit(num):
        return (num == (dupNum[0]) % 10)

    # This is the key line in this
    # method. Note that all recursive
    # calls have a separate copy of
    # num, but they all share same
    # copy of *dupNum. We divide num
    # while moving up the recursion tree
    if not isPalUtil(num //10, dupNum):
        return False

    # The following statements are
    # executed when we move up the
    # recursion call tree
    dupNum[0] = dupNum[0] //10

    # At this point, if num%10
    # contains i'th digit from
    # beginning, then (*dupNum)%10
    # contains i'th digit from end
    return (num % 10 == (dupNum[0]) % 10)

# The main function that uses
# recursive function isPalUtil()
# to find out whether num is
# palindrome or not
def isPal(num):
    # If num is negative,
    # make it positive
    if (num < 0):
        num = (-num)

    # Create a separate copy of
    # num, so that modifications
    # made to address dupNum
    # don't change the input number.
    dupNum = [num] # *dupNum = num

    return isPalUtil(num, dupNum)

# Driver Code
n = 12321
if isPal(n):
    print("Yes")
else:
    print("No")

n = 12
if isPal(n) :
    print("Yes")
else:
    print("No")

n = 88
if isPal(n) :
    print("Yes")
else:
    print("No")

n = 8999
if isPal(n) :
    print("Yes")
else:
    print("No")

# This code is contributed by mits
```

## C#

```
// A recursive C# program to
// check whether a given number
// is palindrome or not
using System;

class GFG
{

// A function that returns true
// only if num contains one digit
public static int oneDigit(int num)
{
    // comparison operation is
    // faster than division
    // operation. So using
    // following instead of
    // "return num / 10 == 0;"
    if((num >= 0) &&(num < 10))
    return 1;
    else
    return 0;
}

// A recursive function to
// find out whether num is
// palindrome or not.
// Initially, dupNum contains
// address of a copy of num.
public static int isPalUtil(int num,
                            int dupNum)
{
    // Base case (needed for recursion
    // termination): This statement
    // mainly compares the first digit
    // with the last digit
    if (oneDigit(num) == 1)
        if(num == (dupNum) % 10)
        return 1;
        else
        return 0;

    // This is the key line in
    // this method. Note that
    // all recursive calls have
    // a separate copy of num,
    // but they all share same
    // copy of *dupNum. We divide
    // num while moving up the
    // recursion tree
    if (isPalUtil((int)(num / 10), dupNum) == 0)
        return -1;

    // The following statements
    // are executed when we move
    // up the recursion call tree
    dupNum = (int)(dupNum / 10);

    // At this point, if num%10
    // contains i'th digit from
    // beginning, then (*dupNum)%10
    // contains i'th digit from end
    if(num % 10 == (dupNum) % 10)
        return 1;
    else
        return 0;
}

// The main function that uses
// recursive function isPalUtil()
// to find out whether num is
// palindrome or not
public static int isPal(int num)
{
    // If num is negative,
    // make it positive
    if (num < 0)
    num = (-num);

    // Create a separate copy
    // of num, so that modifications
    // made to address dupNum
    // don't change the input number.
    int dupNum = (num); // *dupNum = num

    return isPalUtil(num, dupNum);
}

// Driver Code
public static void Main()
{
int n = 12321;
if(isPal(n) == 0)
    Console.WriteLine("Yes");
else
    Console.WriteLine("No");

n = 12;
if(isPal(n) == 0)
    Console.WriteLine("Yes");
else
    Console.WriteLine( "No");

n = 88;
if(isPal(n) == 1)
    Console.WriteLine("Yes");
else
    Console.WriteLine("No");

n = 8999;
if(isPal(n) == 0)
    Console.WriteLine("Yes");
else
    Console.WriteLine("No");
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A recursive PHP program to
// check whether a given number
// is palindrome or not

// A function that returns true
// only if num contains one digit
function oneDigit($num)
{
    // comparison operation is faster
    // than division operation. So
    // using following instead of
    // "return num / 10 == 0;"
    return (($num >= 0) &&
            ($num < 10));
}

// A recursive function to find
// out whether num is palindrome
// or not. Initially, dupNum
// contains address of a copy of num.
function isPalUtil($num, $dupNum)
{
    // Base case (needed for recursion
    // termination): This statement
    // mainly compares the first digit
    // with the last digit
    if (oneDigit($num))
        return ($num == ($dupNum) % 10);

    // This is the key line in this
    // method. Note that all recursive
    // calls have a separate copy of
    // num, but they all share same
    // copy of *dupNum. We divide num
    // while moving up the recursion tree
    if (!isPalUtil((int)($num / 10),
                         $dupNum))
        return -1;

    // The following statements are
    // executed when we move up the
    // recursion call tree
    $dupNum = (int)($dupNum / 10);

    // At this point, if num%10 
    // contains i'th digit from
    // beginning, then (*dupNum)%10
    // contains i'th digit from end
    return ($num % 10 == ($dupNum) % 10);
}

// The main function that uses
// recursive function isPalUtil()
// to find out whether num is
// palindrome or not
function isPal($num)
{
    // If num is negative,
    // make it positive
    if ($num < 0)
    $num = (-$num);

    // Create a separate copy of
    // num, so that modifications
    // made to address dupNum
    // don't change the input number.
    $dupNum = ($num); // *dupNum = num

    return isPalUtil($num, $dupNum);
}

// Driver Code
$n = 12321;
if(isPal($n) == 0)
    echo "Yes\n";
else
    echo "No\n";

$n = 12;
if(isPal($n) == 0)
    echo "Yes\n";
else
    echo "No\n";

$n = 88;
if(isPal($n) == 1)
    echo "Yes\n";
else
    echo "No\n";

$n = 8999;
if(isPal($n) == 0)
    echo "Yes\n";
else
    echo "No\n";

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>
// A recursive javascript program to
// check whether a given number
// is palindrome or not

    // A function that returns true
    // only if num contains one digit
    function oneDigit(num) {

        if ((num >= 0) && (num < 10))
            return 1;
        else
            return 0;
    }

    function isPalUtil
    (num , dupNum) {

        // base condition to return once we
        // move past first digit
        if (num == 0) {
            return dupNum;
        } else {
            dupNum = isPalUtil(parseInt(num / 10), dupNum);
        }

        // Check for equality of first digit of
        // num and dupNum
        if (num % 10 == dupNum % 10) {
            // if first digit values of num and
            // dupNum are equal divide dupNum
            // value by 10 to keep moving in sync
            // with num.
            return parseInt(dupNum / 10);
        } else {
            // At position values are not
            // matching throw exception and exit.
            // no need to proceed further.
            throw e;
        }

    }

    function isPal(num)
    {

        if (num < 0)
            num = (-num);

        var dupNum = (num);

        return isPalUtil(num, dupNum);
    }

    var n = 1242;
    try {
        isPal(n);
        document.write("<br>Yes");
    } catch (e) {
        document.write("<br>No");
    }
    n = 1231;
    try {
        isPal(n);
        document.write("<br>Yes");
    } catch (e) {
        document.write("<br>No");
        }

        n = 12;
        try {
            isPal(n);
            document.write("<br>Yes");
    } catch (e) {
        document.write("<br>No");
        }

        n = 88;
        try {
            isPal(n);
            document.write("<br>Yes");
    } catch (e) {
        document.write("<br>No");
        }

        n = 8999;
        try {
            isPal(n);
            document.write("<br>Yes");
    } catch (e) {
        document.write("<br>No");
    }

// This code is contributed by Amit Katiyar
</script>
```

**输出:**

```
Yes
No
Yes
No 
```

[不使用任何多余的空格来检查一个数字是不是回文](https://www.geeksforgeeks.org/check-number-palindrome-not-without-using-extra-space/)
**方法 2:使用 string()方法**

1.  当那个数的位数超过 10 <sup>18</sup> 时，由于 long long int 的范围不满足给定的数，所以我们不能把那个数当作整数。
2.  所以把输入当成一个字符串，从开始到长度/2 运行一个循环，检查字符串的第一个字符(数字)到最后一个字符，第二个到第二个最后一个字符，以此类推。如果任何字符不匹配，字符串就不是回文。

下面是上述方法的实现

## C++14

```
// C++ implementation of the above approach
#include <iostream>
using namespace std;

// Function to check palindrome
int checkPalindrome(string str)
{
    // Calculating string length
    int len = str.length();

    // Traversing through the string
    // upto half its length
    for (int i = 0; i < len / 2; i++) {

        // Comparing i th character
        // from starting and len-i
        // th character from end
        if (str[i] != str[len - i - 1])
            return false;
    }

    // If the above loop doesn't return then it is
    // palindrome
    return true;
}

// Driver Code
int main()
{ // taking number as string
    string st
        = "112233445566778899000000998877665544332211";
    if (checkPalindrome(st) == true)
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
// this code is written by vikkycirus
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;

class GFG{

// Function to check palindrome
static boolean checkPalindrome(String str)
{

    // Calculating string length
    int len = str.length();

    // Traversing through the string
    // upto half its length
    for(int i = 0; i < len / 2; i++)
    {

        // Comparing i th character
        // from starting and len-i
        // th character from end
        if (str.charAt(i) !=
            str.charAt(len - i - 1))
            return false;
    }

    // If the above loop doesn't return then
    // it is palindrome
    return true;
}

// Driver Code
public static void main(String[] args)
{

    // Taking number as string
    String st = "112233445566778899000000998877665544332211";

    if (checkPalindrome(st) == true)
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by subhammahato348
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# function to check palindrome
def checkPalindrome(str):

    # Run loop from 0 to len/2
    for i in range(0, len(str)//2):
        if str[i] != str[len(str)-i-1]:
            return False

    # If the above loop doesn't
    #return then it is palindrome
    return True

# Driver code
st = "112233445566778899000000998877665544332211"
if(checkPalindrome(st) == True):
    print("it is a palindrome")
else:
    print("It is not a palindrome")
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function to check palindrome
static bool checkPalindrome(string str)
{

    // Calculating string length
    int len = str.Length;

    // Traversing through the string
    // upto half its length
    for(int i = 0; i < len / 2; i++)
    {

        // Comparing i th character
        // from starting and len-i
        // th character from end
        if (str[i] != str[len - i - 1])
            return false;
    }

    // If the above loop doesn't return then
    // it is palindrome
    return true;
}

// Driver Code
public static void Main()
{

    // Taking number as string
    string st = "112233445566778899000000998877665544332211";

    if (checkPalindrome(st) == true)
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by subhammahato348
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to check palindrome
function checkPalindrome(str)
{
    // Calculating string length
    var len = str.length;

    // Traversing through the string
    // upto half its length
    for (var i = 0; i < len / 2; i++) {

        // Comparing ith character
        // from starting and len-ith
        // character from end
        if (str[i] != str[len - i - 1])
            return false;
    }

    // If the above loop doesn't return then it is
    // palindrome
    return true;
}

// Driver Code
 // taking number as string
    let st
        = "112233445566778899000000998877665544332211";
    if (checkPalindrome(st) == true)
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by Mayank Tyagi

</script>
```

**Output**

```
Yes
```

***时间复杂度:** O(|str|)*

本文由[aashis Barnwal](https://www.facebook.com/barnwal.aashish?fref=ts)编辑。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。