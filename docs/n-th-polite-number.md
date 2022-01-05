# 第 N 个礼貌号码

> 原文:[https://www.geeksforgeeks.org/n-th-polite-number/](https://www.geeksforgeeks.org/n-th-polite-number/)

礼貌数字是一个正整数，可以写成两个或多个连续正整数的和。给定 N，找到第 N 个礼貌数字。
示例:

```
Input : 4
Output : 7
Explanation: The first 3 are 3(1+2), 5(2+3), 
             6(1+2+3).

Input : 7
Output : 11
Explanation:  3, 5, 6, 7, 9, 10, 11.
```

存在一种有趣的模式，即在一系列礼貌数字中，只有 2 的幂不存在。基于这一事实，第 N 个礼貌数存在以下公式([兰贝克-莫瑟定理](https://en.wikipedia.org/wiki/Lambek%E2%80%93Moser_theorem))。
![f(n) = n+ \left \lfloor log_2 (n+ log_2 n) \right \rfloor  ](img/48c608f3e222f46ee24957ae3a2cd647.png "Rendered by QuickLaTeX.com")
在这里要找到第 n 个礼貌数字，我们必须把 **n 作为 n+1** 在上面的等式
中，内置的 log 函数计算 log base-e，所以用 log base-e 除以 2 会得到 log base-2 的值。
下面给出的是上述方法的实现:

## C++

```
// CPP program to find Nth polite number
#include <bits/stdc++.h>
using namespace std;

// function to evaluate Nth polite number
double polite(double n)
{
    n += 1;
    double base = 2;
    return n + (log((n + (log(n) /
                 log(base))))) / log(base);
}

// driver code
int main()
{
    double n = 7;

    cout << (int)polite(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for finding N-th polite number
import java.io.*;

class GFG {

    // function to find N-th polite number
    static double polite(double n)
    {
        n += 1;
        double base = 2;
        return n + (Math.log((n + (Math.log(n) /
               Math.log(base))))) / Math.log(base);
    }

    // driver code
    public static void main(String[] args)
    {
        double n = 7;
        System.out.println((int)polite(n));
    }
}
```

## 计算机编程语言

```
import math
# function to find Nth polite number
def Polite(n):
    n = n + 1
    return (int)(n+(math.log((n + math.log(n, 2)), 2)))

# Driver code
n = 7
print Polite(n)
```

## C#

```
// Java program for finding
// N-th polite number
using System;

class GFG {

    // Function to find N-th polite number
    static double polite(double n)
    {
        n += 1;
        double base1 = 2;
        return n + (Math.Log((n + (Math.Log(n) /
                     Math.Log(base1))))) /
                     Math.Log(base1);
    }

    // Driver code
    public static void Main(String []args)
    {
        double n = 7;
        Console.Write((int)polite(n));
    }
}

// This code is contributed by
// Smitha Dinesh Semwal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// Nth polite number

// function to evaluate
// Nth polite number
function polite($n)
{
    $n += 1;
    $base = 2;
    return $n + (log(($n + (log($n) /
                 log($base))))) / log($base);
}

// Driver code
$n = 7;
echo((int)polite($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// Nth polite number

// function to evaluate
// Nth polite number
function polite(n)
{
    n += 1;
    let base = 2;
    return n + (Math.log((n + (Math.log(n) /
                Math.log(base))))) / Math.log(base);
}

// Driver code
n = 7;
document.write(parseInt(polite(n)));

// This code is contributed by _saurabh_jaiswal.

</script>
```

**输出:**

```
11
```

参考:[维基百科](https://en.wikipedia.org/wiki/Polite_number)