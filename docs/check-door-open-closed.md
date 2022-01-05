# 检查门是开着还是关着

> 原文:[https://www.geeksforgeeks.org/check-door-open-closed/](https://www.geeksforgeeks.org/check-door-open-closed/)

给定 n 扇门和 n 个人。门的编号为 1 到 n，每个人的身份证号为 1 到 n。每个门只能有两种打开和关闭状态。最初所有的门都处于关闭状态。如果某人更改了所有门的当前状态，即如果状态为打开，则更改为关闭，反之亦然，则查找所有门的最终状态。如果“j”是“I”的倍数，则 id 为“I”的人有权更改编号为“j”的门的状态。
**注意:**
–一个人必须准确地改变一次他被授权的所有门的当前状态。
–可能会出现这样的情况:在一个人更改门的状态之前，另一个同样获得同一扇门授权的人更改了门的状态。
**例:**

```
Input : 3
Output : open closed closed
```

**说明:**由于 n = 3，因此有
3 个门{1，2，3}和
3 个 id 为{1，2，3}的人
id = 1 的人可以更改门 1，2，3 的状态
id = 2 的人可以更改门 2 的状态
id = 3 的人可以更改门 3 的状态
所有门的当前状态:关闭关闭关闭
考虑一系列事件，

1.  id = 1 的人改变门 2 的状态
    所有门的当前状态:关闭打开关闭
2.  id = 3 的人改变门 3 的状态
    所有门的当前状态:关闭打开打开
3.  id = 1 的人改变门 1、3 的状态
    所有门的当前状态:打开打开关闭
4.  id = 2 的人改变门 2 的状态
    所有门的当前状态:打开关闭关闭

**另一个例子:**

```
Input : 5
Output : open closed closed open closed

Note: Sequence of open/closed is displayed in
increasing door number 
```

**方法:**是数学逻辑方法。如果我们观察得当，那么我们会发现编号为 **i** 的门的最终状态是打开的，如果‘I’有奇数个因子，则状态是关闭的，如果‘I’有偶数个因子。它不取决于门的状态改变的顺序。要知道数的除数是偶数还是奇数，可以看[查看除数是偶数还是奇数](https://www.geeksforgeeks.org/check-if-total-number-of-divisors-are-even-or-odd/)帖子。

## C++

```
// C++ implementation of
// doors open or closed
#include <bits/stdc++.h>
using namespace std;

// Function to check whether 'n'
// has even number of factors or not
bool hasEvenNumberOfFactors(int n)
{
    int root_n = sqrt(n);

    // if 'n' is a perfect square
    // it has odd number of factors
    if ((root_n*root_n) == n)
        return false;

    // else 'n' has even
    // number of factors
    return true;
}

// Function to find and print
// status of each door
void printStatusOfDoors(int n)
{
    for (int i=1; i<=n; i++)
    {
        // If even number of factors
        // final status is closed
        if (hasEvenNumberOfFactors(i))
            cout << "closed" << " ";

        // else odd number of factors
        // final status is open
        else
            cout << "open" << " ";
    }
}

// Driver program
int main()
{
    int n = 5;
    printStatusOfDoors(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java implementation of
// doors open or closed
import java.io.*;

class GFG {

    // Function to check whether 'n'
    // has even number of factors or not
    static boolean hasEvenNumberOfFactors(int n)
    {
        double root_n = Math.sqrt(n);

        // if 'n' is a perfect square
        // it has odd number of factors
        if ((root_n*root_n) == n)
            return false;

        // else 'n' has even
        // number of factors
        return true;
    }

    // Function to find and print
    // status of each door
    static void printStatusOfDoors(int n)
    {
        for (int i = 1 ; i <= n; i++)
        {
            // If even number of factors
            // final status is closed
            if (hasEvenNumberOfFactors(i))
                System .out.print( "closed" + " ");

            // else odd number of factors
            // final status is open
            else
                System.out.print( "open" + " ");
        }
    }

    // Driver program
    public static void main (String[] args) {
        int n = 5;
        printStatusOfDoors(n);

    }
}

// This article is contributed by vt_m
```

## 蟒蛇 3

```
# Python 3 implementation of
# doors open or closed
import math

# Function to check whether
# 'n' has even number of
# factors or not
def hasEvenNumberOfFactors(n):

    root_n = math.sqrt(n)

    # if 'n' is a perfect square
    # it has odd number of factors
    if ((root_n * root_n) == n):
        return False

    # else 'n' has even
    # number of factors
    return True

# Function to find and print
# status of each door
def printStatusOfDoors(n):

    for i in range(1, n + 1):

        # If even number of factors
        # final status is closed
        if (hasEvenNumberOfFactors(i) == True):
            print("closed", end =" ")

        # else odd number of factors
        # final status is open
        else:
            print("open", end =" ")

# Driver program
n = 5

printStatusOfDoors(n)

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# implementation of
// doors open or closed
using System;

class GFG
{

// Function to check whether
// 'n' has even number of
// factors or not
static bool hasEvenNumberOfFactors(int n)
{
    double root_n = Math.Sqrt(n);

    // if 'n' is a perfect square
    // it has odd number of factors
    if ((root_n * root_n) == n)
        return false;

    // else 'n' has even
    // number of factors
    return true;
}

// Function to find and print
// status of each door
static void printStatusOfDoors(int n)
{
    for (int i = 1 ; i <= n; i++)
    {
        // If even number of factors
        // final status is closed
        if (hasEvenNumberOfFactors(i))
            Console.Write("closed" + " ");

        // else odd number of factors
        // final status is open
        else
            Console.Write("open" + " ");
    }
}

// Driver Code
static public void Main ()
{
    int n = 5;
    printStatusOfDoors(n);
}
}

// This Code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of
// doors open or closed

// Function to check whether
// 'n' has even number of
// factors or not

function hasEvenNumberOfFactors($n)
{
    $root_n = sqrt($n);

    // if 'n' is a perfect square
    // it has odd number of factors
    if (($root_n * $root_n) == $n)
        return false;

    // else 'n' has even
    // number of factors
    return true;
}

// Function to find and print
// status of each door
function printStatusOfDoors($n)
{
    for ($i = 1; $i <= $n; $i++)
    {
        // If even number of factors
        // final status is closed
        if (hasEvenNumberOfFactors($i))
            echo "closed" ," ";

        // else odd number of factors
        // final status is open
        else
            echo "open" ," ";
    }
}

// Driver Code
$n = 5;
printStatusOfDoors($n);

// This code is contributed by ajit@
?>
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to check whether 'n'
    // has even number of factors or not
    function hasEvenNumberOfFactors(n)
    {
        let root_n = Math.sqrt(n);

        // if 'n' is a perfect square
        // it has odd number of factors
        if ((root_n*root_n) == n)
            return false;

        // else 'n' has even
        // number of factors
        return true;
    }

    // Function to find and print
    // status of each door
    function printStatusOfDoors(n)
    {
        for (let i = 1 ; i <= n; i++)
        {
            // If even number of factors
            // final status is closed
            if (hasEvenNumberOfFactors(i))
                document.write( "closed" + " ");

            // else odd number of factors
            // final status is open
            else
                document.write( "open" + " ");
        }
    }

// Driver Code

    let n = 5;
    printStatusOfDoors(n);

// This code is contributed by susmitakundugoaldanga.
</script>
```

**输出:**

```
open closed closed open closed
```

**时间复杂度:** O(n)
参考文献:在 TCS
的采访中被问到本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。