# 两个整数的逐位递归加法

> 原文:[https://www . geesforgeks . org/bitwise-recursive-add-two-integer/](https://www.geeksforgeeks.org/bitwise-recursive-addition-two-integers/)

当手工添加两个二进制数时，我们会记住进位位，并同时添加它。但是要在程序中做同样的事情，我们需要很多检查。递归解可以想象为将*进位*和 *a^b* (两个输入)相加，直到*进位*变为 0。

**示例:**

```
Input : int x = 45, y = 45
Output : 90

Input : int x = 4, y = 78
Output : 82
```

两个比特的和可以通过对两个比特执行 XOR (^)来获得。进位位可以通过对两位执行 AND (&)来获得。

上面是简单的[半加法器](http://en.wikipedia.org/wiki/Adder_%28electronics%29#Half_adder)逻辑，可以用来加 2 个单比特。我们可以把这个逻辑推广到整数。如果 x 和 y 在相同位置没有设置位，则 x 和 y 的按位异或(^)得到 x 和 y 的和。为了合并公共设置位，使用按位与(&)。x 和 y 的按位“与”给出所有进位。我们计算(x & y) < < 1，并将其与 x ^ y 相加，得到所需的结果。

一个重要的观察是，如果(x & y)变成 0，那么结果就是 x ^ y。

## C

```
// C program to do recursive addition
// of two integers
#include <stdio.h>

int add(int x, int y) {
    int keep = (x & y) << 1;
    int res = x^y;

    // If bitwise & is 0, then there
    // is not going to be any carry.
    // Hence result of XOR is addition.
    if (keep == 0)
        return res;

    add(keep, res);
}

// Driver code
int main(){
    printf("%d", add(15, 38));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to do recursive addition
// of two integers
import java.io.*;

class GFG {

    static int add(int x, int y)
    {
        int keep = (x & y) << 1;
        int res = x^y;

        // If bitwise & is 0, then there
        // is not going to be any carry.
        // Hence result of XOR is addition.
        if (keep == 0)
            return res;

        return add(keep, res);
    }

    // Driver code
    public static void main (String[] args)
    {
        System.out.println(add(15, 38));
    }
}

// This code is contributed by Ajit.
```

## 蟒蛇 3

```

# Python program to do recursive addition
# of two integers

def add(x, y):
    keep = (x & y) << 1;
    res = x^y;

    # If bitwise & is 0, then there
    # is not going to be any carry.
    # Hence result of XOR is addition.
    if (keep == 0):
        return res;

    return add(keep, res);

# Driver code

print(add(15, 38));

#  This code is contributed by Princi Singh
```

## C#

```
// C# program to do recursive
// addition of two integers
using System;

class GFG {

    static int add(int x, int y)
    {
        int keep = (x & y) << 1;
        int res = x^y;

        // If bitwise & is 0, then there
        // is not going to be any carry.
        // Hence result of XOR is addition.
        if (keep == 0)
            return res;

        return add(keep, res);
    }

    // Driver code
    public static void Main ()
    {
        Console.Write(add(15, 38));
    }
}

// This code is contributed by Smitha.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php program to do recursive addition
// of two integers

function add($x, $y) {
    $keep = ($x & $y) << 1;
    $res = $x^$y;

    // If bitwise & is 0, then there
    // is not going to be any carry.
    // Hence result of XOR is addition.
    if ($keep == 0)
    {
        echo $res;
        exit(0);
    }

    add($keep, $res);
}

// Driver code
$k= add(15, 38);

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>

// Javascript program to do recursive
// addition of two integers
function add(x, y)
{
    let keep = (x & y) << 1;
    let res = x ^ y;

    // If bitwise & is 0, then there
    // is not going to be any carry.
    // Hence result of XOR is addition.
    if (keep == 0)
        return res;

    return add(keep, res);
}

// Driver code
document.write(add(15, 38));

// This code is contributed by decode2207

</script>
```

**Output:** 

```
53
```