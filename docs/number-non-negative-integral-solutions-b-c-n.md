# a+b+c = n 的非负积分解个数

> 原文:[https://www . geesforgeks . org/number-non-negative-integral-solutions-B- c-n/](https://www.geeksforgeeks.org/number-non-negative-integral-solutions-b-c-n/)

给定一个数 n，找出我们可以将 3 个非负整数相加的方法，使它们的和为 n。
示例:

```
Input : n = 1
Output : 3
There are four ways to get sum 1.
(1, 0, 0), (0, 1, 0) and (0, 0, 1)

Input : n = 2
Output : 6
There are six ways to get sum 2.
(2, 0, 0), (0, 2, 0), (0, 0, 2), (1, 1, 0)
(1, 0, 1) and (0, 1, 1)

Input : n = 3
Output : 10
There are ten ways to get sum 10.
(3, 0, 0), (0, 3, 0), (0, 0, 3), (1, 2, 0)
(1, 0, 2), (0, 1, 2), (2, 1, 0), (2, 0, 1),
(0, 2, 1) and (1, 1, 1)
```

**方法 1【蛮力:O(n<sup>3</sup>)】**
一个简单的解决方法是考虑使用三个循环的所有三胞胎。对于每个三元组，检查其总和是否等于 n。如果总和为 n，则增加解的数量。
下面是实现。

## C++

```
// A naive C++ solution to count solutions of
// a + b + c = n
#include<bits/stdc++.h>
using namespace std;

// Returns count of solutions of a + b + c = n
int countIntegralSolutions(int n)
{
    // Initialize result
    int result = 0;

    // Consider all triplets and increment
    // result whenever sum of a triplet is n.
    for (int i=0; i<=n; i++)
      for (int j=0; j<=n-i; j++)
          for (int k=0; k<=(n-i-j); k++)
             if (i + j + k == n)
              result++;

    return result;
}

// Driver code
int main()
{
    int n = 3;
    cout <<  countIntegralSolutions(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A naive Java solution to count
// solutions of a + b + c = n
import java.io.*;

class GFG
{
    // Returns count of solutions of a + b + c = n
    static int countIntegralSolutions(int n)
    {
        // Initialize result
        int result = 0;

        // Consider all triplets and increment
        // result whenever sum of a triplet is n.
        for (int i = 0; i <= n; i++)
        for (int j = 0; j <= n - i; j++)
            for (int k = 0; k <= (n - i - j); k++)
                if (i + j + k == n)
                result++;

        return result;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 3;
        System.out.println( countIntegralSolutions(n));

    }
}

// This article is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 code to count
# solutions of a + b + c = n

# Returns count of solutions
# of a + b + c = n
def countIntegralSolutions (n):

    # Initialize result
    result = 0

    # Consider all triplets and
    # increment result whenever
    # sum of a triplet is n.
    for i in range(n + 1):
        for j in range(n + 1):
            for k in range(n + 1):
                if i + j + k == n:
                    result += 1

    return result

# Driver code
n = 3
print(countIntegralSolutions(n))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// A naive C# solution to count
// solutions of a + b + c = n
using System;

class GFG {

    // Returns count of solutions
    // of a + b + c = n
    static int countIntegralSolutions(int n)
    {

        // Initialize result
        int result = 0;

        // Consider all triplets and increment
        // result whenever sum of a triplet is n.
        for (int i = 0; i <= n; i++)
            for (int j = 0; j <= n - i; j++)
                for (int k = 0; k <= (n - i - j); k++)
                    if (i + j + k == n)
                    result++;

        return result;
    }

    // Driver code
    public static void Main ()
    {
        int n = 3;
        Console.Write(countIntegralSolutions(n));

    }
}

// This article is contributed by Smitha.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A naive PHP solution
// to count solutions of
// a + b + c = n

// Returns count of
// solutions of a + b + c = n
function countIntegralSolutions( $n)
{

    // Initialize result
    $result = 0;

    // Consider all triplets and increment
    // result whenever sum of a triplet is n.
    for ($i = 0; $i <= $n; $i++)
        for ($j = 0; $j <= $n - $i; $j++)
            for ($k = 0; $k <= ($n - $i - $j); $k++)
            if ($i + $j + $k == $n)
            $result++;

    return $result;
}

    // Driver Code
    $n = 3;
    echo countIntegralSolutions($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program solution to count
// solutions of a + b + c = n

  // Returns count of solutions of a + b + c = n
    function countIntegralSolutions(n)
    {
        // Initialize result
        let result = 0;

        // Consider all triplets and increment
        // result whenever sum of a triplet is n.
        for (let i = 0; i <= n; i++)
        for (let j = 0; j <= n - i; j++)
            for (let k = 0; k <= (n - i - j); k++)
                if (i + j + k == n)
                result++;

        return result;
    }

// Driver Code

    let n = 3;
    document.write(countIntegralSolutions(n));

</script>
```

**输出:**

```
10
```

**方法二【直接公式:O(1)】**
如果我们仔细看一下模式，可以发现解的个数是((n+1) * (n+2)) / 2。这个问题相当于在三个盒子里分配 n + 1 个相同的球(0 到 n)，解决方法是 <sup>n+2</sup> C <sub>2</sub> 。一般来说，如果有 m 个变量(或框)和 n 个可能值，则公式变为**<sup>n+m-1</sup>C<sub>m-1</sub>**。

## C++

```
// A naive C++ solution to count solutions of
// a + b + c = n
#include<bits/stdc++.h>
using namespace std;

// Returns count of solutions of a + b + c = n
int countIntegralSolutions(int n)
{
    return ((n+1)*(n+2))/2;
}

// Driver code
int main()
{
    int n = 3;
    cout <<  countIntegralSolutions(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java solution to count
// solutions of a + b + c = n
import java.io.*;

class GFG
{
    // Returns count of solutions
    // of a + b + c = n
    static int countIntegralSolutions(int n)
    {
    return ((n + 1) * (n + 2)) / 2;

    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 3;
        System.out.println ( countIntegralSolutions(n));

    }
}
// This article is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 solution to count
# solutions of a + b + c = n

# Returns count of solutions
# of a + b + c = n
def countIntegralSolutions (n):
    return int(((n + 1) * (n + 2)) / 2)

# Driver code
n = 3
print(countIntegralSolutions(n))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# solution to count
// solutions of a + b + c = n
using System;

class GFG {

    // Returns count of solutions
    // of a + b + c = n
    static int countIntegralSolutions(int n)
    {
        return ((n + 1) * (n + 2)) / 2;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int n = 3;
        Console.Write ( countIntegralSolutions(n));

    }
}

// This code is contributed by parashar.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A naive PHP solution
// to count solutions of
// a + b + c = n

// Returns count of solutions
// of a + b + c = n
function countIntegralSolutions($n)
{
    return (($n + 1) * ($n + 2)) / 2;
}

    // Driver Code
    $n = 3;
    echo countIntegralSolutions($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// A naive JavaScript solution
// to count solutions of
// a + b + c = n

// Returns count of solutions of a + b + c = n
function countIntegralSolutions(n)
{
    return Math.floor(((n+1)*(n+2))/2);
}

// Driver code

    let n = 3;
    document.write(countIntegralSolutions(n));

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
10
```

本文由**希瓦姆·古普塔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息