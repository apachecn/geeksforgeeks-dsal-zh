# 求前 n 个自然数的第 m 次求和。

> 原文:[https://www . geesforgeks . org/find-mth-summary-first-n-natural-numbers/](https://www.geeksforgeeks.org/find-mth-summation-first-n-natural-numbers/)

前 n 个自然数的第 m 次求和定义如下。

```
If m > 1
  SUM(n, m) = SUM(SUM(n, m - 1), 1)
Else 
  SUM(n, 1) = Sum of first n natural numbers.
```

给我们 m 和 n，我们需要求 SUM(n，m)。
示例:

```
Input  : n = 4, m = 1 
Output : SUM(4, 1) = 10
Explanation : 1 + 2 + 3 + 4 = 10

Input  : n = 3, m = 2 
Output : SUM(3, 2) = 21
Explanation : SUM(3, 2) 
             = SUM(SUM(3, 1), 1) 
             = SUM(6, 1) 
             = 21
```

**朴素方法:**我们可以使用两个嵌套循环来解决这个问题，其中外部循环迭代 m，内部循环迭代 n。在单个外部迭代完成后，我们应该在执行整个内部循环时更新 n，然后必须更改 n 的值。时间复杂度应为 O(n*m)。

```
for (int i = 1;i <= m;i++)
{
    sum = 0;
    for (int j = 1;j <= n;j++)
        sum += j;
    n = sum;  // update n
}
```

**高效方法:**
我们可以用直接公式求前 n 个数的和来减少时间。
我们也可以用递归。在这种方法中，m = 1 将是我们的基本条件，对于任何中间步骤 SUM(n，m)，我们将调用 SUM (SUM(n，m-1)，1)，对于单个步骤 SUM(n，1) = n * (n + 1) / 2 将被使用。这将把我们的时间复杂度降低到 0(m)。

```
int SUM (int n, int m)
{
    if (m == 1)
        return (n * (n + 1) / 2);
    int sum = SUM(n, m-1);
    return (sum * (sum + 1) / 2);
}
```

以下是上述思路的实现:

## C++

```
// CPP program to find m-th summation
#include <bits/stdc++.h>
using namespace std;

// Function to return mth summation
int SUM(int n, int m)
{  
    // base case
    if (m == 1)
        return (n * (n + 1) / 2);

    int sum = SUM(n, m-1);
    return (sum * (sum + 1) / 2);
}

// driver program
int main()
{
    int n = 5;
    int m = 3;
    cout << "SUM(" << n << ", " << m
         << "): " << SUM(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find m-th summation.
class GFG {

    // Function to return mth summation
    static int SUM(int n, int m) {

        // base case
        if (m == 1)
            return (n * (n + 1) / 2);

        int sum = SUM(n, m - 1);

        return (sum * (sum + 1) / 2);
    }

    // Driver code
    public static void main(String[] args) {

        int n = 5;
        int m = 3;

        System.out.println("SUM(" + n + ", "
                        + m + "): "    + SUM(n, m));
    }
}

// This code is contributed by Anant Agarwal.
```

<gfg-tab role="tab" slot="tab" id="gfg-tab-2">蟒 3</gfg-tab>T3

```
 # Python3 program to find m-th summation 

# Function to return mth summation
def SUM(n, m):

    # base case
    if (m == 1):
        return (n * (n + 1) / 2)

    sum = SUM(n, m-1)
    return int(sum * (sum + 1) / 2)

# driver program
n = 5
m = 3
print("SUM(", n, ", ", m, "):", SUM(n, m))

# This code is contributed by Smitha Dinesh Semwal 
```

T4

## C#

```
// C# program to find m-th summation.
using System;

class GFG
{

    // Function to return mth summation
    static int SUM(int n, int m)
    {

        // base case
        if (m == 1)
            return (n * (n + 1) / 2);

        int sum = SUM(n, m - 1);

        return (sum * (sum + 1) / 2);
    }

    // Driver Code
    public static void Main()
    {

        int n = 5;
        int m = 3;

        Console.Write("SUM(" + n + ", "
                       + m + "): " + SUM(n, m));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find m-th summation

// Function to return
// mth summation
function SUM($n, $m)
{

    // base case
    if ($m == 1)
        return ($n * ($n + 1) / 2);

    $sum = SUM($n, $m - 1);
    return ($sum * ($sum + 1) / 2);
}

    // Driver Code
    $n = 5;
    $m = 3;
    echo "SUM(" , $n , ", " , $m ,
         "): " , SUM($n, $m);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>
// javascript program to find m-th summation

// Function to return mth summation
function SUM( n,  m)
{  
    // base case
    if (m == 1)
        return (n * (n + 1) / 2);

    let sum = SUM(n, m-1);
    return (sum * (sum + 1) / 2);
}

// driver program

    let n = 5;
    let m = 3;
   document.write( "SUM(" + n + ", " + m
         + "): " + SUM(n, m));

// This code contributed by Rajput-Ji

</script>
```

输出:

```
SUM(5, 3): 7260
```

本文由[**Shivam Pradhan(anuj _ charm)**](http://www.facebook.com/ma5ter6it)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。