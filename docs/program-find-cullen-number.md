# 程序查找卡伦号

> 原文:[https://www.geeksforgeeks.org/program-find-cullen-number/](https://www.geeksforgeeks.org/program-find-cullen-number/)

库伦数是一个数字，其形式为 2 <sup>n</sup> * n + 1，其中 n 是整数。前几个库伦数字是 1、3、9、25、65、161、385、897、2049、4609。。。。。。
**例:**

```
Input : n = 4
Output :65

Input : n = 0
Output : 1

Input : n = 6
Output : 161
```

下面是公式的实现。我们使用按位左移运算符找到 2 <sup>n</sup> ，然后将结果乘以 n，最后返回(1 < < n)*n + 1。

## C++

```
// C++ program to find Cullen number
#include <bits/stdc++.h>
using namespace std;

// function to find n'th cullen number
unsigned findCullen(unsigned n)
{
    return (1 << n) * n + 1;
}

// Driver code
int main()
{
    int n = 2;
    cout << findCullen(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Cullen number
import java.io.*;

class GFG {
    // function to find n'th cullen number
    static int findCullen(int n)
    {
        return (1 << n) * n + 1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 2;
        System.out.println(findCullen(n));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python program to
# find Cullen number

# Function to calculate
# Cullen number
def findCullen(n):

    # Formula to calculate
    # nth Cullen number

    return (1 << n) * n + 1

# Driver Code
n = 2
print(findCullen(n))

# This code is contributed
# by aj_36                
```

## C#

```
// C# program to find Cullen number
using System;

class GFG {
    // function to find n'th cullen number
    static int findCullen(int n)
    {
        return (1 << n) * n + 1;
    }

    // Driver code
    public static void Main()
    {
        int n = 2;
        Console.WriteLine(findCullen(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to
// find Cullen number

// function to find n'th
// cullen number
function findCullen($n)
{
    return (1 << $n) * $n + 1;
}

    // Driver code
    $n = 2;
    echo findCullen($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program to find Cullen number

// function to find n'th cullen number
    function findCullen(n)
    {
        return (1 << n) * n + 1;
    }

// Driver Code
    let n = 2;
    document.write(findCullen(n));

</script>
```

**输出:**

```
9
```

**库伦编号的属性:**

1.  库伦数字大多是复合数字。
2.  如果 p 是 8k–3 形式的素数，第 n 个库伦数可被 p = 2n–1 整除。

**参考:**[https://en.wikipedia.org/wiki/Cullen_number](https://en.wikipedia.org/wiki/Cullen_number)
本文由 [**丹麦语 _RAZA**](https://www.facebook.com/danish.raza.98096721) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。