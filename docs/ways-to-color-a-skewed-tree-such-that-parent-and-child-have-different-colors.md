# 给倾斜的树上色，使父树和子树有不同颜色的方法

> 原文:[https://www . geeksforgeeks . org/给歪斜的树上色的方法这样父母和孩子就有不同的颜色了/](https://www.geeksforgeeks.org/ways-to-color-a-skewed-tree-such-that-parent-and-child-have-different-colors/)

给定一个有 N 个节点和 K 种颜色的倾斜树(每个节点最多有一个子节点)。你必须给每个节点分配一个从 1 到 K 的颜色，这样父节点和子节点就有不同的颜色。找到给节点着色的**方式的**最大**数量**。
**示例–**

```
Input : N = 2, K = 2.
Output :  
Let A1 and A2 be the two nodes.
Let A1 is parent of A2.
Colors are Red and Blue.
Case 1: A1 is colored Red 
       and A2 is colored Blue.
Case 2: A1 is colored Blue 
       and A2 is colored Red.
No. of ways : 2      

Input : N = 3, K = 3.
Output : 
A1, A2, A3 are the nodes. 
A1 is parent of A2 
and A2 is parent of A3.
Let colors be R, B, G.
A1 can choose any three colors 
and A2 can choose 
any other two colors
and A3 can choose 
any other two colors 
than its parents.
No. of ways: 12
```

注意**只有根**和**子**(子，孙，孙。和所有)应该有**不同的**颜色。树根可以选择 K 种颜色中的任何一种。每隔一个节点可以选择其父节点以外的其他 K-1 颜色。所以每个节点都有 K-1 个选择。
这里，我们选择树作为每个节点作为唯一的一个子节点。我们可以为树根选择任何 K 种颜色，所以 K 种方式。而我们留给它的孩子的是 K-1 的颜色。所以对于每个孩子，我们可以给他们指定一种不同于父母的颜色。因此，对于 N-1 个节点中的每一个，我们只剩下 K-1 种颜色。因此答案是 **K*(K-1)^(N-1)** 。
我们可以利用时间复杂度为 O(N)的正态幂函数来寻找答案。但是为了获得更好的时间复杂度，我们使用了取 0(对数 N)时间复杂度的快速指数函数。

## C++

```
// C++ program to count number of ways to color
// a N node skewed tree with k colors such that
// parent and children have different colors.
#include <bits/stdc++.h>
using namespace std;

// fast_way is recursive
// method to calculate power
int fastPow(int N, int K)
{
    if (K == 0)
        return 1;
    int temp = fastPow(N, K / 2);
    if (K % 2 == 0)
        return temp * temp;
    else
        return N * temp * temp;
}

int countWays(int N, int K)
{
    return K * fastPow(K - 1, N - 1);
}

// driver program
int main()
{
    int N = 3, K = 3;
    cout << countWays(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of ways to color
// a N node skewed tree with k colors such that
// parent and children have different colors.
import java.io.*;

class GFG {
    // fast_way is recursive
    // method to calculate power
    static int fastPow(int N, int K)
    {
        if (K == 0)
            return 1;
        int temp = fastPow(N, K / 2);
        if (K % 2 == 0)
            return temp * temp;
        else
            return N * temp * temp;
    }

    static int countWays(int N, int K)
    {
        return K * fastPow(K - 1, N - 1);
    }

    // Driver program
    public static void main(String[] args)
    {
        int N = 3, K = 3;
        System.out.println(countWays(N, K));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to count 
# number of ways to color
# a N node skewed tree with
# k colors such that parent
# and children have different
# colors.

# fast_way is recursive
# method to calculate power
def fastPow(N, K):
    if (K == 0):
        return 1;

    temp = fastPow(N, int(K / 2));
    if (K % 2 == 0):
        return temp * temp;
    else:
        return N * temp * temp;

def countWays(N, K):
    return K * fastPow(K - 1, N - 1);

# Driver Code
N = 3;
K = 3;
print(countWays(N, K));

# This code is contributed by mits
```

## C#

```
// C# program to count number of ways
// to color a N node skewed tree with
// k colors such that parent and
// children  have different colors
using System;

class GFG {

    // fast_way is recursive
    // method to calculate power
    static int fastPow(int N, int K)
    {
        if (K == 0)
            return 1;
        int temp = fastPow(N, K / 2);
        if (K % 2 == 0)
            return temp * temp;
        else
            return N * temp * temp;
    }

    static int countWays(int N, int K)
    {
        return K * fastPow(K - 1, N - 1);
    }

    // Driver code
    public static void Main()
    {
        int N = 3, K = 3;
        Console.WriteLine(countWays(N, K));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number
// of ways to color a N node
// skewed tree with k colors
// such that parent and children
// have different colors.

// fast_way is recursive
// method to calculate power
function fastPow($N, $K)
{
    if ($K == 0)
        return 1;

    $temp = fastPow($N, $K / 2);

    if ($K % 2 == 0)
        return $temp * $temp;
    else
        return $N * $temp * $temp;
}

function countWays($N, $K)
{
    return $K * fastPow($K - 1, $N - 1);
}

    // Driver Code
    $N = 3;
    $K = 3;
    echo countWays($N, $K);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to count number of ways to color
// a N node skewed tree with k colors such that
// parent and children have different colors.

    // fast_way is recursive
    // method to calculate power
    function fastPow(N, K)
    {
        if (K == 0)
            return 1;
        let temp = fastPow(N, Math.floor(K / 2));
        if (K % 2 == 0)
            return temp * temp;
        else
            return N * temp * temp;
    }

    function countWays(N, K)
    {
        return K * fastPow(K - 1, N - 1);
    }

// Driver code
    let N = 3, K = 3;
    document.write(countWays(N, K));

    // This code is contributed by sanjoy_62.
</script>
```

## java 描述语言

```
<script>

// Javascript program to count number of ways to color
// a N node skewed tree with k colors such that
// parent and children have different colors.

    // fast_way is recursive
    // method to calculate power
    function fastPow(N, K)
    {
        if (K == 0 || N == 0)
            return 1;
        return K *(K - 1)*(N - 1);
    }

// Driver code
    let N = 3, K = 3;
    document.write(fastPow(N, K));

    // This code is contributed by sanjoy_62.
</script>
```

**输出:**

```
 12
```

**时间复杂度:** O(对数 N)

**辅助空间:** O(1)
本文由**哈沙·莫加利**供稿。如果你喜欢极客博客并想投稿，你也可以用 write.geeksforgeeks.org 写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。