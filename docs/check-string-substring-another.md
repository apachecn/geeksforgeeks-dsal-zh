# 检查一个字符串是否是另一个

的子字符串

> 原文:[https://www . geesforgeks . org/check-string-substring-other/](https://www.geeksforgeeks.org/check-string-substring-another/)

给定两个字符串 s1 和 s2，找出 s1 是否是 s2 的子串。如果是，返回第一次出现的索引，否则返回-1。

**示例:**

```
Input: s1 = "for", s2 = "geeksforgeeks"
Output: 5
Explanation:
String "for" is present as a substring
of s2.

Input: s1 = "practice", s2 = "geeksforgeeks"
Output: -1.
Explanation:
There is no occurrence of "practice" in
"geeksforgeeks"
```

**<u>简单方法:</u>** 想法是从头到尾运行一个循环，对于给定字符串中的每个索引，检查子字符串是否可以从该索引形成。这可以通过运行遍历给定字符串的嵌套循环来完成，并在该循环中运行另一个循环来检查每个索引中的子字符串。
*例如，*认为有一个长度为 N 的字符串和一个长度为 M 的子串，然后运行一个嵌套循环，其中外循环从 0 到(N-M)运行，内循环从 0 到 M 运行，对于每个索引，检查内循环遍历的子串是否是给定的子串。

## C++

```
// C++ program to check if a string is
// substring of other.
#include <bits/stdc++.h>
using namespace std;

// Returns true if s1 is substring of s2
int isSubstring(string s1, string s2)
{
    int M = s1.length();
    int N = s2.length();

    /* A loop to slide pat[] one by one */
    for (int i = 0; i <= N - M; i++) {
        int j;

        /* For current index i, check for
 pattern match */
        for (j = 0; j < M; j++)
            if (s2[i + j] != s1[j])
                break;

        if (j == M)
            return i;
    }

    return -1;
}

/* Driver code */
int main()
{
    string s1 = "for";
    string s2 = "geeksforgeeks";
    int res = isSubstring(s1, s2);
    if (res == -1)
        cout << "Not present";
    else
        cout << "Present at index " << res;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a string is
// substring of other.
class GFG {

    // Returns true if s1 is substring of s2
    static int isSubstring(
        String s1, String s2)
    {
        int M = s1.length();
        int N = s2.length();

        /* A loop to slide pat[] one by one */
        for (int i = 0; i <= N - M; i++) {
            int j;

            /* For current index i, check for
            pattern match */
            for (j = 0; j < M; j++)
                if (s2.charAt(i + j)
                    != s1.charAt(j))
                    break;

            if (j == M)
                return i;
        }

        return -1;
    }

    /* Driver code */
    public static void main(String args[])
    {
        String s1 = "for";
        String s2 = "geeksforgeeks";

        int res = isSubstring(s1, s2);

        if (res == -1)
            System.out.println("Not present");
        else
            System.out.println(
                "Present at index "
                + res);
    }
}

// This code is contributed by JaideepPyne.
```

## 蟒蛇 3

```
# Python3 program to check if
# a string is substring of other.

# Returns true if s1 is substring of s2
def isSubstring(s1, s2):
    M = len(s1)
    N = len(s2)

    # A loop to slide pat[] one by one
    for i in range(N - M + 1):

        # For current index i,
        # check for pattern match
        for j in range(M):
            if (s2[i + j] != s1[j]):
                break

        if j + 1 == M :
            return i

    return -1

# Driver Code
if __name__ == "__main__":
    s1 = "for"
    s2 = "geeksforgeeks"
    res = isSubstring(s1, s2)
    if res == -1 :
        print("Not present")
    else:
        print("Present at index " + str(res))

# This code is contributed by ChitraNayal
```

## C#

```
// C# program to check if a string is
// substring of other.
using System;
class GFG {

    // Returns true if s1 is substring of s2
    static int isSubstring(string s1, string s2)
    {
        int M = s1.Length;
        int N = s2.Length;

        /* A loop to slide pat[] one by one */
        for (int i = 0; i <= N - M; i++) {
            int j;

            /* For current index i, check for
            pattern match */
            for (j = 0; j < M; j++)
                if (s2[i + j] != s1[j])
                    break;

            if (j == M)
                return i;
        }

        return -1;
    }

    /* Driver code */
    public static void Main()
    {
        string s1 = "for";
        string s2 = "geeksforgeeks";

        int res = isSubstring(s1, s2);

        if (res == -1)
            Console.Write("Not present");
        else
            Console.Write("Present at index "
                          + res);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a
// string is substring of other.

// Returns true if s1 is substring of s2
function isSubstring($s1, $s2)
{
    $M = strlen($s1);
    $N = strlen($s2);

    // A loop to slide
    // pat[] one by one
    for ($i = 0; $i <= $N - $M; $i++)
    {
        $j = 0;

        // For current index i,
        // check for pattern match
        for (; $j < $M; $j++)
            if ($s2[$i + $j] != $s1[$j])
                break;

        if ($j == $M)
            return $i;
    }

    return -1;
}

// Driver Code
$s1 = "for";
$s2 = "geeksforgeeks";
$res = isSubstring($s1, $s2);
if ($res == -1)
    echo "Not present";
else
    echo "Present at index " . $res;

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to check if a string is
// substring of other.

// Returns true if s1 is substring of s2
function isSubstring(s1, s2)
{
    var M = s1.length;
    var N = s2.length;

    /* A loop to slide pat[] one by one */
    for (var i = 0; i <= N - M; i++) {
        var j;

        /* For current index i, check for
 pattern match */
        for (j = 0; j < M; j++)
            if (s2[i + j] != s1[j])
                break;

        if (j == M)
            return i;
    }

    return -1;
}

/* Driver code */
var s1 = "for";
var s2 = "geeksforgeeks";
var res = isSubstring(s1, s2);
if (res == -1)
    document.write( "Not present");
else
    document.write( "Present at index " + res);

</script>
```

**Output**

```
Present at index 5
```