# 检查两个字符串之间的编辑距离是否为 1

> 原文:[https://www . geeksforgeeks . org/check-if-two-给定字符串处于编辑距离-one/](https://www.geeksforgeeks.org/check-if-two-given-strings-are-at-edit-distance-one/)

两个字符串之间的编辑是以下更改之一。

1.  添加字符
2.  删除字符
3.  改变一个角色

给定两个字符串 s1 和 s2，只需编辑一次，就可以知道 s1 是否可以转换为 s2。预期的时间复杂度是 O(m+n)，其中 m 和 n 是两个字符串的长度。
示例:

```
Input:  s1 = "geeks", s2 = "geek"
Output: yes
Number of edits is 1

Input:  s1 = "geeks", s2 = "geeks"
Output: no
Number of edits is 0

Input:  s1 = "geaks", s2 = "geeks"
Output: yes
Number of edits is 1

Input:  s1 = "peaks", s2 = "geeks"
Output: no
Number of edits is 2
```

一个**简单的解决方案**是使用动态编程找到[编辑距离。如果距离为 1，则返回真，否则返回假。这个解决方案的时间复杂度是 O(n <sup>2</sup> )
一个**高效的解决方案**是同时遍历两个字符串并跟踪不同字符的计数。下面是完整的算法。](https://www.geeksforgeeks.org/dynamic-programming-set-5-edit-distance/) 

```
Let the input strings be s1 and s2 and lengths of input 
strings be m and n respectively.

1) If difference between m an n is more than 1, 
     return false.
2) Initialize count of edits as 0.
3) Start traversing both strings from first character.
    a) If current characters don't match, then
       (i)   Increment count of edits
       (ii)  If count becomes more than 1, return false
       (iii) If length of one string is more, then only
             possible  edit is to remove a character.
             Therefore, move ahead in larger string.
       (iv)  If length is same, then only possible edit
             is to  change a character. Therefore, move
             ahead in both strings. 
    b) Else, move ahead in both strings. 
```

以下是上述思路的实现:

## C++

```
// C++ program to check if given two strings are
// at distance one.
#include <bits/stdc++.h>
using namespace std;

// Returns true if edit distance between s1 and
// s2 is one, else false
bool isEditDistanceOne(string s1, string s2)
{
    // Find lengths of given strings
    int m = s1.length(), n = s2.length();

    // If difference between lengths is more than
    // 1, then strings can't be at one distance
    if (abs(m - n) > 1)
        return false;

    int count = 0; // Count of edits

    int i = 0, j = 0;
    while (i < m && j < n)
    {
        // If current characters don't match
        if (s1[i] != s2[j])
        {
            if (count == 1)
                return false;

            // If length of one string is
            // more, then only possible edit
            // is to remove a character
            if (m > n)
                i++;
            else if (m< n)
                j++;
            else //Iflengths of both strings is same
            {
                i++;
                j++;
            }

            // Increment count of edits
            count++;
        }

        else // If current characters match
        {
            i++;
            j++;
        }
    }

    // If last character is extra in any string
    if (i < m || j < n)
        count++;

    return count == 1;
}

// Driver program
int main()
{
   string s1 = "gfg";
   string s2 = "gf";
   isEditDistanceOne(s1, s2)?
           cout << "Yes": cout << "No";
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if given
// two strings are at distance one.
class GFG
{
// Returns true if edit distance
// between s1 and s2 is one, else false
static boolean isEditDistanceOne(String s1,
                                 String s2)
{
    // Find lengths of given strings
    int m = s1.length(), n = s2.length();

    // If difference between lengths is
    // more than 1, then strings can't
    // be at one distance
    if (Math.abs(m - n) > 1)
        return false;

    int count = 0; // Count of edits

    int i = 0, j = 0;
    while (i < m && j < n)
    {
        // If current characters don't match
        if (s1.charAt(i) != s2.charAt(j))
        {
            if (count == 1)
                return false;

            // If length of one string is
            // more, then only possible edit
            // is to remove a character
            if (m > n)
                i++;
            else if (m< n)
                j++;
            else // Iflengths of both strings
                // is same
            {
                i++;
                j++;
            }

            // Increment count of edits
            count++;
        }

        else // If current characters match
        {
            i++;
            j++;
        }
    }

    // If last character is extra
    // in any string
    if (i < m || j < n)
        count++;

    return count == 1;
}

// driver code
public static void main (String[] args)
{
    String s1 = "gfg";
    String s2 = "gf";
    if(isEditDistanceOne(s1, s2))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Anant Agarwal.
```

## 计算机编程语言

```
# Python program to check if given two strings are
# at distance one

# Returns true if edit distance between s1 and s2 is
# one, else false
def isEditDistanceOne(s1, s2):

    # Find lengths of given strings
    m = len(s1)
    n = len(s2)

    # If difference between lengths is more than 1,
    # then strings can't be at one distance
    if abs(m - n) > 1:
        return false

    count = 0    # Count of isEditDistanceOne

    i = 0
    j = 0
    while i < m and j < n:
        # If current characters dont match
        if s1[i] != s2[j]:
            if count == 1:
                return false

            # If length of one string is
            # more, then only possible edit
            # is to remove a character
            if m > n:
                i+=1
            elif m < n:
                j+=1
            else:    # If lengths of both strings is same
                i+=1
                j+=1

            # Increment count of edits
            count+=1

        else:    # if current characters match
            i+=1
            j+=1

    # if last character is extra in any string
    if i < m or j < n:
        count+=1

    return count == 1

# Driver program
s1 = "gfg"
s2 = "gf"
if isEditDistanceOne(s1, s2):
    print "Yes"
else:
    print "No"

# This code is contributed by Bhavya Jain
```

## C#

```
// C# program to check if given
// two strings are at distance one.
using System;

class GFG
{

// Returns true if edit distance
// between s1 and s2 is one, else false
static bool isEditDistanceOne(String s1,
                              String s2)
{

    // Find lengths of given strings
    int m = s1.Length, n = s2.Length;

    // If difference between lengths is
    // more than 1, then strings can't
    // be at one distance
    if (Math.Abs(m - n) > 1)
        return false;

        // Count of edits
        int count = 0;
        int i = 0, j = 0;

    while (i < m && j < n)
    {
        // If current characters
        // don't match
        if (s1[i] != s2[j])
        {
            if (count == 1)
                return false;

            // If length of one string is
            // more, then only possible edit
            // is to remove a character
            if (m > n)
                i++;
            else if (m< n)
                j++;

             // If lengths of both
             // strings is same
            else
            {
                i++;
                j++;
            }

            // Increment count of edits
            count++;
        }

        // If current characters match
        else
        {
            i++;
            j++;
        }
    }

    // If last character is extra
    // in any string
    if (i < m || j < n)
        count++;

    return count == 1;
}

// Driver code
public static void Main ()
{
    String s1 = "gfg";
    String s2 = "gf";
    if(isEditDistanceOne(s1, s2))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if given
// two strings are at distance one.

// Returns true if edit distance
// between s1 and s2 is one, else
// false
function isEditDistanceOne($s1, $s2)
{

    // Find lengths of given strings
    $m = strlen($s1);
    $n = strlen($s2);

    // If difference between
    // lengths is more than
    // 1, then strings can't
    // be at one distance
    if (abs($m - $n) > 1)
        return false;

    // Count of edits
    $count = 0;

    $i = 0; $j = 0;
    while ($i < $m && $j < $n)
    {
        // If current characters
        // don't match
        if ($s1[$i] != $s2[$j])
        {
            if ($count == 1)
                return false;

            // If length of one string is
            // more, then only possible edit
            // is to remove a character
            if ($m > $n)
                $i++;
            else if ($m< $n)
                $j++;

             // If lengths of both
             // strings is same
            else
            {
                $i++;
                $j++;
            }

            // Increment count of edits
            $count++;
        }

        // If current characters
        // match
        else
        {
            $i++;
            $j++;
        }
    }

    // If last character is
    // extra in any string
    if ($i < $m || $j < $n)
        $count++;

    return $count == 1;
}

// Driver Code
$s1 = "gfg";
$s2 = "gf";
if(isEditDistanceOne($s1, $s2))
    echo "Yes";
else
    echo "No";

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
    // Javascript program to check if given
    // two strings are at distance one.

    // Returns true if edit distance
    // between s1 and s2 is one, else false
    function isEditDistanceOne(s1, s2)
    {

        // Find lengths of given strings
        let m = s1.length, n = s2.length;

        // If difference between lengths is
        // more than 1, then strings can't
        // be at one distance
        if (Math.abs(m - n) > 1)
            return false;

            // Count of edits
            let count = 0;
            let i = 0, j = 0;

        while (i < m && j < n)
        {
            // If current characters
            // don't match
            if (s1[i] != s2[j])
            {
                if (count == 1)
                    return false;

                // If length of one string is
                // more, then only possible edit
                // is to remove a character
                if (m > n)
                    i++;
                else if (m< n)
                    j++;

                 // If lengths of both
                 // strings is same
                else
                {
                    i++;
                    j++;
                }

                // Increment count of edits
                count++;
            }

            // If current characters match
            else
            {
                i++;
                j++;
            }
        }

        // If last character is extra
        // in any string
        if (i < m || j < n)
            count++;

        return count == 1;
    }

    let s1 = "gfg";
    let s2 = "gf";
    if(isEditDistanceOne(s1, s2))
        document.write("Yes");
    else
        document.write("No");

    // This code is contributed by decode2207.
</script>
```

输出:

```
Yes
```

时间复杂度:O(n)
辅助空间:O(1)
感谢 Gaurav Ahirwar 提出上述解决方案。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息