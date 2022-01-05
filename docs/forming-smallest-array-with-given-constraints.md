# 在给定约束条件下形成最小阵列

> 原文:[https://www . geeksforgeeks . org/forming-最小数组-带给定约束/](https://www.geeksforgeeks.org/forming-smallest-array-with-given-constraints/)

给定三个整数 **x，y** 和 **z** (可以是负数)。任务是找到最小数组的长度，使得相邻元素之间的绝对差小于或等于 1，数组的第一个元素是 x，有一个整数 y，最后一个元素是 z。
示例:

> 输入:x = 5，y = 7，z = 11
> 输出:7
> 最小的以 5 开始，有 7，以 11 结束
> ，绝对差 1
> 为{ 5，6，7，8，9，10，11 }。
> 输入:x = 3，y = 1，z = 2
> 输出:4
> 数组将变成{ 3，2，1，2 }

想法是考虑数字线，因为相邻元素之间的差是 1，所以要从 X 移动到 Y，X 和 Y 之间的所有数字都必须被覆盖，并且以整数 z 结束数组，所以从元素 Y 移动到元素 z。
因此，可以形成的最小数组的长度将是从 X 到 z 覆盖的点数，即

```
1 + abs(x - y) + abs(y - z) (1 is added to count point x).
```

## C++

```
// C++ program to find the length of
// smallest array begin with x, having y,
// ends with z and having absolute difference
// between adjacent elements <= 1.
#include <bits/stdc++.h>
using namespace std;

// Return the size of smallest
// array with given constraint.
int minimumLength(int x, int y, int z)
{
    return 1 + abs(x - y) + abs(y - z);
}

// Drivers code
int main()
{
    int x = 3, y = 1, z = 2;
    cout << minimumLength(x, y, z);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the length
// of smallest array begin with x,
// having y, ends with z and having
// absolute difference between
// adjacent elements <= 1.
import java.io.*;

class GFG {

    // Return the size of smallest
    // array with given constraint.
    static int minimumLength(int x,
                      int y, int z)
    {
        return 1 + Math.abs(x - y)
                 + Math.abs(y - z);
    }

    // Drivers code

    public static void main(String[] args)
    {
        int x = 3, y = 1, z = 2;
        System.out.println(
              minimumLength(x, y, z));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python 3 program to find
# the length of smallest
# array begin with x, having
# y, ends with z and having
# absolute difference between
# adjacent elements <= 1.

# Return the size of smallest
# array with given constraint.
def minimumLength(x, y, z):

    return (1 + abs(x - y)
              + abs(y - z))

# Drivers code
x = 3
y = 1
z = 2
print(minimumLength(x, y, z))

# This code is contributed
# by Smitha
```

## C#

```
// C# program to find the length
// of smallest array begin with x,
// having y, ends with z and having
// absolute difference between
// adjacent elements <= 1.
using System;
class GFG {

    // Return the size of smallest
    // array with given constraint.
    static int minimumLength(int x,
                             int y,
                             int z)
    {
        return 1 + Math.Abs(x - y)
                 + Math.Abs(y - z);
    }

    // Driver Code
    public static void Main()
    {
        int x = 3, y = 1, z = 2;
        Console.WriteLine(minimumLength(x, y, z));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the length of
// smallest array begin with x, having y,
// ends with z and having absolute difference
// between adjacent elements <= 1.

// Return the size of smallest
// array with given constraint.
function minimumLength($x, $y,$z)
{
    return 1 + abs($x - $y) +
               abs($y - $z);
}

    // Driver Code
    $x = 3;
    $y = 1;
    $z = 2;
    echo minimumLength($x, $y, $z);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find the length of
// smallest array begin with x, having y,
// ends with z and having absolute difference
// between adjacent elements <= 1.

// Return the size of smallest
// array with given constraint.
function minimumLength(x, y, z)
{
    return 1 + Math.abs(x - y) + Math.abs(y - z);
}

// Drivers code
var x = 3, y = 1, z = 2;
document.write( minimumLength(x, y, z));

// This code is contributed by noob2000.
</script>
```

**输出**T2】

```
4
```