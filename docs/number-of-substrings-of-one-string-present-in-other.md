# 存在于其他

中的一个字符串的子字符串数量

> 原文:[https://www . geeksforgeeks . org/one-string-present-in-other 的子字符串数/](https://www.geeksforgeeks.org/number-of-substrings-of-one-string-present-in-other/)

假设给我们一个字符串 s1，我们需要找到字符串 s2 中出现的 s1 的子字符串(包括同一子字符串的多次出现)的总数。

**示例:**

```
Input : s1 = aab
        s2 = aaaab
Output :6
Substrings of s1 are ["a", "a", "b", "aa", 
"ab", "aab"]. These all are present in s2\. 
Hence, answer is 6.

Input :s1 = abcd
       s2 = swalencud
Output :3 
```

想法是考虑 s1 的所有子串，并检查它是否出现在 s2 中。

## C++

```
// CPP program to count number of substrings of s1
// present in s2.
#include<iostream>
#include<string>
using namespace std;

int countSubstrs(string s1, string s2)
{
    int ans = 0;

    for (int i = 0; i < s1.length(); i++) {

        // s3 stores all substrings of s1
        string s3;
        for (int j = i; j < s1.length(); j++) {
            s3 += s1[j];

            // check the presence of s3 in s2
            if (s2.find(s3) != string::npos)
                ans++;
        }
    }
    return ans;
}

// Driver code
int main()
{
    string s1 = "aab", s2 = "aaaab";
    cout << countSubstrs(s1, s2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of
// substrings of s1 present in s2.
import java.util.*;

class GFG
{

static int countSubstrs(String s1,
                        String s2)
{
int ans = 0;

for (int i = 0; i < s1.length(); i++)
{

    // s3 stores all substrings of s1
    String s3 = "";
    char[] s4 = s1.toCharArray();
    for (int j = i; j < s1.length(); j++)
    {
        s3 += s4[j];

        // check the presence of s3 in s2
        if (s2.indexOf(s3) != -1)
            ans++;
    }
}
return ans;
}

// Driver code
public static void main(String[] args)
{
    String s1 = "aab", s2 = "aaaab";
    System.out.println(countSubstrs(s1, s2));
}
}

// This code is contributed by ChitraNayal
```

## 蟒蛇 3

```
# Python 3 program to count number of substrings of s1
# present in s2.

# Function for counting no. of substring
# of s1 present in s2
def countSubstrs(s1, s2) :
    ans = 0
    for i in range(len(s1)) :
        s3 = ""

        # s3 stores all substrings of s1
        for j in range(i, len(s1)) :
            s3 += s1[j]

            # check the presence of s3 in s2
            if s2.find(s3) != -1 :
                ans += 1
    return ans

# Driver code
if __name__ == "__main__" :
    s1 = "aab"
    s2 = "aaaab"

    # function calling
    print(countSubstrs(s1, s2))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to count number of
// substrings of s1 present in s2.
using System;

class GFG
{
static int countSubstrs(String s1,
                        String s2)
{
int ans = 0;

for (int i = 0; i < s1.Length; i++)
{

    // s3 stores all substrings of s1
    String s3 = "";
    char[] s4 = s1.ToCharArray();
    for (int j = i; j < s1.Length; j++)
    {
        s3 += s4[j];

        // check the presence of s3 in s2
        if (s2.IndexOf(s3) != -1)
            ans++;
    }
}
return ans;
}

// Driver code
public static void Main(String[] args)
{
    String s1 = "aab", s2 = "aaaab";
    Console.WriteLine(countSubstrs(s1, s2));
}
}

// This code is contributed
// by Kirti_Mangal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number of
// substrings of s1 present in s2.

function countSubstrs($s1, $s2)
{
    $ans = 0;

    for ($i = 0; $i < strlen($s1); $i++)
    {

        // s3 stores all substrings of s1
        $s3 = "";
        for ($j = $i;
             $j < strlen($s1); $j++)
        {
            $s3 += $s1[$j];

            // check the presence of s3 in s2
            if (stripos($s2, $s3, 0) != -1)
                $ans++;
        }
    }
    return $ans;
}

// Driver code
$s1 = "aab";
$s2 = "aaaab";
echo countSubstrs($s1, $s2);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// javascript program to count number of
// substrings of s1 present in s2.

function countSubstrs( s1, s2)
{
var ans = 0;

for (var i = 0; i < s1.length; i++)
{

    // s3 stores all substrings of s1
    var s3 = "";
    var s4 = s1 ;
    for (var j = i; j < s1.length; j++)
    {
        s3 += s4[j];

        // check the presence of s3 in s2
        if (s2.indexOf(s3) != -1)
            ans++;
    }
}
return ans;
}

// Driver code

    var s1 = "aab", s2 = "aaaab";
    document.write(countSubstrs(s1, s2));

</script>
```

**Output:** 

```
6
```