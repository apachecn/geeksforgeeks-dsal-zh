# 两根弦之间的汉明距离

> 原文:[https://www.geeksforgeeks.org/hamming-distance-two-strings/](https://www.geeksforgeeks.org/hamming-distance-two-strings/)

给你两个等长的字符串，你要找出这两个字符串之间的[汉明距离](https://en.wikipedia.org/wiki/Hamming_distance)。
其中两个等长字符串之间的汉明距离是对应字符不同的位置数。
**示例:**

```
Input : str1[] = "geeksforgeeks", str2[] = "geeksandgeeks"
Output : 3
Explanation : The corresponding character mismatch are highlighted.
"geeks<u>for</u>geeks" and "geeks<u>and</u>geeks"

Input : str1[] = "1011101", str2[] = "1001001"
Output : 2
Explanation : The corresponding character mismatch are highlighted.
"10<u>1</u>1<u>1</u>01" and "10<u>0</u>1<u>0</u>01"
```

这个问题可以通过一个简单的方法来解决，我们遍历字符串并计算相应位置的不匹配。这个问题的扩展形式是[编辑距离。](https://www.geeksforgeeks.org/dynamic-programming-set-5-edit-distance/)
**算法:**

```
int hammingDist(char str1[], char str2[])
{
    int i = 0, count = 0;
    while(str1[i]!='\0')
    {
        if (str1[i] != str2[i])
            count++;
        i++;
    }
    return count;
}
```

下面是两个字符串的实现。

## C++

```
// C++ program to find hamming distance b/w
// two string
#include<bits/stdc++.h>
using namespace std;

// function to calculate Hamming distance
int hammingDist(char *str1, char *str2)
{
    int i = 0, count = 0;
    while (str1[i] != '\0')
    {
        if (str1[i] != str2[i])
            count++;
        i++;
    }
    return count;
}

// driver code
int main()
{
    char str1[] = "geekspractice";
    char str2[] = "nerdspractise";

    // function call
    cout << hammingDist (str1, str2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find hamming distance
// b/w two string
class GFG
{
// function to calculate Hamming distance
static int hammingDist(String str1, String str2)
{
    int i = 0, count = 0;
    while (i < str1.length())
    {
        if (str1.charAt(i) != str2.charAt(i))
            count++;
        i++;
    }
    return count;
}

// Driver code
public static void main (String[] args)
{
    String str1 = "geekspractice";
    String str2 = "nerdspractise";

    // function call
    System.out.println(hammingDist (str1, str2));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find
# hamming distance b/w two
# string

# Function to calculate
# Hamming distance
def hammingDist(str1, str2):
    i = 0
    count = 0

    while(i < len(str1)):
        if(str1[i] != str2[i]):
            count += 1
        i += 1
    return count

# Driver code 
str1 = "geekspractice"
str2 = "nerdspractise"

# function call
print(hammingDist(str1, str2))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to find hamming
// distance b/w two string
using System;

class GFG {

// function to calculate
// Hamming distance
static int hammingDist(String str1,
                       String str2)
{
    int i = 0, count = 0;
    while (i < str1.Length)
    {
        if (str1[i] != str2[i])
            count++;
        i++;
    }
    return count;
}

// Driver code
public static void Main ()
{
    String str1 = "geekspractice";
    String str2 = "nerdspractise";

    // function call
    Console.Write(hammingDist(str1, str2));
}
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find hamming distance b/w
// two string

// function to calculate
// Hamming distance
function hammingDist($str1, $str2)
{
    $i = 0; $count = 0;
    while (isset($str1[$i]) != '')
    {
        if ($str1[$i] != $str2[$i])
            $count++;
        $i++;
    }
    return $count;
}

    // Driver Code
    $str1 = "geekspractice";
    $str2 = "nerdspractise";

    // function call
    echo hammingDist ($str1, $str2);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
// JavaScript program to find hamming distance b/w
// two string

// function to calculate Hamming distance
function hammingDist(str1, str2)
{
    let i = 0, count = 0;
    while (i < str1.length)
    {
        if (str1[i] != str2[i])
            count++;
        i++;
    }
    return count;
}

// driver code
    let str1 = "geekspractice";
    let str2 = "nerdspractise";

    // function call
    document.write(hammingDist (str1, str2));

// This code is contributed by Manoj.
</script>
```

**输出:**

```
4
```

时间复杂度:O(n)
**注:**对于两个二进制数的汉明距离，我们可以简单地在两个数的异或中返回一个集合比特数。
本文由 [**希瓦姆·普拉丹(anuj_charm)**](https://www.facebook.com/anuj.charm) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。