# 伍达尔号

> 原文:[https://www.geeksforgeeks.org/woodall-number/](https://www.geeksforgeeks.org/woodall-number/)

伍德豪尔号的形式为:

> w<sub>n</sub>= n . 2<sup>n</sup>–1

前几个伍达尔数字是:1，7，23，63，159，383，895……
给定一个数字 **X** 。任务是检查 X 是否是伍德尔数。
示例:

```
Input : X = 383
Output : Yes
For n = 6, Wn = n.2n - 1 = 383.

Input : X = 200
Output : No
```

1.  我们可以观察到所有的伍达尔数都是奇数。所以，首先我们检查给定的数字是不是奇数。
2.  现在检查一个数是否是伍德尔数，给定数加 1，然后除以 2，直到它是偶数，并计算它可被整除的次数。并且在每个点检查计数是否等于数字。

以下是该方法的实现:

## C++

```
// CPP program to check if a number is
// Woodball or not.
#include <bits/stdc++.h>
using namespace std;

bool isWoodall(int x)
{
    // If number is even, return false.
    if (x % 2  == 0)
        return false;

    // If x is 1, return true.
    if (x == 1)
        return true;

    x++;  // Add 1 to make x even

    // While x is divisible by 2
    int p = 0;
    while (x % 2 == 0) {

        // Divide x by 2
        x = x/2;

        // Count the power
        p++;

        // If at any point power and
        // x became equal, return true.
        if (p == x)
            return true;
    }

    return false;
}

// Driven Program
int main()
{
    int x = 383;

    (isWoodall(x)) ? (cout << "Yes" << endl) :
                     (cout << "No" << endl);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to check if a number
// is Woodall or not.
class GFG {

    static boolean isWoodall(int x)
    {
        // If number is even, return false.
        if (x % 2  == 0)
            return false;

        // If x is 1, return true.
        if (x == 1)
            return true;

        x++;  // Add 1 to make x even

        // While x is divisible by 2
        int p = 0;
        while (x % 2 == 0) {

            // Divide x by 2
            x = x / 2;

            // Count the power
            p++;

            // If at any point power and
            // x became equal, return true.
            if (p == x)
                return true;
        }

        return false;
    }

    // Driven Program
    public static void main(String args[])
    {
        int x = 383;

        if(isWoodall(x))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 计算机编程语言

```
# Python program to check if a number
# is Woodball or not.

def isWoodall(x) :

    # If number is even, return false.
    if (x % 2  == 0) :
        return False

    # If x is 1, return true.
    if (x == 1) :
        return True

    x = x + 1  # Add 1 to make x even

    # While x is divisible by 2
    p = 0
    while (x % 2 == 0) :

        # Divide x by 2
        x = x/2

        # Count the power
        p = p + 1

        # If at any point power and
        # x became equal, return true.
        if (p == x) :
            return True

    return False

# Driven Program
x = 383
if(isWoodall(x)) :
    print "Yes"
else  :
    print "No"

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to check if a number
// is Woodall or not.
using System;

class GFG {

    static bool isWoodall(int x)
    {
        // If number is even, return false.
        if (x % 2 == 0)
            return false;

        // If x is 1, return true.
        if (x == 1)
            return true;

        x++; // Add 1 to make x even

        // While x is divisible by 2
        int p = 0;
        while (x % 2 == 0) {

            // Divide x by 2
            x = x / 2;

            // Count the power
            p++;

            // If at any point power and
            // x became equal, return true.
            if (p == x)
                return true;
        }

        return false;
    }

    // Driver Code
    public static void Main()
    {
        int x = 383;

        if(isWoodall(x))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Nikita Tiwari.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check
// if a number is
// Woodball or not.

function isWoodall($x)
{

    // If number is even,
    // return false.
    if ($x % 2 == 0)
        return false;

    // If x is 1,
    // return true.
    if ($x == 1)
        return true;

    // Add 1 to
    // make x even
    $x++;

    // While x is
    // divisible by 2
    $p = 0;
    while ($x % 2 == 0)
    {

        // Divide x by 2
        $x = $x/2;

        // Count the power
        $p++;

        // If at any point power and
        // x became equal, return true.
        if ($p == $x)
            return true;
    }

    return false;
}

    // Driver Code
    $x = 383;

    if(isWoodall($x))
    echo "Yes" ;
    else
    echo "No" ;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Javascript program to check
// if a number is
// Woodball or not.

function isWoodall(x)
{

    // If number is even,
    // return false.
    if (x % 2 == 0)
        return false;

    // If x is 1,
    // return true.
    if (x == 1)
        return true;

    // Add 1 to
    // make x even
    x++;

    // While x is
    // divisible by 2
    let p = 0;
    while (x % 2 == 0)
    {

        // Divide x by 2
        x = x/2;

        // Count the power
        p++;

        // If at any point power and
        // x became equal, return true.
        if (p == x)
            return true;
    }

    return false;
}

    // Driver Code
    let x = 383;

    if(isWoodall(x))
    document.write("Yes") ;
    else
    document.write("No") ;

// This code is contributed by _saurabh_jaiswal
</script>
```

输出:

```
Yes
```

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。