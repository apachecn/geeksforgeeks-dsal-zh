# 共 n 点共 m 条共线的不同直线的计数

> 原文:[https://www . geesforgeks . org/count-different-直线-total-n-points-m-共线/](https://www.geeksforgeeks.org/count-different-straight-lines-total-n-points-m-collinear/)

平面上有 n 个点，m 个点共线。能形成多少条不同的直线？
示例:

```
Input : n = 3, m = 3
Output : 1
We can form only 1 distinct straight line
using 3 collinear points

Input : n = 10, m = 4
Output : 40
```

> 不同直线的数量=**<sup>n</sup>C<sub>2</sub>–<sup>m</sup>C<sub>2</sub>+1**
> **这个公式是如何工作的？**
> 考虑上面的第二个例子。共有 10 个点，其中 4 个共线。这十个点中的任意两个点将形成一条直线。因此，形成一条直线相当于选择 10 个点中的任意两个。在 <sup>n</sup> C <sub>2</sub> 方式的 10 个点中可以选择两个点。
> 10 个点共线时形成的直线个数=**<sup>10</sup>C<sub>2</sub>**…..……(I)
> 同样，4 个点中没有 2 个共线时形成的直线数=**<sup>4</sup>C<sub>2</sub>**……。(二)
> 由于这 4 个点形成的直线是同向的，所以它们形成的直线将减少到只有一条。
> 所需形成的直线数=<sup>10</sup>C<sub>2</sub>–<sup>4</sup>C<sub>2</sub>+1 = 45–6+1 = 40

该方法的实现方式如下:

## C++

```
// CPP program to count number of straight lines
// with n total points, out of which m are
// collinear.
#include <bits/stdc++.h>

using namespace std;

// Returns value of binomial coefficient
// Code taken from https://goo.gl/vhy4jp
int nCk(int n, int k)
{

    int C[k+1];
    memset(C, 0, sizeof(C));

    C[0] = 1;  // nC0 is 1

    for (int i = 1; i <= n; i++)
    {

        // Compute next row of pascal triangle
        // using the previous row
        for (int j = min(i, k); j > 0; j--)

            C[j] = C[j] + C[j-1];
    }

    return C[k];
}

/* function to calculate number of straight lines
   can be formed */
int count_Straightlines(int n,int m)
{

    return (nCk(n, 2) - nCk(m, 2)+1);

}

/* driver function*/
int main()
{

    int n = 4, m = 3 ;
    cout << count_Straightlines(n, m);
    return 0;

}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of straight lines
// with n total points, out of which m are
// collinear.
import java.util.*;
import java.lang.*;

public class GfG  {

    // Returns value of binomial coefficient
    // Code taken from https://goo.gl/vhy4jp
    public static int nCk(int n, int k)
    {
        int[] C = new int[k + 1];

        C[0] = 1; // nC0 is 1

        for (int i = 1; i <= n; i++)  {

            // Compute next row of pascal triangle
            // using the previous row
            for (int j = Math.min(i, k); j > 0; j--)
                C[j] = C[j] + C[j - 1];
        }

        return C[k];
    }

    /* function to calculate number of straight lines
    can be formed */
    public static int count_Straightlines(int n, int m)
    {
        return (nCk(n, 2) - nCk(m, 2) + 1);
    }

    // Driver function
    public static void main(String argc[])
    {
        int n = 4, m = 3;
        System.out.println(count_Straightlines(n, m));
    }

    // This code is contributed by Sagar Shukla
}
```

## 计算机编程语言

```
# Python program to count number of straight lines
# with n total points, out of which m are
# collinear.

# Returns value of binomial coefficient
# Code taken from https://goo.gl/vhy4jp
def nCk(n, k):

    C = [0]* (k+1)

    C[0] = 1 # nC0 is 1

    for i in range(1, n+1):

        # Compute next row of pascal triangle
        # using the previous row
        j = min(i, k)

        while(j>0):

            C[j] = C[j] + C[j-1]
            j = j - 1

    return C[k]

#function to calculate number of straight lines
# can be formed
def count_Straightlines(n, m):

    return (nCk(n, 2) - nCk(m, 2)+1)

# Driven code
n = 4
m = 3
print( count_Straightlines(n, m) );

# This code is contributed by "rishabh_jain".
```

## C#

```
// C# program to count number of straight
// lines with n total points, out of
// which m are collinear.
using System;

public class GfG {

    // Returns value of binomial coefficient
    // Code taken from https://goo.gl/vhy4jp
    public static int nCk(int n, int k)
    {
        int[] C = new int[k + 1];

        // nC0 is 1
        C[0] = 1;

        for (int i = 1; i <= n; i++)
        {

            // Compute next row of pascal triangle
            // using the previous row
            for (int j = Math.Min(i, k); j > 0; j--)
                C[j] = C[j] + C[j - 1];
        }

        return C[k];
    }

    // Function to calculate number of
    // straight lines can be formed
    public static int count_Straightlines(int n, int m)
    {
        return (nCk(n, 2) - nCk(m, 2) + 1);
    }

    // Driver Code
    public static void Main(String []args)
    {
        int n = 4, m = 3;
        Console.WriteLine(count_Straightlines(n, m));
    }

}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number of straight lines
// with n total points, out of which m are
// collinear.

// Returns value of binomial coefficient
function nCk($n, $k)
{
    $C = array_fill(0, $k + 1, NULL);

    $C[0] = 1; // nC0 is 1

    for ($i = 1; $i <= $n; $i++)
    {

        // Compute next row of pascal triangle
        // using the previous row
        for ($j = min($i, $k); $j > 0; $j--)
            $C[$j] = $C[$j] + $C[$j-1];
    }
    return $C[$k];
}

// function to calculate
// number of straight lines
// can be formed
function count_Straightlines($n, $m)
{

    return (nCk($n, 2) - nCk($m, 2) + 1);

}

// Driver Code
$n = 4;
$m = 3;
echo(count_Straightlines($n, $m));

// This code is contributed
// by Prasad Kshirsagar
?>
```

## java 描述语言

```
<script>
    // Javascript program to count number of straight
    // lines with n total points, out of
    // which m are collinear.

    // Returns value of binomial coefficient
    // Code taken from https://goo.gl/vhy4jp
    function nCk(n, k)
    {

        let C = new Array(k+1);
        C.fill(0);

        C[0] = 1;  // nC0 is 1

        for (let i = 1; i <= n; i++)
        {

            // Compute next row of pascal triangle
            // using the previous row
            for (let j = Math.min(i, k); j > 0; j--)

                C[j] = C[j] + C[j-1];
        }

        return C[k];
    }

    /* function to calculate number of straight lines
       can be formed */
    function count_Straightlines(n,m)
    {
        return (nCk(n, 2) - nCk(m, 2)+1);
    }

    let n = 4, m = 3 ;
    document.write(count_Straightlines(n, m));

    // This code is contributed by divyesh072019.
</script>
```

输出:

```
4
```