# 一个数组可以用 0 和 1 填充的方式数，使得没有连续的元素是 1

> 原文:[https://www . geesforgeks . org/number-way-array-can-filled-0s-1s-no-continuous-elements-1/](https://www.geeksforgeeks.org/number-ways-array-can-filled-0s-1s-no-consecutive-elements-1/)

给定一个数字 N，找出构造一个大小为 N 的数组的方法，这样它只包含 1 和 0，但没有两个连续的索引值为 1。

示例:

```
Input  : 2
Output : 3
Explanation:
For n=2, the possible arrays are:
{0, 1} {1, 0} {0, 0}

Input  : 3
Output : 5
Explanation:
For n=3, the possible arrays are:
{0, 0, 0} {1, 0, 0} {0, 1, 0} {0, 0, 1} {1, 0, 1} 
```

**天真方法:**
基本的蛮力方法是构造所有可能的方式，使数组可以用 1 和 0 填充，然后检查数组中是否有任何两个连续的 1 如果有，不要计算这些数组。
由于每个元素有 2 个可能值，1 和 0，并且总共有 n 个元素，所以没有任何限制的数组总数将是指数级的，即 2 <sup>n</sup> 。

**高效方法:**
如果我们稍微仔细观察，我们可以注意到在输入和输出中有一种模式正在形成。
对于 **n = 1** ，路数为 **2** 即{0}，{1}
对于 **n = 2** ，路数为**3**T13】同样地，
对于 **n = 3** 路数为**5**T19】对于 **n = 4** 路数为 **8 【T23**

设 T()是给出大小为 n 的数组可以填充的次数的函数，那么我们得到以下递推关系

> T(n) = T(n-1) + T(n-2)

而这就是 [**斐波那契数列<**](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/) 的递推关系。
因此，任意 n 的输出等于斐波那契数列从 1 开始的第 **(n+2) <sup>个</sup>项**。
即 1 1 2 3 5 8 11……
所以现在我们只需要计算直到第(n+2) <sup>个</sup>元素的斐波那契数列，这就是答案。

**时间复杂度为 O(n)**

## C++

```
// C++ implementation of the
// above approach
#include <iostream>
using namespace std;

    // The total number of ways
    // is equal to the (n+2)th
    // Fibonacci term, hence we
    // only need to find that.
    int nth_term(int n)
    {
        int a = 1, b = 1, c = 1;

        // Construct fibonacci upto
        // (n+2)th term the first
        // two terms being 1 and 1
        for (int i = 0; i < n; i++)
        {
            c = a + b;
            a = b;
            b = c;
        }

        return c;
    }

    // Driver Code
    int main()
    {

        // Take input n
        int n = 10;
        int c = nth_term(n);

        // printing output
        cout << c;
    }

// This code is contributed by Sumit Sudhakar.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
class Main
{

    // The total number of ways
    // is equal to the (n+2)th
    // Fibonacci term, hence we
    // only need to find that.
    public static int nth_term(int n)
    {
        int a = 1, b = 1, c = 1;

        // Construct fibonacci upto
        // (n+2)th term the first
        // two terms being 1 and 1
        for (int i = 0; i < n; i++)
        {
            c = a + b;
            a = b;
            b = c;
        }

        return c;
    }

    // Driver program
    public static void main(String[] args)
    {
        // Take input n
        int n = 10;
        int c = nth_term(n);

        // printing output
        System.out.println(c);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# The total number of ways
# is equal to the (n+2)th
# Fibonacci term, hence we
# only need to find that.
def nth_term(n) :

    a = 1
    b = 1
    c = 1

    # Construct fibonacci upto
    # (n+2)th term the first
    # two terms being 1 and 1
    for i in range(0, n) :
        c = a + b
        a = b
        b = c
    return c

# Driver Code

# Take input n
n = 10
c = nth_term(n)

# printing output
print (c)
# This code is contributed by
# Manish Shaw (manishshaw1)
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG {

    // The total number of ways
    // is equal to the (n+2)th
    // Fibonacci term, hence we
    // only need to find that.
    static int nth_term(int n)
    {
        int a = 1, b = 1, c = 1;

        // Construct fibonacci upto
        // (n+2)th term the first
        // two terms being 1 and 1
        for (int i = 0; i < n; i++)
        {
            c = a + b;
            a = b;
            b = c;
        }

        return c;
    }

    // Driver Code
    public static void Main()
    {

        // Take input n
        int n = 10;
        int c = nth_term(n);

        // printing output
        Console.WriteLine(c);

    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the
// above approach

    // The total number of ways
    // is equal to the (n+2)th
    // Fibonacci term, hence we
    // only need to find that.
    function nth_term($n)
    {
        $a = 1; $b = 1; $c = 1;

        // Construct fibonacci upto
        // (n+2)th term the first
        // two terms being 1 and 1
        for ($i = 0; $i < $n; $i++)
        {
            $c = $a + $b;
            $a = $b;
            $b = $c;
        }

        return $c;
    }

        // Driver Code

        // Take input n
        $n = 10;
        $c = nth_term($n);

        // printing output
        echo $c;

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the
// above approach

// The total number of ways
// is equal to the (n+2)th
// Fibonacci term, hence we
// only need to find that.
function nth_term(n)
{
    let a = 1, b = 1, c = 1;

    // Construct fibonacci upto
    // (n+2)th term the first
    // two terms being 1 and 1
    for(let i = 0; i < n; i++)
    {
        c = a + b;
        a = b;
        b = c;
    }
    return c;
}

// Driver code

// Take input n
let n = 10;
let c = nth_term(n);

// Printing output
document.write(c);

// This code is contributed by rameshtravel07

</script>
```

**输出:**

```
144
```

我们可以进一步优化上述解，使之在 O(Log n)中工作，利用矩阵求幂解求第 n 个斐波那契数(斐波那契数见[程序方法 4、5、6)。](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)