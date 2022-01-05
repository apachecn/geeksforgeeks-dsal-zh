# 找出一个字符串在给定字符串中作为子序列出现的次数

> 原文:[https://www . geesforgeks . org/find-number-times-string-occurs-给定-string/](https://www.geeksforgeeks.org/find-number-times-string-occurs-given-string/)

给定两个字符串，找出第二个字符串在第一个字符串中出现的次数，无论是连续的还是不连续的。

**示例:**

```
Input:  
string a = "GeeksforGeeks"
string b = "Gks"

Output: 4

Explanation:  
The four strings are - (Check characters marked in bold)
GeeksforGeeks
GeeksforGeeks
GeeksforGeeks
GeeksforGeeks
```

如果我们仔细分析给定的问题，我们可以看到它可以很容易地分为子问题。其思想是从左侧或右侧开始逐一处理两个字符串的所有字符。让我们从右上角遍历，每对被遍历的字符有两种可能。

```
m: Length of str1 (first string)
n: Length of str2 (second string)

If last characters of two strings are same, 
   1\. We consider last characters and get count for remaining 
      strings. So we recur for lengths m-1 and n-1\. 
   2\. We can ignore last character of first string and 
      recurse for lengths m-1 and n.
else 
If last characters are not same, 
   We ignore last character of first string and 
   recurse for lengths m-1 and n.
```

以下是上述朴素递归解决方案的实现–

## C++

```
// A Naive recursive C++ program to find the number of
// times the second string occurs in the first string,
// whether continuous or discontinuous
#include <iostream>
using namespace std;

// Recursive function to find the number of times
// the second string occurs in the first string,
// whether continuous or discontinuous
int count(string a, string b, int m, int n)
{
    // If both first and second string is empty,
    // or if second string is empty, return 1
    if ((m == 0 && n == 0) || n == 0)
        return 1;

    // If only first string is empty and second
    // string is not empty, return 0
    if (m == 0)
        return 0;

    // If last characters are same
    // Recur for remaining strings by
    // 1\. considering last characters of both strings
    // 2\. ignoring last character of first string
    if (a[m - 1] == b[n - 1])
        return count(a, b, m - 1, n - 1) +
               count(a, b, m - 1, n);
    else
        // If last characters are different, ignore
        // last char of first string and recur for
        // remaining string
        return count(a, b, m - 1, n);
}

// Driver code
int main()
{
    string a = "GeeksforGeeks";
    string b = "Gks";

    cout << count(a, b, a.size(), b.size()) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Naive recursive java program to find the number of
// times the second string occurs in the first string,
// whether continuous or discontinuous
import java.io.*;

class GFG
{

    // Recursive function to find the number of times
    // the second string occurs in the first string,
    // whether continuous or discontinuous
    static int count(String a, String b, int m, int n)
    {
        // If both first and second string is empty,
        // or if second string is empty, return 1
        if ((m == 0 && n == 0) || n == 0)
            return 1;

        // If only first string is empty and
        // second string is not empty, return 0
        if (m == 0)
            return 0;

        // If last characters are same
        // Recur for remaining strings by
        // 1\. considering last characters of
        // both strings
        // 2\. ignoring last character of
        // first string
        if (a.charAt(m - 1) == b.charAt(n - 1))
            return count(a, b, m - 1, n - 1) +
                   count(a, b, m - 1, n);
        else
            // If last characters are different, 
            // ignore last char of first string
            // and recur for  remaining string
            return count(a, b, m - 1, n);
    }

    // Driver code
    public static void main (String[] args)
    {
        String a = "GeeksforGeeks";
        String b = "Gks";
        System.out.println( count(a, b, a.length(), b.length())) ;

    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# A Naive recursive Python program
# to find the number of times the
# second string occurs in the first
# string, whether continuous or
# discontinuous

# Recursive function to find the
# number of times the second string
# occurs in the first string,
# whether continuous or discontinuous
def count(a, b, m, n):

    # If both first and second string
    # is empty, or if second string
    # is empty, return 1
    if ((m == 0 and n == 0) or n == 0):
        return 1

    # If only first string is empty
    # and second string is not empty,
    # return 0
    if (m == 0):
        return 0

    # If last characters are same
    # Recur for remaining strings by
    # 1\. considering last characters
    #    of both strings
    # 2\. ignoring last character
    #    of first string
    if (a[m - 1] == b[n - 1]):
        return (count(a, b, m - 1, n - 1) +
                count(a, b, m - 1, n))
    else:

        # If last characters are different,
        # ignore last char of first string
        # and recur for remaining string
        return count(a, b, m - 1, n)

# Driver code
a = "GeeksforGeeks"
b = "Gks"

print(count(a, b, len(a),len(b)))

# This code is contributed by ash264
```

## C#

```
// A Naive recursive C# program to find the number of
// times the second string occurs in the first string,
// whether continuous or discontinuous
using System;

class GFG
{

    // Recursive function to find the number of times
    // the second string occurs in the first string,
    // whether continuous or discontinuous
    static int count(string a, string b, int m, int n)
    {
        // If both first and second string is empty,
        // or if second string is empty, return 1
        if ((m == 0 && n == 0) || n == 0)
            return 1;

        // If only first string is empty and
        // second string is not empty, return 0
        if (m == 0)
            return 0;

        // If last characters are same
        // Recur for remaining strings by
        // 1\. considering last characters of
        // both strings
        // 2\. ignoring last character of
        // first string
        if (a[m - 1] == b[n - 1])
            return count(a, b, m - 1, n - 1) +
                   count(a, b, m - 1, n);
        else
            // If last characters are different, 
            // ignore last char of first string
            // and recur for  remaining string
            return count(a, b, m - 1, n);
    }

    // Driver code
    public static void Main ()
    {
        string a = "GeeksforGeeks";
        string b = "Gks";
        Console.Write( count(a, b, a.Length, b.Length) );

    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Naive recursive PHP program to find the number of
// times the second string occurs in the first string,
// whether continuous or discontinuous

// Recursive function to find the number of times
// the second string occurs in the first string,
// whether continuous or discontinuous
function count_1($a, $b, $m, $n)
{
    // If both first and second string is empty,
    // or if second string is empty, return 1
    if (($m == 0 && $n == 0) || $n == 0)
        return 1;

    // If only first string is empty and second
    // string is not empty, return 0
    if ($m == 0)
        return 0;

    // If last characters are same
    // Recur for remaining strings by
    // 1\. considering last characters of both strings
    // 2\. ignoring last character of first string
    if ($a[$m - 1] == $b[$n - 1])
        return count_1($a, $b, $m - 1, $n - 1) +
               count_1($a, $b, $m - 1, $n);
    else
        // If last characters are different, ignore
        // last char of first string and recur for
        // remaining string
        return count_1($a, $b, $m - 1, $n);
}

// Driver code

$a = "GeeksforGeeks";
$b = "Gks";
echo count_1($a, $b, strlen($a), strlen($b)) ."\n";
return 0;
?>
```

## java 描述语言

```
<script>
// A Naive recursive javascript program to find the number of
// times the second string occurs in the first string,
// whether continuous or discontinuous

    // Recursive function to find the number of times
    // the second string occurs in the first string,
    // whether continuous or discontinuous
    function count( a,  b , m , n)
    {

        // If both first and second string is empty,
        // or if second string is empty, return 1
        if ((m == 0 && n == 0) || n == 0)
            return 1;

        // If only first string is empty and
        // second string is not empty, return 0
        if (m == 0)
            return 0;

        // If last characters are same
        // Recur for remaining strings by
        // 1\. considering last characters of
        // both strings
        // 2\. ignoring last character of
        // first string
        if (a[m - 1] == b[n - 1])
            return count(a, b, m - 1, n - 1) + count(a, b, m - 1, n);
        else

            // If last characters are different,
            // ignore last char of first string
            // and recur for remaining string
            return count(a, b, m - 1, n);
    }

    // Driver code
    var a = "GeeksforGeeks";
    var b = "Gks";
    document.write(count(a, b, a.length, b.length));

// This code is contributed by Amit Katiyar
</script>
```

**输出:**

```
4
```

上述解的时间复杂度是指数的。如果仔细分析，可以看到很多子问题一次又一次的解决。由于相同的子问题被再次调用，所以这个问题具有重叠子问题的性质。所以这个问题同时具有动态规划问题的两个性质(参见[这个](https://www.geeksforgeeks.org/dynamic-programming-set-1/)和[这个](https://www.geeksforgeeks.org/dynamic-programming-set-2-optimal-substructure-property/))。像其他典型的动态规划问题一样，可以通过构造存储子问题结果的临时数组来避免相同子问题的重新计算。

下面是它使用动态编程的实现–

## C++

```
// A Dynamic Programming based C++ program to find the
// number of times the second string occurs in the first
// string, whether continuous or discontinuous
#include <iostream>
using namespace std;

// Iterative DP function to find the number of times
// the second string occurs in the first string,
// whether continuous or discontinuous
int count(string a, string b)
{
    int m = a.length();
    int n = b.length();

    // Create a table to store results of sub-problems
    int lookup[m + 1][n + 1] = { { 0 } };

    // If first string is empty
    for (int i = 0; i <= n; ++i)
        lookup[0][i] = 0;

    // If second string is empty
    for (int i = 0; i <= m; ++i)
        lookup[i][0] = 1;

    // Fill lookup[][] in bottom up manner
    for (int i = 1; i <= m; i++)
    {
        for (int j = 1; j <= n; j++)
        {
            // If last characters are same, we have two
            // options -
            // 1\. consider last characters of both strings
            //    in solution
            // 2\. ignore last character of first string
            if (a[i - 1] == b[j - 1])
                lookup[i][j] = lookup[i - 1][j - 1] +
                               lookup[i - 1][j];

            else
                // If last character are different, ignore
                // last character of first string
                lookup[i][j] = lookup[i - 1][j];
        }
    }

    return lookup[m][n];
}

// Driver code
int main()
{
    string a = "GeeksforGeeks";
    string b = "Gks";

    cout << count(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Dynamic Programming based
// Java program to find the
// number of times the second
// string occurs in the first
// string, whether continuous
// or discontinuous
import java.io.*;

class GFG
{

// Iterative DP function to
// find the number of times
// the second string occurs
// in the first string, whether
// continuous or discontinuous
static int count(String a, String b)
{
    int m = a.length();
    int n = b.length();

    // Create a table to store
    // results of sub-problems
    int lookup[][] = new int[m + 1][n + 1];

    // If first string is empty
    for (int i = 0; i <= n; ++i)
        lookup[0][i] = 0;

    // If second string is empty
    for (int i = 0; i <= m; ++i)
        lookup[i][0] = 1;

    // Fill lookup[][] in
    // bottom up manner
    for (int i = 1; i <= m; i++)
    {
        for (int j = 1; j <= n; j++)
        {
            // If last characters are
            // same, we have two options -
            // 1\. consider last characters
            //    of both strings in solution
            // 2\. ignore last character
            //    of first string
            if (a.charAt(i - 1) == b.charAt(j - 1))
                lookup[i][j] = lookup[i - 1][j - 1] +
                               lookup[i - 1][j];

            else
                // If last character are
                // different, ignore last
                // character of first string
                lookup[i][j] = lookup[i - 1][j];
        }
    }

    return lookup[m][n];
}

// Driver Code
public static void main (String[] args)
{
    String a = "GeeksforGeeks";
    String b = "Gks";

    System.out.println(count(a, b));
}
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# A Dynamic Programming based Python
# program to find the number of times
# the second string occurs in the first
# string, whether continuous or discontinuous

# Iterative DP function to find the 
# number of times the second string
# occurs in the first string,
# whether continuous or discontinuous
def count(a, b):
    m = len(a)
    n = len(b)

    # Create a table to store results of sub-problems
    lookup = [[0] * (n + 1) for i in range(m + 1)]

    # If first string is empty
    for i in range(n+1):
        lookup[0][i] = 0

    # If second string is empty
    for i in range(m + 1):
        lookup[i][0] = 1

    # Fill lookup[][] in bottom up manner
    for i in range(1, m + 1):
        for j in range(1, n + 1):

            # If last characters are same, 
            # we have two options -
            # 1\. consider last characters of 
            # both strings in solution
            # 2\. ignore last character of first string
            if a[i - 1] == b[j - 1]:
                lookup[i][j] = lookup[i - 1][j - 1] + lookup[i - 1][j]

            else:
                # If last character are different, ignore
                # last character of first string
                lookup[i][j] = lookup[i - 1][j]

    return lookup[m][n]

# Driver code
if __name__ == '__main__':
    a = "GeeksforGeeks"
    b = "Gks"

    print(count(a, b))

# this code is contributed by PranchalK
```

## C#

```
// A Dynamic Programming based
// C# program to find the
// number of times the second
// string occurs in the first
// string, whether continuous
// or discontinuous
using System;

class GFG
{

// Iterative DP function to
// find the number of times
// the second string occurs
// in the first string, whether
// continuous or discontinuous
static int count(String a, String b)
{
    int m = a.Length;
    int n = b.Length;

    // Create a table to store
    // results of sub-problems
    int[,] lookup = new int[m + 1, n + 1];

    // If first string is empty
    for (int i = 0; i <= n; ++i)
        lookup[0, i] = 0;

    // If second string is empty
    for (int i = 0; i <= m; ++i)
        lookup[i, 0] = 1;

    // Fill lookup[][] in
    // bottom up manner
    for (int i = 1; i <= m; i++)
    {
        for (int j = 1; j <= n; j++)
        {
            // If last characters are
            // same, we have two options -
            // 1\. consider last characters
            // of both strings in solution
            // 2\. ignore last character
            // of first string
            if (a[i - 1] == b[j - 1])
                lookup[i, j] = lookup[i - 1, j - 1] +
                            lookup[i - 1, j];

            else
                // If last character are
                // different, ignore last
                // character of first string
                lookup[i, j] = lookup[i - 1, j];
        }
    }

    return lookup[m, n];
}

// Driver Code
public static void Main()
{
    String a = "GeeksforGeeks";
    String b = "Gks";

    Console.WriteLine(count(a, b));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Dynamic Programming based PHP program to find the
// number of times the second string occurs in the first
// string, whether continuous or discontinuous

// Iterative DP function to find the number of times
// the second string occurs in the first string,
// whether continuous or discontinuous
function count1($a, $b)
{
    $m = strlen($a);
    $n = strlen($b);

    // Create a table to store results of sub-problems
    $lookup = array_fill(0, $m + 1, array_fill(0, $n + 1, 0));

    // If second string is empty
    for ($i = 0; $i <= $m; ++$i)
        $lookup[$i][0] = 1;

    // Fill lookup[][] in bottom up manner
    for ($i = 1; $i <= $m; $i++)
    {
        for ($j = 1; $j <= $n; $j++)
        {
            // If last characters are same, we have two
            // options -
            // 1\. consider last characters of both strings
            // in solution
            // 2\. ignore last character of first string
            if ($a[$i - 1] == $b[$j - 1])
                $lookup[$i][$j] = $lookup[$i - 1][$j - 1] +
                            $lookup[$i - 1][$j];

            else
                // If last character are different, ignore
                // last character of first string
                $lookup[$i][$j] = $lookup[$i - 1][$j];
        }
    }

    return $lookup[$m][$n];
}

// Driver code

    $a = "GeeksforGeeks";
    $b = "Gks";

    echo count1($a, $b);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

// A Dynamic Programming based
// Javascript program to find the
// number of times the second
// string occurs in the first
// string, whether continuous
// or discontinuous

// Iterative DP function to
// find the number of times
// the second string occurs
// in the first string, whether
// continuous or discontinuous
function count(a, b)
{
    var m = a.length;
    var n = b.length;

    // Create a table to store
    // results of sub-problems
    var lookup = Array(m + 1);
    for(var i = 0; i < m + 1; i++)
        lookup[i] = Array(n + 1).fill(0);

    // If first string is empty
    for(i = 0; i <= n; ++i)
        lookup[0][i] = 0;

    // If second string is empty
    for(i = 0; i <= m; ++i)
        lookup[i][0] = 1;

    // Fill lookup in
    // bottom up manner
    for(i = 1; i <= m; i++)
    {
        for(j = 1; j <= n; j++)
        {

            // If last characters are
            // same, we have two options -
            // 1\. consider last characters
            // of both strings in solution
            // 2\. ignore last character
            // of first string
            if (a.charAt(i - 1) == b.charAt(j - 1))
                lookup[i][j] = lookup[i - 1][j - 1] +
                               lookup[i - 1][j];
            else

                // If last character are
                // different, ignore last
                // character of first string
                lookup[i][j] = lookup[i - 1][j];
        }
    }
    return lookup[m][n];
}

// Driver Code
var a = "GeeksforGeeks";
var b = "Gks";

document.write(count(a, b));

// This code is contributed by gauravrajput1

</script>
```

**输出:**

```
4
```

**以上解的时间复杂度**为 O(MN)。
T3】辅助空间所使用的程序是 O(MN)。

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.GeeksforGeeks.org](http://www.contribute.GeeksforGeeks.org)写一篇文章或者把你的文章邮寄到 contribute@GeeksforGeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。