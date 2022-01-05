# k 次迭代后剩下的巧克力数量

> 原文:[https://www . geeksforgeeks . org/巧克力数量-k 次迭代后剩余/](https://www.geeksforgeeks.org/number-of-chocolates-left-after-k-iterations/)

给定一堆巧克力和一个整数“k”，即迭代次数，任务是找出 k 次迭代后剩下的巧克力数量。
**注:**在每次迭代中，我们可以选择巧克力数量最多的一堆，之后剩下的平方根巧克力就剩下了，剩下的吃掉。
**示例:**

```
Input: Chocolates = 100000000, Iterations = 3
Output: 10

Input: Chocolates = 200, Iterations = 2
Output: 4
```

**注意:**输出在四舍五入后打印，如第二个例子，输出大约在 **3.76 左右。**
**方法:**
假设选择了最大数量的巧克力，那么考虑总堆数，因为它将是最大的。
接下来，假设在每次迭代中只剩下方形巧克力，因此通过考虑
的数学方程

```
(((number)n)n)...n for k times = (number)nk
```

因为这里执行 k 次平方根，所以(1/2) <sup>k</sup> 由 n
供电考虑 100000000 块巧克力的例子，迭代次数是 3，那么它将是

```
(((100000000)1/2)1/2)1/2 = (100000000)(1/2)3 = 10
```

**以下是找到剩余巧克力所需的配方:**

```
round(pow(n, (1.0/pow(2, k))))
```

## C++

```
// C++ program to find remaining
// chocolates after k iterations
#include <bits/stdc++.h>
using namespace std;

// Function to find the chocolates left
int results(int n, int k)
{
    return round(pow(n, (1.0 / pow(2, k))));
}

// Driver code
int main()
{
    int k = 3, n = 100000000;

    cout << "Chocolates left after " << k
         << " iterations are " << results(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find remaining
// chocolates after k iterations
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{
// Function to find the
// chocolates left
static int results(int n, int k)
{
    return (int)Math.round(Math.pow(n,
           (1.0 / Math.pow(2.0, k))));
}

// Driver code
public static void main(String args[])
{
    int k = 3, n = 100000000;

    System.out.print("Chocolates left after " + k +
               " iterations are " + results(n, k));
}
}

// This code is contributed by Subhadeep
```

## C#

```
// C# program to find remaining
// chocolates after k iterations
using System;

class GFG
{
// Function to find the
// chocolates left
static int results(int n, int k)
{
    return (int)Math.Round(Math.Pow(n,
           (1.0 / Math.Pow(2.0, k))));
}

// Driver code
public static void Main()
{
    int k = 3, n = 100000000;

    Console.Write("Chocolates left after " +
                    k + " iterations are " +
                             results(n, k));
}
}

// This code is contributed
// by ChitraNayal
```

## 计算机编程语言

```
# Python program to find
# remaining chocolates
# after k iterations

# Function to find the
# chocolates left
def results(n, k):

    return round(pow(n, (1.0 /
                 pow(2, k))))

# Driver code
k = 3
n = 100000000

print("Chocolates left after"),
print(k),
print("iterations are"),
print(int(results(n, k)))

# This code is contributed
# by Shivi_Aggarwal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find remaining
// chocolates after k iterations

// Function to find
// the chocolates left
function results($n, $k)
{
    return round(pow($n, (1.0 /
                 pow(2, $k))));
}

// Driver code
$k = 3;
$n = 100000000;
echo ("Chocolates left after ");
echo ($k);

echo (" iterations are ");
echo (results($n, $k));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// javascript program to find remaining
// chocolates after k iterations    // Function to find the
    // chocolates left
    function results(n , k) {
        return parseInt( Math.round(Math.pow(n,
        (1.0 / Math.pow(2.0, k)))));
    }

    // Driver code

        var k = 3, n = 100000000;

        document.write("Chocolates left after " +
        k + " iterations are " + results(n, k));

// This code contributed by aashish1995
</script>
```

**Output:** 

```
Chocolates left after 3 iterations are 10
```