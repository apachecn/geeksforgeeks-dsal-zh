# 合并两个数组这样保留顺序的方式数量

> 原文:[https://www . geesforgeks . org/number-way-merge-two-array-retaining-order/](https://www.geeksforgeeks.org/number-ways-merge-two-arrays-retaining-order/)

给定两个大小为 **n** 和 m 的数组，任务是找出我们可以将给定数组合并成一个数组的方法，这样每个数组的元素顺序就不会改变。
**例:**

```
Input : n = 2, m = 2
Output : 6
Let first array of size n = 2 be [1, 2] and second array of size m = 2 be [3, 4].
So, possible merged array of n + m elements can be:
[1, 2, 3, 4]
[1, 3, 2, 4]
[3, 4, 1, 2]
[3, 1, 4, 2]
[1, 3, 4, 2]
[3, 1, 2, 4]

Input : n = 4, m = 6
Output : 210
```

这个想法是利用组合学的概念。假设我们有两个数组 A{a1，a2，…。，am}和 B{b1，b2，…。，bn}分别有 m 和 n 个元素，现在我们必须合并它们而不丢失它们的顺序。
合并后我们知道合并后元素总数会是(m + n)个元素。所以，现在我们只需要从(m + n)中选择 m 个位置的方法，您将按照数组 A 的实际顺序放置数组 A 的元素，即 <sup>m + n</sup> C <sub>n</sub> 。
放置数组 A 的 m 个元素后，会留下 n 个空格，可以用数组 B 的 n 个元素按其实际顺序填充。
因此，合并两个数组以使它们在合并数组中的顺序相同的方法总数是**<sup>m+n</sup>C<sub>n</sub>**
下面是该方法的实现:

## C++

```
// CPP Program to find number of ways
// to merge two array such that their
// order in merged array is same
#include <bits/stdc++.h>
using namespace std;

// function to find the binomial coefficient
int binomialCoeff(int n, int k)
{
    int C[k + 1];
    memset(C, 0, sizeof(C));

    C[0] = 1; // nC0 is 1

    for (int i = 1; i <= n; i++) {

        // Compute next row of pascal triangle
        // using the previous row
        for (int j = min(i, k); j > 0; j--)
            C[j] = C[j] + C[j - 1];
    }
    return C[k];
}

// function to find number of ways
// to merge two array such that their
// order in merged array is same
int numOfWays(int n, int m)
{
    return binomialCoeff(m + n, m);
}

// Driven Program
int main()
{
    int n = 2, m = 2;
    cout << numOfWays(n, m) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find number of ways
// to merge two array such that their
// order in merged array is same

import java.io.*;

class GFG {

    // function to find the binomial
    // coefficient
    static int binomialCoeff(int n, int k)
    {
        int C[] = new int[k + 1];
        // memset(C, 0, sizeof(C));

        C[0] = 1; // nC0 is 1

        for (int i = 1; i <= n; i++) {

            // Compute next row of pascal
            // triangle using the previous
            // row
            for (int j = Math.min(i, k);
                               j > 0; j--)
                C[j] = C[j] + C[j - 1];
        }

        return C[k];
    }

    // function to find number of ways
    // to merge two array such that their
    // order in merged array is same
    static int numOfWays(int n, int m)
    {
        return binomialCoeff(m + n, m);
    }

    // Driven Program
    public static void main (String[] args)
    {
        int n = 2, m = 2;
        System.out.println(numOfWays(n, m));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python 3 Program to find number of ways
# to merge two array such that their
# order in merged array is same

# function to find the binomial coefficient
def binomialCoeff(n, k):
    C = [0 for i in range(k + 1)]

    C[0] = 1

    for i in range(1, n + 1, 1):

        # Compute next row of pascal
        # triangle using the previous row
        j = min(i, k)
        while(j > 0):
            C[j] = C[j] + C[j - 1]
            j -= 1

    return C[k]

# function to find number of ways
# to merge two array such that their
# order in merged array is same
def numOfWays(n, m):
    return binomialCoeff(m + n, m)

# Driver Code
if __name__ == '__main__':
    n = 2
    m = 2
    print(numOfWays(n, m))

# This code is contributed by
# Sahil_shelangia
```

## C#

```
// C# Program to find number of ways
// to merge two array such that their
// order in merged array is same

using System;

class GFG {

    // function to find the binomial
    // coefficient
    static int binomialCoeff(int n, int k)
    {
        int []C = new int[k + 1];
        // memset(C, 0, sizeof(C));

        C[0] = 1; // nC0 is 1

        for (int i = 1; i <= n; i++) {

            // Compute next row of pascal
            // triangle using the previous
            // row
            for (int j = Math.Min(i, k);
                            j > 0; j--)
                C[j] = C[j] + C[j - 1];
        }

        return C[k];
    }

    // function to find number of ways
    // to merge two array such that their
    // order in merged array is same
    static int numOfWays(int n, int m)
    {
        return binomialCoeff(m + n, m);
    }

    // Driven Program
    public static void Main ()
    {
        int n = 2, m = 2;
        Console.WriteLine(numOfWays(n, m));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find number of ways
// to merge two array such that their
// order in merged array is same

// function to find the binomial coefficient
function binomialCoeff($n, $k)
{
     $C = array($k + 1);
      for($i=0; $i < count($C); $i++)
        $C[$i] = 0;

    $C[0] = 1; // nC0 is 1

    for ( $i = 1; $i <= $n; $i++) {

        // Compute next row of pascal triangle
        // using the previous row
        for ( $j = min($i, $k); $j > 0; $j--)
            $C[$j] = $C[$j] + $C[$j - 1 ];
    }
    return $C[$k];
}

// function to find number of ways
// to merge two array such that their
// order in merged array is same
function numOfWays( $n, $m)
{
    return binomialCoeff($m + $n, $m);
}

    $n = 2; $m = 2;
    echo numOfWays($n, $m);
   //This code is contributed by Rajput-Ji.
?>
```

## java 描述语言

```
<script>
    // Javascript Program to find number of ways
    // to merge two array such that their
    // order in merged array is same

    // function to find the binomial
    // coefficient
    function binomialCoeff(n, k)
    {
        let C = new Array(k + 1);
        C.fill(0);
        // memset(C, 0, sizeof(C));

        C[0] = 1; // nC0 is 1

        for (let i = 1; i <= n; i++) {

            // Compute next row of pascal
            // triangle using the previous
            // row
            for (let j = Math.min(i, k); j > 0; j--)
                C[j] = C[j] + C[j - 1];
        }

        return C[k];
    }

    // function to find number of ways
    // to merge two array such that their
    // order in merged array is same
    function numOfWays(n, m)
    {
        return binomialCoeff(m + n, m);
    }

    let n = 2, m = 2;
      document.write(numOfWays(n, m));

   // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
6
```

利用二项式系数的[线性时间实现，我们可以在线性时间内解决上述问题。](https://www.geeksforgeeks.org/space-and-time-efficient-binomial-coefficient/)