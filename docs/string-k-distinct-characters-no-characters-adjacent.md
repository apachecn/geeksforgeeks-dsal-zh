# k 个不同字符且相邻字符不相同的字符串

> 原文:[https://www . geeksforgeeks . org/string-k-distinct-characters-no-characters-相邻/](https://www.geeksforgeeks.org/string-k-distinct-characters-no-characters-adjacent/)

给定 N 和 K，打印一个有 N 个字符的字符串。字符串应该正好有 k 个不同的字符，并且没有相邻的位置。
**例:**

```
Input  : n = 5, k = 3 
Output :  abcab
Explanation: 3 distinct character a, b, c
and n length string. 

Input: 3 2
Output: aba 
Explanation: 2 distinct character 'a' 
and 'b' and n length string.
```

考虑前 k 个拉丁字母。我们将按顺序把它们加到答案中，首先，我们加上 a，然后是 b，以此类推。如果字母写完了，但答案的长度仍然小于要求的长度，那么我们从字母表的开头开始重新添加字母。我们重复这个过程，直到答案的长度变成 n，然后打印出来。
以下是上述方法的实施

## C++

```
// CPP program to construct a n length string
// with k distinct characters such that no two
// same characters are adjacent.
#include <iostream>
using namespace std;

// Function to find a string of length
// n with k distinct characters.
string findString(int n, int k)
{
    // Initialize result with first k
    // Latin letters
    string res = "";
    for (int i = 0; i < k; i++)
        res = res + (char)('a' + i);

    // Fill remaining n-k letters by
    // repeating k letters again and again.
    int count = 0;
    for (int i = 0; i < n - k; i++) {
        res = res + (char)('a' + count);
        count++;
        if (count == k)
            count = 0;
    }
    return res;
}

// Driver code
int main()
{
    int n = 5, k = 2;
    cout << findString(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to construct a n length
// string with k distinct characters
// such that no two same characters
// are adjacent.
import java.io.*;

public class GFG {

    // Function to find a string of
    // length n with k distinct characters.
    static String findString(int n, int k)
    {

        // Initialize result with first k
        // Latin letters
        String res = "";

        for (int i = 0; i < k; i++)
            res = res + (char)('a' + i);

        // Fill remaining n-k letters by
        // repeating k letters again and
        // again.
        int count = 0;

        for (int i = 0; i < n - k; i++)
        {
            res = res + (char)('a' + count);
            count++;

            if (count == k)
                count = 0;
        }

        return res;
    }

    // Driver code
    static public void main (String[] args)
    {

        int n = 5, k = 2;

        System.out.println(findString(n, k));
    }
}

// This article is contributed by vt_m.
```

## 蟒蛇 3

```
# Python 3 program to construct a n
# length string with k distinct characters
# such that no two same characters are adjacent.

# Function to find a string of length
# n with k distinct characters.
def findString(n, k):

    # Initialize result with first k
    # Latin letters
    res = ""
    for i in range(k):
        res = res + chr(ord('a') + i)

    # Fill remaining n-k letters by
    # repeating k letters again and again.
    count = 0
    for i in range(n - k) :
        res = res + chr(ord('a') + count)
        count += 1
        if (count == k):
            count = 0;

    return res

# Driver code
if __name__ == "__main__":

    n = 5
    k = 2
    print(findString(n, k))

# This code is contributed by ita_c
```

## C#

```
// C# program to construct a n length
// string with k distinct characters
// such that no two same characters
// are adjacent.
using System;

public class GFG {

    // Function to find a string
    // of length n with k distinct
    // characters.
    static string findString(int n, int k)
    {

        // Initialize result with
        // first k Latin letters
        string res = "";

        for (int i = 0; i < k; i++)
            res = res + (char)('a' + i);

        // Fill remaining n-k letters by
        // repeating k letters again and
        // again.
        int count = 0;

        for (int i = 0; i < n - k; i++)
        {
            res = res + (char)('a' + count);
            count++;

            if (count == k)
                count = 0;
        }

        return res;
    }

    // Driver code
    static public void Main ()
    {

        int n = 5, k = 2;

        Console.WriteLine(findString(n, k));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php program to construct a n length
// string with k distinct characters
// such that no two same characters
// are adjacent.

// Function to find a string of length
// n with k distinct characters.
function findString($n, $k)
{
    // Initialize result with first k
    // Latin letters
    $res = "";
    for ($i = 0; $i < $k; $i++)
        $res = $res . chr(ord('a') + $i);

    // Fill remaining n-k letters by
    // repeating k letters again and
    // again.
    $count = 0;
    for ($i = 0; $i < $n - $k; $i++)
    {
        $res = $res . chr(ord('a')
                          + $count);
        $count++;
        if ($count == $k)
            $count = 0;
    }
    return $res;
}

// Driver code
    $n = 5;
    $k = 2;

    echo findString($n, $k);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript program to construct a n length
// string with k distinct characters
// such that no two same characters
// are adjacent.

    // Function to find a string of
    // length n with k distinct characters.
    function findString(n, k)
    {

        // Initialize result with first k
        // Latin letters
        let res = "";

        for (let i = 0; i < k; i++)
            res = res + String.fromCharCode('a'.charCodeAt(0) + i);

        // Fill remaining n-k letters by
        // repeating k letters again and
        // again.
        let count = 0;

        for (let i = 0; i < n - k; i++)
        {
            res = res + String.fromCharCode('a'.charCodeAt(0) + count);
            count++;

            if (count == k)
                count = 0;
        }

        return res;
    }

     // Driver code
     let n = 5, k = 2;
     document.write(findString(n, k));

    // This code is contributed by rag2127
</script>
```

输出:

```
ababa
```

**时间复杂度** : O(n)
本文由[**Raja vikramatitya**](https://www.facebook.com/raja.vikramaditya.7)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。