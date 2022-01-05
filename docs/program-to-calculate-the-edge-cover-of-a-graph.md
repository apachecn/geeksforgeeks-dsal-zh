# 计算图形边缘覆盖的程序

> 原文:[https://www . geeksforgeeks . org/计算图形边缘覆盖的程序/](https://www.geeksforgeeks.org/program-to-calculate-the-edge-cover-of-a-graph/)

给定图的顶点数 N。任务是确定边缘覆盖。
**边覆盖:**覆盖所有顶点所需的最小边数称为边覆盖。
**示例:**

```
Input : N = 5
Output : 3

Input : N = 4
Output : 2
```

**示例 1:** 对于 N = 5 个顶点，

![](img/41fcfa7d1b208d11a0deb6a893ad0599.png)

边缘覆盖为:3(选择红色标记的边缘，所有顶点将被覆盖)

![](img/c0aa0a293716b998a60b5adddc1f14c3.png)

**示例 2:** 对于 N = 8 个顶点，

![](img/8a1f62204fc8eb5cbddfe454b3330719.png)

边缘覆盖为:4(选择红色标记的边缘，所有顶点将被覆盖)

![](img/7b76e855860e79d7073da80d196b3b3b.png)

**公式:**

```
Edge Cover = ceil (no. of vertices / 2)
```

以下是上述方法的实现:

## C++

```
// C++ program to find Edge Cover
#include <bits/stdc++.h>
using namespace std;

// Function that calculates Edge Cover
int edgeCover(int n)
{
    float result = 0;

    result = ceil(n / 2.0);

    return result;
}

// Driver Code
int main()
{
    int n = 5;

    cout << edgeCover(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Edge Cover
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{
// Function that calculates Edge Cover
static int edgeCover(int n)
{
    int result = 0;

    result = (int)Math.ceil((double)n / 2.0);

    return result;
}

// Driver Code
public static void main(String args[])
{
    int n = 5;

    System.out.print(edgeCover(n));
}

}
```

## 蟒蛇 3

```
# Python 3 implementation of the above approach.

import math

# Function that calculates Edge Cover
def edgeCover(n):

    result = 0

    result = math.ceil(n / 2.0)

    return result

# Driver code     
if __name__ == "__main__" :

    n =  5

    print(int(edgeCover(n)))

# this code is contributed by Naman_Garg
```

## C#

```
// C# program to find Edge Cover
using System;

class GFG
{
// Function that calculates Edge Cover
static int edgeCover(int n)
{
    int result = 0;

    result = (int)Math.Ceiling((double)n / 2.0);

    return result;
}

// Driver Code
static public void Main ()
{
    int n = 5;

    Console.Write(edgeCover(n));
}
}

// This code is contributed by Raj
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find Edge Cover

// Function that calculates
// Edge Cover
function edgeCover($n)
{
    $result = 0;

    $result = ceil($n / 2.0);

    return $result;
}

// Driver Code
$n = 5;

echo edgeCover($n);

// This code is contributed by Raj
?>
```

## java 描述语言

```
<script>

// javascript program to find Edge Cover

// Function that calculates Edge Cover
    function edgeCover(n) {
        var result = 0;

        result = parseInt( Math.ceil(n / 2.0));

        return result;
    }

    // Driver Code

        var n = 5;

        document.write(edgeCover(n));

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
3
```