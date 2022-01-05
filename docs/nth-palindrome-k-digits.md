# 第 N 个 K 位数回文

> 原文:[https://www.geeksforgeeks.org/nth-palindrome-k-digits/](https://www.geeksforgeeks.org/nth-palindrome-k-digits/)

给定两个整数 **n** 和 **k** ，求 k 位数字的字典序 n <sup>th</sup> 回文。
**举例:**

```
Input  : n = 5, k = 4
Output : 1441
Explanation:
4 digit lexicographical palindromes are:
1001, 1111, 1221, 1331, 1441
5th palindrome = 1441

Input  :  n = 4, k = 6
Output : 103301
```

**天真的方法**

蛮力就是从最小的 k <sup>第</sup>个数字开始循环，检查每个数字是不是回文。如果是回文数字，则递减 k 的值。因此循环运行，直到 k 耗尽。

## C++

```
// A naive approach of C++ program of finding nth
// palindrome of k digit
#include<bits/stdc++.h>
using namespace std;

// Utility function to reverse the number n
int reverseNum(int n)
{
    int rem, rev=0;
    while (n)
    {
        rem = n % 10;
        rev = rev * 10 + rem;
        n /= 10;
    }
    return rev;
}

// Boolean Function to check for palindromic
// number
bool isPalindrom(int num)
{
    return num == reverseNum(num);
}

// Function for finding nth palindrome of k digits
int nthPalindrome(int n,int k)
{
    // Get the smallest k digit number
    int num = (int)pow(10, k-1);

    while (true)
    {
        // check the number is palindrom or not
        if (isPalindrom(num))
            --n;

        // if n'th palindrome found break the loop
        if (!n)
            break;

        // Increment number for checking next palindrome
        ++num;
    }

    return num;
}

// Driver code
int main()
{
    int n = 6, k = 5;
    printf("%dth palindrome of %d digit = %d\n",
           n, k, nthPalindrome(n, k));

    n = 10, k = 6;
    printf("%dth palindrome of %d digit = %d",
           n, k, nthPalindrome(n, k));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A naive approach of Java program of finding nth
// palindrome of k digit
import java.util.*;

class GFG
{
// Utility function to reverse the number n
static int reverseNum(int n)
{
    int rem, rev = 0;
    while (n > 0)
    {
        rem = n % 10;
        rev = rev * 10 + rem;
        n /= 10;
    }
    return rev;
}

// Boolean Function to check for palindromic
// number
static boolean isPalindrom(int num)
{
    return num == reverseNum(num);
}

// Function for finding nth palindrome of k digits
static int nthPalindrome(int n, int k)
{
    // Get the smallest k digit number
    int num = (int)Math.pow(10, k-1);

    while (true)
    {
        // check the number is palindrom or not
        if (isPalindrom(num))
            --n;

        // if n'th palindrome found break the loop
        if (n == 0)
            break;

        // Increment number for checking next palindrome
        ++num;
    }

    return num;
}

// Driver code
public static void main(String[] args)
{
    int n = 6, k = 5;
    System.out.println(n + "th palindrome of " + k + " digit = " + nthPalindrome(n, k));

    n = 10; k = 6;
    System.out.println(n + "th palindrome of " + k + " digit = " + nthPalindrome(n, k));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# A naive approach of Python3 program
# of finding nth palindrome of k digit
import math;
# Utility function to
# reverse the number n
def reverseNum(n):
    rev = 0;
    while (n):
        rem = n % 10;
        rev = (rev * 10) + rem;
        n = int(n / 10);

    return rev;

# Boolean Function to check for
# palindromic number
def isPalindrom(num):
    return num == reverseNum(num);

# Function for finding nth
# palindrome of k digits
def nthPalindrome(n, k):
    # Get the smallest k digit number
    num = math.pow(10, k - 1);

    while (True):
        # check the number is
        # palindrom or not
        if (isPalindrom(num)):
            n-=1;

        # if n'th palindrome found
        # break the loop
        if (not n):
            break;

        # Increment number for checking
        # next palindrome
        num+=1;

    return int(num);

# Driver code
n = 6;
k = 5;
print(n,"th palindrome of",k,"digit =",nthPalindrome(n, k));

n = 10;
k = 6;
print(n,"th palindrome of",k,"digit =",nthPalindrome(n, k));

# This code is contributed by mits
```

## C#

```
// A naive approach of C# program of finding nth
// palindrome of k digit
using System;

class GFG
{
// Utility function to reverse the number n
static int reverseNum(int n)
{
    int rem, rev = 0;
    while (n > 0)
    {
        rem = n % 10;
        rev = rev * 10 + rem;
        n /= 10;
    }
    return rev;
}

// Boolean Function to check for palindromic
// number
static bool isPalindrom(int num)
{
    return num == reverseNum(num);
}

// Function for finding nth palindrome of k digits
static int nthPalindrome(int n, int k)
{
    // Get the smallest k digit number
    int num = (int)Math.Pow(10, k-1);

    while (true)
    {
        // check the number is palindrom or not
        if (isPalindrom(num))
            --n;

        // if n'th palindrome found break the loop
        if (n == 0)
            break;

        // Increment number for checking next palindrome
        ++num;
    }

    return num;
}

// Driver code
public static void Main()
{
    int n = 6, k = 5;
    Console.WriteLine(n + "th palindrome of " + k + " digit = " + nthPalindrome(n, k));

    n = 10; k = 6;
    Console.WriteLine(n + "th palindrome of " + k + " digit = " + nthPalindrome(n, k));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A naive approach of PHP program
// of finding nth palindrome of k digit

// Utility function to
// reverse the number n
function reverseNum($n)
{
    $rem;
    $rev = 0;
    while ($n)
    {
        $rem = $n % 10;
        $rev = ($rev * 10) + $rem;
        $n = (int)($n / 10);
    }
    return $rev;
}

// Boolean Function to check for
// palindromic number
function isPalindrom($num)
{
    return $num == reverseNum($num);
}

// Function for finding nth
// palindrome of k digits
function nthPalindrome($n, $k)
{
    // Get the smallest k digit number
    $num = pow(10, $k - 1);

    while (true)
    {
        // check the number is
        // palindrom or not
        if (isPalindrom($num))
            --$n;

        // if n'th palindrome found
        // break the loop
        if (!$n)
            break;

        // Increment number for checking
        // next palindrome
        ++$num;
    }

    return $num;
}

// Driver code
$n = 6;
$k = 5;
echo $n, "th palindrome of ", $k, " digit = ",
                  nthPalindrome($n, $k), "\n";

$n = 10;
$k = 6;
echo $n,"th palindrome of ", $k, " digit = ",
                 nthPalindrome($n, $k), "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // A naive approach of Javascript
    // program of finding nth
    // palindrome of k digit

    // Utility function to
    // reverse the number n
    function reverseNum(n)
    {
        let rem, rev = 0;
        while (n > 0)
        {
            rem = n % 10;
            rev = rev * 10 + rem;
            n = parseInt(n / 10);
        }
        return rev;
    }

    // Boolean Function to
    // check for palindromic
    // number
    function isPalindrom(num)
    {
        return num == reverseNum(num);
    }

    // Function for finding nth
    // palindrome of k digits
    function nthPalindrome(n, k)
    {
        // Get the smallest k digit number
        let num = Math.pow(10, k-1);

        while (true)
        {
            // check the number is
            // palindrom or not
            if (isPalindrom(num))
                --n;

            // if n'th palindrome found
            // break the loop
            if (n == 0)
                break;

            // Increment number for checking
            // next palindrome
            ++num;
        }

        return num;
    }

    let n = 6, k = 5;
    document.write(n + "th palindrome of " + k +
    " digit = " + nthPalindrome(n, k) + "</br>");

    n = 10; k = 6;
    document.write(n + "th palindrome of " + k +
    " digit = " + nthPalindrome(n, k));

</script>
```

**输出:**

```
6th palindrome of 5 digit = 10501
10th palindrome of 6 digit = 109901
```

**时间复杂度:**O(10<sup>k</sup>)
T5】辅助空间: O(1)

**高效方法**

一个有效的方法是寻找一个模式。首先根据回文的性质，半位数与其余半位数的顺序相反。因此，我们只需要寻找前半个数字，因为其余的数字很容易生成。让我们假设 k = 8，最小的回文总是从 1 开始作为前导数字，对于数字的前 4 位也是如此。

```
First half values for k = 8
1st: 1000
2nd: 1001
3rd: 1002
...
...
100th: 1099

So we can easily write the above sequence for nth
palindrome as: (n-1) + 1000
For k digit number, we can generalize above formula as:

If k is odd
=> num = (n-1) + 10k/2
else 
=> num = (n-1) + 10k/2 - 1 

Now rest half digits can be expanded by just 
printing the value of num in reverse order. 
But before this if k is odd then we have to truncate 
the last digit of a value num 
```

**插图:**
n = 6 k = 5

1.  确定前半位数=楼层(5/2) = 2
2.  使用公式:num = (6-1) + 10 <sup>2</sup> = 105
3.  通过反转 num 的值来展开剩余的半位数。
    最终答案为 10501

以下是上述步骤的实施

## C++

```
// C++ program of finding nth palindrome
// of k digit
#include<bits/stdc++.h>
using namespace std;

void nthPalindrome(int n, int k)
{
    // Determine the first half digits
    int temp = (k & 1) ? (k / 2) : (k/2 - 1);
    int palindrome = (int)pow(10, temp);
    palindrome += n - 1;

    // Print the first half digits of palindrome
    printf("%d", palindrome);

    // If k is odd, truncate the last digit
    if (k & 1)
        palindrome /= 10;

    // print the last half digits of palindrome
    while (palindrome)
    {
        printf("%d", palindrome % 10);
        palindrome /= 10;
    }
    printf("\n");
}

// Driver code
int main()
{
    int n = 6, k = 5;
    printf("%dth palindrome of %d digit = ",n ,k);
    nthPalindrome(n ,k);

    n = 10, k = 6;
    printf("%dth palindrome of %d digit = ",n ,k);
    nthPalindrome(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of finding nth palindrome
// of k digit

class GFG{
static void nthPalindrome(int n, int k)
{
    // Determine the first half digits
    int temp = (k & 1)!=0 ? (k / 2) : (k/2 - 1);
    int palindrome = (int)Math.pow(10, temp);
    palindrome += n - 1;

    // Print the first half digits of palindrome
    System.out.print(palindrome);

    // If k is odd, truncate the last digit
    if ((k & 1)>0)
        palindrome /= 10;

    // print the last half digits of palindrome
    while (palindrome>0)
    {
        System.out.print(palindrome % 10);
        palindrome /= 10;
    }
    System.out.println("");
}

// Driver code
public static void main(String[] args)
{
    int n = 6, k = 5;
    System.out.print(n+"th palindrome of "+k+" digit = ");
    nthPalindrome(n ,k);

    n = 10;
    k = 6;
    System.out.print(n+"th palindrome of "+k+" digit = ");
    nthPalindrome(n, k);

}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program of finding nth palindrome
# of k digit

def nthPalindrome(n, k):

    # Determine the first half digits
    if(k & 1):
        temp = k // 2
    else:
        temp = k // 2 - 1

    palindrome = 10**temp
    palindrome = palindrome + n - 1

    # Print the first half digits of palindrome
    print(palindrome, end="")

    # If k is odd, truncate the last digit
    if(k & 1):
        palindrome = palindrome // 10

    # print the last half digits of palindrome
    while(palindrome):
        print(palindrome % 10, end="")
        palindrome = palindrome // 10

# Driver code
if __name__=='__main__':
    n = 6
    k = 5
    print(n, "th palindrome of", k, " digit = ", end=" ")
    nthPalindrome(n, k)
    print()
    n = 10
    k = 6
    print(n, "th palindrome of", k, "digit = ",end=" ")
    nthPalindrome(n, k)

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program of finding nth palindrome
// of k digit
using System;

class GFG
{
static void nthPalindrome(int n, int k)
{
    // Determine the first half digits
    int temp = (k & 1) != 0 ? (k / 2) : (k / 2 - 1);
    int palindrome = (int)Math.Pow(10, temp);
    palindrome += n - 1;

    // Print the first half digits
    // of palindrome
    Console.Write(palindrome);

    // If k is odd, truncate the last digit
    if ((k & 1) > 0)
        palindrome /= 10;

    // print the last half digits
    // of palindrome
    while (palindrome>0)
    {
        Console.Write(palindrome % 10);
        palindrome /= 10;
    }
    Console.WriteLine("");
}

// Driver code
static public void Main ()
{
    int n = 6, k = 5;
    Console.Write(n+"th palindrome of " + k +
                                " digit = ");
    nthPalindrome(n, k);

    n = 10;
    k = 6;
    Console.Write(n+"th palindrome of " + k +
                                " digit = ");
    nthPalindrome(n, k);
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program of finding nth palindrome
// of k digit

function nthPalindrome($n, $k)
{
    // Determine the first half digits
    $temp = ($k & 1) ?
            (int)($k / 2) : (int)($k / 2 - 1);
    $palindrome = (int)pow(10, $temp);
    $palindrome += $n - 1;

    // Print the first half digits of palindrome
    print($palindrome);

    // If k is odd, truncate the last digit
    if ($k & 1)
        $palindrome = (int)($palindrome / 10);

    // print the last half digits of palindrome
    while ($palindrome > 0)
    {
        print($palindrome % 10);
        $palindrome = (int)($palindrome / 10);
    }
    print("\n");
}

// Driver code
$n = 6;
$k = 5;
print($n."th palindrome of $k digit = ");
nthPalindrome($n, $k);

$n = 10;
$k = 6;
print($n."th palindrome of $k digit = ");
nthPalindrome($n, $k);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
    // Javascript program of finding nth palindrome of k digit

    function nthPalindrome(n, k)
    {
        // Determine the first half digits
        let temp = (k & 1) != 0 ? parseInt(k / 2, 10) : (parseInt(k / 2, 10) - 1);
        let palindrome = parseInt(Math.pow(10, temp), 10);
        palindrome += n - 1;

        // Print the first half digits
        // of palindrome
        document.write(palindrome);

        // If k is odd, truncate the last digit
        if ((k & 1) > 0)
            palindrome = parseInt(palindrome / 10, 10);

        // print the last half digits
        // of palindrome
        while (palindrome>0)
        {
            document.write(palindrome % 10);
            palindrome = parseInt(palindrome / 10, 10);
        }
        document.write("" + "</br>");
    }

    let n = 6, k = 5;
    document.write(n+"th palindrome of " + k + " digit = ");
    nthPalindrome(n, k);

    n = 10;
    k = 6;
    document.write(n+"th palindrome of " + k + " digit = ");
    nthPalindrome(n, k);

</script>
```

**输出:**

```
6th palindrome of 5 digit = 10501
10th palindrome of 6 digit = 109901
```

**时间复杂度:** O(k)
**辅助空间:** O(1)
**参考:**
[http://stackoverflow . com/questions/11925840/如何高效计算第 n 位数字回文](http://stackoverflow.com/questions/11925840/how-to-calculate-nth-n-digit-palindrome-efficiently)
本文由 [Shubham Bansal](https://www.facebook.com/banalshubham) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。