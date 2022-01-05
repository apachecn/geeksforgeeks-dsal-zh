# 求数列 9，45，243，1377 的第 n 项

> 原文:[https://www . geesforgeks . org/find-the-n-term-of-series-9-45-2431377/](https://www.geeksforgeeks.org/find-the-nth-term-of-the-series-9-45-2431377/)

给定一个整数 **N** ，任务是打印系列 **9、45、243、1377、8019、……**
**的 **N <sup>第</sup>** 项示例:**

> **输入:** N = 3
> **输出:** 243
> **输入:** N = 5
> **输出:** 8019

**方法:**让 **N <sup>第</sup>T5】项为**A<sub>N</sub>T9】，通过观察系列:
我们可以很容易的得到 **N <sup>第</sup>T13】项******

> 9、45、243、1377、8019、……<sup>1、</sup> + 2、 <sup>1、</sup>* 3、 <sup>1、</sup>、<sup>2、</sup> + 2、 <sup>2、</sup> (1)<sup>n</sup>+2<sup>n</sup>)* 3<sup>n</sup>
> so，**a<sub>n</sub>=(1<sup>n</sup>+2)**

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the nth term of the given series
long nthterm(int n)
{

    // nth term
    int An = (pow(1, n) + pow(2, n)) * pow(3, n);

    return An;
}

// Driver code
int main()
{
    int n = 3;

    cout << nthterm(n);

    return 0;
}
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function to return the nth term of the given series
def nthterm(n):

    # nth term
    An = (1**n + 2**n) * (3**n)

    return An;

# Driver code
n = 3
print(nthterm(n))
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
import java.lang.*;
import java.io.*;

public class GFG {

    // Function to return the nth term of the given series
    static int nthTerm(int n)
    {
        int An
            = ((int)Math.pow(1, n) + (int)Math.pow(2, n))
              * (int)Math.pow(3, n);

        return An;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 3;
        System.out.println(nthTerm(n));
    }
}
```

## C#

```
// C# implementation of the approach
using System;
public class GFG {

    // Function to return the nth term of the given series
    static int nthTerm(int n)
    {

        int An
            = ((int)Math.Pow(1, n) + (int)Math.Pow(2, n))
              * (int)Math.Pow(3, n);

        return An;
    }

    // Driver code
    public static void Main()
    {
        int n = 3;
        Console.WriteLine(nthTerm(n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the nth term of the given series
function nthterm($n)
{

    $An = (pow(1, $n) + pow(2, $n)) * pow(3, $n);

    // nth term of the given series
    return $An;

}

// Driver code
$n = 3;
echo nthterm($n);
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the nth term of the given series
function nthterm(n)
{

    // nth term
    let An = (Math.pow(1, n) + Math.pow(2, n)) * Math.pow(3, n);

    return An;
}

// Driver code
let n = 3;

document.write(nthterm(n));

// This code is contributed by subhammahato348.
</script>
```

**Output:** 

```
243
```