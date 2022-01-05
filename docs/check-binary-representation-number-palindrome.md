# 检查一个数字的二进制表示是否是回文

> 原文:[https://www . geesforgeks . org/check-binary-表象-数字-回文/](https://www.geeksforgeeks.org/check-binary-representation-number-palindrome/)

给定一个整数“x”，写一个 C 函数，如果 x 的二进制表示是回文，则返回 true，否则返回 false。
例如二进制表示为 10 的数字..01 是回文和数字，二进制表示为 10..00 不是回文。
这个想法类似于[检查一个字符串是不是回文](http://geeksquiz.com/c-program-check-given-string-palindrome/)。我们从最左边和最右边的位开始，逐个比较位。如果发现不匹配，则返回 false。

**算法:**
ispalindome(x)
1)使用 sizeof()运算符查找 x 中的位数。
2)将左右位置分别初始化为 1 和 n。
3)当左“l”小于右“r”时，执行以下操作。
..…..a)如果“l”位置的位与“r”位置的位不同，则返回 false。
..…..b)递增‘l’和递减‘r’，即做 l++和 r –-。
4)如果我们到达这里，这意味着我们没有发现一个不匹配的位。
找到给定位置的位，可以用类似[这个](https://www.geeksforgeeks.org/how-to-turn-off-a-particular-bit-in-a-number/)帖子的思路。表达式“**x&(1<<(k-1))**”在从右数第 k 个位置的位被置位时给出非零值，在第 k 个位未被置位时给出零值。

下面是上述算法的实现。

## C++

```
// C++ Program to Check if binary representation
// of a number is palindrome
#include<iostream>
using namespace std;

// This function returns true if k'th bit in x
// is set (or 1). For example if x (0010) is 2
// and k is 2, then it returns true
bool isKthBitSet(unsigned int x, unsigned int k)
{
    return (x & (1 << (k - 1))) ? true : false;
}

// This function returns true if binary
// representation of x is palindrome.
// For example (1000...001) is palindrome
bool isPalindrome(unsigned int x)
{
    int l = 1; // Initialize left position
    int r = sizeof(unsigned int) * 8; // initialize right position

    // One by one compare bits
    while (l < r)
    {
        if (isKthBitSet(x, l) != isKthBitSet(x, r))
            return false;
        l++; r--;
    }
    return true;
}

// Driver Code
int main()
{
    unsigned int x = 1 << 15 + 1 << 16;
    cout << isPalindrome(x) << endl;
    x = 1 << 31 + 1;
    cout << isPalindrome(x) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to Check if binary representation
// of a number is palindrome
class GFG
{

    // This function returns true if k'th bit in x
    // is set (or 1). For example if x (0010) is 2
    // and k is 2, then it returns true
    static int isKthBitSet(long x, long k)
    {
        int rslt = ((x & (1 << (k - 1))) != 0) ? 1 : 0;
        return rslt;
    }

    // This function returns true if binary
    // representation of x is palindrome.
    // For example (1000...001) is palindrome
    static int isPalindrome( long x)
    {
        long l = 1; // Initialize left position
        long r = (Integer.SIZE/8 )* 8; // initialize right position

        // One by one compare bits
        while (l < r)
        {
            if (isKthBitSet(x, l) != isKthBitSet(x, r))
            {
                return 0;
            }
            l++; r--;
        }
        return 1;
    }

    // Driver Code
    public static void main (String[] args)
    {
        long x = 1 << 15 + 1 << 16 ;
        System.out.println(isPalindrome(x));

        x = (1 << 31) + 1 ;
        System.out.println(isPalindrome(x));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# python 3 Program to Check if binary representation
# of a number is palindrome
import sys
# This function returns true if k'th bit in x
# is set (or 1). For example if x (0010) is 2
# and k is 2, then it returns true
def isKthBitSet(x, k):
    if ((x & (1 << (k - 1))) !=0):
        return True
    else:
        return False

# This function returns true if binary
# representation of x is palindrome.
# For example (1000...001) is palindrome
def isPalindrome(x):
    l = 1 # Initialize left position
    r = 2 * 8 # initialize right position

    # One by one compare bits
    while (l < r):
        if (isKthBitSet(x, l) != isKthBitSet(x, r)):
            return False
        l += 1
        r -= 1

    return True

# Driver Code
if __name__ =='__main__':
    x = 1 << 15 + 1 << 16
    print(int(isPalindrome(x)))
    x = 1 << 31 + 1
    print(int(isPalindrome(x)))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# Program to Check if binary representation
// of a number is palindrome
using System;

class GFG
{

    // This function returns true if k'th bit in x
    // is set (or 1). For example if x (0010) is 2
    // and k is 2, then it returns true
    static int isKthBitSet(long x, long k)
    {
        int rslt = ((x & (1 << (int)(k - 1))) != 0) ? 1 : 0;
        return rslt;
    }

    // This function returns true if binary
    // representation of x is palindrome.
    // For example (1000...001) is palindrome
    static int isPalindrome( long x)
    {
        long l = 1; // Initialize left position
        long r = 4 * 8; // initialize right position

        // One by one compare bits
        while (l < r)
        {
            if (isKthBitSet(x, l) != isKthBitSet(x, r))
            {
                return 0;
            }
            l++; r--;
        }
        return 1;
    }

    // Driver Code
    public static void Main ()
    {
        long x = 1 << 15 + 1 << 16 ;
        Console.WriteLine(isPalindrome(x));

        x = (1 << 31) + 1 ;
        Console.WriteLine(isPalindrome(x));
    }
}

// This code is contributed by AnkitRai01
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to Check if binary representation
// of a number is palindrome

// This function returns true if k'th bit in x
// is set (or 1). For example if x (0010) is 2
// and k is 2, then it returns true
function isKthBitSet($x, $k)
{
    return ($x & (1 << ($k - 1))) ? true : false;
}

// This function returns true if binary
// representation of x is palindrome.
// For example (1000...001) is palindrome
function isPalindrome($x)
{
    $l = 1; // Initialize left position
    $r = sizeof(4) * 8; // initialize right position

    // One by one compare bits
    while ($l < $r)
    {
        if (isKthBitSet($x, $l) != isKthBitSet($x, $r))
            return false;
        $l++;
        $r--;
    }
    return true;
}

// Driver Code
$x = 1 << 15 + 1 << 16;
echo isPalindrome($x), "\n";
$x = 1 << 31 + 1;
echo isPalindrome($x), "\n";

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to Check if binary
// representation of a number is palindrome

// This function returns true if k'th bit in x
// is set (or 1). For example if x (0010) is 2
// and k is 2, then it returns true
function isKthBitSet(x, k)
{
    let rslt = ((x & (1 << (k - 1))) != 0) ? 1 : 0;
    return rslt;
}

// This function returns true if binary
// representation of x is palindrome.
// For example (1000...001) is palindrome
function isPalindrome(x)
{

    // Initialize left position
    let l = 1;

    // initialize right position
    let r = 4 * 8;

    // One by one compare bits
    while (l < r)
    {
        if (isKthBitSet(x, l) !=
            isKthBitSet(x, r))
        {
            return 0;
        }
        l++; r--;
    }
    return 1;
}

// Driver code
let x = 1 << 15 + 1 << 16;
document.write(isPalindrome(x) + "</br>");

x = (1 << 31) + 1;
document.write(isPalindrome(x));

// This code is contributed by divyesh072019

</script>
```

**输出:**

```
1
1
```

时间复杂度:0(x)

辅助空间:0(1)

本文由**绍拉布·古普塔**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。