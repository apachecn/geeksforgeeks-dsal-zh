# 除范围[L，R]

内所有自然数的最大除数

> 原文:[https://www . geeksforgeeks . org/最大除数除以范围内所有自然数-l-r/](https://www.geeksforgeeks.org/greatest-divisor-which-divides-all-natural-number-in-range-l-r/)

给定两个整数 **L** 和 **R** ，任务是找到在**【L，R】**范围内除所有自然数的最大除数。
**举例:**

> **输入:** L = 3，R = 12
> **输出:** 1
> **输入:** L = 24，R = 24
> **输出:** 24

**方法:**对于一系列连续的整数元素，有两种情况:

*   如果 **L = R** 那么答案将是 **L** 。
*   如果 **L < R** 那么这个范围内所有连续的自然数都是同素的。因此， **1** 是唯一能够划分范围内所有元素的数字。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the greatest divisor that
// divides all the natural numbers in the range [l, r]
int find_greatest_divisor(int l, int r)
{
    if (l == r)
        return l;

    return 1;
}

// Driver Code
int main()
{
    int l = 2, r = 12;

    cout << find_greatest_divisor(l, r);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG {

// Function to return the greatest divisor that
// divides all the natural numbers in the range [l, r]
    static int find_greatest_divisor(int l, int r) {
        if (l == r) {
            return l;
        }

        return 1;
    }

// Driver Code
    public static void main(String[] args) {
        int l = 2, r = 12;

        System.out.println(find_greatest_divisor(l, r));
    }
}
// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the greatest divisor that
# divides all the natural numbers in the range [l, r]
def find_greatest_divisor(l, r):

    if (l == r):
        return l;

    return 1;

# Driver Code

l = 2;
r = 12;

print(find_greatest_divisor(l, r));

#This code is contributed by Shivi_Aggarwal
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to return the greatest divisor that
    // divides all the natural numbers in the range [l, r]
    static int find_greatest_divisor(int l, int r) {
        if (l == r) {
            return l;
        }

        return 1;
    }

    // Driver Code
    public static void Main() {
        int l = 2,  r = 12 ;

        Console.WriteLine(find_greatest_divisor(l, r));
    }
    // This code is contributed by Ryuga

}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the greatest
// divisor that divides all the natural
// numbers in the range [l, r]
function find_greatest_divisor($l, $r)
{
    if ($l == $r)
        return $l;

    return 1;
}

// Driver Code
$l = 2;
$r = 12;

echo find_greatest_divisor($l, $r);

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the greatest
// divisor that divides all the natural
// numbers in the range [l, r]
function find_greatest_divisor(l, r)
{
    if (l == r)
        return l;

    return 1;
}

// Driver Code
let l = 2;
let r = 12;

document.write( find_greatest_divisor(l, r));

// This code is contributed
// by bobby

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(1)