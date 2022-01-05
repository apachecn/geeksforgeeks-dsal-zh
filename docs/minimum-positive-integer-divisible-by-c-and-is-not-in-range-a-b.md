# 可被 C 整除且不在[A，B]

范围内的最小正整数

> 原文:[https://www . geesforgeks . org/最小正整数可被 c 整除且不在范围内-a-b/](https://www.geeksforgeeks.org/minimum-positive-integer-divisible-by-c-and-is-not-in-range-a-b/)

给定三个正整数 **A** 、 **B** 和 **C** 。任务是找到最小整数 **X > 0** ，这样:

1.  **X % C = 0** 和
2.  **X** 一定不属于**【A，B】**范围

**例:**

> **输入:** A = 2，B = 4，C = 2
> **输出:** 6
> **输入:** A = 5，B = 10，C = 4
> **输出:** 4

**进场:**

*   如果 **C** 不属于**【A，B】**即 **C < A** 或 **C > B** ，那么 **C** 就是需要的数字。
*   否则取 **C** 大于 **B** 的第一倍数，这是必选项。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the required number
int getMinNum(int a, int b, int c)
{

    // If doesn't belong to the range
    // then c is the required number
    if (c < a || c > b)
        return c;

    // Else get the next multiple of c
    // starting from b + 1
    int x = ((b / c) * c) + c;

    return x;
}

// Driver code
int main()
{
    int a = 2, b = 4, c = 4;
    cout << getMinNum(a, b, c);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
import java.math.*;
public class GFG
{
    // Function to return the required number
    int getMinNum(int a, int b, int c)
    {

        // If doesn't belong to the range
        // then c is the required number
        if (c < a || c > b)
        {
            return c;
        }

        // Else get the next multiple of c
        // starting from b + 1
        int x = ((b / c) * c) + c;

        return x;
    }

// Driver code
public static void main(String args[])
{
    int a = 2;
    int b = 4;
    int c = 4;
    GFG g = new GFG();
    System.out.println(g.getMinNum(a, b, c));
}
}

// This code is contributed by Shivi_Aggarwal
```

## 蟒蛇 3

```
# Python3 implementation of the approach
# Function to return the required number
def getMinNum(a, b, c):

    # If doesn't belong to the range
    # then c is the required number
    if (c < a or c > b):
        return c

    # Else get the next multiple of c
    # starting from b + 1
    x = ((b // c) * c) + c

    return x

# Driver code
a, b, c = 2, 4, 4
print(getMinNum(a, b, c))

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to return the required number
    static int getMinNum(int a, int b, int c)
    {

        // If doesn't belong to the range
        // then c is the required number
        if (c < a || c > b)
        {
            return c;
        }

        // Else get the next multiple of c
        // starting from b + 1
        int x = ((b / c) * c) + c;

        return x;
    }

    // Driver code
    static public void Main ()
    {
        int a = 2, b = 4, c = 4;
        Console.WriteLine( getMinNum(a, b, c));
    }
}

// This Code is contributed by ajit..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to return the required number
function getMinNum($a, $b, $c)
{

    // If doesn't belong to the range
    // then c is the required number
    if ($c < $a || $c > $b)
        return $c;

    // Else get the next multiple of c
    // starting from b + 1
    $x = (floor(($b / $c)) * $c) + $c;

    return $x;
}

// Driver code
$a = 2;
$b = 4;
$c = 4;

echo getMinNum($a, $b, $c);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the required number
function getMinNum(a, b, c)
{

    // If doesn't belong to the range
    // then c is the required number
    if (c < a || c > b)
        return c;

    // Else get the next multiple of c
    // starting from b + 1
    let x = (parseInt(b / c) * c) + c;

    return x;
}

// Driver code
    let a = 2, b = 4, c = 4;
    document.write(getMinNum(a, b, c));

// This code is contributed by souravmahato348
</script>
```

**Output:** 

```
8
```