# 四舍五入到下一个 8 的较小倍数

> 原文:[https://www . geesforgeks . org/round-to-next-small-倍数 8/](https://www.geeksforgeeks.org/round-to-next-smaller-multiple-of-8/)

给定一个无符号整数 x。仅使用按位运算将其向下舍入到 8 的下一个较小倍数。
**例:**

```
Input : 35
Output : 32

Input : 40
Output : 40 
As 40 is already a multiple of 8\. So, no 
modification is done.
```

**解 1:** 用算术运算符解决这个问题的一个简单方法是:
让 x 是数字，然后，
x = x –( x % 8)
这将把 x 向下舍入到下一个更小的 8 的倍数。但是我们不允许使用算术运算符。
**解决方案 2:** 使用按位“与”运算解决此问题的有效方法是:x = x & (-8)
这将把 x 向下舍入到下一个更小的倍数 8。这个想法是基于 8 的倍数中的最后三位必须是 0 的事实，
下面是上面想法的实现:

## C++

```
// CPP program to find next smaller
// multiple of 8.
#include <bits/stdc++.h>
using namespace std;

int RoundDown(int& a)
{
    return a & (-8);
}

int main()
{
    int x = 39;
    cout << RoundDown(x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to find next smaller
// multiple of 8.

import java.io.*;

class GFG {
static int RoundDown(int a)
{
    return a & (-8);
}

    public static void main (String[] args) {

    int x = 39;
    System.out.println (RoundDown(x));
    }
}
//This Code is Contributed by ajit
```

## 蟒蛇 3

```
# Python 3 program to find next
# smaller multiple of 8.

def RoundDown(a):
    return a & (-8)

# Driver Code
if __name__ == '__main__':
    x = 39
    print(RoundDown(x))

# This code is contributed
# by Surendra_Gangwar
```

## C#

```
// C# program to find next smaller
// multiple of 8.
using System;

class GFG
{
static int RoundDown(int a)
{
    return a & (-8);
}

public static void Main()
{
    int x = 39;
    Console.Write(RoundDown(x));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find next smaller
// multiple of 8.

function RoundDown($a)
{
    return ($a & (-8));
}

// Driver Code
$x = 39;
echo RoundDown($x);

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>
    // Javascript program to find next smaller multiple of 8.

    function RoundDown(a)
    {
        return a & (-8);
    }

    let x = 39;
    document.write(RoundDown(x));

</script>
```

**Output:** 

```
32
```

**时间复杂度:**该方法的时间复杂度为 O(1)
T3】空间复杂度:该方法的空间复杂度为 O(1)