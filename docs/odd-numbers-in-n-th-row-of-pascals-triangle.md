# 帕斯卡三角形第 N 行奇数

> 原文:[https://www . geesforgeks . org/奇数行帕斯卡三角形/](https://www.geeksforgeeks.org/odd-numbers-in-n-th-row-of-pascals-triangle/)

给定 N，帕斯卡三角形的行号(从 0 开始的行)。求帕斯卡三角形第 N 行奇数的计数。
**先决条件:** [帕斯卡三角](https://www.geeksforgeeks.org/pascal-triangle/) | [计算 N 的二进制表示中 1 的个数](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)

**示例:**

```
Input : 11
Output : 8

Input : 20
Output : 4 
```

![](img/0fc4258dc26e2cc028385ebef6a9b1a2.png)

**方法:**看起来答案总是 2 的幂。事实上，存在以下定理:
**定理:**帕斯卡三角形第 N 行奇数项的个数在 N 的二进制展开中是 2 提升到 1 的个数
例:既然 83 = 64 + 16 + 2 + 1 有二进制展开(1010011)，那么第 83 行就有幂(2，4) = 16 个奇数。

**以下是上述方法的实现:**

## C++

```

// CPP code to find the count of odd numbers
// in n-th row of Pascal's Triangle
#include <bits/stdc++.h>    
using namespace std ;

/* Function to get no of set
   bits in binary representation
   of positive integer n */
int countSetBits(int n)
{
    unsigned int count = 0;
    while (n)
    {
        count += n & 1;
        n >>= 1;
    }

    return count;
}

int countOfOddsPascal(int n)
{
    // Count number of 1's in binary
    // representation of n.
    int c = countSetBits(n);

    // Number of odd numbers in n-th
    // row is 2 raised to power the count.
    return pow(2, c);
}

// Driver code
int main()
{
    int n = 20;   
    cout << countOfOddsPascal(n) ;   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the count of odd
// numbers in n-th row of Pascal's
// Triangle
import java.io.*;

class GFG {

    /* Function to get no of set
    bits in binary representation
    of positive integer n */
    static int countSetBits(int n)
    {
        long count = 0;
        while (n > 0)
        {
            count += n & 1;
            n >>= 1;
        }

        return (int)count;
    }

    static int countOfOddsPascal(int n)
    {

        // Count number of 1's in binary
        // representation of n.
        int c = countSetBits(n);

        // Number of odd numbers in n-th
        // row is 2 raised to power the
        // count.
        return (int)Math.pow(2, c);
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 20;
        System.out.println(
                     countOfOddsPascal(n));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python code to find the count of
# odd numbers in n-th row of
# Pascal's Triangle

# Function to get no of set
# bits in binary representation
# of positive integer n
def countSetBits(n):
    count =0
    while n:
        count += n & 1
        n >>= 1

    return count

def countOfOddPascal(n):

    # Count number of 1's in binary
    # representation of n.
    c = countSetBits(n)

    # Number of odd numbers in n-th
    # row is 2 raised to power the count.
    return pow(2, c)

# Driver Program
n = 20
print(countOfOddPascal(n))

# This code is contributed by Shrikant13
```

## C#

```
// C# code to find the count of odd numbers
// in n-th row of Pascal's Triangle
using System;

class GFG {

    /* Function to get no of set
    bits in binary representation
    of positive integer n */
    static int countSetBits(int n)
    {
        int count = 0;
        while (n > 0)
        {
            count += n & 1;
            n >>= 1;
        }

        return count;
    }

    static int countOfOddsPascal(int n)
    {
        // Count number of 1's in binary
        // representation of n.
        int c = countSetBits(n);

        // Number of odd numbers in n-th
        // row is 2 raised to power the
        // count.
        return (int)Math.Pow(2, c);
    }

    // Driver code
    public static void Main ()
    {
        int n = 20;
        Console.WriteLine(
                 countOfOddsPascal(n)) ;
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find the
// count of odd numbers
// in n-th row of Pascal's
// Triangle

/* Function to get no of set
   bits in binary representation
   of positive integer n */
function countSetBits($n)
{
    $count = 0;
    while ($n)
    {
        $count += $n & 1;
        $n >>= 1;
    }

    return $count;
}

function countOfOddsPascal($n)
{

    // Count number of 1's in binary
    // representation of n.
    $c = countSetBits($n);

    // Number of odd numbers in n-th
    // row is 2 raised to power the count.
    return pow(2, $c);
}

    // Driver code
    $n = 20;
    echo countOfOddsPascal($n) ;

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>   
    // Javascript code to find the count of odd numbers
    // in n-th row of Pascal's Triangle

    /* Function to get no of set
    bits in binary representation
    of positive integer n */
    function countSetBits(n)
    {
        let count = 0;
        while (n > 0)
        {
            count += n & 1;
            n >>= 1;
        }

        return count;
    }

    function countOfOddsPascal(n)
    {
        // Count number of 1's in binary
        // representation of n.
        let c = countSetBits(n);

        // Number of odd numbers in n-th
        // row is 2 raised to power the
        // count.
        return Math.pow(2, c);
    }

    let n = 20;
    document.write(countOfOddsPascal(n)) ;

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(L)，其中 L 是给定 n 的二进制表示的长度