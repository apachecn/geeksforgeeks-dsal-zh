# 检查一个数字的实际二进制表示是否是回文

> 原文:[https://www . geesforgeks . org/check-actual-binary-表象-数字-回文/](https://www.geeksforgeeks.org/check-actual-binary-representation-number-palindrome/)

给定一个非负整数 **n** 。问题是检查 **n** 的二进制表示是否回文。请注意，数字的实际二进制表示被考虑用于回文检查，不考虑前导 0。
**例:**

```
Input : 9
Output : Yes
(9)10 = (1001)2

Input : 10
Output : No
(10)10 = (1010)2
```

**进场:**以下为步骤:

1.  得到 **n** 二进制表示中的反位得到的数。参考[这篇](https://www.geeksforgeeks.org/reverse-actual-bits-given-number/)帖子。也罢**启**。
2.  如果 n == rev，则打印“是”或“否”。

## C++

```
// C++ implementation to check whether binary
// representation of a number is palindrome or not
#include <bits/stdc++.h>
using namespace std;

// function to reverse bits of a number
unsigned int reverseBits(unsigned int n)
{
    unsigned int rev = 0;

    // traversing bits of 'n' from the right
    while (n > 0) {

        // bitwise left shift 'rev' by 1
        rev <<= 1;

        // if current bit is '1'
        if (n & 1 == 1)
            rev ^= 1;

        // bitwise right shift 'n' by 1
        n >>= 1;
    }

    // required number
    return rev;
}

// function to check whether binary representation
// of a number is palindrome or not
bool isPalindrome(unsigned int n)
{
    // get the number by reversing bits in the
    // binary representation of 'n'
    unsigned int rev = reverseBits(n);

    return (n == rev);
}

// Driver program to test above
int main()
{
    unsigned int n = 9;
    if (isPalindrome(n))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code  to check whether 
// binary representation of a
// number is palindrome or not
import java.util.*;
import java.lang.*;

public class GfG
{
    // function to reverse bits of a number
    public static long reverseBits(long n)
    {
        long rev = 0;

        // traversing bits of 'n'
        // from the right
        while (n > 0)
        {
            // bitwise left shift 'rev' by 1
            rev <<= 1;

            // if current bit is '1'
            if ((n & 1) == 1)
                rev ^= 1;

            // bitwise right shift 'n' by 1
            n >>= 1;
        }

        // required number
        return rev;
    }

    // function to check a number
    // is palindrome or not
    public static boolean isPalindrome(long n)
    {
        // get the number by reversing
        // bits in the  binary
        // representation of 'n'
        long rev = reverseBits(n);

        return (n == rev);
    }

    // Driver function
    public static void main(String argc[])
    {
        long n = 9;
        if (isPalindrome(n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }

}

// This code is contributed by Sagar Shukla
```

## 蟒蛇 3

```
# Python 3 implementation to check
# whether binary representation of
# a number is palindrome or not

# function to reverse bits of a number
def reverseBits(n) :
    rev = 0

  # traversing bits of 'n' from the right
  while (n > 0) :

     # bitwise left shift 'rev' by 1
     rev = rev << 1

     # if current bit is '1'
     if (n & 1 == 1) :
     rev = rev ^ 1

     # bitwise right shift 'n' by 1
     n = n >> 1

     # required number
     return rev

# function to check whether binary
# representation of a number is
# palindrome or not
def isPalindrome(n) :

    # get the number by reversing
    # bits in the binary
    # representation of 'n'
    rev = reverseBits(n)

    return (n == rev)

# Driver program to test above
n = 9
if (isPalindrome(n)) :
    print("Yes")
else :
    print("No")

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# code to check whether
// binary representation of a
// number is palindrome or not
using System;

public class GfG
{
    // function to reverse bits of a number
    public static long reverseBits(long n)
    {
        long rev = 0;

        // traversing bits of 'n'
        // from the right
        while (n > 0)
        {
            // bitwise left shift 'rev' by 1
            rev <<= 1;

            // if current bit is '1'
            if ((n & 1) == 1)
                rev ^= 1;

            // bitwise right shift 'n' by 1
            n >>= 1;
        }

        // required number
        return rev;
    }

    // function to check a number
    // is palindrome or not
    public static bool isPalindrome(long n)
    {
        // get the number by reversing
        // bits in the binary
        // representation of 'n'
        long rev = reverseBits(n);

        return (n == rev);
    }

    // Driver function
    public static void Main()
    {
        long n = 9;
        if (isPalindrome(n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }

}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to check
// whether binary representation
// of a number is palindrome or not

// function to reverse bits of a number
function reverseBits($n)
{
    $rev = 0;

    // traversing bits of 'n'
    // from the right
    while ($n > 0)
    {

        // bitwise left shift 'rev' by 1
        $rev <<= 1;

        // if current bit is '1'
        if ($n & 1 == 1)
            $rev ^= 1;

        // bitwise right shift 'n' by 1
        $n >>= 1;
    }

    // required number
    return $rev;
}

// function to check whether
// binary representation of a
// number is palindrome or not
function isPalindrome($n)
{
    // get the number by reversing
    // bits in the binary representation
    // of 'n'
    $rev = reverseBits($n);

    return ($n == $rev);
}

// Driver code
$n = 9;
if (isPalindrome($n))
    echo "Yes";
else
    echo "No";
return 0;

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program  to check whether 
// binary representation of a
// number is palindrome or not

    // function to reverse bits of a number
    function reverseBits(n)
    {
        let rev = 0;

        // traversing bits of 'n'
        // from the right
        while (n > 0)
        {
            // bitwise left shift 'rev' by 1
            rev <<= 1;

            // if current bit is '1'
            if ((n & 1) == 1)
                rev ^= 1;

            // bitwise right shift 'n' by 1
            n >>= 1;
        }

        // required number
        return rev;
    }

    // function to check a number
    // is palindrome or not
    function isPalindrome(n)
    {
        // get the number by reversing
        // bits in the  binary
        // representation of 'n'
        let rev = reverseBits(n);

        return (n == rev);
    }

// Driver code

        let n = 9;
        if (isPalindrome(n))
            document.write("Yes");
        else
            document.write("No");

</script>
```

**输出:**

```
Yes
```

时间复杂度:O(num)，其中 **num** 是 **n** 二进制表示中的位数。