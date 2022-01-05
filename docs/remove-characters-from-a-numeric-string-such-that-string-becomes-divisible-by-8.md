# 从数字字符串中删除字符，使字符串可以被 8 整除

> 原文:[https://www . geesforgeks . org/从数字字符串中移除字符，这样字符串就可以被 8 整除/](https://www.geeksforgeeks.org/remove-characters-from-a-numeric-string-such-that-string-becomes-divisible-by-8/)

给定一个非负整数，以数字字符串 **str** 的形式表示。从字符串中删除零个或多个字符，使数字成为可被 8 整除的**。如果可能，删除字符后打印字符串，否则打印 **-1** 。
**举例:**** 

> ****输入:**str = " 3454 "
> T3】输出: 344
> 去掉‘5’后，字符串变成 344，可被 8 整除。
> **输入:** str = "111"
> **输出:** -1**

****方法:**考虑到 8 的[可除性规则，我们只需要检查 str 最后 3 个字符组成的数是否能被 8 整除。因此，我们可以迭代 8 到 1000 的所有倍数，并检查在给定的字符串中是否有任何倍数作为子序列存在，那么这个倍数就是我们需要的答案。否则，不存在答案，因为所有大于 1000 的 8 的倍数也需要有已经检查过的数字(由最后 3 位数字组成)。
以下是上述方法的实施:](https://www.geeksforgeeks.org/check-large-number-divisible-8-not/)** 

## **C++**

```
// C++ program to remove digits from a
// numeric string such that the number
// becomes divisible by 8
#include <bits/stdc++.h>
using namespace std;

// Function that return true if sub
// is a sub-sequence in s
int checkSub(string sub, string s)
{
    int j = 0;
    for (int i = 0; i < s.size(); i++)
        if (sub[j] == s[i])
            j++;
    return j == (int)sub.size();
}

// Function to return a multiple of 8
// formed after removing 0 or more characters
// from the given string
int getMultiple(string s)
{
    // Iterate over all multiples of 8
    for (int i = 0; i < 1e3; i += 8) {

        // If current multiple
        // exists as a subsequence
        // in the given string
        if (checkSub(to_string(i), s))
            return i;
    }

    return -1;
}

// Driver Code
int main()
{
    string s = "3454";
    cout << getMultiple(s);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to remove digits from a
// numeric string such that the number
// becomes divisible by 8

class GFG
{

    // Function that return true if sub
    // is a sub-sequence in s
    static boolean checkSub(String sub, String s)
    {
        int j = 0;
        for (int i = 0; i < s.length(); i++)
            if (sub.charAt(j) == s.charAt(i))
                j++;

        return j == sub.length();
    }

    // Function to return a multiple of 8
    // formed after removing 0 or more characters
    // from the given string
    static int getMultiple(String s)
    {
        // Iterate over all multiples of 8
        for (int i = 0; i < 1E3; i += 8)
        {

            // If current multiple
            // exists as a subsequence
            // in the given string
            if (checkSub(Integer.toString(i), s))
                return i;
        }
        return -1;
    }

    // Driver Code
    public static void main (String[] args)
    {
            String s = "3454";
            System.out.println(getMultiple(s));
    }
}

// This code is contributed by mits
```

## **蟒蛇 3**

```
# Python3 program to remove digits from
# a numeric string such that the number
# becomes divisible by 8
import math as mt

# Function that return true if sub
# is a sub-sequence in s
def checkSub(sub, s):

    j = 0
    for i in range(len(s)):
        if (sub[j] == s[i]):
            j += 1

    if j == int(len(sub)):
        return True
    else:
        return False

# Function to return a multiple of 8
# formed after removing 0 or more
# characters from the given string
def getMultiple(s):

    # Iterate over all multiples of 8
    for i in range(0, 10**3, 8):

        # If current multiple
        # exists as a subsequence
        # in the given string
        if (checkSub(str(i), s)):
            return i

    return -1

# Driver Code
s = "3454"
print(getMultiple(s))

# This code is contributed
# by Mohit Kumar 29
```

## **C#**

```
// C# program to remove digits from a
// numeric string such that the number
// becomes divisible by 8
using System;

class GFG
{

    // Function that return true if sub
    // is a sub-sequence in s
    static bool checkSub(string sub, string s)
    {
        int j = 0;
        for (int i = 0; i < s.Length; i++)
            if (sub[j] == s[i])
                j++;

        return j == sub.Length;
    }

    // Function to return a multiple of 8
    // formed after removing 0 or more characters
    // from the given string
    static int getMultiple(string s)
    {
        // Iterate over all multiples of 8
        for (int i = 0; i < 1e3; i += 8)
        {

            // If current multiple
            // exists as a subsequence
            // in the given string
            if (checkSub(i.ToString(), s))
                return i;
        }
        return -1;
    }

    // Driver Code
    static void Main()
    {
            string s = "3454";
            Console.WriteLine(getMultiple(s));
    }
}

// This code is contributed by Ryuga
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP program to remove digits from a
// numeric string such that the number
// becomes divisible by 8

// Function that return true if sub
// is a sub-sequence in s
function checkSub($sub, $s)
{
    $j = 0;
    for ($i = 0; $i < strlen($s); $i++)
        if ($sub[$j] == $s[$i])
            $j++;
    return $j == strlen($sub);
}

// Function to return a multiple of 8
// formed after removing 0 or more
// characters from the given string
function getMultiple($s)
{
    // Iterate over all multiples of 8
    for ($i = 0; $i < 1e3; $i += 8)
    {

        // If current multiple
        // exists as a subsequence
        // in the given string
        if (checkSub((string)($i), $s))
            return $i;
    }

    return -1;
}

// Driver Code
$s = "3454";
echo getMultiple($s);

// This code is contributed
// by Akanksha Rai
```

## **java 描述语言**

```
<script>

    // JavaScript program to remove digits from a
    // numeric string such that the number
    // becomes divisible by 8

    // Function that return true if sub
    // is a sub-sequence in s
    function checkSub(sub, s)
    {
        let j = 0;
        for (let i = 0; i < s.length; i++)
            if (sub[j] == s[i])
                j++;

        return j == sub.length;
    }

    // Function to return a multiple of 8
    // formed after removing 0 or more characters
    // from the given string
    function getMultiple(s)
    {
        // Iterate over all multiples of 8
        for (let i = 0; i < 1e3; i += 8)
        {

            // If current multiple
            // exists as a subsequence
            // in the given string
            if (checkSub(i.toString(), s))
                return i;
        }
        return -1;
    }

    let s = "3454";
      document.write(getMultiple(s));

</script>
```

****Output:** 

```
344
```**