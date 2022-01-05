# 查询重复字符串中的字符

> 原文:[https://www . geesforgeks . org/查询重复字符串中的字符/](https://www.geeksforgeeks.org/queries-for-characters-in-a-repeated-string/)

给定一根弦 **X** 。通过多次重复字符串 X 形成一个字符串 S，即多次将字符串 X 附加到自身。有表格 I 和 j 的 **Q** 查询。任务是如果索引 I 的元素与 S 中索引 j 的元素相同，则打印“是”，否则为每个查询打印“否”。
**例:**

```
Input : X = "geeksforgeeks", Q = 3.
Query 1: 0 8
Query 2: 8 13
Query 3: 6 15

Output :
Yes
Yes
No

String S will be "geeksforgeeksgeeksforgeeks....".
For Query 1, index 0 and index 8 have same element i.e 'g'.
For Query 2, index 8 and index 13 have same element i.e 'g'.
For Query 3, index 6 = 'o' and index 15 = 'e' which are not same.
```

设字符串 X 的长度为 n，观察索引 0，n，2n，3n，…处的元素。都是一样的。类似地，对于索引 I，位置 I，n+i，2n+i，3n+i，…..包含相同的元素。
因此，对于每个查询，查找(i%n)和(j%n)并且如果两者对于字符串 x 都相同。
下面是上述思想的实现:

## C++

```
// Queries for same characters in a repeated
// string
#include<bits/stdc++.h>
using namespace std;

// Print whether index i and j have same
// element or not.
void query(char s[], int i, int j)
{
    int n = strlen(s);

    // Finding relative position of index i,j.
    i %= n;
    j %= n;

    // Checking is element are same at index i, j.
    (s[i]==s[j])? (cout << "Yes" << endl):
                  (cout << "No" << endl);
}

// Driven Program
int main()
{
    char X[] = "geeksforgeeks";

    query(X, 0, 8);
    query(X, 8, 13);
    query(X, 6, 15);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to Queries for
// same characters in a
// repeated string
import java.io.*;

public class GFG{

// Print whether index i and j
// have same element or not
static void query(String s, int i,
                  int j)
{
    int n = s.length();

    // Finding relative position
    // of index i,j
    i %= n;
    j %= n;

    // Checking is element are same
    // at index i, j
    if(s.charAt(i) == s.charAt(j))
    System.out.println("Yes");
    else
    System.out.println("No");
}

    // Driver Code
    static public void main (String[] args)
    {
    String X = "geeksforgeeks";

    query(X, 0, 8);
    query(X, 8, 13);
    query(X, 6, 15);

    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Queries for same characters in a repeated
# string

# Print whether index i and j have same
# element or not.
def query(s, i, j):
    n = len(s)

    # Finding relative position of index i,j.
    i %= n
    j %= n

    # Checking is element are same at index i, j.
    print("Yes") if s[i] == s[j] else print("No")

# Driver code
if __name__ == "__main__":
    X = "geeksforgeeks"
    query(X, 0, 8)
    query(X, 8, 13)
    query(X, 6, 15)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# Program to Queries for
// same characters in a
// repeated string
using System;

public class GFG{

// Print whether index i and j
// have same element or not
static void query(string s, int i,
                  int j)
{
    int n = s.Length;

    // Finding relative position
    // of index i,j.
    i %= n;
    j %= n;

    // Checking is element are
    // same at index i, j
    if(s[i] == s[j])
    Console.WriteLine("Yes");
    else
    Console.WriteLine("No");
}

    // Driver Code
    static public void Main ()
    {
    string X = "geeksforgeeks";

    query(X, 0, 8);
    query(X, 8, 13);
    query(X, 6, 15);

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Queries for same characters
// in a repeated string

// Print whether index i and j
// have same element or not.
function query($s, $i, $j)
{
    $n = strlen($s);

    // Finding relative position
    // of index i,j.
    $i %= $n;
    $j %= $n;

    // Checking is element are
    // same at index i, j.
    if(($s[$i] == $s[$j]))
        echo "Yes\n" ;
    else
        echo "No" ;
}

// Driver Code
$X = "geeksforgeeks";

query($X, 0, 8);
query($X, 8, 13);
query($X, 6, 15);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
    // Javascript Program to Queries for
    // same characters in a
    // repeated string

    // Print whether index i and j
    // have same element or not
    function query(s, i, j)
    {
        let n = s.length;

        // Finding relative position
        // of index i,j.
        i %= n;
        j %= n;

        // Checking is element are
        // same at index i, j
        if(s[i] == s[j])
            document.write("Yes" + "</br>");
        else
            document.write("No" + "</br>");
    }

    let X = "geeksforgeeks";

    query(X, 0, 8);
    query(X, 8, 13);
    query(X, 6, 15);

</script>
```

**输出:**

```
Yes
Yes
No
```

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。