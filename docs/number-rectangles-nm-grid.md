# N * M 网格中的矩形数量

> 原文:[https://www.geeksforgeeks.org/number-rectangles-nm-grid/](https://www.geeksforgeeks.org/number-rectangles-nm-grid/)

给我们一个 N*M 的网格，在其中打印矩形的数量。
示例:

```
Input  : N = 2, M = 2
Output : 9
There are 4 rectangles of size 1 x 1.
There are 2 rectangles of size 1 x 2
There are 2 rectangles of size 2 x 1
There is one rectangle of size 2 x 2.

Input  : N = 5, M = 4
Output : 150

Input :  N = 4, M = 3
Output: 60
```

我们已经讨论了[计算 n×m 网格中的正方形数量](https://www.geeksforgeeks.org/count-number-of-squares-in-a-rectangle/)，
让我们推导出矩形数量的公式。
如果网格是 1×1，则有 1 个矩形。
如果网格是 2×1，会有 2 + 1 = 3 个矩形
如果网格是 3×1，会有 3 + 2 + 1 = 6 个矩形。
我们可以说对于 N*1 会有 N+(N-1)+(N-2)……+1 =(N)(N+1)/2 个矩形
如果我们在 N×1 上再加一列，首先我们在第二列的矩形会和第一列一样多，
然后我们就有了同样数量的 2×M 个矩形。
所以 N×2 = 3 (N)(N+1)/2
在推导出这个之后，我们可以说
对于 N*M，我们将有(M)(M+1)/2(N)(N+1)/2 =**M(M+1)(N)(N+1)/4**
所以总矩形的公式将是 M(M+1)(N)(N+1)/4

。

**组合逻辑:**

N*M 网格可以表示为(N+1)条垂直线和(M+1)条水平线。
在一个矩形中，我们需要两个不同的水平线和两个不同的垂直线。
所以按照组合数学的逻辑，我们可以选择 2 条垂直线和 2 条水平线组成一个矩形。这些组合的总数是网格中可能的矩形数量。

N*M 网格中的矩形总数:**T1】N+1C<sub>2</sub>*<sup>M+1</sup>C<sub>2</sub>T9】=**(N *(N+1)/2！)*(M*(M+1)/2！)**=**N *(N+1)* M *(M+1)/4**** 

## C++

```
// C++ program to count number of rectangles
// in a n x m grid
#include <bits/stdc++.h>
using namespace std;

int rectCount(int n, int m)
{
    return (m * n * (n + 1) * (m + 1)) / 4;
}

/* driver code */
int main()
{
    int n = 5, m = 4;
    cout << rectCount(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code to count number of
// rectangles in N*M grid
import java.util.*;

class GFG {

    public static long  rectCount(int n, int m)
    {
        return (m * n * (n + 1) * (m + 1)) / 4;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int n = 5, m = 4;
       System.out.println(rectCount(n, m));
    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 program to count number
# of rectangles in a n x m grid

def rectCount(n, m):

    return (m * n * (n + 1) * (m + 1)) // 4

# Driver code
n, m = 5, 4
print(rectCount(n, m))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# Code to count number of
// rectangles in N*M grid
using System;

class GFG {

    public static long  rectCount(int n, int m)
    {
        return (m * n * (n + 1) * (m + 1)) / 4;
    }

    // Driver program
    public static void Main()
    {
        int n = 5, m = 4;
       Console.WriteLine(rectCount(n, m));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// number of rectangles
// in a n x m grid

function rectCount($n, $m)
{
    return ($m * $n *
           ($n + 1) *
           ($m + 1)) / 4;
}

// Driver Code
$n = 5;
$m = 4;
echo rectCount($n, $m);

// This code is contributed
// by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript Code to count number
    // of rectangles in N*M grid

    function rectCount(n, m)
    {
        return parseInt((m * n * (n + 1) *
                        (m + 1)) / 4, 10);
    }

      let n = 5, m = 4;
      document.write(rectCount(n, m));

</script>
```

**输出:**

```
150
```

本文由**普拉纳夫**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。