# 程序求数列 1*3 + 3*5 +的和……

> 原文:[https://www . geesforgeks . org/program-to-find-sum-of-series-13-35/](https://www.geeksforgeeks.org/program-to-find-sum-of-the-series-13-35/)

给定一个系列:

> S <sub>n</sub> = 1*3 + 3*5 + 5*7 + …

要求求这个数列的前 n 项之和，用 S <sub>n</sub> 表示，其中 n 是给定的取值输入。
**示例** :

```
Input : n = 2 
Output : S<sub>n</sub> = 18
Explanation:
The sum of first 2 terms of Series is
1*3 + 3*5
= 3 + 15 
= 28

Input : n = 4 
Output : S<sub>n</sub> = 116
Explanation:
The sum of first 4 terms of Series is
1*3 + 3*5 + 5*7 + 7*9
= 3 + 15 + 35 + 63
= 116
```

让第 n 项用 t <sub>n</sub> 表示。
这个问题很容易通过观察第 n 项可以用以下方法建立来解决:

> t <sub>n</sub> =(第 n 个(1，3，5，…)项)*(第 n 个(3，5，7，…)项。))

现在，系列 1、3、5 的第 n 项由 **2*n-1**
给出，系列 3、5、7 的第 n 项由 **2*n+1**
给出，将这两个值放入 t <sub>n</sub> :

> t<sub>n</sub>=(2 * n-1)*(2 * n+1)= 4 * n * n-1

现在，前 n 项的总和将由下式给出:

> s<sub>n</sub>=∑(4 * n * n–1)
> =∑4 * { n * n }-∑(1)

现在已知级数 n*n (1，4，9，…)的前 n 项之和由下式给出:n*(n+1)*(2*n+1)/6
而 1 的 n 个数之和就是 n 本身。
现在，将值放入 S<sub>n</sub>:T4

> s<sub>n</sub>= 4 * n *(n+1)*(2 * n+1)/6–n
> = n *(4 * n * n+6 * n–1)/3

现在，S <sub>n</sub> 值可以很容易地通过输入 n 的期望值找到
下面是上面方法的实现:

## C++

```
// C++ program to find sum of first n terms
#include <bits/stdc++.h>
using namespace std;

int calculateSum(int n)
{
    // Sn = n*(4*n*n + 6*n - 1)/3
    return (n * (4 * n * n + 6 * n - 1) / 3);
}

int main()
{
    // number of terms to be included in the sum
    int n = 4;

    // find the Sn
    cout << "Sum = " << calculateSum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum
// of first n terms
class GFG
{
    static int calculateSum(int n)
    {
        // Sn = n*(4*n*n + 6*n - 1)/3
        return (n * (4 * n * n +
                     6 * n - 1) / 3);
    }

    // Driver Code
    public static void main(String args[])
    {
        // number of terms to be
        // included in the sum
        int n = 4;

        // find the Sn
        System.out.println("Sum = " +
                            calculateSum(n));
    }
}

// This code is contributed by Bilal
```

## 计算机编程语言

```
# Python program to find sum
# of first n terms
def calculateSum(n):

    # Sn = n*(4*n*n + 6*n - 1)/3
    return (n * (4 * n * n +
                 6 * n - 1) / 3);

# Driver Code

# number of terms to be
# included in the sum
n = 4

# find the Sn
print("Sum =",calculateSum(n))

# This code is contributed by Bilal
```

## C#

```
// C# program to find sum
// of first n terms
using System;

class GFG
{

static int calculateSum(int n)
{
    // Sn = n*(4*n*n + 6*n - 1)/3
    return (n * (4 * n * n +
                 6 * n - 1) / 3);
}

// Driver code
static public void Main ()
{
    // number of terms to be
    // included in the sum
    int n = 4;

    // find the Sn
    Console.WriteLine("Sum = " +
                       calculateSum(n));
}
}

// This code is contributed
// by mahadev
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum
// of first n terms

function calculateSum($n)
{
    // Sn = n*(4*n*n + 6*n - 1)/3
    return ($n * (4 * $n * $n +
                  6 * $n - 1) / 3);
}

// number of terms to be
// included in the sum
$n = 4;

// find the Sn
echo "Sum = " . calculateSum($n);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum
// of first n terms

    function calculateSum( n) {
        // Sn = n*(4*n*n + 6*n - 1)/3
        return (n * (4 * n * n + 6 * n - 1) / 3);
    }

    // Driver Code

        // number of terms to be
        // included in the sum
        let n = 4;

        // find the Sn
        document.write("Sum = " + calculateSum(n));

// This code contributed by Princi Singh

</script>
```

**Output:** 

```
Sum = 116
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*