# 检查给定的字符串是否为异码

> 原文:[https://www . geesforgeks . org/check-when-given-string-heterogram-not/](https://www.geeksforgeeks.org/check-whether-given-string-heterogram-not/)

给定一根绳子 **S** 。任务是检查给定的字符串是否是杂凑图。一个[异形词](https://en.wikipedia.org/wiki/Heterogram_(literature))是一个单词、短语或句子，其中字母表中没有一个字母出现超过一次。

**例:**

```
Input : S = "the big dwarf only jumps"
Output : Yes
Each alphabet in the string S is occurred
only once.

Input : S = "geeksforgeeks" 
Output : No
Since alphabet 'g', 'e', 'k', 's' occurred
more than once.
```

想法是创建一个大小为 26 的散列数组，初始化为 0。遍历给定字符串的每个字母表，并在相应的哈希数组位置标记 1。如果第一次遇到该字母表，则返回 false。

下面是该方法的实现:

## C++

```
// C++ Program to check whether the given string is Heterogram or not.
#include<bits/stdc++.h>
using namespace std;

bool isHeterogram(char s[], int n)
{
    int hash[26] = { 0 };

    // traversing the string.
    for (int i = 0; i < n; i++)
    {
        // ignore the space
        if (s[i] != ' ')
        {
            // if already encountered
            if (hash[s[i] - 'a'] == 0)
                hash[s[i] - 'a'] = 1;

            // else return false.
            else
                return false;
        }
    }

    return true;
}

// Driven Program
int main()
{
    char s[] = "the big dwarf only jumps";
    int n = strlen(s);
    (isHeterogram(s, n))?(cout << "YES"):(cout << "NO");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check whether the
// given string is Heterogram or not.
class GFG {

    static boolean isHeterogram(String s, int n)
    {
        int hash[] = new int[26];

        // traversing the string.
        for (int i = 0; i < n; i++)
        {
            // ignore the space
            if (s.charAt(i) != ' ')
            {
                // if already encountered
                if (hash[s.charAt(i) - 'a'] == 0)
                    hash[s.charAt(i) - 'a'] = 1;

                // else return false.
                else
                    return false;
            }
        }

        return true;
    }

// Driver code
public static void main (String[] args)
{
    String s = "the big dwarf only jumps";
    int n = s.length();

    if(isHeterogram(s, n))
        System.out.print("YES");
    else
        System.out.print("NO");
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 code to check
# whether the given
# string is Heterogram
# or not.

def isHeterogram(s, n):
    hash = [0] * 26

    # traversing the
    # string.
    for i in range(n):

        # ignore the space
        if s[i] != ' ':

            # if already
            # encountered
            if hash[ord(s[i]) - ord('a')] == 0:
                hash[ord(s[i]) - ord('a')] = 1

            # else return false.
            else:
                return False

    return True

# Driven Code
s = "the big dwarf only jumps"
n = len(s)

print("YES" if isHeterogram(s, n) else "NO")

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# Program to check whether the
// given string is Heterogram or not.
using System;

class GFG {

    static bool isHeterogram(string s, int n)
    {
        int []hash = new int[26];

        // traversing the string.
        for (int i = 0; i < n; i++)
        {
            // ignore the space
            if (s[i] != ' ')
            {
                // if already encountered
                if (hash[s[i] - 'a'] == 0)
                    hash[s[i] - 'a'] = 1;

                // else return false.
                else
                    return false;
            }
        }

        return true;
    }

    // Driver code
    public static void Main ()
    {
        string s = "the big dwarf only jumps";
        int n = s.Length;

        if(isHeterogram(s, n))
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }
}

// This code is contributed by Vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to check
// whether the given string
// is Heterogram or not.

function isHeterogram($s, $n)
{
    $hash = array();
    for($i = 0; $i < 26; $i++)
        $hash[$i] = 0;

    // traversing the string.
    for ($i = 0; $i < $n; $i++)
    {
        // ignore the space
        if ($s[$i] != ' ')
        {
            // if already encountered
            if ($hash[ord($s[$i]) -
                      ord('a')] == 0)
                $hash[ord($s[$i]) -
                      ord('a')] = 1;

            // else return false.
            else
                return false;
        }
    }    
    return true;
}

// Driven Code
$s = "the big dwarf only jumps";
$n = strlen($s);
if (isHeterogram($s, $n))
    echo ("YES");
else
    echo ("NO");

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// Javascript program to check whether
// the given string is Heterogram or not.
function isHeterogram(s, n)
{
    var hash = Array(26).fill(0);

    // Traversing the string.
    for(var i = 0; i < n; i++)
    {

        // Ignore the space
        if (s[i] != ' ')
        {

            // If already encountered
            if (hash[s[i].charCodeAt(0) -
                      'a'.charCodeAt(0)] == 0)
                hash[s[i].charCodeAt(0) -
                      'a'.charCodeAt(0)] = 1;

            // Else return false.
            else
                return false;
        }
    }
    return true;
}

// Driver code
var s = "the big dwarf only jumps";
var n = s.length;

(isHeterogram(s, n)) ? (document.write("YES")) :
                       (document.write("NO"));

// This code is contributed by rutvik_56

</script>
```

**输出:**

```
YES
```

**时间复杂度:** O(N)

**辅助空间:** O(26)