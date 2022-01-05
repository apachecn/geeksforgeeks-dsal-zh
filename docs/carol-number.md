# 卡罗尔号

> 原文:[https://www.geeksforgeeks.org/carol-number/](https://www.geeksforgeeks.org/carol-number/)

卡罗尔数是 4<sup>n</sup>–2<sup>(n+1)</sup>–1 形式的整数。一个等价的公式是(2<sup>n</sup>-1)<sup>2</sup>–2。
**一个有趣的性质:**
对于 n > 2，第 n 个 Carol 数的二进制表示为 n-2 个连续的 1，中间一个零，再 n + 1 个连续的 1。例如，n = 4 卡罗尔数是 223，223 的二进制数是 11011111，这里 n-2 = 4-2 = 2 个连续的 1 在开始，然后中间是单 0，然后 n + 1 = 4 + 1 = 5 个连续的 1 在它之后。
给定一个数字 n，任务是找到第 n 个卡罗尔数字。首先，很少有卡罗尔数字是-1，7，47，223，959…等等。

**示例:**

```
Input : n = 2
Output: 7

Input : n = 4
Output: 223
```

## C++

```
// C++ program to find n'th Carol number
#include <bits/stdc++.h>
using namespace std;

// Function to find n'th carol number
int carol(int n)
{
    int result = pow(2, n) - 1;
    return result * result - 2;
}

// Driver program to ru the case
int main()
{
    int n = 4;
    cout << carol(n);
    return 0;
}
```

## 计算机编程语言

```
# Python program to find n'th Carol number
def carol(n):
    # a**b is a ^ b in python
    result = (2**n) - 1
    return result * result - 2

# driver program to run the case
n = 4
print carol(n)
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to find n'th Carol number */
class GFG {
    static int carol(int n)
    {
        double tmp = Math.pow(2, n) - 1;
        return (int)tmp;
    }

    public static void main(String[] args)
    {
        int n = 4;
        System.out.println(carol(n));
    }
}
```

## C#

```
/* C# program to find n'th Carol number */
using System;

class GFG {
    static int carol(int n)
    {
        int result = (int)Math.Pow(2, n) - 1;
        return result * result - 2;
    }

    // Driver code
    public static void Main()
    {
        int n = 4;
        Console.WriteLine(carol(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// n'th Carol number

// Function to find
// n'th carol number
function carol($n)
{
    $result = pow(2, $n) - 1;
    return $result * $result - 2;
}

// Driver Code
$n = 4;
echo carol($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    /* Javascript program to find n'th Carol number */

    function carol(n)
    {
        let result = Math.pow(2, n) - 1;
        return result * result - 2;
    }

    let n = 4;
      document.write(carol(n));

</script>
```

**输出:**

```
223
```

参考:
[【https://en.wikipedia.org/wiki/Carol_number】](https://en.wikipedia.org/wiki/Carol_number)
本文由 [**沙莎克·米什拉(古卢)**](https://www.facebook.com/shashank.mishra.92167) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。