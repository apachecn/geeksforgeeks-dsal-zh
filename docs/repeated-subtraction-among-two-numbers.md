# 两个数重复相减

> 原文:[https://www . geesforgeks . org/重复-两数相减/](https://www.geeksforgeeks.org/repeated-subtraction-among-two-numbers/)

给定一对正数 x 和 y。我们反复从大的整数中减去两个整数中较小的一个，直到其中一个整数变成 0。任务是在我们停止之前计算步数(其中一个数字变成 0)。
**例:**

```
Input : x = 5, y = 13
Output : 6
Explanation : There are total 6 steps before 
we reach 0:
(5,13) --> (5,8) --> (5,3) --> (2,3) 
--> (2,1) --> (1,1) --> (1,0).

Input : x = 3, y = 5
Output : 4
Explanation : There are 4 steps:
(5,3) --> (2,3) --> (2,1) --> (1,1) --> (1,0)

Input : x = 100, y = 19
Output : 13
```

一个简单的解决方案是实际遵循流程并计算步骤数。
更好的解决方法是使用下面的步骤。让 y 是两个数字中较小的一个
1)如果 y 除 x 然后返回(x/y)
2)否则返回((x/y) +求解(y，x%y) )
**说明:**
如果我们从(x，y)开始，y 除 x，那么答案将是(x/y)，因为我们可以从 x 减去 y 正好(x/y)次。
对于另一种情况，我们举个例子看看它是如何工作的:(100，19)
我们可以把 100 减去 19 正好[100/19] = 5 次得到(19，5)。
我们可以把 19 减去 5 正好[19/5] = 3 次得到(5，4)。
我们可以用 5 减去 4 正好[5/4] = 1 次得到(4，1)。
我们可以用 4 减去 1，正好[4/1] = 4 次，得到(1，0)
因此总共有 5 + 3 + 1 + 4 = 13 步。
以下是基于上述思路的实现。

## C++

```
// C++ program to count of steps until one
// of the two numbers become 0.
#include<bits/stdc++.h>
using namespace std;

// Returns count of steps before one
// of the numbers become 0 after repeated
// subtractions.
int countSteps(int x, int y)
{
    // If y divides x, then simply return
    // x/y.
    if (x%y == 0)
        return x/y;

    // Else recur. Note that this function
    // works even if x is smaller than y because
    // in that case first recursive call exchanges
    // roles of x and y.
    return x/y + countSteps(y, x%y);
}

// Driver code
int main()
{
   int x = 100, y = 19;
   cout << countSteps(x, y);
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count of
// steps until one of the
// two numbers become 0.
import java.io.*;

class GFG
{

// Returns count of steps
// before one of the numbers
// become 0 after repeated
// subtractions.
static int countSteps(int x,
                      int y)
{
    // If y divides x, then
    // simply return x/y.
    if (x % y == 0)
        return x / y;

    // Else recur. Note that this
    // function works even if x is
    // smaller than y because
    // in that case first recursive
    // call exchanges roles of x and y.
    return x / y + countSteps(y, x % y);
}

// Driver code
public static void main (String[] args)
{
    int x = 100, y = 19;
    System.out.println(countSteps(x, y));

}
}

// This code is contributed by aj_36
```

## 蟒蛇 3

```
# Python3 program to count of steps until
# one of the two numbers become 0.
import math

# Returns count of steps before one of
# the numbers become 0 after repeated
# subtractions.
def countSteps(x, y):

    # If y divides x, then simply
    # return x/y.
    if (x % y == 0):
        return math.floor(x / y);

    # Else recur. Note that this function
    # works even if x is smaller than y
    # because in that case first recursive
    # call exchanges roles of x and y.
    return math.floor((x / y) +
           countSteps(y, x % y));

# Driver code
x = 100;
y = 19;
print(countSteps(x, y));

# This code is contributed by mits
```

## C#

```
// C# program to count of
// steps until one of the
// two numbers become 0.
using System;

class GFG
{
// Returns count of steps
// before one of the numbers
// become 0 after repeated
// subtractions.
static int countSteps(int x,
                      int y)
{
    // If y divides x, then
    // simply return x/y.
    if (x % y == 0)
        return x / y;

    // Else recur. Note that this
    // function works even if x is
    // smaller than y because
    // in that case first recursive
    // call exchanges roles of x and y.
    return x / y + countSteps(y, x % y);
}

// Driver Code
static public void Main ()
{
int x = 100, y = 19;
Console.WriteLine(countSteps(x, y));
}
}

// This code is contributed by m_kit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count of
// steps until one of the
// two numbers become 0.

// Returns count of steps
// before one of the numbers
// become 0 after repeated
// subtractions.
function countSteps($x, $y)
{
    // If y divides x, then
    // simply return x/y.
    if ($x % $y == 0)
        return floor(((int)$x / $y));

    // Else recur. Note that this
    // function works even if x is
    // smaller than y because in that
    // case first recursive call
    // exchanges roles of x and y.
    return floor(((int)$x / $y) +
                   countSteps($y, $x % $y));
}

// Driver code
$x = 100;
$y = 19;
echo countSteps($x, $y);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// Javascript program to count of steps until one
// of the two numbers become 0.

// Returns count of steps before one
// of the numbers become 0 after repeated
// subtractions.
function countSteps(x, y)
{
    // If y divides x, then simply return
    // x/y.
    if (x%y == 0)
        return Math.floor(x/y);

    // Else recur. Note that this function
    // works even if x is smaller than y because
    // in that case first recursive call exchanges
    // roles of x and y.
    return Math.floor(x/y) + countSteps(y, x%y);
}

// Driver code

    let x = 100, y = 19;
    document.write(countSteps(x, y));

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
13
```

***时间复杂度:** O(log(n))*

***辅助空间:** O(1)*
本文由 **Shubham Agrawal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。