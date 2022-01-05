# 打印不包含相邻副本的最接近的字符串

> 原文:[https://www . geesforgeks . org/print-一个不包含相邻副本的最近字符串/](https://www.geeksforgeeks.org/print-a-closest-string-that-does-not-contain-adjacent-duplicates/)

给定字符串 S，更改 S 中的最小字母数，使所有相邻字符都不同。打印结果字符串。
**例:**

```
Input : S = "aab"
Output: acb
Explanation :
Loop will start for i-th character, which 
is second ‘a’. It’s cannot be ‘b’ since it 
matches with third char. So output should
be ‘acb’.

Input : S = "geeksforgeeks"
Output: geaksforgeaks
Explanation :
Resultant string, after making minimal 
changes. S = "geaksforgeaks". We made two 
changes, which is the optimal solution here.
```

我们可以用贪婪的方法来解决这个问题。让我们考虑一段长度为 k 的连续相同字符。我们必须在段中进行至少[K/2]个更改，以确保一行中没有相同的字符。我们也可以改变第二，第四等..字符串的字符不应等于左边的字母和右边的字母。
从起始索引(i = 1)开始遍历字符串，如果任意两个相邻字母(i & i-1)相等，则用“a”初始化第(I)个字符，并开始另一个循环，使第(I)个字符不同于左右字母。
以下是上述方法的实施:

## C++

```
// C++ program to print a string with no adjacent
// duplicates by doing  minimum changes to original
// string
#include <bits/stdc++.h>
using namespace std;

// Function to print simple string
string noAdjacentDup(string s)
{
    int n = s.length();
    for (int i = 1; i < n; i++)
    {
        // If any two adjacent characters are equal
        if (s[i] == s[i - 1])
        {
            s[i] = 'a'; // Initialize it to 'a'

            // Traverse the loop until it is different
            // from the left and right letter.
            while (s[i] == s[i - 1] ||
                (i + 1 < n && s[i] == s[i + 1]))            
                s[i]++;

            i++;
        }
    }
    return s;
}

// Driver Function
int main()
{
    string s = "geeksforgeeks";
    cout << noAdjacentDup(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print a string with
// no adjacent duplicates by doing
// minimum changes to original string
import java.util.*;
import java.lang.*;

public class GfG{

    // Function to print simple string
    public static String noAdjacentDup(String s1)
    {
        int n = s1.length();
        char[] s = s1.toCharArray();
        for (int i = 1; i < n; i++)
        {
            // If any two adjacent
            // characters are equal
            if (s[i] == s[i - 1])
            {
                // Initialize it to 'a'
                s[i] = 'a';

                // Traverse the loop until it 
                // is different from the left
                // and right letter.
                while (s[i] == s[i - 1] ||
                    (i + 1 < n && s[i] == s[i + 1]))            
                    s[i]++;

                i++;
            }
        }
        return (new String(s));
    }

    // Driver function
    public static void main(String argc[]){

        String s = "geeksforgeeks";
        System.out.println(noAdjacentDup(s));

    }

}

/* This code is contributed by Sagar Shukla */
```

## 蟒蛇 3

```
# Python program to print a string with
# no adjacent duplicates by doing minimum
# changes to original string

# Function to print simple string
def noAdjacentDup(s):

    n = len(s)
    for i in range(1, n):

        # If any two adjacent characters are equal
        if (s[i] == s[i - 1]):

            s[i] = "a" # Initialize it to 'a'

            # Traverse the loop until it is different
            # from the left and right letter.
            while (s[i] == s[i - 1] or
                (i + 1 < n and s[i] == s[i + 1])):            
                s[i] += 1

            i += 1

    return s

# Driver Function
s = list("geeksforgeeks")
print("".join(noAdjacentDup(s)))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to print a string with
// no adjacent duplicates by doing
// minimum changes to original string
using System;

class GfG{

    // Function to print simple string
    public static String noAdjacentDup(String s1)
    {
        int n = s1.Length;

        char[] s = s1.ToCharArray();
        for (int i = 1; i < n; i++)
        {
            // If any two adjacent
            // characters are equal
            if (s[i] == s[i - 1])
            {
                // Initialize it to 'a'
                s[i] = 'a';

                // Traverse the loop until it
                // is different from the left
                // and right letter.
                while (s[i] == s[i - 1] ||
                      (i + 1 < n && s[i] == s[i + 1]))            
                 s[i]++;

                i++;
            }
        }
        return (new String(s));
    }

    // Driver function
    public static void Main(String[] argc)
    {
        String s = "geeksforgeeks";

        // Function calling
        Console.Write(noAdjacentDup(s));
    }
}

/* This code is contributed by parashar */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print a
// string with no adjacent
// duplicates by doing minimum
// changes to original string

// Function to print
// simple string
function noAdjacentDup($s)
{
    $n = strlen($s);
    for ($i = 1; $i < $n; $i++)
    {
        // If any two adjacent
        // characters are equal
        if ($s[$i] == $s[$i - 1])
        {
            // Initialize it to 'a'
            $s[$i] = 'a';

            // Traverse the loop
            // until it is different
            // from the left and
            // right letter.
            while ($s[$i] == $s[$i - 1] ||
                  ($i + 1 < $n &&
                   $s[$i] == $s[$i + 1]))            
                $s[$i]++;

            $i++;
        }
    }
    return $s;
}

// Driver Code
$s = "geeksforgeeks";
echo (noAdjacentDup($s));

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// Javascript program to print a string with
// no adjacent duplicates by doing
// minimum changes to original string

    // Function to print simple string
    function noAdjacentDup(s1)
    {
        let n = s1.length;
        let s = s1.split('');
        for (let i = 1; i < n; i++)
        {
            // If any two adjacent
            // characters are equal
            if (s[i] == s[i - 1])
            {
                // Initialize it to 'a'
                s[i] = 'a';

                // Traverse the loop until it 
                // is different from the left
                // and right letter.
                while (s[i] == s[i - 1] ||
                    (i + 1 < n && s[i] == s[i + 1]))            
                    s[i]++;

                i++;
            }
        }
        return (s);
    }

// driver code

        let s = "geeksforgeeks";
        document.write(noAdjacentDup(s));

</script>
```

**输出:**

```
geaksforgeaks
```

**时间复杂度:** O(N <sup>2</sup> )

**辅助空间:** O(1)