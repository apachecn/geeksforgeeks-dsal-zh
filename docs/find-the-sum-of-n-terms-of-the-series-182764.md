# 求数列 1，8，27，64 的 n 项之和。

> 原文:[https://www . geesforgeks . org/find-the-sum-n-terms-of-series-182764/](https://www.geeksforgeeks.org/find-the-sum-of-n-terms-of-the-series-182764/)

给定一个数列，任务是找出下面数列的和，最多 n 项:

> 1, 8, 27, 64, …

**例:**

```
Input: N = 2
Output: 9
9 = (2*(2+1)/2)^2

Input: N = 4
Output: 100
100 = (4*(4+1)/2)^2
```

**方法:**我们可以用下面的公式来解决这个问题:

```
    Sn = 1 + 8 + 27 + 64 + .........up to n terms
    Sn = (n*(n+1)/2)^2
```

以下是上述方法的实现:

## C++

```
// C++ program to find the sum of n terms
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the sum
int calculateSum(int n)
{

    // Return total sum
    return pow(n * (n + 1) / 2, 2);
}

// Driver code
int main()
{

    int n = 4;
    cout << calculateSum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of n terms
import java.io.*;

class GFG {

// Function to calculate the sum
static int calculateSum(int n)
{

    // Return total sum
    return (int)Math.pow(n * (n + 1) / 2, 2);
}

// Driver code

    public static void main (String[] args) {
        int n = 4;
    System.out.println( calculateSum(n));

    }
}
// This code is contributed by inder_verma..
```

## 蟒蛇 3

```
# Python3 program to find the
# sum of n terms

#Function to calculate the sum
def calculateSum(n):

    #return total sum
    return (n * (n + 1) / 2)**2

#Driver code
if __name__=='__main__':
    n = 4
    print(calculateSum(n))

#this code is contributed by Shashank_Sharma
```

## C#

```
// C# program to find the sum of n terms
using System;

class GFG
{

// Function ot calculate the sum
static int calculateSum(int n)
{

    // Return total sum
    return (int)Math.Pow(n * (n + 1) / 2, 2);
}

// Driver code
public static void Main ()
{
    int n = 4;
    Console.WriteLine(calculateSum(n));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// the sum of n terms

// Function to calculate the sum
function calculateSum($n)
{
    // Return total sum
    return pow($n * ($n + 1) / 2 , 2);
}

// Driver code
$n = 4;
echo calculateSum($n);

// This code is contributed
// by ANKITRAI1
?>
```

## java 描述语言

```
<script>

// javascript program to find the sum of n terms

// Function to calculate the sum
function calculateSum(n)
{

    // Return total sum
    return parseInt(Math.pow(n * (n + 1) / 2, 2));
}

// Driver code
 var n = 4;
document.write( calculateSum(n));

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
100
```