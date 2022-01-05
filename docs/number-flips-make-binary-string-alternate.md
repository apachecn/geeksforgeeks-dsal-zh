# 使二进制字符串交替的翻转次数|设置 1

> 原文:[https://www . geesforgeks . org/number-flips-make-binary-string-alternate/](https://www.geeksforgeeks.org/number-flips-make-binary-string-alternate/)

给定一个二进制字符串，即它只包含 0 和 1。我们需要通过翻转一些位来使这个字符串成为交替字符的序列，我们的目标是最小化要翻转的位数。
**例:**

```
Input : str = “001”
Output : 1
Minimum number of flips required = 1
We can flip 1st bit from 0 to 1 

Input : str = “0001010111”
Output : 2
Minimum number of flips required = 2
We can flip 2nd bit from 0 to 1 and 9th 
bit from 1 to 0 to make alternate 
string “0101010101”.
```

预期时间复杂度:O(n)，其中 n 是输入字符串的长度。

我们可以通过考虑所有可能的结果来解决这个问题，因为我们应该得到备用字符串，只有两种可能性，备用字符串从 0 开始，备用字符串从 1 开始。我们将尝试这两种情况，并选择需要最小翻转次数的字符串作为最终答案。
尝试一个案例需要 O(n)个时间，在这个时间里我们将循环给定字符串的所有字符，如果当前字符是交替出现的预期字符，那么我们将什么也不做，否则我们将翻转计数增加 1。在尝试从 0 开始和从 1 开始的字符串后，我们将选择翻转次数最少的字符串。
解的总时间复杂度为 0(n)

## C++

```
// C/C++ program to find minimum number of
// flip to make binary string alternate
#include <bits/stdc++.h>
using namespace std;

//  Utility method to flip a character
char flip(char ch)
{
    return (ch == '0') ? '1' : '0';
}

//  Utility method to get minimum flips when
//  alternate string starts with expected char
int getFlipWithStartingCharcter(string str,
                                char expected)
{
    int flipCount = 0;
    for (int i = 0; i < str.length(); i++)
    {
        //  if current character is not expected,
        // increase flip count
        if (str[i] != expected)
            flipCount++;

        //  flip expected character each time
        expected = flip(expected);
    }
    return flipCount;
}

// method return minimum flip to make binary
// string alternate
int minFlipToMakeStringAlternate(string str)
{
    //  return minimum of following two
    //  1) flips when alternate string starts with 0
    //  2) flips when alternate string starts with 1
    return min(getFlipWithStartingCharcter(str, '0'),
               getFlipWithStartingCharcter(str, '1'));
}

//  Driver code to test above method
int main()
{
    string str = "0001010111";
    cout << minFlipToMakeStringAlternate(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number of
// flip to make binary string alternate
class GFG
{
    //  Utility method to flip a character
    public static char flip(char ch)
    {
        return (ch == '0') ? '1' : '0';
    }

    //  Utility method to get minimum flips when
    //  alternate string starts with expected char
    public static int getFlipWithStartingCharcter(String str,
                                    char expected)
    {
        int flipCount = 0;
        for (int i = 0; i < str.length(); i++)
        {
            //  if current character is not expected,
            // increase flip count
            if (str.charAt(i) != expected)
                flipCount++;

            //  flip expected character each time
            expected = flip(expected);
        }
        return flipCount;
    }

    // method return minimum flip to make binary
    // string alternate
    public static int minFlipToMakeStringAlternate(String str)
    {
        //  return minimum of following two
        //  1) flips when alternate string starts with 0
        //  2) flips when alternate string starts with 1
        return Math.min(getFlipWithStartingCharcter(str, '0'),
                   getFlipWithStartingCharcter(str, '1'));
    }

    //  Driver code to test above method
    public static void main(String args[])
    {
        String str = "0001010111";
        System.out.println(minFlipToMakeStringAlternate(str));
    }
}

// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python 3 program to find minimum number of
# flip to make binary string alternate

# Utility method to flip a character
def flip( ch):
    return '1' if (ch == '0') else '0'

# Utility method to get minimum flips when
# alternate string starts with expected char
def getFlipWithStartingCharcter(str, expected):

    flipCount = 0
    for i in range(len( str)):

        # if current character is not expected,
        # increase flip count
        if (str[i] != expected):
            flipCount += 1

        # flip expected character each time
        expected = flip(expected)
    return flipCount

# method return minimum flip to make binary
# string alternate
def minFlipToMakeStringAlternate(str):

    # return minimum of following two
    # 1) flips when alternate string starts with 0
    # 2) flips when alternate string starts with 1
    return min(getFlipWithStartingCharcter(str, '0'),
            getFlipWithStartingCharcter(str, '1'))

# Driver code to test above method
if __name__ == "__main__":

    str = "0001010111"
    print(minFlipToMakeStringAlternate(str))
```

## C#

```
// C# program to find minimum number of
// flip to make binary string alternate
using System;

class GFG
{
    // Utility method to
    // flip a character
    public static char flip(char ch)
    {
        return (ch == '0') ? '1' : '0';
    }

    // Utility method to get minimum flips
    // when alternate string starts with
    // expected char
    public static int getFlipWithStartingCharcter(String str,
                                                char expected)
    {
        int flipCount = 0;
        for (int i = 0; i < str.Length; i++)
        {
            // if current character is not
            // expected, increase flip count
            if (str[i] != expected)
                flipCount++;

            // flip expected character each time
            expected = flip(expected);
        }
        return flipCount;
    }

    // method return minimum flip to
    // make binary string alternate
    public static int minFlipToMakeStringAlternate(string str)
    {
        // return minimum of following two
        // 1) flips when alternate string starts with 0
        // 2) flips when alternate string starts with 1
        return Math.Min(getFlipWithStartingCharcter(str, '0'),
                getFlipWithStartingCharcter(str, '1'));
    }

    // Driver Code
    public static void Main()
    {
        string str = "0001010111";
        Console.Write(minFlipToMakeStringAlternate(str));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum number of
// flip to make binary string alternate

// Utility method to flip a character
function flip( $ch)
{
    return ($ch == '0') ? '1' : '0';
}

// Utility method to get minimum flips when
// alternate string starts with expected char
function getFlipWithStartingCharcter($str,
                                $expected)
{

    $flipCount = 0;
    for ($i = 0; $i < strlen($str); $i++)
    {

        // if current character is not expected,
        // increase flip count
        if ($str[$i] != $expected)
            $flipCount++;

        // flip expected character each time
        $expected = flip($expected);
    }
    return $flipCount;
}

// method return minimum flip to make binary
// string alternate
function minFlipToMakeStringAlternate( $str)
{

    // return minimum of following two
    // 1) flips when alternate string starts with 0
    // 2) flips when alternate string starts with 1
    return min(getFlipWithStartingCharcter($str, '0'),
               getFlipWithStartingCharcter($str, '1'));
}

// Driver code to test above method
$str = "0001010111";
echo minFlipToMakeStringAlternate($str);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum number of
// flip to make binary string alternate

    //  Utility method to flip a character
    function flip(ch)
    {
        return (ch == '0') ? '1' : '0';
    }

    //  Utility method to get minimum flips when
    //  alternate string starts with expected char
    function getFlipWithStartingCharcter(str,expected)
    {
        let flipCount = 0;
        for (let i = 0; i < str.length; i++)
        {
            //  if current character is not expected,
            // increase flip count
            if (str.charAt(i) != expected)
                flipCount++;

            //  flip expected character each time
            expected = flip(expected);
        }
        return flipCount;
    }

    // method return minimum flip to make binary
    // string alternate
    function minFlipToMakeStringAlternate(str)
    {
         //  return minimum of following two
        //  1) flips when alternate string starts with 0
        //  2) flips when alternate string starts with 1
        return Math.min(getFlipWithStartingCharcter(str, '0'),
                   getFlipWithStartingCharcter(str, '1'));
    }

    //  Driver code to test above method
    let str = "0001010111";
    document.write(minFlipToMakeStringAlternate(str));

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
2
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)
[**使二进制字符串交替的最小替换次数|集合 2**](https://www.geeksforgeeks.org/minimum-number-of-replacements-to-make-the-binary-string-alternating-set-2/)

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。