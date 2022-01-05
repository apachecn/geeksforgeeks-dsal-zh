# 变换一个字符串，使其具有 abcd..z 作为子序列

> 原文:[https://www . geesforgeks . org/transform-string-store-subsequence-first-26-English-alphabets/](https://www.geeksforgeeks.org/transform-string-store-subsequence-first-26-english-alphabets/)

给定一串只有小英文字母的 S。我们需要通过一些移动(任何次数)来转换字符串，以获得字符串“abcdefghijklmnopqrstuvwxyz”作为该字符串中的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)。在一次移动中，您可以按字母顺序将字符串的任何字符替换为下一个字符，即“a”可以替换为“b”，“b”可以替换为“c”等等。字母“z”不能被任何字符替换。如果无法从该字符串中获取子序列，则打印“不可能”。
**注:**字符串的子序列是删除某些位置的某些字符得到的字符串。
示例:

```
Input : aaaaaaaaaaaaaaaaaaaaaaaaaa
Output : abcdefghijklmnopqrstuvwxyz
Explanation: Second occurrence of letter 'a' will be 
replaced by 'b', third occurrence of letter 'a' will 
be first replaced by 'b' and then by 'c' and so on.

Input : helloworld
Output : Not Possible
```

这个问题可以用贪婪的方法解决。我们的想法是首先观察到，在一次移动中，我们只能将任何角色递增到下一个角色。也就是说，“c”可以增加到“d”、“e”、“f”或任何大于“c”的字符。所以我们将创建一个变量 *ch* ，最初初始化为‘a’，通过迭代字符串，如果我们发现字符串的当前字符不大于 ch，我们将用 ch 替换它，并按字母顺序增加 ch 的值。由于 ch 最初等于“a”，我们将找到“a”，用 ch 替换它，增加 ch 以存储“b”，并在字符串中向前移动，然后如果我们找到任何不大于“b”的字符，用“b”替换它，并再次增加 ch 以存储“c”，并在字符串中向前移动。我们将重复这些步骤，直到 ch 到达“z”或整个字符串被处理。如果遍历整个字符串后，ch 没有到达“z ”,则不可能获得所需的子序列。
以下是上述办法的实施情况。

## C++

```
// C Plus Plus Program to transform the
// given string to contain the required
// subsequence
#include <bits/stdc++.h>
using namespace std;

// function to transform string with string
// passed as reference
bool transformString(string& s)
{
    // initializing the variable ch to 'a'
    char ch = 'a';

    // if the length of string is less than
    // 26, we can't obtain the required
    // subsequence
    if (s.size() < 26)
        return false;   

    for (int i = 0; i < s.size(); i++) {

        // if ch has reached 'z', it means we have
        // transformed our string such that required
        // subsequence can be obtained
        if (int(ch) > int('z'))
            break;

        // current character is not greater than ch,
        // then replace it with ch and increment ch
        if (s[i] <= ch) {
            s[i] = ch;
            ch = char(int(ch) + 1);
        }
    }

    if (ch <= 'z')
        return false;
    return true;
}

// Driver Code
int main()
{
    string str = "aaaaaaaaaaaaaaaaaaaaaaaaaa";   
    if (transformString(str))
        cout << str << endl;
    else
        cout << "Not Possible" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to transform the given string
// to contain the required subsequence
import java.io.*;

public class GFG {

    // function to transform string with
    // string passed as reference
    static boolean transformString(StringBuilder s)
    {

        // initializing the variable ch to 'a'
        char ch = 'a';

        // if the length of string is less than
        // 26, we can't obtain the required
        // subsequence
        if (s.length() < 26)
            return false;

        for (int i = 0; i < s.length(); i++) {

            // if ch has reached 'z', it means
            // we have transformed our string
            // such that required subsequence
            // can be obtained
            if ((int)ch > (int)'z')
                break;

            // current character is not greater
            // than ch, then replace it with
            // ch and increment ch
            if (s.charAt(i) <= ch) {
                s.setCharAt(i, ch);
                ch = (char)((int)ch + 1);
            }
        }

        if (ch <= 'z')
            return false;
        return true;
    }

    // Driver Code
    public static void main(String args[])
    {
        StringBuilder str =
        new StringBuilder("aaaaaaaaaaaaaaaaaaaaaaaaaa");

        if (transformString(str))
            System.out.println(str.toString());
        else
            System.out.println("Not Possible");
    }
}

// This code is contributed by Manish Shaw
// (manishshaw1)
```

## 蟒蛇 3

