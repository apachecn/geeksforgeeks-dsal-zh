# 求级数的和？3 + ?12 +………最新条款

> 原文:[https://www . geesforgeks . org/find-系列之和-% E2 % 88% 9 a3-% E2 % 88% 9a 12-up-n-terms/](https://www.geeksforgeeks.org/find-sum-of-the-series-%e2%88%9a3-%e2%88%9a12-upto-n-terms/)

给定一个数 n，任务是求这个级数前 n 项的和。以下是该系列:

![$\sqrt{3}+\sqrt{12}+\sqrt{27}+\sqrt{48}+\sqrt{75}+\cdots$   ](img/7a20948c970ed47e5c497f207919e88c.png "Rendered by QuickLaTeX.com")

**例:**

```
Input: n = 10
Output: 95.2628

Input: n = 5
Output: 25.9808
```

这个系列可以看作是-

![$1\sqrt{3}+2\sqrt{3}+3\sqrt{3}+4\sqrt{3}+5\sqrt{3}+\cdots$ Now, take $\sqrt{3} $ as common, we get- $\sqrt{3}\left[1+2+3+4+5+\cdots\right]$ $sum=\sqrt{3}*\left(\frac{n*(n+1)}{2}\right)$   ](img/6193e85a652c4ffc4fa23c5510ae1b00.png "Rendered by QuickLaTeX.com")

**下面是需要的实现:**

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to find the sum
double findSum(ll n)
{

    // Apply AP formula
    return sqrt(3) * (n * (n + 1) / 2);
}
// Driver code
int main()
{
    // number of terms
    ll n = 10;

    cout << findSum(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// above approach
import java.io.*;

class GFG
{

// Function to find the sum
static double findSum(long n)
{
    // Apply AP formula
    return Math.sqrt(3) * (n *
                    (n + 1) / 2);
}
// Driver code
public static void main (String[] args)
{
    // number of terms
    long n = 10;

    System.out.println( findSum(n));
}
}

// This code is contributed
// by inder_verma..
```

## 蟒蛇 3

```
# Python3 implementation of above approach

#Function to find the sum
import math
def findSum(n):
    # Apply AP formula
    return math.sqrt(3) * (n * (n + 1) / 2)

# Driver code
# number of terms
if __name__=='__main__':
    n = 10
    print(findSum(n))

# This code is contributed by sahilshelangia
```

## C#

```
// C# implementation of
// above approach
using System;

class GFG
{

// Function to find the sum
static double findSum(long n)
{
    // Apply AP formula
    return Math.Sqrt(3) * (n *
                    (n + 1) / 2);
}
// Driver code
public static void Main ()
{
    // number of terms
    long n = 10;

    Console.WriteLine( findSum(n));
}
}

// This code is contributed
// by inder_verma..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to find the sum
function findSum($n)
{

    // Apply AP formula
    return sqrt(3) * ($n * ($n + 1) / 2);
}

// Driver code

// number of terms
$n = 10;

echo findSum($n);

// This code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>
// Javascript implementation of
// above approach

    // Function to find the sum
    function findSum( n)
    {

        // Apply AP formula
        return Math.sqrt(3) * (n * (n + 1) / 2);
    }

    // Driver code

    // number of terms
    let n = 10;

    document.write(findSum(n).toFixed(4));

// This code is contributed by 29AjayKumar 
</script>
```

**Output:** 

```
95.2628
```