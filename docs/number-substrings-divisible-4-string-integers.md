# 整数串中可被 4 整除的子串数

> 原文:[https://www . geesforgeks . org/number-substrings-整除-4-string-integers/](https://www.geeksforgeeks.org/number-substrings-divisible-4-string-integers/)

给定一个由 0 到 9 的整数组成的字符串。任务是计算子串的数量，当转换为整数时，这些子串可以被 4 整除。子字符串可能包含前导零。

**示例:**

```
Input : "124"
Output : 4
Substrings divisible by 4 are  "12", "4", "24", "124" .

Input : "04"
Output : 3
Substring divisible by 4 are "0", "4", "04" .
```

**方法一:(蛮力)**思路是[找到给定字符串的所有子串](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，[检查子串是否能被 4 整除。](https://www.geeksforgeeks.org/check-large-number-divisible-4-not/)
**时间复杂度:O(**

```
*** QuickLaTeX cannot compile formula:

*** Error message:
Error: Nothing to show, formula is empty

```

**)。**

**高效解决方案:**如果一个数的最后两位数可被 4 整除，并且可被 4 整除的一位数是 4、8 和 0，则该数可被 4 整除。因此，为了计算可被 4 整除的子串的数量，我们首先计算字符串中 0、4 和 8 的数量。然后，我们将所有两个连续字符配对，并将其转换为整数。把它转换成整数后，我们检查它是否能被 4 整除。如果它能被 4 整除，那么所有以最后两个字符结尾的子串都可以被 4 整除。现在，**这样的子串数量基本上是对**第 1 个字符的索引。为了更清楚，考虑字符串“14532465”，那么可能的对是“14”、“45”、“53”、“32”、“24”、“46”、“65”。在这些对中，当转换成整数时，只有“32”和“24”可被 4 整除。然后，可被 4 整除的子串(长度> = 2)必须以“32”或“24”结尾。因此，以“32”结尾的子串的数量是“14532”、“4532”、“532”、“32”，即 4，索引“3”也是 4。类似地，以“24”结尾的子字符串数量是 5。

这样我们就得到一个 O(n)解。下面是这个方法的实现。

## C++

```
// C++ program to count number of substrings
// divisible by 4.
#include <bits/stdc++.h>
using namespace std;

int countDivisbleby4(char s[])
{
    int n = strlen(s);

    // In the first loop we will count number of
    // 0's, 4's and 8's present in the string
    int count = 0;
    for (int i = 0; i < n; ++i)
    if (s[i] == '4' || s[i] == '8' || s[i] == '0')
            count++ ;

    // In second loop we will convert pairs
    // of two consecutive characters into
    // integer and store it in variable h .
    // Then we check whether h is divisible by 4
    // or not . If h is divisible we increases
    // the count with ( i + 1 ) as index of
    // first character of pair
    for (int i = 0; i < n - 1; ++i) {
    int h = ( s[i] - '0' ) * 10 + ( s[i+1] - '0' );
    if (h % 4 == 0)
        count = count + i + 1 ;
    }

    return count;
}

// Driver code to test above function
int main()
{
    char s[] = "124";
    cout << countDivisbleby4(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of substrings
// divisible by 4
import java.io.*;

class GFG
{
    // Function to count number of substrings
    // divisible by 4
    static int countDivisbleby4(String s)
    {
        int n = s.length();

        // In the first loop we will count number of
        // 0's, 4's and 8's present in the string
        int count = 0;
        for (int i = 0; i < n; ++i)
            if (s.charAt(i) == '4' || s.charAt(i) == '8' || s.charAt(i) == '0')
                count++ ;

        // In second loop we will convert pairs
        // of two consecutive characters into
        // integer and store it in variable h .
        // Then we check whether h is divisible by 4
        // or not . If h is divisible we increases
        // the count with ( i + 1 ) as index of
        // first character of pair
        for (int i = 0; i < n - 1; ++i)
        {
            int h = ( s.charAt(i) - '0' ) * 10 + ( s.charAt(i+1) - '0' );
            if (h % 4 == 0) 
                count = count + i + 1 ;
        }

        return count;
    }

    // driver program
    public static void main (String[] args)
    {
        String s = "124";
        System.out.println(countDivisbleby4(s));
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python3 program to count the number of substrings
# divisible by 4.

def countDivisbleby4(s):
    n = len(s)

    # In the first loop we will count number of
    # 0's, 4's and 8's present in the string
    count = 0;
    for i in range(0,n,1):
        if (s[i] == '4' or s[i] == '8' or s[i] == '0'):
            count += 1

    # In second loop we will convert pairs
    # of two consecutive characters into
    # integer and store it in variable h .
    # Then we check whether h is divisible by 4
    # or not . If h is divisible we increases
    # the count with ( i + 1 ) as index of
    # first character of pair
    for i in range(0,n - 1,1):
        h = (ord(s[i]) - ord('0')) * 10 + (ord(s[i+1]) - ord('0'))
        if (h % 4 == 0):
            count = count + i + 1

    return count

# Driver code to test above function
if __name__ == '__main__':
    s = ['1','2','4']
    print(countDivisbleby4(s))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to count number of
// substrings divisible by 4
using System;

public class GFG
{

    // Function to count number of
    // substrings divisible by 4
    static int countDivisbleby4(string s)
    {
        int n = s.Length;

        // In the first loop we will count
        // number of 0's, 4's and 8's present 
        // in the string
        int count = 0;
        for (int i = 0; i < n; ++i)

            if (s[i] == '4' || s[i] == '8'
                            || s[i] == '0')
                count++ ;

        // In second loop we will convert pairs
        // of two consecutive characters into
        // integer and store it in variable h .
        // Then we check whether h is divisible
        // by 4 or not . If h is divisible, we
        // increases the count with ( i + 1 )
        // as index of first character of pair
        for (int i = 0; i < n - 1; ++i)
        {
            int h = (s[i] - '0' ) * 10 +
                    (s[i + 1] - '0' );
            if (h % 4 == 0)
                count = count + i + 1 ;
        }

        return count;
    }

    // Driver Code
    public static void Main ()
    {
        string s = "124";
        Console.WriteLine(countDivisbleby4(s));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number
// of substrings divisible by 4.

function countDivisbleby4( $s)
{
    $n = strlen($s);

    // In the first loop we
    // will count number of
    // 0's, 4's and 8's present
    // in the string
    $count = 0;
    for($i = 0; $i < $n; ++$i)
    if ($s[$i] == '4' or $s[$i] == '8'
                    or $s[$i] == '0')
            $count++ ;

    // In second loop we will convert pairs
    // of two consecutive characters into
    // integer and store it in variable h .
    // Then we check whether h is divisible by 4
    // or not . If h is divisible we increases
    // the count with ( i + 1 ) as index of
    // first character of pair
    for ( $i = 0; $i < $n - 1; ++$i)
    {
        $h = ( $s[$i] - '0' ) * 10 +
                 ( $s[$i+1] - '0' );
        if ($h % 4 == 0)
            $count = $count + $i + 1 ;
    }

    return $count;
}

    // Driver Code
    $s = "124";
    echo countDivisbleby4($s);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to count number
// of substrings divisible by 4.
function countDivisbleby4(s)
{
    let n = s.length;

    // In the first loop we
    // will count number of
    // 0's, 4's and 8's present
    // in the string
    let count = 0;
    for(let i = 0; i < n; ++i)
        if (s[i] == '4' || s[i] == '8' ||
            s[i] == '0')
            count++;

    // In second loop we will convert pairs
    // of two consecutive characters into
    // integer and store it in variable h .
    // Then we check whether h is divisible by 4
    // or not . If h is divisible we increases
    // the count with ( i + 1 ) as index of
    // first character of pair
    for(let i = 0; i < n - 1; ++i)
    {
        let h = (s[i] - '0') * 10 +
                (s[i + 1] - '0');

        if (h % 4 == 0)
            count = count + i + 1 ;
    }
    return count;
}

// Driver Code
let s = "124";

document.write(countDivisbleby4(s));

// This code is contributed by _saurabh_jaiswal.

</script>
```

**输出:**

```
4
```

本文由 **Surya Priy** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。