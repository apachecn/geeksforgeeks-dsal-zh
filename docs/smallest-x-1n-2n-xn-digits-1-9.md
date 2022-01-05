# 最小的 x，使得 1*n，2*n，… x*n 具有从 1 到 9 的所有数字

> 原文:[https://www . geesforgeks . org/minist-x-1n-2n-xn-digits-1-9/](https://www.geeksforgeeks.org/smallest-x-1n-2n-xn-digits-1-9/)

给定一个正数 n。我们需要找到 x，这样 1*n，2*n，3*n…..x*n 给所有 10 位数字至少一次。如果没有这样的 x，打印-1。
**例:**

```
Input : n = 1692
Output : 3
Explanation:
n = 1692, we got the digits- 1, 2, 6, 9
2*n = 3384, we got the digits- 1, 2, 3, 4, 
6, 8, 9.
3*n = 5076, we got the digits- 1, 2, 3, 4, 
5, 6, 7, 8, 9.
At this step we got all the digits at least
once. Therefore our answer is 3.

Input  : 1
Output : 10

Input  : 0
Output :-1
```

这里使用的想法很简单。我们从 1 开始，不断与 n 相乘，直到我们至少一次没有得到所有的 10 位数。为了跟踪每次迭代中出现的所有数字，我们使用了一个大小为 10 的临时数组，最初所有数字都是零。每当我们第一次得到一个数字时，我们就用 1 初始化它在数组中的索引。当所有数字都被访问一次时，我们就完成了。
下面是它的实现。

## C++

```
// CPP program to find x such that 1*n, 2*n, 3*n
// ...x * n have all digits from 1 to 9 at least
// once
#include <bits/stdc++.h>
using namespace std;

// Returns smallest value x such that 1*n, 2*n,
// 3*n ...x * n have all digits from 1 to 9 at
// least once
int smallestX(int n)
{
    // taking temporary array and variable.
    int temp[10] = { 0 };

    if (n == 0)
        return -1;

    // iterate till we get all the 10 digits
    // at least once
    int count = 0, x = 0;
    for (x = 1; count < 10; x++) {
        int y = x * n;

        // checking all the digits
        while (y) {
            if (temp[y % 10] == false) {
                count++;
                temp[y % 10] = true;
            }
            y /= 10;
        }
    }
    return x - 1;
}

// driver function
int main()
{
    int n = 5;
    cout <<smallestX(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find x such
// that 1*n, 2*n, 3*n...x * n
// have all digits from 1 to 9
// at least once
import java.io.*;
import java.util.*;

class GFG
{

// Returns smallest value x
// such that 1*n, 2*n, 3*n
// ...x * n have all digits
// from 1 to 9 at least once
public static int smallestX(int n)
{
    // taking temporary
    // array and variable.
    int[] temp = new int[10];
    for(int i = 0; i < 10; i++)
    temp[i] = 0;

    if (n == 0)
        return -1;

    // iterate till we get
    // all the 10 digits
    // at least once
    int count = 0, x = 0;
    for (x = 1; count < 10; x++)
    {
        int y = x * n;

        // checking all
        // the digits
        while (y > 0)
        {
            if (temp[y % 10] == 0)
            {
                count++;
                temp[y % 10] = 1;
            }
            y /= 10;
        }
    }
    return x - 1;
}

// Driver Code
public static void main(String args[])
{
    int n = 5;
    System.out.print(smallestX(n));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 蟒蛇 3

```
# Python3 program to find x such
# that 1*n, 2*n, 3*n ...x * n
# have all digits from 1 to 9
# at least once

# Returns smallest value x such
# that 1*n, 2*n, 3*n ...x * n
# have all digits from 1 to 9
# at least once
def smallestX(n):
    # taking temporary
    # array and variable.
    temp = [0]*10

    if (n == 0):
        return -1

    # iterate till we get
    # all the 10 digits
    # at least once
    count = 0
    x = 1
    while(count < 10):
        y = x * n

        # checking all
        # the digits
        while (y>0):
            if (temp[y % 10] == 0):
                count+=1
                temp[y % 10] = 1
            y = int(y / 10)
        x+=1

    return x - 1

# Driver code
if __name__=='__main__':
    n = 5
    print(smallestX(n))

# This code is contributed
# by mits
```

## C#

```
// C# program to find x such
// that 1*n, 2*n, 3*n...x * n
// have all digits from 1 to 9
// at least once
using System;

class GFG
{

// Returns smallest value x
// such that 1*n, 2*n, 3*n
// ...x * n have all digits
// from 1 to 9 at least once
public static int smallestX(int n)
{
    // taking temporary
    // array and variable.
    int[] temp = new int[10];
    for(int i = 0; i < 10; i++)
    temp[i] = 0;

    if (n == 0)
        return -1;

    // iterate till we get
    // all the 10 digits
    // at least once
    int count = 0, x = 0;
    for (x = 1; count < 10; x++)
    {
        int y = x * n;

        // checking all the digits
        while (y > 0)
        {
            if (temp[y % 10] == 0)
            {
                count++;
                temp[y % 10] = 1;
            }
            y /= 10;
        }
    }
    return x - 1;
}

// dDriver Code
static void Main()
{
    int n = 5;
    Console.Write(smallestX(n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find x such
// that 1*n, 2*n, 3*n ...x * n
// have all digits from 1 to 9
// at least once

// Returns smallest value x such
// that 1*n, 2*n, 3*n ...x * n
// have all digits from 1 to 9
// at least once
function smallestX($n)
{
    // taking temporary
    // array and variable.
    $temp = array_fill(0, 10, false);

    if ($n == 0)
        return -1;

    // iterate till we get
    // all the 10 digits
    // at least once
    $count = 0;
    $x = 0;
    for ($x = 1; $count < 10; $x++)
    {
        $y = $x * $n;

        // checking all
        // the digits
        while ($y)
        {
            if ($temp[$y % 10] == false)
            {
                $count++;
                $temp[$y % 10] = true;
            }
            $y = (int)($y / 10);
        }
    }
    return $x - 1;
}

// Driver code
$n = 5;
echo smallestX($n);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find x such
// that 1*n, 2*n, 3*n...x * n
// have all digits from 1 to 9
// at least once

// Returns smallest value x
// such that 1*n, 2*n, 3*n
// ...x * n have all digits
// from 1 to 9 at least once
function smallestX(n)
{
    // taking temporary
    // array and variable.
    let temp = Array.from({length: 10},
              (_, i) => 0);
    for(let i = 0; i < 10; i++)
    temp[i] = 0;

    if (n == 0)
        return -1;

    // iterate till we get
    // all the 10 digits
    // at least once
    let count = 0, x = 0;
    for (x = 1; count < 10; x++)
    {
        let y = x * n;

        // checking all
        // the digits
        while (y > 0)
        {
            if (temp[y % 10] == 0)
            {
                count++;
                temp[y % 10] = 1;
            }
            y /= 10;
        }
    }
    return x - 1;
}

// driver program

    let n = 5;
    document.write(smallestX(n));

</script>
```

**输出:**

```
18
```

本文由**萨洛尼·古普塔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。