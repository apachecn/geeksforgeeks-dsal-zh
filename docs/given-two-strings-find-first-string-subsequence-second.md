# 给定两个字符串，找出第一个字符串是否是第二个

的子序列

> 原文:[https://www . geesforgeks . org/given-two-string-find-first-string-subsequence-second/](https://www.geeksforgeeks.org/given-two-strings-find-first-string-subsequence-second/)

给定两个字符串 str1 和 str2，找出 str1 是否是 str2 的子序列。子序列是可以通过删除一些元素而不改变其余元素的顺序从另一个序列中派生出来的序列(来源: [wiki](http://en.wikipedia.org/wiki/Subsequence) )。预期时间复杂度是线性的。

**例:**

```
Input: str1 = "AXY", str2 = "ADXCPY"
Output: True (str1 is a subsequence of str2)

Input: str1 = "AXY", str2 = "YADXCP"
Output: False (str1 is not a subsequence of str2)

Input: str1 = "gksrek", str2 = "geeksforgeeks"
Output: True (str1 is a subsequence of str2)
```

想法很简单，我们从一边到另一边遍历两个字符串(比如从最右边的字符到最左边的)。如果我们找到一个匹配的字符，我们将在两个字符串中前进。否则，我们只能在 str2 中前进。

以下是上述思想的**递归**实现。

## C++

```
// Recursive C++ program to check
// if a string is subsequence
// of another string
#include <cstring>
#include <iostream>
using namespace std;

// Returns true if str1[] is a
// subsequence of str2[]. m is
// length of str1 and n is length of str2
bool isSubSequence(char str1[], char str2[],
                                 int m, int n)
{

    // Base Cases
    if (m == 0)
        return true;
    if (n == 0)
        return false;

    // If last characters of two
    // strings are matching
    if (str1[m - 1] == str2[n - 1])
        return isSubSequence(str1, str2, m - 1, n - 1);

    // If last characters are
    // not matching
    return isSubSequence(str1, str2, m, n - 1);
}

// Driver program to test methods of graph class
int main()
{
    char str1[] = "gksrek";
    char str2[] = "geeksforgeeks";
    int m = strlen(str1);
    int n = strlen(str2);
    isSubSequence(str1, str2, m, n) ? cout << "Yes "
                                    : cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program to check if a string
// is subsequence of another string
import java.io.*;

class SubSequence {
    // Returns true if str1[] is a subsequence of str2[]
    // m is length of str1 and n is length of str2
    static boolean isSubSequence(String str1, String str2,
                                 int m, int n)
    {
        // Base Cases
        if (m == 0)
            return true;
        if (n == 0)
            return false;

        // If last characters of two strings are matching
        if (str1.charAt(m - 1) == str2.charAt(n - 1))
            return isSubSequence(str1, str2, m - 1, n - 1);

        // If last characters are not matching
        return isSubSequence(str1, str2, m, n - 1);
    }

    // Driver program
    public static void main(String[] args)
    {
        String str1 = "gksrek";
        String str2 = "geeksforgeeks";
        int m = str1.length();
        int n = str2.length();
        boolean res = isSubSequence(str1, str2, m, n);
        if (res)
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// Contributed by Pramod Kumar
```

## 计算机编程语言

```
# Recursive Python program to check
# if a string is subsequence
# of another string

# Returns true if str1[] is a
# subsequence of str2[].

def isSubSequence(string1, string2, m, n):
    # Base Cases
    if m == 0:
        return True
    if n == 0:
        return False

    # If last characters of two
    # strings are matching
    if string1[m-1] == string2[n-1]:
        return isSubSequence(string1, string2, m-1, n-1)

    # If last characters are not matching
    return isSubSequence(string1, string2, m, n-1)

# Driver program to test the above function
string1 = "gksrek"
string2 = "geeksforgeeks"

if isSubSequence(string1, string2, len(string1), len(string2)):
    print "Yes"
else:
    print "No"

# This code is contributed by BHAVYA JAIN
```

## C#

```
// Recursive C# program to check if a string
// is subsequence of another string
using System;

class GFG {

    // Returns true if str1[] is a
    // subsequence of str2[] m is
    // length of str1 and n is length
    // of str2
    static bool isSubSequence(string str1,
                  string str2, int m, int n)
    {

        // Base Cases
        if (m == 0)
            return true;
        if (n == 0)
            return false;

        // If last characters of two strings
        // are matching
        if (str1[m-1] == str2[n-1])
            return isSubSequence(str1, str2,
                                    m-1, n-1);

        // If last characters are not matching
        return isSubSequence(str1, str2, m, n-1);
    }

    // Driver program
    public static void Main ()
    {
        string str1 = "gksrek";
        string str2 = "geeksforgeeks";
        int m = str1.Length;
        int n = str2.Length;
        bool res = isSubSequence(str1, str2, m, n);

        if(res)
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Recursive PHP program to check
// if a string is subsequence of
// another string

// Returns true if str1[] is a
// subsequence of str2[]. m is
// length of str1 and n is
// length of str2

function isSubSequence($str1, $str2,
                             $m, $n)
{
    // Base Cases
    if ($m == 0) return true;
    if ($n == 0) return false;

    // If last characters of two
    // strings are matching
    if ($str1[$m - 1] == $str2[$n - 1])
        return isSubSequence($str1, $str2,
                          $m - 1, $n - 1);

    // If last characters
    // are not matching
    return isSubSequence($str1, $str2,
                          $m, $n - 1);
}

// Driver Code
$str1= "gksrek";
$str2 = "geeksforgeeks";
$m = strlen($str1);
$n = strlen($str2);

$t = isSubSequence($str1, $str2, $m, $n) ?
                                   "Yes ":
                                     "No";

if($t = true)
    echo "Yes";
else
    echo "No";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Recursive Javascript program to check if
// a string is subsequence of another string

// Returns true if str1[] is a
// subsequence of str2[] m is
// length of str1 and n is length
// of str2
function isSubSequence(str1, str2, m, n)
{

    // Base Cases
    if (m == 0)
        return true;
    if (n == 0)
        return false;

    // If last characters of two strings
    // are matching
    if (str1[m - 1] == str2[n - 1])
        return isSubSequence(str1, str2,
                             m - 1, n - 1);

    // If last characters are not matching
    return isSubSequence(str1, str2, m, n - 1);
}

// Driver code
let str1 = "gksrek";
let str2 = "geeksforgeeks";
let m = str1.length;
let n = str2.length;
let res = isSubSequence(str1, str2, m, n);

if (res)
    document.write("Yes");
else
    document.write("No");

// This code is contributed by divyesh072019

</script>
```

**输出:**

```
Yes
```

以下是**迭代实现**:

## c++

```
// Iterative C++ program to check
// if a string is subsequence
// of another string
#include <cstring>
#include <iostream>
using namespace std;

// Returns true if str1[] is a
// subsequence of str2[]. m is
// length of str1 and n is length of str2
bool isSubSequence(char str1[], char str2[], int m, int n)
{
    int j = 0; // For index of str1 (or subsequence

    // Traverse str2 and str1, and
    // compare current character
    // of str2 with first unmatched char
    // of str1, if matched
    // then move ahead in str1
    for (int i = 0; i < n && j < m; i++)
        if (str1[j] == str2[i])
            j++;

    // If all characters of str1 were found in str2
    return (j == m);
}

// Driver program to test methods of graph class
int main()
{
    char str1[] = "gksrek";
    char str2[] = "geeksforgeeks";
    int m = strlen(str1);
    int n = strlen(str2);
    isSubSequence(str1, str2, m, n) ? cout << "Yes "
                                    : cout << "No";
    return 0;
}
```

## Java

```
// Iterative Java program to check if a string
// is subsequence of another string
import java.io.*;

class GFG {

    // Returns true if str1[] is a subsequence
    // of str2[] m is length of str1 and n is
    // length of str2
    static boolean isSubSequence(String str1, String str2,
                                 int m, int n)
    {
        int j = 0;

        // Traverse str2 and str1, and compare
        // current character of str2 with first
        // unmatched char of str1, if matched
        // then move ahead in str1
        for (int i = 0; i < n && j < m; i++)
            if (str1.charAt(j) == str2.charAt(i))
                j++;

        // If all characters of str1 were found
        // in str2
        return (j == m);
    }

    // Driver program to test methods of
    // graph class
    public static void main(String[] args)
    {
        String str1 = "gksrek";
        String str2 = "geeksforgeeks";
        int m = str1.length();
        int n = str2.length();
        boolean res = isSubSequence(str1, str2, m, n);

        if (res)
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Pramod Kumar
```

T17】PythonT2T21【c#T3

## PHP

T4

## Javascript

T5

**输出:**

```
Yes
```

问进:[雅高](https://practice.geeksforgeeks.org/company/Accolite/)[乐购](https://practice.geeksforgeeks.org/company/Tesco/)

上面两个实现的时间复杂度都是 O(n)，其中 n 是 str2 的长度。

本文由**萨钦·古普塔**供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论