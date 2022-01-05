# 检查是否可以从给定坐标移动到所需坐标

> 原文:[https://www . geesforgeks . org/check-可能-移动-给定-坐标-所需-坐标/](https://www.geeksforgeeks.org/check-possible-move-given-coordinate-desired-coordinate/)

给定两个坐标(x，y)和(a，b)。找出是否有可能从(a，b)到达(x，y)。
从任何坐标(I，j)唯一可能的移动是

*   (i-j，j)
*   (I，i-j)
*   (i+j，j)
*   (I，i+j)

给定 x，y，a，b 可以是负的。
示例:

```
Input : (x, y) = (1, 1) and  (a, b) = (2, 3).
Output : Yes.
(1, 1) -> (2, 1) -> (2, 3).

Input : (x, y) = (2, 1) and  (a, b) = (2, 3).
Output : Yes.

Input : (x, y) = (35, 15) and  (a, b) = (20, 25).
Output : Yes.
(35, 15) -> (20, 15) -> (5, 15) -> (5, 10) -> (5, 5) ->
(10, 5) -> (15, 5) -> (20, 5) -> (20, 25)
```

如果我们仔细看一下这个问题，我们可以注意到这些动作是类似于[欧几里德算法寻找 GCD](https://en.wikipedia.org/wiki/Euclidean_algorithm) 的步骤。所以，只有当 x，y 的 GCD 等于 a，b 的 GCD 时，才有可能从(x，y)到达坐标(a，b)，否则是不可能的。
设(x，y)的 gcd 为 GCD。从(x，y)，我们可以达到(gcd，gcd)，从这一点，我们可以达到(a，b)当且仅当‘a’和‘b’的 gcd 也是 GCD。
以下是本办法的实施:

C/C++

## C++

```
// C++ program to check if it is possible to reach
// (a, b) from (x, y).
#include <bits/stdc++.h>
using namespace std;

// Returns GCD of i and j
int gcd(int i, int j)
{
    if (i == j)
        return i;

    if (i > j)
        return gcd(i - j, j);
    return gcd(i, j - i);
}

// Returns true if it is possible to go to (a, b)
// from (x, y)
bool ispossible(int x, int y, int a, int b)
{
    // Find absolute values of all as sign doesn't
    // matter.
    x = abs(x), y = abs(y), a = abs(a), b = abs(b);

    // If gcd is equal then it is possible to reach.
    // Else not possible.
    return (gcd(x, y) == gcd(a, b));
}

// Driven Program
int main()
{
    // Converting coordinate into positive integer
    int x = 35, y = 15;
    int a = 20, b = 25;
    (ispossible(x, y, a, b)) ? (cout << "Yes") : (cout << "No");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if it is possible
// to reach (a, b) from (x, y).
class GFG {

    // Returns GCD of i and j
    static int gcd(int i, int j)
    {
        if (i == j)
            return i;

        if (i > j)
            return gcd(i - j, j);
        return gcd(i, j - i);
    }

    // Returns true if it is possible to go to (a, b)
    // from (x, y)
    static boolean ispossible(int x, int y, int a, int b)
    {

        // Find absolute values of all as
        // sign doesn't matter.
        x = Math.abs(x);
        y = Math.abs(y);
        a = Math.abs(a);
        b = Math.abs(b);

        // If gcd is equal then it is possible to reach.
        // Else not possible.
        return (gcd(x, y) == gcd(a, b));
    }

    // Driver code
    public static void main(String[] args)
    {

        // Converting coordinate into positive integer
        int x = 35, y = 15;
        int a = 20, b = 25;
        if (ispossible(x, y, a, b))
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}
// This code is contributed by Anant Agarwal.
```

## 计算机编程语言

```
# Python program to check if it is possible to reach
# (a, b) from (x, y).
# Returns GCD of i and j
def gcd(i, j):
    if (i == j):
        return i

    if (i > j):
        return gcd(i - j, j)
    return gcd(i, j - i)

# Returns true if it is possible to go to (a, b)
# from (x, y)
def ispossible(x, y, a, b):
    # Find absolute values of all as sign doesn't
    # matter.
    x, y, a, b = abs(x), abs(y), abs(a), abs(b)

    # If gcd is equal then it is possible to reach.
    # Else not possible.
    return (gcd(x, y) == gcd(a, b))

# Driven Program
    # Converting coordinate into positive integer
x, y = 35, 15
a, b = 20, 25
if(ispossible(x, y, a, b)):
    print "Yes"
else:
    print "No"
# Contributed by Afzal Ansari
```

## C#

```
// C# program to check if it is possible
// to reach (a, b) from (x, y).
using System;

class GFG {

    // Returns GCD of i and j
    static int gcd(int i, int j)
    {
        if (i == j)
            return i;

        if (i > j)
            return gcd(i - j, j);
        return gcd(i, j - i);
    }

    // Returns true if it is possible
    // to go to (a, b) from (x, y)
    static bool ispossible(int x, int y,
                           int a, int b)
    {

        // Find absolute values of all as
        // sign doesn't matter.
        x = Math.Abs(x);
        y = Math.Abs(y);
        a = Math.Abs(a);
        b = Math.Abs(b);

        // If gcd is equal then it is possible
        // to reach. Else not possible.
        return (gcd(x, y) == gcd(a, b));
    }

    // Driver code
    public static void Main()
    {

        // Converting coordinate
        // into positive integer
        int x = 35, y = 15;
        int a = 20, b = 25;

        if (ispossible(x, y, a, b))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if it
// is possible to reach
// (a, b) from (x, y).

// Returns GCD of i and j
function gcd($i, $j)
{
    if ($i == $j)
        return $i;

    if ($i > $j)
        return gcd($i - $j, $j);
    return gcd($i, $j - $i);
}

// Returns true if it is
// possible to go to (a, b)
// from (x, y)
function ispossible($x, $y, $a, $b)
{

    // Find absolute values
    // of all as sign doesn't
    // matter.
    $x = abs($x);
    $y = abs($y);
    $a = abs($a);
    $b = abs($b);

    // If gcd is equal then
    // it is possible to reach.
    // Else not possible.
    return (gcd($x, $y) == gcd($a, $b));
}

// Driver Code
{

    // Converting coordinate
    // into positive integer
    $x = 35; $y = 15;
    $a = 20; $b = 25;
    if (ispossible($x, $y, $a, $b))
        echo( "Yes");
    else
        echo( "No");
    return 0;
}

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
// javascript program to check if it is possible
// to reach (a, b) from (x, y).   
// Returns GCD of i and j
    function gcd(i , j) {
        if (i == j)
            return i;

        if (i > j)
            return gcd(i - j, j);
        return gcd(i, j - i);
    }

    // Returns true if it is possible to go to (a, b)
    // from (x, y)
    function ispossible(x , y , a , b)
    {

        // Find absolute values of all as
        // sign doesn't matter.
        x = Math.abs(x);
        y = Math.abs(y);
        a = Math.abs(a);
        b = Math.abs(b);

        // If gcd is equal then it is possible to reach.
        // Else not possible.
        return (gcd(x, y) == gcd(a, b));
    }

    // Driver code

        // Converting coordinate into positive integer
        var x = 35, y = 15;
        var a = 20, b = 25;
        if (ispossible(x, y, a, b))
            document.write("Yes");
        else
            document.write("No");

// This code is contributed by todaysgaurav
</script>
```

输出:

```
Yes
```

本文由[**Anuj Chauhan(Anuj 0503)**](https://web.facebook.com/anuj0503)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。