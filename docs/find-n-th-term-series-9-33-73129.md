# 求数列 9，33，73，129 中的第 n 项……

> 原文:[https://www . geesforgeks . org/find-n-th-term-series-9-33-73129/](https://www.geeksforgeeks.org/find-n-th-term-series-9-33-73129/)

给定一个数列 9，33，73，129…求数列的第 n 项。
示例:

```
Input : n = 4
Output : 129 

Input : n = 5
Output : 201
```

给定的序列有一个模式，在一次移位后从其自身中减去该模式后可见

```
S = 9 + 33 + 73 + 129 + … tn-1 + tn
S =     9 + 33 + 73 + … tn-2 + tn-1 + tn
———————————————
0 = 9 + (24 + 40 + 56 + ….) - tn 

Since 24 + 40 + 56.. series in A.P with
common difference of 16, we get

 tn = 9 + [((n-1)/2)*(2*24 + (n-1-1)d)] 

On solving this we get 

 tn = 8n<sup>2 + 1</sup>
```

以下是上述方法的实现:

## C++

```
// Program to find n-th element in the
// series 9, 33, 73, 128..
#include <bits/stdc++.h>
using namespace std;

// Returns n-th  element of the series
int series(int n)
{
    return (8 * n * n) + 1;
}

// driver program to test the above function
int main()
{
    int n = 5;
    cout << series(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to find n-th element in the
// series 9, 33, 73, 128..
import java.io.*;

class GFG{

    // Returns n-th  element of the series
    static int series(int n)
    {
        return (8 * n * n) + 1;
    }

    // driver program to test the above
    // function
    public static void main(String args[])
    {
        int n = 5;
        System.out.println(series(n));
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python Program to find n-th element
# in the series 9, 33, 73, 128...

# Returns n-th element of the series
def series(n):
    print (( 8 * n ** 2) + 1)

# Driver Code
series(5)

# This code is contributed by Abhishek Agrawal.
```

## C#

```
// C# program to find n-th element in the
// series 9, 33, 73, 128..
using System;

class GFG {

    // Returns n-th element of the series
    static int series(int n)
    {
        return (8 * n * n) + 1;
    }

    // driver function
    public static void Main()
    {
        int n = 5;
        Console.WriteLine(series(n));
    }
}

/*This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find n-th element
// in the series 9, 33, 73, 128..

// Returns n-th element
// of the series
function series($n)
{
    return (8 * $n * $n) + 1;
}

// Driver Code
$n = 5;
echo(series($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Program to find n-th element in the
// series 9, 33, 73, 128..

// Returns n-th  element of the series
function series(n)
{
    return (8 * n * n) + 1;
}

// driver program to test the above function
let n = 5;
document.write(series(n));

</script>
```

**输出:**

```
201
```

**时间复杂度:** O(1)
本文由 [**奋斗者**](https://www.facebook.com/raja.vikramaditya.7) 投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。