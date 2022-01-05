# 程序查找星号

> 原文:[https://www.geeksforgeeks.org/program-to-find-star-number/](https://www.geeksforgeeks.org/program-to-find-star-number/)

一个数被称为星数，如果它是一个居中的数字，代表一个类似中国棋局的居中卦(六芒星)。少数几个星形数字是 1，13，37，73，121，181，253，337，433，…
**例:**

```
Input : n = 2
Output : 13

Input : n = 4
Output : 73

Input : n = 6
Output : 181
```

如果我们举几个例子，我们可以注意到第 n 个星数由公式给出:

```
n-th star number = 6n(n - 1) + 1 
```

下面是上面公式的实现。

## C++

```
// C++ program to find star number
#include <bits/stdc++.h>
using namespace std;

// Returns n-th star number
int findStarNum(int n)
{
    return (6 * n * (n - 1) + 1);
}

// Driver code
int main()
{
    int n = 3;
    cout << findStarNum(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find star number
import java.io.*;

class GFG {
    // Returns n-th star number
    static int findStarNum(int n)
    {
        return (6 * n * (n - 1) + 1);
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 3;
        System.out.println(findStarNum(n));
    }
}

// This code is contributed
// by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python3 program to
# find star number

# Returns n-th
# star number
def findStarNum(n):

    return (6 * n * (n - 1) + 1)

# Driver code
n = 3
print(findStarNum(n))

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# program to find star number
using System;

class GFG {
    // Returns n-th star number
    static int findStarNum(int n)
    {
        return (6 * n * (n - 1) + 1);
    }

    // Driver code
    public static void Main()
    {
        int n = 3;
        Console.Write(findStarNum(n));
    }
}

// This code is contributed
// by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP program to find star number

// Returns n-th star number
function findStarNum($n)
{
    return (6 * $n * ($n - 1) + 1);
}

// Driver code
$n = 3;
echo findStarNum($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// Javascript program to find star number

// Returns n-th star number
function findStarNum(n)
{
    return (6 * n * (n - 1) + 1);
}

// Driver code
let n = 3;
document.write(findStarNum(n));

// This code is contributed by rishavmahato348.
</script>
```

**输出:**

```
37
```

**起始号码的有趣属性:**

1.  一个星号的[数字根](https://www.geeksforgeeks.org/digital-rootrepeated-digital-sum-given-integer/)总是 1 或 4，按照 1，4，1 的顺序进行。
2.  基数为 10 的星形数字的最后两位总是 01、13、21、33、37、41、53、61、73、81 或 93。
3.  星号的[生成函数](https://en.wikipedia.org/wiki/Generating_function)是

```
x*(x^2 + 10*x + 1) / (1-x)^3 = x + 13*x^2 + 37*x^3 +73*x^4 .......
```

1.  星形数满足线性递归方程

```
S(n) = S(n-1) + 12(n-1)
```

**参考文献:**
[http://mathworld.wolfram.com/StarNumber.html](http://mathworld.wolfram.com/StarNumber.html)
[https://en.wikipedia.org/wiki/Star_number](https://en.wikipedia.org/wiki/Star_number)
本文由 [**丹麦语 _RAZA**](https://www.facebook.com/danish.raza.98096721) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。