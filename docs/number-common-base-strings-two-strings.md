# 两个弦的公共基弦数

> 原文:[https://www . geesforgeks . org/number-common-base-strings-two-strings/](https://www.geeksforgeeks.org/number-common-base-strings-two-strings/)

给定两个字符串 s1 和 s2，我们需要找到两个公共基字符串的数目。如果串 s 的子串的重复连接导致串 s，则串 s 的子串被称为基串。例如:

```
Input : s1 = "pqrspqrs"
        s2 = "pqrspqrspqrspqrs"
Output : 2
The two common base strings are "pqrs"
and "pqrspqrs".

Input: s1 = "bbb"
       s2 = "bb"
Output: 1
There is only one common base string
which is "b". 
```

公共基本字符串的最大可能长度等于两个字符串中较小者的长度。因此，我们运行一个循环，考虑较小字符串的所有前缀，并对每个前缀检查它是否是一个公共基数。
以下是以下方法的实施

## C++

```
// CPP program to count common base strings
// of s1 and s2.
#include <bits/stdc++.h>
using namespace std;

// function for finding common divisor .
bool isCommonBase(string base, string s1, 
                               string s2)
{
    // Checking if 'base' is base string 
    // of 's1'
    for (int j = 0; j < s1.length(); ++j)
        if (base[j % base.length()] != s1[j])
            return false;

    // Checking if 'base' is base string
    // of 's2'
    for (int j = 0; j < s2.length(); ++j)
        if (base[j % base.length()] != s2[j])
            return false;   

    return true;
}

int countCommonBases(string s1, string s2) {
   int n1 = s1.length(), n2 = s2.length();
   int count = 0;
   for (int i=1; i<=min(n1, n2); i++)
   {
       string base = s1.substr(0, i);
       if (isCommonBase(base, s1, s2))
           count++;
   }
   return count;
}

// Driver code
int main()
{
    string s1 = "pqrspqrs";
    string s2 = "pqrspqrspqrspqrs";
    cout << countCommonBases(s1, s2) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count common
// base strings of s1 and s2.

class GFG
{

// function for finding common divisor
static boolean isCommonBase(String base,
                            String s1,
                            String s2)
{
    // Checking if 'base' is base
    // String of 's1'
    for (int j = 0; j < s1.length(); ++j)
    {
        if (base.charAt(j %
            base.length()) != s1.charAt(j))
        {
            return false;
        }
    }

    // Checking if 'base' is base
    // String of 's2'
    for (int j = 0; j < s2.length(); ++j)
    {
        if (base.charAt(j %
            base.length()) != s2.charAt(j))
        {
            return false;
        }
    }

    return true;
}

static int countCommonBases(String s1,
                            String s2)
{
    int n1 = s1.length(),
        n2 = s2.length();
    int count = 0;
    for (int i = 1; i <= Math.min(n1, n2); i++)
    {
        String base = s1.substring(0, i);
        if (isCommonBase(base, s1, s2))
        {
            count++;
        }
    }
    return count;
}

// Driver code
public static void main(String[] args)
{
    String s1 = "pqrspqrs";
    String s2 = "pqrspqrspqrspqrs";

    System.out.println(countCommonBases(s1, s2));
}
}

// This code is contributed by Rajput-JI
```

## 蟒蛇 3

```
# Python 3 program to count common
# base strings of s1 and s2.

# function for finding common divisor .
def isCommonBase(base, s1, s2):

    # Checking if 'base' is base
    # string of 's1'
    for j in range(len(s1)):
        if (base[j % len(base)] != s1[j]):
            return False

    # Checking if 'base' is base
    # string of 's2'
    for j in range(len(s2)):
        if (base[j % len( base)] != s2[j]):
            return False

    return True

def countCommonBases(s1, s2):
    n1 = len(s1)
    n2 = len(s2)
    count = 0
    for i in range(1, min(n1, n2) + 1):
        base = s1[0: i]
        if (isCommonBase(base, s1, s2)):
            count += 1

    return count

# Driver code
if __name__ == "__main__":

    s1 = "pqrspqrs"
    s2 = "pqrspqrspqrspqrs"
    print(countCommonBases(s1, s2))

# This code is contributed by ita_c
```

## C#

```
// C# program to count common base
// strings of s1 and s2.
using System;

class GFG
{
// function for finding common divisor
static bool isCommonBase(String Base,
                         String s1,
                         String s2)
{
    // Checking if 'base' is base
    // String of 's1'
    for (int j = 0; j < s1.Length; ++j)
    {
        if (Base[j % Base.Length] != s1[j])
        {
            return false;
        }
    }

    // Checking if 'base' is base
    // String of 's2'
    for (int j = 0; j < s2.Length; ++j)
    {
        if (Base[j % Base.Length] != s2[j])
        {
            return false;
        }
    }

    return true;
}

static int countCommonBases(String s1,
                            String s2)
{
    int n1 = s1.Length, n2 = s2.Length;
    int count = 0;
    for (int i = 1;
             i <= Math.Min(n1, n2); i++)
    {
        String Base = s1.Substring(0, i);
        if (isCommonBase(Base, s1, s2))
        {
            count++;
        }
    }
    return count;
}

// Driver code
public static void Main()
{
    String s1 = "pqrspqrs";
    String s2 = "pqrspqrspqrspqrs";

    Console.Write(countCommonBases(s1, s2));
}
}

// This code is contributed by Rajput-JI
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count common base strings
// of s1 and s2.

// function for finding common divisor .
function isCommonBase($base,$s1, $s2)
{
    // Checking if 'base' is base string
    // of 's1'
    for ($j = 0; $j < strlen($s1); ++$j)
        if ($base[$j % strlen($base)] != $s1[$j])
            return false;

    // Checking if 'base' is base string
    // of 's2'
    for ($j = 0; $j < strlen($s2); ++$j)
        if ($base[$j % strlen($base)] != $s2[$j])
            return false;

    return true;
}

function countCommonBases($s1, $s2)
{
    $n1 = strlen($s1);
    $n2 = strlen($s2);
    $count = 0;
    for ($i = 1; $i <= min($n1, $n2); $i++)
    {
        $base = substr($s1,0, $i);
        if (isCommonBase($base, $s1, $s2))
            $count++;
    }
    return $count;
}

// Driver code
    $s1 = "pqrspqrs";
    $s2 = "pqrspqrspqrspqrs";
    echo countCommonBases($s1, $s2)."\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to count common
// base strings of s1 and s2.

    // function for finding common divisor
    function isCommonBase(base,s1,s2)
    {

        // Checking if 'base' is base
    // String of 's1'
    for (let j = 0; j < s1.length; ++j)
    {
        if (base[j % base.length] != s1[j])
        {
            return false;
        }
    }

    // Checking if 'base' is base
    // String of 's2'
    for (let j = 0; j < s2.length; ++j)
    {
        if (base[j %base.length] != s2[j])
        {
            return false;
        }
    }

    return true;
    }

    function countCommonBases(s1,s2)
    {
        let n1 = s1.length,
        n2 = s2.length;
    let count = 0;
    for (let i = 1; i <= Math.min(n1, n2); i++)
    {
        let base = s1.substring(0, i);
        if (isCommonBase(base, s1, s2))
        {
            count++;
        }
    }
    return count;
    }

    // Driver code
    let s1 = "pqrspqrs";
    let s2 = "pqrspqrspqrspqrs";
    document.write(countCommonBases(s1, s2));

    // This code is contributed by rag2127
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(min(n1，n2) * (n1 + n2))