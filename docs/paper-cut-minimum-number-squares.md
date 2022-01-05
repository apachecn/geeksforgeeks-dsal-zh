# 切割成最小方块数的纸张

> 原文:[https://www . geesforgeks . org/剪纸-最小数字-方块/](https://www.geeksforgeeks.org/paper-cut-minimum-number-squares/)

给定一张大小为 A x B 的纸，任务是将纸切成任何大小的正方形。找出能从纸上切下的最小方块数。
**例:**

```
Input  : 13 x 29
Output : 9
Explanation : 
2 (squares of size 13x13) + 
4 (squares of size 3x3) + 
3 (squares of size 1x1)=9

Input  : 4 x 5
Output : 5
Explanation : 
1 (squares of size 4x4) + 
4 (squares of size 1x1)
```

我们知道，如果我们想从纸上切下最小数量的正方形，那么我们必须首先从纸上切下最大的正方形，最大的正方形将与纸的较小的一边具有相同的边。例如，如果纸张的尺寸是 13 x 29，那么最大的正方形是 13 边。所以我们可以切 2 个尺寸为 13×13(29/13 = 2)的正方形。现在剩余的纸张大小将为 3 x 13。同样，我们可以用 4 个大小为 3×3 的正方形和 3 个大小为 1×1 的正方形来切割剩余的纸张。所以从 13×29 的纸上至少可以切下 9 个正方形。

![dig1](img/88526aabe723f6bf2a25b758f5db2fbb.png)

下面是上述方法的实现。

## C++

```
// C++ program to find minimum number of squares
// to cut a paper.
#include<bits/stdc++.h>
using namespace std;

// Returns min number of squares needed
int minimumSquare(int a, int b)
{
    long long result = 0, rem = 0;

    // swap if a is small size side .
    if (a < b)
        swap(a, b);

    // Iterate until small size side is
    // greater then 0
    while (b > 0)
    {
        // Update result
        result += a/b;

        long long rem = a % b;
        a = b;
        b = rem;
    }

    return result;
}

// Driver code
int main()
{
    int n = 13, m = 29;
    cout << minimumSquare(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum
// number of squares to cut a paper.
class GFG{

// To swap two numbers
static void swap(int a,int b)
{
    int temp = a;
    a = b;
    b = temp;
}

// Returns min number of squares needed
static int minimumSquare(int a, int b)
{
    int result = 0, rem = 0;

    // swap if a is small size side .
    if (a < b)
        swap(a, b);

    // Iterate until small size side is
    // greater then 0
    while (b > 0)
    {
        // Update result
        result += a/b;
        rem = a % b;
        a = b;
        b = rem;
    }

    return result;
}

// Driver code
public static void main(String[] args)
{
    int n = 13, m = 29;
    System.out.println(minimumSquare(n, m));
}
}

//This code is contributed by Smitha Dinesh Semwal.
```

## 蟒蛇 3

```
# Python 3 program to find minimum
# number of squares to cut a paper.

# Returns min number of squares needed
def minimumSquare(a, b):

    result = 0
    rem = 0

    # swap if a is small size side .
    if (a < b):
        a, b = b, a

    # Iterate until small size side is
    # greater then 0
    while (b > 0):

        # Update result
        result += int(a / b)

        rem = int(a % b)
        a = b
        b = rem

    return result

# Driver code
n = 13
m = 29

print(minimumSquare(n, m))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to find minimum
// number of squares to cut a paper.
using System;

class GFG
{

// To swap two numbers
static void swap(int a, int b)
{
    int temp = a;
    a = b;
    b = temp;
}

// Returns min number of squares needed
static int minimumSquare(int a, int b)
{
    int result = 0, rem = 0;

    // swap if a is small size side .
    if (a < b)
        swap(a, b);

    // Iterate until small size side is
    // greater then 0
    while (b > 0)
    {
        // Update result
        result += a / b;
        rem = a % b;
        a = b;
        b = rem;
    }
    return result;
}

// Driver code
public static void Main(String[] args)
{
    int n = 13, m = 29;
    Console.WriteLine(minimumSquare(n, m));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find
// minimum number of squares
// to cut a paper.

// Returns min number of squares needed
function minimumSquare(a, b)
{
    let result = 0, rem = 0;

    // swap if a is small size side .
    if (a < b) {
        let temp = a;
        a = b;
        b = temp;
    }

    // Iterate until small size side is
    // greater then 0
    while (b > 0)
    {
        // Update result
        result += parseInt(a/b);

        let rem = a % b;
        a = b;
        b = rem;
    }

    return result;
}

// Driver code
    let n = 13, m = 29;
    document.write(minimumSquare(n, m));

</script>
```

**输出:**

```
9
```

**注意，上面的贪婪解并不总是产生最优结果**。例如，如果输入是 36 x 30，上面的算法将产生输出 6，但是我们可以将纸张切割成 5 个正方形
1)三个 12 x 12 的正方形
2)两个 18 x 18 的正方形。
感谢谢尔盖·佩雷斯拉夫采夫指出上述情况。
本文由**库尔迪普·辛格(kulli_d_coder)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。