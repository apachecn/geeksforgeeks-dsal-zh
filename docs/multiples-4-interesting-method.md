# 4 的倍数(有趣的方法)

> 原文:[https://www . geesforgeks . org/multiples-4-interest-method/](https://www.geeksforgeeks.org/multiples-4-interesting-method/)

给定一个数字 n，任务是在不使用+、-、*、/和%运算符的情况下检查这个数字是否是 4 的倍数。
**例:**

```
Input: n = 4  Output - Yes
       n = 20 Output - Yes
       n = 19 Output - No
```

**方法 1(使用异或)**
n>1 的一个有趣的事实是，我们对从 1 到 n 的所有数字进行异或运算，如果结果等于 n，那么 n 是 4 的倍数，否则不是。

## C++

```
// An interesting XOR based method to check if
// a number is multiple of 4.
#include<bits/stdc++.h>
using namespace std;

// Returns true if n is a multiple of 4.
bool isMultipleOf4(int n)
{
    if (n == 1)
       return false;

    // Find XOR of all numbers from 1 to n
    int XOR = 0;
    for (int i = 1; i <= n; i++)
        XOR = XOR ^ i;

    // If XOR is equal n, then return true
    return (XOR == n);
}

// Driver code to print multiples of 4
int main()
{
    // Printing multiples of 4 using above method
    for (int n=0; n<=42; n++)
       if (isMultipleOf4(n))
         cout << n << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An interesting XOR based method to check if
// a number is multiple of 4.

class Test
{
    // Returns true if n is a multiple of 4.
    static boolean isMultipleOf4(int n)
    {
        if (n == 1)
           return false;

        // Find XOR of all numbers from 1 to n
        int XOR = 0;
        for (int i = 1; i <= n; i++)
            XOR = XOR ^ i;

        // If XOR is equal n, then return true
        return (XOR == n);
    }

    // Driver method
    public static void main(String[] args)
    {
        // Printing multiples of 4 using above method
        for (int n=0; n<=42; n++)
           System.out.print(isMultipleOf4(n) ? n : " ");
    }
}
```

## 蟒蛇 3

```
# An interesting XOR based
# method to check if a
# number is multiple of 4.

# Returns true if n is a
# multiple of 4.
def isMultipleOf4(n):

    if (n == 1):
        return False

    # Find XOR of all numbers
    # from 1 to n
    XOR = 0
    for i in range(1, n + 1):
        XOR = XOR ^ i

    # If XOR is equal n, then
    # return true
    return (XOR == n)

# Driver code to print
# multiples of 4 Printing
# multiples of 4 using
# above method
for n in range(0, 43):
    if (isMultipleOf4(n)):
        print(n, end = " ")

# This code is contributed
# by Smitha
```

## C#

```
// An interesting XOR based method
// to check if a number is multiple
// of 4.
using System;
class GFG {

    // Returns true if n is a
    // multiple of 4.
    static bool isMultipleOf4(int n)
    {
        if (n == 1)
        return false;

        // Find XOR of all numbers
        // from 1 to n
        int XOR = 0;
        for (int i = 1; i <= n; i++)
            XOR = XOR ^ i;

        // If XOR is equal n, then
        // return true
        return (XOR == n);
    }

    // Driver method
    public static void Main()
    {

        // Printing multiples of 4
        // using above method
        for (int n = 0; n <= 42; n++)
        {
            if (isMultipleOf4(n))
                Console.Write(n+" ");
        }
    }
}

// This code is contributed by Smitha.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if
// a number is multiple of 4.

// Returns true if n is
// a multiple of 4.
function isMultipleOf4($n)
{
    if ($n == 1)
    return false;

    // Find XOR of all
    // numbers from 1 to n
    $XOR = 0;
    for ($i = 1; $i <= $n; $i++)
        $XOR = $XOR ^ $i;

    // If XOR is equal n,
    // then return true
    return ($XOR == $n);
}

// Driver Code

// Printing multiples of 4
// using above method
for ($n = 0; $n <= 42; $n++)
if (isMultipleOf4($n))
    echo $n, " ";

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program of interesting XOR based method to check if
// a number is multiple of 4.

    // Returns true if n is a multiple of 4.
    function isMultipleOf4(n)
    {
        if (n == 1)
           return false;

        // Find XOR of all numbers from 1 to n
        let XOR = 0;
        for (let i = 1; i <= n; i++)
            XOR = XOR ^ i;

        // If XOR is equal n, then return true
        return (XOR == n);
    }

// Driver Code

        // Printing multiples of 4 using above method
        for (let n = 0; n <= 42; n++)
           document.write(isMultipleOf4(n) ? n : " ");

          // This code is contributed by avijitmondal1998.
</script>
```

**输出:**

```
0 4 8 12 16 20 24 28 32 36 40 
```

时间复杂度:0(n)

辅助空间:0(1)

**这是如何工作的？**
当我们对数字进行异或运算时，我们在 4 的倍数之前得到 0 作为异或值。这在每 4 的倍数之前不断重复。

```
Number Binary-Repr  XOR-from-1-to-n
1         1           [0001]
2        10           [0011]
3        11           [0000]
```

**方法 2(使用按位移位运算符)**
思路是使用> >去掉最后两位，然后使用< <乘以 4。如果最终结果与 n 相同，那么最后两位是 0，因此数字是 4 的倍数。

## C++

```
// An interesting XOR based method to check if
// a number is multiple of 4.
#include<bits/stdc++.h>
using namespace std;

// Returns true if n is a multiple of 4.
bool isMultipleOf4(long long n)
{
    if (n==0)
        return true;

    return (((n>>2)<<2) == n);
}

// Driver code to print multiples of 4
int main()
{
    // Printing multiples of 4 using above method
    for (int n=0; n<=42; n++)
        if (isMultipleOf4(n))
            cout << n << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An interesting XOR based method to check if
// a number is multiple of 4.

class Test
{
    // Returns true if n is a multiple of 4.
    static boolean isMultipleOf4(long n)
    {
        if (n==0)
            return true;

        return (((n>>2)<<2) == n);
    }

    // Driver method
    public static void main(String[] args)
    {
        // Printing multiples of 4 using above method
        for (int n=0; n<=42; n++)
           System.out.print(isMultipleOf4(n) ? n : " ");
    }
}
```

## C#

```
// An interesting XOR based method to
// check if a number is multiple of 4.
using System;

class GFG {

    // Returns true if n is a multiple
    // of 4.
    static bool isMultipleOf4(int n)
    {
        if (n == 0)
            return true;

        return (((n >> 2) << 2) == n);
    }

    // Driver code to print multiples
    // of 4
    static void Main()
    {

        // Printing multiples of 4 using
        // above method
        for (int n = 0; n <= 42; n++)
            if (isMultipleOf4(n))
                Console.Write(n + " ");
    }
}

// This code is contributed by Anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if
// a number is multiple of 4.

// Returns true if n is
// a multiple of 4.
function isMultipleOf4($n)
{
    if ($n == 0)
        return true;

    return ((($n >> 2) << 2) == $n);
}

// Driver Code

// Printing multiples of 4
// using above method
for ($n = 0; $n <= 42; $n++)
    if (isMultipleOf4($n))
        echo $n , " ";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

    // An interesting XOR based method to
    // check if a number is multiple of 4.

    // Returns true if n is a multiple
    // of 4.
    function isMultipleOf4(n)
    {
        if (n == 0)
            return true;

        return (((n >> 2) << 2) == n);
    }

    // Printing multiples of 4 using
    // above method
    for (let n = 0; n <= 42; n++)
      if (isMultipleOf4(n))
        document.write(n + " ");

</script>
```

**输出:**

```
0 4 8 12 16 20 24 28 32 36 40 
```

时间复杂度:0(1)

辅助空间:0(1)

如我们所见，求 4 的重数的主要思想是检查给定数的最低有效位。我们知道，对于任何偶数，最低有效位总是零(即 0)。类似地，对于任何 4 的倍数的数，至少有两个有效位是零。在同样的逻辑下，对于任何 8 的倍数，最低三个有效位都是零。这就是为什么我们可以使用 AND 运算符(&)以及其他操作数如 0x3 来求 4 的重数。
本文由 [**萨希尔·查布拉(KILLER)**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。