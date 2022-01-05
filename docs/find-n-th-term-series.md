# 求数列 7、15、32 中的第 n 项，…

> 原文:[https://www.geeksforgeeks.org/find-n-th-term-series/](https://www.geeksforgeeks.org/find-n-th-term-series/)

给定一个数列 7，15，32，…求这个数列的第 n 项。

**示例:**

```
Input : 5
Output : 138

Input : 7
Output : 568 
```

**进场:**通过看系列的图案我们很容易识别出是一个混合系列。
S = 7，15，32…..
序列中的每个元素乘以 2，然后比前一个元素多加 1。
S = 7，15 (2 * 7 + 1)，32 (2 * 15 + 2)……。
利用迭代，我们可以很容易地找到级数的第 n 项。

下面是上述方法的实现:

## C++

```
// CPP program to find nth term
#include <bits/stdc++.h>
using namespace std;

// utility function
int findTerm(int n)
{
    if (n == 1)
        return n;

    else {

        // since first element of the
        // series is 7, we initialise
        // a variable with 7
        int term = 7;

        // Using iteration to find nth
        // term
        for (int i = 2; i <= n; i++)
            term = term * 2 + (i - 1);       

        return term;
    }
}

// driver function
int main()
{
    int n = 5;
    cout << findTerm(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find nth term
import java.lang.*;

class GFG {

// utility function
static int findTerm(int n)
{
    if (n == 1)
    return n;

    else {

    // since first element of the
    // series is 7, we initialise
    // a variable with 7
    int term = 7;

    // Using iteration to find nth
    // term
    for (int i = 2; i <= n; i++)
        term = term * 2 + (i - 1);

    return term;
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 5;
    System.out.print(findTerm(n));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find nth term

# utility function
def findTerm(n) :

    if n == 1 :
        return n
    else :

        # since first element of the
        # series is 7, we initialise
        # a variable with 7
        term = 7

        # Using iteration to find nth
        # term
        for i in range(2, n + 1) :
            term = term * 2 + (i - 1);    

    return term;

# driver function
print (findTerm(5))

# This code is contributed by Saloni Gupta
```

## C#

```
// C# program to find nth term
using System;

class GFG {

    // utility function
    static int findTerm(int n)
    {
        if (n == 1)
            return n;

        else {

            // since first element of the
            // series is 7, we initialise
            // a variable with 7
            int term = 7;

            // Using iteration to find nth
            // term
            for (int i = 2; i <= n; i++)
                term = term * 2 + (i - 1);

            return term;
        }
    }

    // Driver code
    public static void Main()
    {
        int n = 5;
        Console.WriteLine(findTerm(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find nth term

// utility function
function findTerm($n)
{
    if ($n == 1)
        return $n;

    else
    {

        // since first element of the
        // series is 7, we initialise
        // a variable with 7
        $term = 7;

        // Using iteration to find nth
        // term
        for ($i = 2; $i <= $n; $i++)
            $term = $term * 2 + ($i - 1);

        return $term;
    }
}

// Driver Code
$n = 5;
echo(findTerm($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// Javascript program to find nth term

// utility function
function findTerm(n)
{
    if (n == 1)
        return n;

    else
    {

        // since first element of the
        // series is 7, we initialise
        // a variable with 7
        let term = 7;

        // Using iteration to find nth
        // term
        for (let i = 2; i <= n; i++)
            term = term * 2 + (i - 1);

        return term;
    }
}

// Driver Code
let n = 5;
document.write(findTerm(n));

// This code is contributed by gfgking.
</script>
```

**输出:**

```
138
```

本文由**萨洛尼·古普塔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。