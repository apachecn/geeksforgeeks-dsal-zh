# 求数列 0，8，64，216，512，.。。

> 原文:[https://www . geesforgeks . org/find-the-n-term-of-series-0-8-64-216-512/](https://www.geeksforgeeks.org/find-the-nth-term-of-the-series-0-8-64-216-512/)

给定一个整数 **N** ，任务是找到以下系列的 **N <sup>第</sup>T5】项:** 

> 0, 8, 64, 216, 512, 1000, 1728, .。。

**例:**

> **输入:** N = 6
> **输出:** 1000
> **输入:** N = 5
> **输出:** 512

**进场:**

*   给定系列 **0、8、64、216、512、1000、1728、…** 也可以写成 **0 * (0 <sup>2</sup> )、2 * (2 <sup>2</sup> )、4 * (4 <sup>2</sup> )、6 * (6 <sup>2</sup> )、8 * (8 <sup>2</sup> )、10 * (10 <sup>2</sup> )、…**
*   观察 **0、2、4、6、10、…** 在 **AP** 中，使用公式**项= a<sub>1</sub>+(n–1)* d**可以找到本系列的**第 n 项**，其中**a<sub>1</sub>T13】为**第一项**， **n** 为**项位置【T19****
*   要得到原系列中的术语，**术语=术语*(术语 <sup>2</sup> )** 即**术语 <sup>3</sup>** 。
*   最后打印**术语**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the nth term of the given series
long term(int n)
{
    // Common difference
    int d = 2;

    // First term
    int a1 = 0;

    // nth term
    int An = a1 + (n - 1) * d;

    // nth term of the given series
    An = pow(An, 3);
    return An;
}

// Driver code
int main()
{
    int n = 5;

    cout << term(n);

    return 0;
}
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

        // Common difference and first term
        int d = 2, a1 = 0;

        // nth term
        int An = a1 + (n - 1) * d;

        // nth term of the given series
        return (int)Math.pow(An, 3);
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 5;
        System.out.println(nthTerm(n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the nth term of the given series
def term(n):

    # Common difference
    d = 2

    # First term
    a1 = 0

    # nth term
    An = a1 +(n-1)*d

    # nth term of the given series
    An = An**3
    return An;

# Driver code
n = 5
print(term(n))
```

## C#

```
// C# implementation of the approach
using System;
public class GFG {

    // Function to return the nth term of the given series
    static int nthTerm(int n)
    {

        // Common difference and first term
        int d = 2, a1 = 0;

        // nth term
        int An = a1 + (n - 1) * d;

        // nth term of the given series
        return (int)Math.Pow(An, 3);
    }

    // Driver code
    public static void Main()
    {
        int n = 5;
        Console. WriteLine(nthTerm(n));
    }
}
// This code is contributed by Mutual singh.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the nth term of the given series
function term($n) 
{ 

    // Common difference
    $d = 2;

    // First term
    $a1 = 0;

    // nth term
    $An=$a1+($n-1)*$d;

    // nth term of the given series
    return pow($An, 3);

} 

// Driver code 
$n = 5;
echo term($n); 
?>
```

## java 描述语言

```
<script>

// javascript implementation of the approach

// Function to return the nth term of the given series
function term(n) 
{ 

    // Common difference
    let d = 2;

    // First term
    let a1 = 0;

    // nth term
    An=a1+(n-1)*d;

    // nth term of the given series
    return Math.pow(An, 3);

} 

// Driver code 
let n = 5;
document.write( term(n)); 

// This code is contributed by sravan kumar

</script>
```

**Output:** 

```
512
```