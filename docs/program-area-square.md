# 正方形面积程序

> 原文:[https://www.geeksforgeeks.org/program-area-square/](https://www.geeksforgeeks.org/program-area-square/)

正方形是一个平面上的平面形状，由四个角上的四个点定义。正方形有四条等长的边和四个直角(90 度角)。正方形是一种长方形。

![](img/6e2b92f44e4493bd7dcc5bcb64ba4341.png)

**例:**

```
Input : 4
Output :16

Input :8
Output :64
```

**公式**
![Area = side*side   ](img/e05fdcfbb2907869a4813220d71298d7.png "Rendered by QuickLaTeX.com")

## C++

```
// CPP program to find
// the area of the square
#include <iostream>
using namespace std;

int areaSquare(int side)
{
    int area = side * side;
    return area;
}

// Driver Code
int main()
{
    int side = 4;
    cout << areaSquare(side);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// the area of the square
import java.util.*;

class GFG
{
    static int areaSquare(int side)
    {
    int area = side * side;
    return area;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int side = 5;
        System.out.println(areaSquare(4));
    }
}
```

## 蟒蛇 3

```
# Python3 code to find
# the area of the square

def areaSquare( side ):
    area = side * side
    return area

# Driver Code
side = 4
print(areaSquare(side))

# This code is contributed
# by "Sharad_Bhardwaj".
```

## C#

```
// C# program to find
// the area of the square
using System;

class GFG
{
    static int areaSquare(int side)
    {
        int area = side * side;
        return area;
    }

    // Driver code
    public static void Main()
    {
        int side = 4;

        Console.WriteLine(areaSquare(side));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// the aria of the square

function areaSquare($side)
{
    $area = $side * $side;
    return $area;
}

// Driver Code
$side = 4;
echo(areaSquare($side));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// the area of the square

function areaSquare(side)
{
    let area = side * side;
    return area;
}

// Driver Code

    let side = 4;
    document.write(areaSquare(side));

// This code is contributed by Mayank Tyagi
</script>
```

**输出:**

```
16
```

本文由 **Ajay Puri** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上述话题的信息，请写评论..