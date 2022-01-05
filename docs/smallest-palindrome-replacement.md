# 替换后最小回文

> 原文:[https://www . geesforgeks . org/minist-回文-替换/](https://www.geeksforgeeks.org/smallest-palindrome-replacement/)

给定一个包含一些小写字母字符和一个特殊字符点(。).我们需要用一些字母字符替换所有的点，这样得到的字符串就变成了回文，如果有很多可能的替换，我们需要选择字典上最小的回文字符串。如果不可能在所有可能的替换后将字符串转换为回文，则输出不可能。
**例:**

```
Input : str = “ab..e.c.a”
Output : abcaeacba
The smallest palindrome which can be made 
after replacement is "abcaeacba"
We replaced first dot with "c", second dot with
"a", third dot with "a" and fourth dot with "b"

Input  : str = “ab..e.c.b”
Output : Not Possible 
It is not possible to convert above string into
palindrome
```

我们可以这样解决这个问题，由于结果字符串需要回文，我们可以检查开始本身的非点字符对，如果它们不匹配，那么直接返回是不可能的，因为我们只能将新字符放在点的位置，而不能放在其他任何地方。
之后，我们对字符串的字符进行迭代，如果当前字符是点，那么我们检查它的配对字符(第(n–I-1)位的字符)，如果该字符也是点，那么我们可以用“a”替换这两个字符，因为“a”是最小的小写字母，这将保证末尾的字典顺序字符串最小，用任何其他字符替换这两个字符将导致字典顺序上更大的回文字符串。在其他情况下，如果配对字符不是点，那么要使字符串回文，我们必须用它的配对字符替换当前字符。

```
So in short,
If both "i", and "n- i- 1" are dot, replace them by ‘a’
If one of them is a dot character replace that by other non-dot character
```

上面的过程给了我们字典上最小的回文串。

## C++

```
// C++ program to get lexicographically smallest
// palindrome string
#include <bits/stdc++.h>
using namespace std;

// Utility method to check str is possible palindrome
// after ignoring .
bool isPossiblePalindrome(string str)
{
    int n = str.length();
    for (int i=0; i<n/2; i++)
    {
        /* If both left and right character are not
           dot and they are not equal also, then it
           is not possible to make this string a
           palindrome   */
        if (str[i] != '.' &&
            str[n-i-1] != '.' &&
            str[i] != str[n-i-1])
            return false;
    }

    return true;
}

// Returns lexicographically smallest palindrom
// string, if possible
string smallestPalindrome(string str)
{
    if (!isPossiblePalindrome(str))
        return "Not Possible";

    int n = str.length();

    //  loop through character of string
    for (int i = 0; i < n; i++)
    {
        if (str[i] == '.')
        {
            // if one of character is dot, replace dot
            // with other character
            if (str[n - i - 1] != '.')
                str[i] = str[n - i - 1];

            // if both character are dot, then replace
            // them with smallest character 'a'
            else
                str[i] = str[n - i - 1] = 'a';
        }
    }

    //  return the result
    return str;
}

//  Driver code to test above methods
int main()
{
    string str = "ab..e.c.a";
    cout << smallestPalindrome(str) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get lexicographically
// smallest palindrome string
class GFG
{
// Utility method to check str is
// possible palindrome after ignoring
static boolean isPossiblePalindrome(char str[])
{
int n = str.length;
for (int i = 0; i < n / 2; i++)
{
    /* If both left and right character
        are not dot and they are not
        equal also, then it is not
        possible to make this string a
        palindrome */
    if (str[i] != '.' &&
        str[n - i - 1] != '.' &&
        str[i] != str[n - i - 1])
        return false;
}

return true;
}

// Returns lexicographically smallest
// palindrome string, if possible
static void smallestPalindrome(char str[])
{
if (!isPossiblePalindrome(str))
    System.out.println("Not Possible");

int n = str.length;

// loop through character of string
for (int i = 0; i < n; i++)
{
    if (str[i] == '.')
    {
        // if one of character is dot,
        // replace dot with other character
        if (str[n - i - 1] != '.')
            str[i] = str[n - i - 1];

        // if both character are dot,
        // then replace them with
        // smallest character 'a'
        else
            str[i] = str[n - i - 1] = 'a';
    }
}

// return the result
for(int i = 0; i < n; i++)
    System.out.print(str[i] + "");
}

// Driver code
public static void main(String[] args)
{
    String str = "ab..e.c.a";
    char[] s = str.toCharArray();
    smallestPalindrome(s);
}
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python 3 program to get lexicographically
# smallest palindrome string

# Utility method to check str is
# possible palindrome after ignoring
def isPossiblePalindrome(str):
    n = len(str)
    for i in range(n // 2):

        # If both left and right character
        # are not dot and they are not
        # equal also, then it is not possible
        # to make this string a palindrome
        if (str[i] != '.' and
            str[n - i - 1] != '.' and
            str[i] != str[n - i - 1]):
            return False

    return True

# Returns lexicographically smallest
# palindrome string, if possible
def smallestPalindrome(str):
    if (not isPossiblePalindrome(str)):
        return "Not Possible"

    n = len(str)
    str = list(str)

    # loop through character of string
    for i in range(n):
        if (str[i] == '.'):

            # if one of character is dot,
            # replace dot with other character
            if (str[n - i - 1] != '.'):
                str[i] = str[n - i - 1]

            # if both character are dot,
            # then replace them with
            # smallest character 'a'
            else:
                str[i] = str[n - i - 1] = 'a'

    # return the result
    return str

# Driver code
if __name__ == "__main__":
    str = "ab..e.c.a"
    print(''.join(smallestPalindrome(str)))

# This code is contributed by ChitraNayal
```

## C#

```
// C# program to get lexicographically
// smallest palindrome string
using System;
public class GFG
    {
    // Utility method to check str is
    // possible palindrome after ignoring
    static bool isPossiblePalindrome(char []str)
    {
    int n = str.Length;
    for (int i = 0; i < n / 2; i++)
    {
        /* If both left and right character
            are not dot and they are not
            equal also, then it is not
            possible to make this string a
            palindrome */
        if (str[i] != '.' &&
            str[n - i - 1] != '.' &&
            str[i] != str[n - i - 1])
            return false;
    }

    return true;
    }

    // Returns lexicographically smallest
    // palindrome string, if possible
    static void smallestPalindrome(char []str)
    {
    if (!isPossiblePalindrome(str))
        Console.WriteLine("Not Possible");

    int n = str.Length;

    // loop through character of string
    for (int i = 0; i < n; i++)
    {
        if (str[i] == '.')
        {
            // if one of character is dot,
            // replace dot with other character
            if (str[n - i - 1] != '.')
                str[i] = str[n - i - 1];

            // if both character are dot,
            // then replace them with
            // smallest character 'a'
            else
                str[i] = str[n - i - 1] = 'a';
        }
    }

    // return the result
    for(int i = 0; i < n; i++)
       Console.Write(str[i] + "");
    }

    // Driver code
    public static void Main()
    {
        String str = "ab..e.c.a";
        char[] s = str.ToCharArray();
        smallestPalindrome(s);
    }
}
// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to get lexicographically
// smallest palindrome string

// Utility method to check str is
// possible palindrome after ignoring
function isPossiblePalindrome($str)
{
    $n = strlen($str);
    for ($i = 0; $i < $n / 2; $i++)
    {
        /* If both left and right
        character are not dot and
        they are not equal also, then
        it is not possible to make this
        string a palindrome */
        if ($str[$i] != '.' &&
            $str[$n - $i - 1] != '.' &&
            $str[$i] != $str[$n - $i - 1])
            return false;
    }

    return true;
}

// Returns lexicographically smallest
// palindrome string, if possible
function smallestPalindrome($str)
{
    if (!isPossiblePalindrome($str))
        return "Not Possible";

    $n = strlen($str);

    // loop through character of string
    for ($i= 0; $i < $n; $i++)
    {
        if ($str[$i] == '.')
        {
            // if one of character is dot,
            // replace dot with other character
            if ($str[$n - $i - 1] != '.')
                $str[$i] = $str[$n - $i - 1];

            // if both character are dot,
            // then replace them with
            // smallest character 'a'
            else
                $str[$i] = $str[$n - $i - 1] = 'a';
        }
    }

    // return the result
    return $str;
}

// Driver code
$str = "ab..e.c.a";
echo smallestPalindrome($str);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to get lexicographically
// smallest palindrome string

    // Utility method to check str is
    // possible palindrome after ignoring
    function isPossiblePalindrome(str)
    {
        let n = str.length;
        for (let i = 0; i < Math.floor(n / 2); i++)
        {
            /* If both left and right character
                are not dot and they are not
                equal also, then it is not
                possible to make this string a
                palindrome */
            if (str[i] != '.' &&
                str[n - i - 1] != '.' &&
                str[i] != str[n - i - 1])
                return false;
        }

        return true;
    }

    // Returns lexicographically smallest
    // palindrome string, if possible
    function smallestPalindrome(str)
    {
        if (!isPossiblePalindrome(str))
            document.write("Not Possible");

        let n = str.length;

        // loop through character of string
        for (let i = 0; i < n; i++)
        {
            if (str[i] == '.')
            {
                // if one of character is dot,
                // replace dot with other character
                if (str[n - i - 1] != '.')
                    str[i] = str[n - i - 1];

                // if both character are dot,
                // then replace them with
                // smallest character 'a'
                else
                    str[i] = str[n - i - 1] = 'a';
            }
        }

        // return the result
        for(let i = 0; i < n; i++)
            document.write(str[i] + "");

    }

    // Driver code
    let str="ab..e.c.a";
    let s = str.split("");
    smallestPalindrome(s);

    // This code is contributed by rag2127

</script>
```

**输出:**

```
abcaeacba
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。