```
# Python3 Program to transform the
# given string to contain the required
# subsequence

# function to transform string with string
# passed as reference
def transformString(s) :

    # initializing the variable ch to 'a'
    ch = 'a'

    # if the length of string is less than
    # 26, we can't obtain the required
    # subsequence
    if (len(s) < 26) :
        return False   

    for i in range(0, len(s)):

        # if ch has reached 'z', it means we have
        # transformed our string such that required
        # subsequence can be obtained
        if (ord(ch) > ord('z')) :
            break

        # current character is not greater than ch,
        # then replace it with ch and increment ch
        if (s[i] <= ch) :
            s[i] = ch
            ch = chr(ord(ch) + 1)

    if (ch <= 'z') :
        print ("Not Possible")
    print ("".join(s))

# Driver Code
s = list("aaaaaaaaaaaaaaaaaaaaaaaaaa")
transformString(s)

# This code is contributed by Manish Shaw
# (manishshaw1)
```

## C#

```
// C# Program to transform the given string
// to contain the required subsequence
using System;
using System.Text;
using System.Collections.Generic;

class GFG {

    // function to transform string with string
    // passed as reference
    static bool transformString(ref StringBuilder s)
    {

        // initializing the variable ch to 'a'
        char ch = 'a';

        // if the length of string is less than
        // 26, we can't obtain the required
        // subsequence
        if (s.Length < 26)
            return false;

        for (int i = 0; i < s.Length; i++) {

            // if ch has reached 'z', it means we
            // have transformed our string such
            // that required subsequence can be
            // obtained
            if ((int)ch > 122)
                break;

            // current character is not greater
            // than ch, then replace it with ch
            // and increment ch
            if (s[i] <= ch) {
                s[i] = ch;
                ch = (char)((int)ch + 1);
            }
        }

        if (ch <= 'z')
            return false;
        return true;
    }

    // Driver Code
    public static void Main()
    {
        StringBuilder str = new
        StringBuilder("aaaaaaaaaaaaaaaaaaaaaaaaaa");

        if (transformString(ref str))
            Console.WriteLine(str + "\n");
        else
            Console.WriteLine("Not Possible" + "\n");
    }
}

// This code is contributed by Manish Shaw
// (manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to transform the
// given string to contain the required
// subsequence

// function to transform string with
// string passed as reference
function transformString(&$s)
{

    // initializing the variable
    // ch to 'a'
    $ch = "a";

    // if the length of string is less than
    // 26, we can't obtain the required
    // subsequence
    if (strlen($s) < 26)
        return false;

    for ($i = 0; $i < strlen($s); $i++)
    {

        // if ch has reached 'z',
        // it means we have
        // transformed our string
        // such that required
        // subsequence can be obtained
        if (ord($ch) > ord("z"))
            break;

        // current character is not
        // greater than ch, then
        // replace it with ch and
        // increment ch
        if ($s[$i] <= $ch)
        {
            $s[$i] = $ch;
            $ch = chr(ord($ch) + 1);
        }
    }

    if ($ch <= "z")
        return false;
    return true;
}

// Driver Code
$str = "aaaaaaaaaaaaaaaaaaaaaaaaaa";
if (transformString($str))
    echo $str;
else
    echo "Not Possible";

// This code is contributed by
// Manish Shaw (manishshaw1)
?>
```

## java 描述语言

```
<script>

// Javascript Plus Plus Program to transform the
// given string to contain the required
// subsequence

// function to transform string with string
// passed as reference
function transformString()
{
    // initializing the variable ch to 'a'
    var ch = 'a';

    // if the length of string is less than
    // 26, we can't obtain the required
    // subsequence
    if (s.length < 26)
        return false;   

    for (var i = 0; i < s.length; i++) {

        // if ch has reached 'z', it means we have
        // transformed our string such that required
        // subsequence can be obtained
        if (ch.charCodeAt(0) > 122)
            break;

        // current character is not greater than ch,
        // then replace it with ch and increment ch
        if (s[i].charCodeAt(0) <= ch.charCodeAt(0)) {
            s[i] = ch;
            ch = String.fromCharCode(ch.charCodeAt(0) + 1);
        }
    }
    s = s.join('')
    if (ch.charCodeAt(0) <= 'z'.charCodeAt(0))
        return false;
    return true;
}

// Driver Code
var s = "aaaaaaaaaaaaaaaaaaaaaaaaaa".split('');   
if (transformString(s))
    document.write(s);
else
    document.write( "Not Possible");

</script>
```

输出:

```
abcdefghijklmnopqrstuvwxyz
```

**时间复杂度** : O(n)，其中 n 为字符串的长度。