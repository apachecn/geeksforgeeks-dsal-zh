# 与英文字母距离相同的字符对的计数

> 原文:[https://www . geesforgeks . org/count-characters-string-distance-English-alphabets/](https://www.geeksforgeeks.org/count-characters-string-distance-english-alphabets/)

给定一个字符串，任务是计算元素距离与英文字母相同的对的数量。
**注:**考虑字符间的绝对距离。
**示例:**

```
Input:  str = "geeksforgeeks"
Output:  4
Explanation: In this (g, s), (e, g), (e, k), (e, g) 
are the pairs that are at same distances as
in English alphabets.

Input:  str = "observation"
Output:  4
Explanation: (b, i), (s, v), (o, n), (v, t) are 
at same distances as in English alphabets.
```

一个简单的解决方案是考虑生成所有对，并将对字符与它们之间的距离进行比较。如果一对的距离相同，则结果递增。

## C++

```
// A Simple C++ program to find pairs with distance
// equal to English alphabet distance
#include <bits/stdc++.h>
using namespace std;

// Function to count pairs
int countPairs(string str)
{
    int result = 0;
    int n = str.length();
    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)

            // Increment count if characters are at
            // same distance
            if (abs(str[i] - str[j]) == abs(i - j))
                result++;

    return result;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    cout << countPairs(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Simple Java program to find pairs with distance
// equal to English alphabet distance
class Test {

    // Method to count pairs
    static int countPairs(String str)
    {
        int result = 0;
        int n = str.length();
        for (int i = 0; i < n; i++)
          for (int j = i + 1; j < n; j++)

            // Increment count if characters
            // are at same distance
            if (Math.abs(str.charAt(i) - str.charAt(j)) ==
                                          Math.abs(i - j))
                result++;

        return result;
    }

    // Driver method
    public static void main(String args[])
    {
        String str = "geeksforgeeks";
        System.out.println(countPairs(str));
    }
}
```

## 蟒蛇 3

```
# Simple Python3 program to find pairs with
# distance equal to English alphabet distance

# Function to count pairs
def countPairs(str1):
    result = 0;
    n = len(str1)
    for i in range(0, n):
        for j in range(i + 1, n):

            # Increment count if characters
            # are at same distance
            if (abs(ord(str1[i]) -
                    ord(str1[j])) == abs(i - j)):
                result += 1;

    return result;

# Driver code
if __name__ == "__main__":
    str1 = "geeksforgeeks";
    print(countPairs(str1));

# This code is contributed
# by Sairahul099
```

## C#

```
// A Simple C# program to find pairs with distance
// equal to English alphabet distance
using System;

class Test {

    // Method to count pairs
    static int countPairs(string str)
    {
        int result = 0;
        int n = str.Length;
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j < n; j++)

            // Increment count if characters
            // are at same distance
            if (Math.Abs(str[i] - str[j]) == Math.Abs(i - j))
                result++;

        return result;
    }

    // Driver method
    public static void Main()
    {
        string str = "geeksforgeeks";
        Console.WriteLine(countPairs(str));
    }
}

// This Code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for Count
// of character pairs at
// same distance as in
// English alphabets

// Function to count pairs
function countPairs($str)
{
    $result = 0;
    $n = strlen($str);
    for ($i = 0; $i < $n; $i++)
        for ($j = $i + 1;
             $j < $n; $j++)

            // Increment count if
            // characters are at
            // same distance
            if (abs(ord($str[$i]) -
                    ord($str[$j])) ==
                    abs($i - $j))
                $result++;

    return $result;
}

// Driver code
$str = "geeksforgeeks";
echo countPairs($str);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
    // A Simple Javascript program to find pairs with distance
    // equal to English alphabet distance

    // Method to count pairs
    function countPairs(str)
    {
        let result = 0;
        let n = str.length;
        for (let i = 0; i < n; i++)
            for (let j = i + 1; j < n; j++)

            // Increment count if characters
            // are at same distance
            if (Math.abs(str[i].charCodeAt() - str[j].charCodeAt()) == Math.abs(i - j))
                result++;

        return result;
    }

    let str = "geeksforgeeks";
      document.write(countPairs(str));

   // This code is contributed by divyesh072019.
</script>
```

**输出:**

```
4
```

上述方法的时间复杂度为 **O(n <sup>2</sup> )** 。上述方法可以通过使用只能有 26 个字母的事实来优化，即，不是检查一个元素直到字符串的长度，而是只检查从当前索引到第 26 个索引。

## C++

```
// An optimized C++ program to find pairs with distance
// equal to English alphabet distance
#include <bits/stdc++.h>
using namespace std;
const int MAX_CHAR = 26;

// Function to count pairs with distance
// equal to English alphabet distance
int countPairs(string str)
{
    int result = 0;
    int n = str.length();

    for (int i = 0; i < n; i++)

        // This loop runs at most 26 times
        for (int j = 1; (i + j) < n && j <= MAX_CHAR; j++)
            if ((abs(str[i + j] - str[i]) == j))
                result++;

    return result;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    cout << countPairs(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An optimized Java program to find pairs with distance
// equal to English alphabet distance

class Test {
    static final int MAX_CHAR = 26;

    // Method to count pairs with distance
    // equal to English alphabet distance
    static int countPairs(String str)
    {
        int result = 0;
        int n = str.length();

        for (int i = 0; i < n; i++)

            // This loop runs at most 26 times
            for (int j = 1; (i + j) < n && j <= MAX_CHAR; j++)
                if ((Math.abs(str.charAt(i + j) - str.charAt(i)) == j))
                    result++;

        return result;
    }

    // Driver method
    public static void main(String args[])
    {
        String str = "geeksforgeeks";
        System.out.println(countPairs(str));
    }
}
```

## 蟒蛇 3

```
# An optimized C++ program to find pairs with
# distance equal to English alphabet distance

MAX_CHAR = 26

# Function to count pairs with distance
# equal to English alphabet distance
def countPairs(str1):
    result = 0;
    n = len(str1)

    for i in range(0, n):

        # This loop runs at most 26 times
        for j in range(1, MAX_CHAR + 1):
            if((i + j) < n):
                if ((abs(ord(str1[i + j]) -
                         ord(str1[i])) == j)):
                    result += 1;

    return result

# Driver code
if __name__ == "__main__":
    str1 = "geeksforgeeks";
    print(countPairs(str1))

# This code is contributed
# by Sairahul099
```

## C#

```
// An optimized C# program to find pairs with distance
// equal to English alphabet distance
using System;

class Test {

    static int MAX_CHAR = 26;

    // Method to count pairs with distance
    // equal to English alphabet distance
    static int countPairs(string str)
    {
        int result = 0;
        int n = str.Length;

        for (int i = 0; i < n; i++)

            // This loop runs at most 26 times
            for (int j = 1; (i + j) < n && j <= MAX_CHAR; j++)
                if ((Math.Abs(str[i + j] - str[i]) == j))
                    result++;

        return result;
    }

    // Driver method
    public static void Main()
    {
        string str = "geeksforgeeks";
        Console.WriteLine(countPairs(str));
    }
}

// This Code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// An optimized PHP program
// to find pairs with distance
// equal to English alphabet distance

// Function to count pairs
// with distance equal to
// English alphabet distance
function countPairs($str)
{
    $result = 0;
    $n = strlen($str);

    for ($i = 0; $i < $n; $i++)

        // This loop runs at
        // most 26 times
        for ($j = 1; ($i + $j) < $n &&
                      $j <= 26; $j++)
            if ((abs(ord($str[$i + $j]) -
                     ord($str[$i]) ) == $j))
                $result++;

    return $result;
}

// Driver code
$str = "geeksforgeeks";
echo countPairs($str);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>   
    // An optimized Javascript program to find pairs with distance
    // equal to English alphabet distance

    let MAX_CHAR = 26;

    // Method to count pairs with distance
    // equal to English alphabet distance
    function countPairs(str)
    {
        let result = 0;
        let n = str.length;

        for (let i = 0; i < n; i++)

            // This loop runs at most 26 times
            for (let j = 1; (i + j) < n && j <= MAX_CHAR; j++)
                if ((Math.abs(str[i + j].charCodeAt() - str[i].charCodeAt()) == j))
                    result++;

        return result;
    }

    let str = "geeksforgeeks";
      document.write(countPairs(str));

</script>
```

**输出:**

```
4
```

在字母表大小不变的假设下，优化解的时间复杂度为 **O(n)** 。
本文由 [**萨希尔·查布拉(akku)**](https://practice.geeksforgeeks.org/user-profile.php?user=sahil_coder) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。