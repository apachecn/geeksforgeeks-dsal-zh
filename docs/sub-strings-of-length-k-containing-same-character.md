# 包含相同字符的长度为 K 的子串

> 原文:[https://www . geesforgeks . org/包含相同字符的长度为 k 的子字符串/](https://www.geeksforgeeks.org/sub-strings-of-length-k-containing-same-character/)

给定一个字符串“str”和一个整数“k”，任务是计算由相同字符组成的长度为“k”的子字符串的数量。给定的字符串只包含小写字母。
**例:**

```
Input: str = "aaaabbbccdddd", k=4
Output: 2
The sub-strings of length 4 which contain identical 
characters are 'aaaa' and 'dddd'. So, the count is 2.

Input: str = "aaaaaa", k=4
Output: 3
```

**简单的方法:**

*   查找字符串中长度为“k”的所有子字符串。
*   检查这些子字符串是否仅由“1”字符组成。
*   如果上述条件成立，则增加计数。
*   显示计数。

**高效方法:**我们将使用[窗口滑动技术](https://www.geeksforgeeks.org/window-sliding-technique/)来解决这个问题。

*   取一个长度为“k”的子字符串(第一个“k”字符)。
*   然后，在子字符串中添加下一个字符。
*   如果子字符串的长度大于“k”，则从字符串的开头删除该字符。
*   并且，借助地图计算子字符串中字符的出现频率。
*   如果子串字符之一的频率等于子串本身的长度，即所有字符都相同。
*   然后，增加计数，否则重复上述步骤，直到最后没有更多的字符要添加。
*   最后显示总计数。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function that counts all the
// sub-strings of length 'k'
// which have all identical characters
void solve(string s, int k)
{
    // count of sub-strings, length,
    // initial position of sliding window
    int count = 0, length = 0, pos = 0;

    // map to store the frequency of
    // the characters of sub-string
    map<char, int> m;

    for (int i = 0; i < s.length(); i++) {

        // increase the frequency of the character
        // and length of the sub-string
        m[s[i]]++;
        length++;

        // if the length of the sub-string
        // is greater than K
        if (length > k) {

            // remove the character from
            // the beginning of sub-string
            m[s[pos++]]--;
            length--;
        }

        // if the length of the sub string
        // is equal to k and frequency of one
        // of its characters is equal to the
        // length of the sub-string
        // i.e. all the characters are same
        // increase the count
        if (length == k && m[s[i]] == length)
            count++;
    }

    // display the number
    // of valid sub-strings
    cout << count << endl;
}

// Driver code
int main()
{
    string s = "aaaabbbccdddd";
    int k = 4;

    solve(s, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class GFG
{
    // Function that counts all the
    // sub-strings of length 'k'
    // which have all identical characters
    static void solve(String s, int k)
    {
        // count of sub-strings, length,
        // initial position of sliding window
        int count = 0, length = 0, pos = 0;

        // map to store the frequency of
        // the characters of sub-string
        HashMap<Character, Integer> m =
                            new HashMap<Character, Integer>();

        for (int i = 0; i < s.length(); i++)
        {

            // increase the frequency of the character
            // and length of the sub-string
            if(m.containsKey(s.charAt(i)))
                m.put(s.charAt(i), m.get(s.charAt(i))+1);
            else
                m.put(s.charAt(i), 1);

            length++;

            // if the length of the sub-string
            // is greater than K
            if (length > k)
            {

                // remove the character from
                // the beginning of sub-string
                m.put(s.charAt(pos), m.get(s.charAt(pos)) -1 );
                pos++;
                length--;
            }

            // if the length of the sub string
            // is equal to k and frequency of one
            // of its characters is equal to the
            // length of the sub-string
            // i.e. all the characters are same
            // increase the count
            if (length == k && m.get(s.charAt(i)) == length)
                count++;
        }

        // display the number
        // of valid sub-strings
        System.out.println( count);
    }

    // Driver code
    public static void main (String[] args)
    {

        String s = "aaaabbbccdddd";
        int k = 4;

        solve(s, k);
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of above
# approach

# Function that counts all the
# sub-strings of length 'k'
# which have all identical characters
def solve(s, k) :

    # count of sub-strings, length,
    # initial position of sliding window
    count, length, pos = 0, 0, 0

    # dictionary to store the frequency of
    # the characters of sub-string
    m = dict.fromkeys(s,0)

    for i in range(len(s)) :

        # increase the frequency of the character
        # and length of the sub-string
        m[s[i]] += 1
        length += 1

        # if the length of the sub-string
        # is greater than K
        if length > k :

            # remove the character from
            # the beginning of sub-string
            m[s[pos]] -= 1
            pos += 1
            length -= 1

        # if the length of the sub string
        # is equal to k and frequency of one
        # of its characters is equal to the
        # length of the sub-string
        # i.e. all the characters are same
        # increase the count
        if length == k and m[s[i]] == length :
            count += 1

    # display the number
    # of valid sub-strings
    print(count)

# Driver code    
if __name__ == "__main__" :

    s = "aaaabbbccdddd"
    k = 4

    # Function call
    solve(s, k)

# This code is contributed by
# ANKITRAI1
```

## C#

```
// C# implementation of above approach

using System;
using System.Collections.Generic;
class GFG
{
    // Function that counts all the
    // sub-strings of length 'k'
    // which have all identical characters
    static void solve(string s, int k)
    {
        // count of sub-strings, length,
        // initial position of sliding window
        int count = 0, length = 0, pos = 0;

        // map to store the frequency of
        // the characters of sub-string
        Dictionary<char, int> m =
                            new Dictionary<char, int>();

        for (int i = 0; i < s.Length; i++) {

            // increase the frequency of the character
            // and length of the sub-string
            if(m.ContainsKey(s[i]))
                m[s[i]]++;
            else
                m[s[i]] = 1;

            length++;

            // if the length of the sub-string
            // is greater than K
            if (length > k) {

                // remove the character from
                // the beginning of sub-string
                m[s[pos]]--;
                pos++;
                length--;
            }

            // if the length of the sub string
            // is equal to k and frequency of one
            // of its characters is equal to the
            // length of the sub-string
            // i.e. all the characters are same
            // increase the count
            if (length == k && m[s[i]] == length)
                count++;
        }

        // display the number
        // of valid sub-strings
        Console.WriteLine(count);
    }

    // Driver code
    public static void Main () {

        string s = "aaaabbbccdddd";
        int k = 4;

        solve(s, k);

    }

}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function that counts all the
// sub-strings of length 'k'
// which have all identical characters
function solve($s, $k)
{
    // count of sub-strings, length,
    // initial position of sliding window
    $count = 0;
    $length = 0;
    $pos = 0;

    // map to store the frequency of
    // the characters of sub-string
    $m = array();

    for ($i = 0; $i < strlen($s); $i++)
    {

        // increase the frequency of the character
        // and length of the sub-string
        $m[$s[$i]]++;
        $length++;

        // if the length of the sub-string
        // is greater than K
        if ($length > $k)
        {

            // remove the character from
            // the beginning of sub-string
            $m[$s[$pos++]]--;
            $length--;
        }

        // if the length of the sub string
        // is equal to k and frequency of one
        // of its characters is equal to the
        // length of the sub-string
        // i.e. all the characters are same
        // increase the count
        if ($length == $k && $m[$s[$i]] == $length)
            $count++;
    }

    // display the number
    // of valid sub-strings
    echo $count . "\n";
}

// Driver code
$s = "aaaabbbccdddd";
$k = 4;

solve($s, $k);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function that counts all the
// sub-strings of length 'k'
// which have all identical characters
function solve( s,  k)
{
    // count of sub-strings, length,
    // initial position of sliding window
    var count = 0, length = 0, pos = 0;

    // map to store the frequency of
    // the characters of sub-string
    var m = new Map();

    for (var i = 0; i < s.length; i++) {

        // increase the frequency of the character
        // and length of the sub-string
        if(!m.has(s[i]))
        {
            m.set(s[i], 0);
        }
        m.set(s[i], m.get(s[i])+1);
        length++;

        // if the length of the sub-string
        // is greater than K
        if (length > k) {

            // remove the character from
            // the beginning of sub-string
            if(!m.has(s[pos]))
            {
                m.set(s[pos], 0);
            }
            m.set(s[pos], m[s[pos]]-1);
            pos+=1;
            length--;
        }

        // if the length of the sub string
        // is equal to k and frequency of one
        // of its characters is equal to the
        // length of the sub-string
        // i.e. all the characters are same
        // increase the count
        if (length == k && m.get(s[i]) == length)
            count++;
    }

    // display the number
    // of valid sub-strings
    document.write( count);
}

// Driver code
var s = "aaaabbbccdddd";
var k = 4;
solve(s, k);

</script>
```

**Output:** 

```
2
```