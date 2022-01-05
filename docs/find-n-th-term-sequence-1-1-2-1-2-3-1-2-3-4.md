# 求序列 1、1、2、1、2、3、1、2、3、4、…。

> 原文:[https://www . geesforgeks . org/find-n-th-term-sequence-1-1-2-1-2-3-1-2-3-4/](https://www.geeksforgeeks.org/find-n-th-term-sequence-1-1-2-1-2-3-1-2-3-4/)

考虑整数的无穷序列:1，1，2，1，2，3，1，2，3，4，1，2，3，4，5…序列是这样建立的:首先写出数字 1，然后是数字 1 到 2，然后是数字 1 到 3，然后是数字 1 到 4，依此类推。
求序列第 n 个位置的数字。
**例:**

```
Input : n = 3
Output : 2
The 3rd number in the sequence is 2.

Input : 55
Output : 10
```

**First Approach:** 思路是先求 n 的块数，要确定第 n 个数的块，我们先从 n 中减去 1(第一块的元素个数)，再减去 2，再减去 3，以此类推，直到得到负 n，减法的个数将是块的个数，块中的位置将是我们得到的最后一个非负数。

## C++

```
// CPP program to find the
// value at n-th place in
// the given sequence
#include <bits/stdc++.h>
using namespace std;

// Returns n-th number in sequence
// 1, 1, 2, 1, 2, 3, 1, 2, 4, ...
int findNumber(int n)
{
    n--;

    // One by one subtract counts
    // elements in different blocks
    int i = 1;
    while (n >= 0)
    {
        n -= i;
        ++i;
    }

    return (n + i);
}

// Driver code
int main()
{
    int n = 3;
    cout << findNumber(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// value at n-th place in
// the given sequence

import java.io.*;

class GFG
{

    // Returns n-th number in sequence
    // 1, 1, 2, 1, 2, 3, 1, 2, 4, ...
    static int findNumber(int n)
    {
        n--;

        // One by one subtract counts
        // elements in different blocks
        int i = 1;
        while (n >= 0)
        {
            n -= i;
            ++i;
        }

        return (n + i);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 3;

        System.out.println(findNumber(n));
    }
}

// This code is contributed by Ajit.
```

## 蟒蛇 3

```
# Python code to find the value at
# n-th place in the given sequence

# Returns n-th number in sequence
# 1, 1, 2, 1, 2, 3, 1, 2, 4, ...
def findNumber( n ):

    n -= 1

    # One by one subtract counts
    # elements in different blocks
    i = 1
    while n >= 0:
        n -= i
        i += 1
    return (n + i)

# Driver code
n = 3
print(findNumber(n))

# This code is contributed
# by "Sharad_Bhardwaj".
```

## C#

```
// C# program to find the
// value at n-th place in
// the given sequence
using System;

class GFG
{

    // Returns n-th number in sequence
    // 1, 1, 2, 1, 2, 3, 1, 2, 4, ...
    static int findNumber(int n)
    {
        n--;

        // One by one subtract counts
        // elements in different blocks
        int i = 1;
        while (n >= 0)
        {
            n -= i;
            ++i;
        }

        return (n + i);
    }

    // Driver code
    public static void Main()
    {
        int n = 3;
        Console.WriteLine(findNumber(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// value at n-th place in
// the given sequence

// Returns n-th number in sequence
// 1, 1, 2, 1, 2, 3, 1, 2, 4, ...
function findNumber( $n)
{
    $n--;

    // One by one subtract counts
    // elements in different blocks
    $i = 1;
    while ($n >= 0)
    {
        $n -= $i;
        ++$i;
    }

    return ($n + $i);
}

// Driver code
$n = 3;
echo findNumber($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find the
    // value at n-th place in
    // the given sequence

    // Returns n-th number in sequence
    // 1, 1, 2, 1, 2, 3, 1, 2, 4, ...
    function findNumber(n)
    {
        n--;

        // One by one subtract counts
        // elements in different blocks
        let i = 1;
        while (n >= 0)
        {
            n -= i;
            ++i;
        }
        return (n + i);
    }

// Driver code
    let n = 3;
    document.write(findNumber(n));

    // This code is contributed by mukesh07.
</script>
```

**输出:**

```
2
```

时间复杂度:O(√n)
**第二种方法:**无限序列的答案可以在 O(1)中完成。我们可以将序列组织为:1 (1)。这意味着第一行的位置是 1，2 (2) 1，2，3 (4) 1，2，3，4 (7) 1，2，3，4，5 (11)然后我们会有一个新的序列，这更容易找到。1 (1) 2 (2) 4 (3) 7 (4) 11 括号中的数字是新序列的数字之间的距离。
要找到数的基数，我们需要解方程 n = x(x+1)/2+1[或 x^2+x+2–2n = 0]。我们需要隔离 x(获得最大地板值)。
然后我们使用在同一个公式中得到的 x，但是现在结果将是这条线的基数。我们只需要计算作为输入的数字和作为基数的数字之间的距离。

```
n — base + 1
```

## C++

```
// CPP program to find the
// value at n-th place in
// the given sequence
#include <bits/stdc++.h>
using namespace std;

// Definition of findNumber
// function
int findNumber(int n)
{
    // Finding x from equation
    // n = x(x + 1)/2 + 1
    int x = (int)floor((-1 +
             sqrt(1 + 8 * n - 8)) / 2);

    // Base of current block
    int base = (x * (x + 1)) / 2 + 1;

    // Value of n-th element
    return n - base + 1;
}

// Driver code
int main()
{
    int n = 55;
    cout << findNumber(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// value at n-th place in
// the given sequence

import java.io.*;

class GFG
{

    // Definition of findNumber function
    static int findNumber(int n)
    {

        // Finding x from equation
        // n = x(x + 1)/2 + 1
        int x = (int)Math.floor((-1 +
                Math.sqrt(1 + 8 * n - 8)) / 2);

        // Base of current block
        int base = (x * (x + 1)) / 2 + 1;

        // Value of n-th element
        return n - base + 1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 55;

        System.out.println(findNumber(n));
    }
}

// This code is contributed by Ajit.
```

## 蟒蛇 3

```
# Python program to find
# the value at n-th place
# in the given sequence
import math

# Definition of findNumber function
def findNumber( n ):

    # Finding x from equation
    # n = x(x + 1)/2 + 1
    x = int(math.floor((-1 + math.sqrt(1
            + 8 * n - 8)) / 2))

    # Base of current block
    base = (x * (x + 1)) / 2 + 1

    # Value of n-th element
    return n - base + 1

# Driver code
n = 55
print(findNumber(n))

# This code is contributed
# by "Abhishek Sharma 44"
```

## C#

```
// C# program to find the
// value at n-th place in
// the given sequence
using System;

class GFG
{

    // Definition of findNumber function
    static int findNumber(int n)
    {

        // Finding x from equation
        // n = x(x + 1)/2 + 1
        int x = (int)Math.Floor((-1 +
        Math.Sqrt(1 + 8 * n - 8)) / 2);

        // Base of current block
        int Base = (x * (x + 1)) / 2 + 1;

        // Value of n-th element
        return n - Base + 1;
    }

    // Driver code
    public static void Main()
    {
        int n = 55;
        Console.WriteLine(findNumber(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// value at n-th place in
// the given sequence

// Definition of findNumber function
function findNumber($n)
{
    // Finding x from equation
    // n = x(x + 1)/2 + 1
    $x = floor((-1 + sqrt(1 +
                8 * $n - 8)) / 2);

    // Base of current block
    $base = ($x * ($x + 1)) / 2 + 1;

    // Value of n-th element
    return $n - $base + 1;
}

// Driver code
$n = 55;
echo findNumber($n) ;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find the
    // value at n-th place in
    // the given sequence

    // Definition of findNumber
    // function
    function findNumber(n)
    {
        // Finding x from equation
        // n = x(x + 1)/2 + 1
        let x = Math.floor((-1 + Math.sqrt(1 + 8 * n - 8)) / 2);

        // Base of current block
        let base = (x * (x + 1)) / 2 + 1;

        // Value of n-th element
        return n - base + 1;
    }

    let n = 55;
    document.write(findNumber(n));

// This code is contributed by suresh07.
</script>
```

**输出:**

```
10 
```

**时间复杂度:** O(1)
本文由 [**萨加尔·舒克拉**](https://auth.geeksforgeeks.org/profile.php?user=Sagar Shukla) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。