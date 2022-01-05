# 如何关闭数字中的特定位？

> 原文:[https://www . geesforgeks . org/如何关闭数字中的特定位/](https://www.geeksforgeeks.org/how-to-turn-off-a-particular-bit-in-a-number/)

给定数字 n 和值 k，关闭 n 中的第 k 位。请注意，k = 1 表示最右边的位。
示例:

```
Input:  n = 15, k = 1
Output: 14

Input:  n = 14, k = 1
Output: 14
The rightmost bit was already off, so no change.

Input:  n = 15, k = 2
Output: 13

Input:  n = 15, k = 3
Output: 11

Input:  n = 15, k = 4
Output: 7

Input:  n = 15, k >= 5
Output: 15 
```

其思想是使用按位<**~(1<<(k–1))**，我们得到一个除了第 k 位之外所有位都已设置的数。如果我们用 n 对这个表达式进行按位&，我们得到一个数，除了第 k 位为 0 之外，所有位都与 n 相同。
下面是上面想法的实现。

## C++

```
#include <iostream>
using namespace std;

// Returns a number that has all bits same as n
// except the k'th bit which is made 0
int turnOffK(int n, int k)
{
    // k must be greater than 0
    if (k <= 0) return n;

    // Do & of n with a number with all set bits except
    // the k'th bit
    return (n & ~(1 << (k - 1)));
}

// Driver program to test above function
int main()
{
    int n = 15;
    int k = 4;
    cout << turnOffK(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to turn off a particular bit in a number
import java.io.*;

class TurnOff
{
    // Function to returns a number that has all bits same as n
    // except the k'th bit which is made 0
    static int turnOffK(int n, int k)
    {
        // k must be greater than 0
        if (k <= 0)
            return n;

        // Do & of n with a number with all set bits except
        // the k'th bit
        return (n & ~(1 << (k - 1)));
    }

    // Driver program
    public static void main (String[] args)
    {
        int n = 15;
        int k = 4;
        System.out.println(turnOffK(n, k));
    }
}
// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Returns a number that
# has all bits same as n
# except the k'th bit
# which is made 0

def turnOffK(n,k):

    # k must be greater than 0
    if (k <= 0):
        return n

    # Do & of n with a number
    # with all set bits except
    # the k'th bit
    return (n & ~(1 << (k - 1)))

# Driver code
n = 15
k = 4
print(turnOffK(n, k))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to turn off a
// particular bit in a number
using System;

class GFG
{

    // Function to returns a number
    // that has all bits same as n
    // except the k'th bit which is
    // made 0
    static int turnOffK(int n, int k)
    {
        // k must be greater than 0
        if (k <= 0)
            return n;

        // Do & of n with a number
        // with all set bits except
        // the k'th bit
        return (n & ~ (1 << (k - 1)));
    }

    // Driver Code
    public static void Main ()
    {
        int n = 15;
        int k = 4;
        Console.Write(turnOffK(n, k));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to turn off a
// particular bit in a number

// Returns a number that has
// all bits same as n except
// the k'th bit which is made 0
function turnOffK($n, $k)
{

    // k must be greater than 0
    if ($k <= 0)
        return $n;

    // Do & of n with a number
    // with all set bits except
    // the k'th bit
    return ($n & ~(1 << ($k - 1)));
}

// Driver Code
$n = 15;
$k = 4;
echo turnOffK($n, $k);

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>
// Returns a number that has all bits same as n
// except the k'th bit which is made 0
function turnOffK( n, k){
    // k must be greater than 0
    if (k <= 0) return n;

    // Do & of n with a number with all set bits except
    // the k'th bit
    return (n & ~(1 << (k - 1)));
}

// Driver program to test above function
let n = 15;
let k = 4;
document.write(turnOffK(n, k));

// This code is contributed by rohitsingh07052.
</script>
```

输出:

```
7
```

**练习:**编写一个函数 turnOnK()，打开第 k 位。
本文由**拉胡尔·贾恩**供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息