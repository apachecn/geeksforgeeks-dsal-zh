# 频率等于给定字符串中其他字符频率之和的字符

> 原文:[https://www . geesforgeks . org/character-其频率等于给定字符串中其他字符的频率总和/](https://www.geeksforgeeks.org/character-whose-frequency-is-equal-to-the-sum-of-frequencies-of-other-characters-of-the-given-string/)

给定一个由小写英文字母组成的字符串。任务是查找字符串中是否有任何字符的频率等于字符串中其他字符的频率之和。如果存在这样的字符，则打印**是**否则打印**否**。
**举例:**

> **输入:**str = " hkklkwwww "
> **输出:**是
> 频率(w) =频率(h) +频率(k) +频率(l)
> 4 = 1 + 2 + 1
> 4 = 4
> **输入:**str = " geeksforgeeks "
> **输出:**否

**方法:**如果字符串的长度是奇数，那么结果总是**否**。对于偶数长度的字符串，计算字符串中每个字符的频率，对于任何字符，如果频率=字符串长度的一半，那么结果将是**是**否则**否**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if some character
// exists in the given string whose frequency
// is equal to the sum frequencies of
// other characters of the string
bool isFrequencyEqual(string str, int len)
{

    // If string is of odd length
    if (len % 2 == 1)
        return false;

    // To store the frequency of each
    // character of the string
    int i, freq[26] = { 0 };

    // Update the frequencies of the characters
    for (i = 0; i < len; i++)
        freq[str[i] - 'a']++;

    for (i = 0; i < 26; i++)
        if (freq[i] == len / 2)
            return true;

    // No such character exists
    return false;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    int len = str.length();
    if (isFrequencyEqual(str, len))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach.
class GFG
{

    // Function that returns true if some character
    // exists in the given string whose frequency
    // is equal to the sum frequencies of
    // other characters of the string
    static boolean isFrequencyEqual(String str, int len)
    {

        // If string is of odd length
        if (len % 2 == 1)
        {
            return false;
        }

        // To store the frequency of each
        // character of the string
        int i, freq[] = new int[26];

        // Update the frequencies of the characters
        for (i = 0; i < len; i++)
        {
            freq[str.charAt(i) - 'a']++;
        }

        for (i = 0; i < 26; i++)
        {
            if (freq[i] == len / 2)
            {
                return true;
            }
        }

        // No such character exists
        return false;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "geeksforgeeks";
        int len = str.length();
        if (isFrequencyEqual(str, len))
        {
            System.out.println("Yes");
        }
        else
        {
            System.out.println("No");
        }
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if some character
# exists in the given string whose frequency
# is equal to the sum frequencies of
# other characters of the string
def isFrequencyEqual(string, length):

    # If string is of odd length
    if length % 2 == 1:
        return False

    # To store the frequency of each
    # character of the string
    freq = [0] * 26

    # Update the frequencies of
    # the characters
    for i in range(0, length):
        freq[ord(string[i]) - ord('a')] += 1

    for i in range(0, 26):
        if freq[i] == length // 2:
            return True

    # No such character exists
    return False

# Driver code
if __name__ == "__main__":

    string = "geeksforgeeks"
    length = len(string)
    if isFrequencyEqual(string, length):
        print("Yes")
    else:
        print("No")

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the above approach.
using System;

class GFG
{

    // Function that returns true if some character
    // exists in the given string whose frequency
    // is equal to the sum frequencies of
    // other characters of the string
    static bool isFrequencyEqual(String str, int len)
    {

        // If string is of odd length
        if (len % 2 == 1)
        {
            return false;
        }

        // To store the frequency of each
        // character of the string
        int i;
        int []freq = new int[26];

        // Update the frequencies of the characters
        for (i = 0; i < len; i++)
        {
            freq[str[i] - 'a']++;
        }

        for (i = 0; i < 26; i++)
        {
            if (freq[i] == len / 2)
            {
                return true;
            }
        }

        // No such character exists
        return false;
    }

    // Driver code
    public static void Main()
    {
        String str = "geeksforgeeks";
        int len = str.Length;
        if (isFrequencyEqual(str, len))
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if some character
// exists in the given string whose frequency
// is equal to the sum frequencies of
// other characters of the string
function isFrequencyEqual($str, $len)
{

    // If string is of odd length
    if ($len % 2 == 1)
        return false;

    // To store the frequency of each
    // character of the string
    $freq = array();
    for($i = 0; $i < 26 ; $i++)
        $freq[$i] = 0;

    // Update the frequencies of the characters
    for($i = 0; $i < $len ; $i++)
        $freq[ord($str[$i]) - 97]++;

    for($i = 0; $i < 26 ; $i++)
            if ($freq[$i] == $len / 2)
            return true;

    // No such character exists
    return false;
}

// Driver code
$str = "geeksforgeeks";
$len = strlen($str);
if (isFrequencyEqual($str, $len))
    echo "Yes";
else
    echo "No";

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if some character
// exists in the given string whose frequency
// is equal to the sum frequencies of
// other characters of the string
function isFrequencyEqual(str, len)
{

    // If string is of odd length
    if (len % 2 == 1)
        return false;

    // To store the frequency of each
    // character of the string
    var i, freq=Array(26).fill(0);

    // Update the frequencies of the characters
    for (i = 0; i < len; i++)
        freq[str[i] - 'a']++;

    for (i = 0; i < 26; i++)
        if (freq[i] == parseInt(len / 2))
            return true;

    // No such character exists
    return false;
}

// Driver code
var str = "geeksforgeeks";
var len = str.length;
if (isFrequencyEqual(str, len))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
No
```

**时间复杂度:** O(len)，其中 len 是给定字符串的长度。