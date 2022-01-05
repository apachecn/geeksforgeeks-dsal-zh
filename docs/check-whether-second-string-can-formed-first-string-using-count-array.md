# 检查第二个字符串是否可以由第一个字符串的字符组成

> 原文:[https://www . geeksforgeeks . org/check-second-string-can-formed-first-string-use-count-array/](https://www.geeksforgeeks.org/check-whether-second-string-can-formed-first-string-using-count-array/)

给定两个字符串 str1 和 str2，检查 str2 是否可以由 str1
**构成示例:**

```
Input : str1 = geekforgeeks, str2 = geeks
Output : Yes
Here, string2 can be formed from string1.

Input : str1 = geekforgeeks, str2 = and
Output :  No
Here string2 cannot be formed from string1.

Input : str1 = geekforgeeks, str2 = geeeek
Output :  Yes
Here string2 can be formed from string1
as string1 contains 'e' comes 4 times in
string2 which is present in string1\. 
```

其思想是在计数数组中对 str1 的字符频率进行计数。然后遍历 str2 并降低 str2 的字符在计数数组中的出现频率。如果某个字符的频率在任何时候变为负值，则返回 false。
以下是上述方法的实施:

## C++

```
// CPP program to check whether second string
// can be formed from first string
#include <bits/stdc++.h>
using namespace std;
const int MAX = 256;

bool canMakeStr2(string str1, string str2)
{
    // Create a count array and count frequencies
    // characters in str1.
    int count[MAX] = {0};
    for (int i = 0; i < str1.length(); i++)
        count[str1[i]]++;

    // Now traverse through str2 to check
    // if every character has enough counts
    for (int i = 0; i < str2.length(); i++)
    {
        if (count[str2[i]] == 0)
           return false;
        count[str2[i]]--;
    }
    return true;
}

// Driver Code
int main()
{
    string str1 = "geekforgeeks";
    string str2 = "for";
    if (canMakeStr2(str1, str2))
       cout << "Yes";
    else
       cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether second string
// can be formed from first string

class GFG {

    static int MAX = 256;

    static boolean canMakeStr2(String str1, String str2)
    {
        // Create a count array and count frequencies
        // characters in str1.
        int[] count = new int[MAX];
        char []str3 = str1.toCharArray();
        for (int i = 0; i < str3.length; i++)
            count[str3[i]]++;

        // Now traverse through str2 to check
        // if every character has enough counts

        char []str4 = str2.toCharArray();
        for (int i = 0; i < str4.length; i++) {
            if (count[str4[i]] == 0)
                return false;
            count[str4[i]]--;
        }
        return true;
    }

    // Driver Code
    static public void main(String []args)
    {
        String str1 = "geekforgeeks";
        String str2 = "for";
        if (canMakeStr2(str1, str2))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python program to check whether second string
# can be formed from first string
def canMakeStr2(s1, s2):

    # Create a count array and count
    # frequencies characters in s1
    count = {s1[i] : 0 for i in range(len(s1))}

    for i in range(len(s1)):
        count[s1[i]] += 1

    # Now traverse through str2 to check
    # if every character has enough counts
    for i in range(len(s2)):
        if (count.get(s2[i]) == None or count[s2[i]] == 0):
            return False
        count[s2[i]] -= 1
    return True

# Driver Code
s1 = "geekforgeeks"
s2 = "for"

if canMakeStr2(s1, s2):
    print("Yes")
else:
    print("No")
```

## C#

```
// C# program to check whether second string
// can be formed from first string
using System;

class GFG {

    static int MAX = 256;

    static bool canMakeStr2(string str1, string str2)
    {
        // Create a count array and count frequencies
        // characters in str1.
        int[] count = new int[MAX];
        for (int i = 0; i < str1.Length; i++)
            count[str1[i]]++;

        // Now traverse through str2 to check
        // if every character has enough counts
        for (int i = 0; i < str2.Length; i++) {
            if (count[str2[i]] == 0)
                return false;
            count[str2[i]]--;
        }
        return true;
    }

    // Driver Code
    static public void Main()
    {
        string str1 = "geekforgeeks";
        string str2 = "for";
        if (canMakeStr2(str1, str2))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check whether
// second string can be formed
// from first string
$MAX = 256;

function canMakeStr2($str1, $str2)
{
    // Create a count array and
    // count frequencies characters
    // in str1.
    $count = (0);
    for ($i = 0; $i < strlen($str1); $i++)

    // Now traverse through str2
    // to check if every character
    // has enough counts
    for ($i = 0; $i < strlen($str2); $i++)
    {
        if ($count[$str2[$i]] == 0)
        return -1;
    }
    return true;
}

// Driver Code
$str1 = "geekforgeeks";
$str2 = "for";
if (canMakeStr2($str1, $str2))
echo "Yes";
else
echo "No";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program to check whether second string
    // can be formed from first string

    let MAX = 256;

    function canMakeStr2(str1, str2)
    {
        // Create a count array and count frequencies
        // characters in str1.
        let count = new Array(MAX);
        count.fill(0);
        for (let i = 0; i < str1.length; i++)
            count[str1[i]]++;

        // Now traverse through str2 to check
        // if every character has enough counts
        for (let i = 0; i < str2.length; i++) {
            if (count[str2[i]] == 0)
                return false;
            count[str2[i]]--;
        }
        return true;
    }

    let str1 = "geekforgeeks";
    let str2 = "for";
    if (canMakeStr2(str1, str2))
      document.write("Yes");
    else
      document.write("No");

</script>
```

**Output**

```
Yes
```