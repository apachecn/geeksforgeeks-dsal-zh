# 时空效率二项式系数

> 原文:[https://www . geeksforgeeks . org/时空效率-二项式系数/](https://www.geeksforgeeks.org/space-and-time-efficient-binomial-coefficient/)

写一个函数，取两个参数 n 和 k，返回二项式系数 C(n，k)的值。
**例:**

```
Input: n = 4 and k = 2
Output: 6
Explanation: 4 C 2 is 4!/(2!*2!) = 6

Input: n = 5 and k = 2
Output: 10
Explanation: 5 C 2 is 5!/(3!*2!) = 20
```

我们在[这篇](https://www.geeksforgeeks.org/binomial-coefficient-dp-9/)的帖子里讨论了一个 O(n*k)时间和 O(k)额外空间的算法。C(n，k)的值可以在 O(k)时间和 O(1)额外空间中计算。
**<u>解:</u>**

```
C(n, k) 
= n! / (n-k)! * k!
= [n * (n-1) *....* 1]  / [ ( (n-k) * (n-k-1) * .... * 1) * 
                            ( k * (k-1) * .... * 1 ) ]
After simplifying, we get
C(n, k) 
= [n * (n-1) * .... * (n-k+1)] / [k * (k-1) * .... * 1]

Also, C(n, k) = C(n, n-k)  
// r can be changed to n-r if r > n-r 
```

1.  如果 r 大于 n-r，将 r 更改为 n-r，并创建一个变量来存储答案。
2.  运行从 0 到 r-1 的循环
3.  在每次迭代中，将 ans 更新为(ans*(n-i))/(i+1)，其中 I 是循环计数器。
4.  所以答案将等于((n/1)*((n-1)/2)*……*((n-r+1)/r！)等于 nCr。

以下实现使用上述公式计算 C(n，k)。

## C++

```
// Program to calculate C(n, k)
#include <bits/stdc++.h>
using namespace std;

// Returns value of Binomial Coefficient C(n, k)
int binomialCoeff(int n, int k)
{
    int res = 1;

    // Since C(n, k) = C(n, n-k)
    if (k > n - k)
        k = n - k;

    // Calculate value of
    // [n * (n-1) *---* (n-k+1)] / [k * (k-1) *----* 1]
    for (int i = 0; i < k; ++i) {
        res *= (n - i);
        res /= (i + 1);
    }

    return res;
}

// Driver Code
int main()
{
    int n = 8, k = 2;
    cout << "Value of C(" << n << ", "
         << k << ") is " << binomialCoeff(n, k);
    return 0;
}

// This is code is contributed by rathbhupendra
```

## C

```
// Program to calculate C(n, k)
#include <stdio.h>

// Returns value of Binomial Coefficient C(n, k)
int binomialCoeff(int n, int k)
{
    int res = 1;

    // Since C(n, k) = C(n, n-k)
    if (k > n - k)
        k = n - k;

    // Calculate value of
    // [n * (n-1) *---* (n-k+1)] / [k * (k-1) *----* 1]
    for (int i = 0; i < k; ++i) {
        res *= (n - i);
        res /= (i + 1);
    }

    return res;
}

/* Driver program to test above function*/
int main()
{
    int n = 8, k = 2;
    printf(
        "Value of C(%d, %d) is %d ",
        n, k, binomialCoeff(n, k));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to calculate C(n, k) in java
class BinomialCoefficient {
    // Returns value of Binomial Coefficient C(n, k)
    static int binomialCoeff(int n, int k)
    {
        int res = 1;

        // Since C(n, k) = C(n, n-k)
        if (k > n - k)
            k = n - k;

        // Calculate value of
        // [n * (n-1) *---* (n-k+1)] / [k * (k-1) *----* 1]
        for (int i = 0; i < k; ++i) {
            res *= (n - i);
            res /= (i + 1);
        }

        return res;
    }

    /* Driver program to test above function*/
    public static void main(String[] args)
    {
        int n = 8;
        int k = 2;
        System.out.println("Value of C(" + n + ", " + k + ") "
                           + "is"
                           + " " + binomialCoeff(n, k));
    }
}
// This Code is Contributed by Saket Kumar
```

## 计算机编程语言

```
# Python program to calculate C(n, k)

# Returns value of Binomial Coefficient
# C(n, k)
def binomialCoefficient(n, k):
    # since C(n, k) = C(n, n - k)
    if(k > n - k):
        k = n - k
    # initialize result
    res = 1
    # Calculate value of
    # [n * (n-1) *---* (n-k + 1)] / [k * (k-1) *----* 1]
    for i in range(k):
        res = res * (n - i)
        res = res // (i + 1)
    return res

# Driver program to test above function
n = 8
k = 2
res = binomialCoefficient(n, k)
print("Value of C(% d, % d) is % d" %(n, k, res))

# This code is contributed by Aditi Sharma
```

## C#

```
// C# Program to calculate C(n, k)
using System;

class BinomialCoefficient {

    // Returns value of Binomial
    // Coefficient C(n, k)
    static int binomialCoeff(int n, int k)
    {
        int res = 1;

        // Since C(n, k) = C(n, n-k)
        if (k > n - k)
            k = n - k;

        // Calculate value of [n * ( n - 1) *---* (
        // n - k + 1)] / [k * (k - 1) *----* 1]
        for (int i = 0; i < k; ++i) {
            res *= (n - i);
            res /= (i + 1);
        }

        return res;
    }

    // Driver Code
    public static void Main()
    {
        int n = 8;
        int k = 2;
        Console.Write("Value of C(" + n + ", " + k + ") "
                      + "is"
                      + " " + binomialCoeff(n, k));
    }
}

// This Code is Contributed by
// Smitha Dinesh Semwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to calculate C(n, k)
// Returns value of Binomial
// Coefficient C(n, k)

function binomialCoeff($n, $k)
{
    $res = 1;

    // Since C(n, k) = C(n, n-k)
    if ( $k > $n - $k )
        $k = $n - $k;

    // Calculate value of
    // [n * (n-1) *---* (n-k+1)] /
    // [k * (k-1) *----* 1]
    for ($i = 0; $i < $k; ++$i)
    {
        $res *= ($n - $i);
        $res /= ($i + 1);
    }

    return $res;
}

    // Driver Code
    $n = 8;
    $k = 2;
    echo " Value of C ($n, $k) is ",
             binomialCoeff($n, $k);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// Program to calculate C(n, k)

// Returns value of Binomial Coefficient C(n, k)
function binomialCoeff(n, k)
{
    let res = 1;

    // Since C(n, k) = C(n, n-k)
    if (k > n - k)
        k = n - k;

    // Calculate value of
    // [n * (n-1) *---* (n-k+1)] / [k * (k-1) *----* 1]
    for (let i = 0; i < k; ++i) {
        res *= (n - i);
        res /= (i + 1);
    }

    return res;
}

// Driver Code

    let n = 8;
    let k = 2;
    document.write("Value of C(" + n + ", " + k + ") "
                  + "is"
                  + " " + binomialCoeff(n, k));

</script>
```

**输出:**

```
Value of C(8, 2) is 28
```

**复杂度分析:**

*   **时间复杂度:** O(r)。
    一个循环必须从 0 运行到 r。所以，时间复杂度是 O(r)。
*   **辅助空间:** O(1)。
    因为不需要额外的空间。

本文由[aashis Barnwal](https://www.facebook.com/barnwal.aashish)编辑，GeeksforGeeks 团队审核。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。