# 字符串的子串数

> 原文:[https://www.geeksforgeeks.org/number-substrings-string/](https://www.geeksforgeeks.org/number-substrings-string/)

查找带有 **N** 字符的字符串的非空[子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)的总数。

> 输入:str = "abc"
> 输出:6
> 给定字符串的每个子串:“a”、“b”、“c”、“ab”、“bc”、“abc”
> 
> 输入:str =“AbcD”
> 输出:10
> 给定字符串的每个子串:“a”、“b”、“c”、“d”、“ab”、“BC”、“cd”、“abc”、“bcd”和“abcd”

非空子串的计数为 n*(n+1)/2
如果我们将空字符串也包含为子串，则计数变为 n*(n+1)/2 + 1

**以上公式是如何工作的？**

1.  长度为 1 的子串数量为 **n** (我们可以选择 n 个字符中的任意一个)
2.  长度为 2 的子串数量为 **n-1** (我们可以选择相邻形成的 n-1 对中的任意一对)
3.  长度为三的子串数量为 **n-2**
    (我们可以从相邻的 n-2 个三元组中选择任意一个)
4.  一般来说，长度为 k 的子串数量为 **n-k+1** ，其中 1 < = k < = n

从 1 到 n 的所有长度的子串总数=
n+(n-1)+(n-2)+(n-3)+…2+1
= n *(n+1)/2

## C++

```
// CPP program to count number of substrings
// of a string
#include <bits/stdc++.h>
using namespace std;

int countNonEmptySubstr(string str)
{
   int n = str.length();
   return n*(n+1)/2;
}

// driver code
int main()
{
    string s = "abcde";
    cout << countNonEmptySubstr(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of substrings
// of a string
import java.io.*;

public class GFG {

    static int countNonEmptySubstr(String str)
    {
        int n = str.length();
        return n * (n + 1) / 2;
    }

    // Driver code
    public static void main(String args[])
    {
        String s = "abcde";
        System.out.println(
                  countNonEmptySubstr(s));
    }
}

// This code is contributed
// by Manish Shaw (manishshaw1)
```

## 蟒蛇 3

```
# Python3 program to count number
# of substrings of a string

def countNonEmptySubstr(str):
    n = len(str);
    return int(n * (n + 1) / 2);

# driver code
s = "abcde";
print (countNonEmptySubstr(s));

# This code is contributed by
# Manish Shaw (manishshaw1)
```

## C#

```
// C# program to count number
// of substrings of a string
using System;
class GFG {

    static int countNonEmptySubstr(string str)
    {
        int n = str.Length;
        return n * (n + 1) / 2;
    }

    // Driver Code
    public static void Main()
    {
        string s = "abcde";
        Console.Write(countNonEmptySubstr(s));
    }
}

// This code is contributed
// by Manish Shaw (manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number
// of substrings of a string

function countNonEmptySubstr($str)
{
    $n = strlen($str);
    return $n * ($n + 1) / 2;
}

// Driver Code
$s = "abcde";
echo countNonEmptySubstr($s);

// This code is contributed by Anuj_67
?>
```

## java 描述语言

```
<script>

// JavaScript program to count number of substrings
// of a string
function countNonEmptySubstr(str)
    {
        let n = str.length;
        return n * (n + 1) / 2;
    }

    // Driver code
        let s = "abcde";
        document.write(countNonEmptySubstr(s));

// This code is contributed shivanisinghss2110

</script>
```

**Output:** 

```
15
```

https://youtu.be/9QxJo

-g0cMA