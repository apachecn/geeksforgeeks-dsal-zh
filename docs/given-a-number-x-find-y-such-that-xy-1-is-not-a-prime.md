# 给定一个数 x，求 y 使得 x*y + 1 不是素数

> 原文:[https://www . geesforgeks . org/给定一个数字-x-find-y-so-xy-1-不是素数/](https://www.geeksforgeeks.org/given-a-number-x-find-y-such-that-xy-1-is-not-a-prime/)

给定一个数 x，求 y (y > 0)，使得 x*y + 1 不是素数。
**例:**

```
Input : 2
Output : 4

Input : 5
Output : 3
```

观察:

> x*(x-2) + 1 = (x-1)^2 不是素数。

方法:

```
For x > 2, y will be x-2 otherwise y will be x+2
```

## C++

```
#include <bits/stdc++.h>
using namespace std;

int findY(int x)
{
    if (x > 2)
        return x - 2;

    return x + 2;
}

// Driver code
int main()
{
    int x = 5;
    cout << findY(x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA implementation of above approach

import java.util.*;

class GFG
{
    public static int findY(int x)
    {
        if (x > 2)
            return x - 2;

        return x + 2;
    }

    // Driver code
    public static void  main(String [] args)
    {
        int x = 5;
        System.out.println(findY(x));

    }

}

// This code is contributed
// by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of above
# approach

def findY(x):

    if (x > 2):
        return x - 2

    return x + 2

# Driver code
if __name__=='__main__':
    x = 5
    print(findY(x))

# This code is contributed
# by ihritik
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{
public static int findY(int x)
{
    if (x > 2)
        return x - 2;

    return x + 2;
}

// Driver code
public static void Main()
{
    int x = 5;
    Console.WriteLine(findY(x));
}
}

// This code is contributed
// by Subhadeep
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach
function findY($x)
{
    if ($x > 2)
        return $x - 2;

    return $x + 2;
}

// Driver code
$x = 5;
echo (findY($x));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of above approach

// Function to check whether it is possible
// or not to move from (0, 0) to (x, y)
// in exactly n steps
function findY(x)
{
    if (x > 2)
        return x - 2;

    return x + 2;
}

// Driver code

var x = 5;
document.write(findY(x));

// This code is contributed by Ankita saini

</script>
```

**输出:**

```
3
```