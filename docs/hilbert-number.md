# 希尔伯特数

> 原文:[https://www.geeksforgeeks.org/hilbert-number/](https://www.geeksforgeeks.org/hilbert-number/)

给定一个正整数 n，任务是打印*n<sup>th</sup>T3**希尔伯特数**。
[**希尔伯特数**](https://en.wikipedia.org/wiki/Hilbert_number) **:** 在数学中，A *希尔伯特数*是形式为 **4*n + 1** 的正整数，其中 n 为非负整数。
前几个希尔伯特数是–* 

> 1、5、9、13、17、21、25、29、33、37、41、45、49、53、57、61、65、69、73、77、81、85、89、93、97

**例:**

```
Input : 5
Output: 21 ( i.e 4*5 + 1 ) 

Input : 9
Output: 37 (i.e 4*9 + 1 )
```

**接近** :

*   序列的第 n 个希尔伯特数可以通过将 n 的值放入公式 **4*n + 1** 中得到。

以下是上述思路的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to find
// nth hilbert Number

#include <bits/stdc++.h>
using namespace std;

// Utility function to return
// Nth Hilbert Number
long nthHilbertNumber(int n)
{

    return 4 * (n - 1) + 1;
}

// Driver code
int main()
{

    int n = 5;

    cout << nthHilbertNumber(n);

    return 0;
}
```

## Java 语言（一种计算机语言，尤用于创建网站）

```
// JAVA program to find
// nth hilbert Number

class GFG {
    // Utility function to return
    // Nth Hilbert Number
    static long nthHilbertNumber(int n)
    {

        return 4 * (n - 1) + 1;
    }

    // Driver code
    public static void main(String[] args)
    {

        int n = 5;

        System.out.println(nthHilbertNumber(n));
    }
}
```

## 计算机编程语言

```
# Python3 program to find
# nth hilbert Number

# Utility function to return
# Nth Hilbert Number
def nthHilbertNumber( n):

    return 4*(n-1) + 1

# Driver code

n = 5

print(nthHilbertNumber(n))
```

## C#

```
// C# program to find
// nth hilbert Number

using System;
class GFG {
    // Utility function to return
    // Nth Hilbert Number
    static long nthHilbertNumber(int n)
    {

        return 4 * (n - 1) + 1;
    }

    // Driver code
    public static void Main()
    {

        int n = 5;

        Console.WriteLine(nthHilbertNumber(n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Python3 program to find
// nth hilbert Number

// Utility function to return
// Nth Hilbert Number
function nthHilbertNumber($n)
{

    return 4*($n-1) + 1;

}

// Driver code

$n=5;

echo nthHilbertNumber($n);

?>
```

## java 描述语言

```
<script>

// Javascript program to find
// nth hilbert Number

// Utility function to return
// Nth Hilbert Number
function nthHilbertNumber(n)
{

    return 4 * (n - 1) + 1;
}

// Driver code
var n = 5;
document.write( nthHilbertNumber(n));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
17
```