# 找出给定字符串中“1(0+)1”的所有模式| SET 1(通用方法)

> 原文:[https://www . geesforgeks . org/find-patterns-101-given-string/](https://www.geeksforgeeks.org/find-patterns-101-given-string/)

字符串包含 1(0+)1 形式的模式，其中(0+)表示任何非空的连续 0 序列。请统计所有此类模式。允许图案重叠。
**注意:**只包含数字和小写字符。字符串不一定是二进制的。100201 不是有效的模式。
这里讨论了一种解决问题的方法，其他使用正则表达式的方法在[第 2 集](https://www.geeksforgeeks.org/find-patterns-101-given-string-set-2regular-expression-approach/)
**中给出:示例:**

```
Input : 1101001
Output : 2

Input : 100001abc101
Output : 2
```

让输入字符串的大小为 n.
1。迭代索引“0”到“n-1”。
2。如果我们遇到“1”，我们迭代直到元素为“0”。
3。在零流结束后，我们检查是否遇到“1”。
4。继续这样做，直到我们到达绳子的尽头。
以下是上述方法的实施。

## C++

```
/* Code to count 1(0+)1 patterns in a string */
#include <bits/stdc++.h>
using namespace std;

/* Function to count patterns */
int patternCount(string str)
{
    /* Variable to store the last character*/
    char last = str[0];

    int i = 1, counter = 0;
    while (i < str.size())
    {
        /* We found 0 and last character was '1',
          state change*/
        if (str[i] == '0' && last == '1')
        {
            while (str[i] == '0')
                i++;

            /* After the stream of 0's, we got a '1',
               counter incremented*/
            if (str[i] == '1')
                counter++;
        }

        /* Last character stored */
        last = str[i];
        i++;
    }

    return counter;
}

/* Driver Code */
int main()
{
    string str = "1001ab010abc01001";
    cout << patternCount(str) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Code to count 1(0+)1
// patterns in a string
import java.io.*;

class GFG
{
    // Function to count patterns
    static int patternCount(String str)
    {
        /* Variable to store the last character*/
        char last = str.charAt(0);

        int i = 1, counter = 0;
        while (i < str.length())
        {
            /* We found 0 and last character was '1',
            state change*/
            if (str.charAt(i) == '0' && last == '1')
            {
                while (str.charAt(i) == '0')
                    i++;

                // After the stream of 0's, we
                // got a '1',counter incremented
                if (str.charAt(i) == '1')
                    counter++;
            }

            /* Last character stored */
            last = str.charAt(i);
            i++;
        }

        return counter;
    }

    // Driver Code
    public static void main (String[] args)
    {
        String str = "1001ab010abc01001";
        System.out.println(patternCount(str));

    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 code to count 1(0+)1 patterns in a

# Function to count patterns
def patternCount(str):

    # Variable to store the last character
    last = str[0]

    i = 1; counter = 0
    while (i < len(str)):

        # We found 0 and last character was '1',
        # state change
        if (str[i] == '0' and last == '1'):
            while (str[i] == '0'):
                i += 1

                # After the stream of 0's, we got a '1',
                # counter incremented
                if (str[i] == '1'):
                    counter += 1

        # Last character stored
        last = str[i]
        i += 1

    return counter

# Driver Code
str = "1001ab010abc01001"
ans = patternCount(str)
print (ans)

# This code is contributed by saloni1297
```

## C#

```
// C# Code to count 1(0 + )1
// patterns in a string
using System;

class GFG
{

    // Function to count patterns
    static int patternCount(String str)
    {
        // Variable to store the
        // last character
        char last = str[0];

        int i = 1, counter = 0;
        while (i < str.Length)
        {
            // We found 0 and last
            // character was '1',
            // state change
            if (str[i] == '0' && last == '1')
            {
                while (str[i] == '0')
                    i++;

                // After the stream of 0's, we
                // got a '1',counter incremented
                if (str[i] == '1')
                    counter++;
            }

            // Last character stored
            last = str[i];
            i++;
        }

        return counter;
    }

    // Driver Code
    public static void Main ()
    {
        String str = "1001ab010abc01001";
        Console.Write(patternCount(str));

    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Code to count 1(0+)1 patterns
// in a string

// Function to count patterns
function patternCount($str)
{

    // Variable to store the
    // last character
    $last = $str[0];

    $i = 1;
    $counter = 0;
    while ($i < strlen($str))
    {

        // We found 0 and last character
        // was '1', state change
        if ($str[$i] == '0' && $last == '1')
        {
            while ($str[$i] == '0')
                $i++;

            // After the stream of 0's,
            // we got a '1', counter
            // incremented
            if ($str[$i] == '1')
                $counter++;
        }

        /* Last character stored */
        $last = $str[$i];
        $i++;
    }

    return $counter;
}

    // Driver Code
    $str = "1001ab010abc01001";
    echo patternCount($str) ;

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>

// javascript Code to count 1(0+)1
// patterns in a string

    // Function to count patterns
    function patternCount(str)
    {
        /* Variable to store the last character*/
        var last = str.charAt(0);

        var i = 1, counter = 0;
        while (i < str.length)
        {
            /* We found 0 and last character was '1',
            state change*/
            if (str.charAt(i) == '0' && last == '1')
            {
                while (str.charAt(i) == '0')
                    i++;

                // After the stream of 0's, we
                // got a '1',counter incremented
                if (str.charAt(i) == '1')
                    counter++;
            }

            /* Last character stored */
            last = str.charAt(i);
            i++;
        }

        return counter;
    }

    // Driver Code
    var str = "1001ab010abc01001";
    document.write(patternCount(str));

// This code is contributed by 29AjayKumar
</script>
```

输出:

```
2
```

本文由 [**罗希特·塔普利亚尔**](https://www.linkedin.com/in/rohit-thapliyal-515b5913a/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。