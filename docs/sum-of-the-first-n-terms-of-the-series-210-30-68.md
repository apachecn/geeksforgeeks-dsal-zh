# 数列 2，10，30，68，…的前 N 项之和。

> 原文:[https://www . geesforgeks . org/系列第一批 n 项之和-210-30-68/](https://www.geeksforgeeks.org/sum-of-the-first-n-terms-of-the-series-210-30-68/)

给定一个数字 N，任务是找出下面系列的前 N 项之和:

> Sn = 2 + 10 + 30 + 68 + …最多 n 项

**例:**

```
Input: N = 2
Output: 12
2 + 10
= 12

Input: N = 4 
Output: 40
2 + 10 + 30 + 68
= 110
```

**方法:**让第 n 项用 tn 表示。
这个问题很容易通过将每个术语拆分如下来解决:

```
Sn = 2 + 10 + 30 + 68 + ......
Sn = (1+1^3) + (2+2^3) + (3+3^3) + (4+4^3) +......
Sn = (1 + 2 + 3 + 4 + ...unto n terms) + (1^3 + 2^3 + 3^3 + 4^3 + ...upto n terms)
```

我们观察到锡可以分解成两个系列的总和。
因此，前 n 项之和如下所示:

```
Sn = (1 + 2 + 3 + 4 + ...unto n terms) + (1^3 + 2^3 + 3^3 + 4^3 + ...upto n terms)
Sn = n*(n + 1)/2 + (n*(n + 1)/2)^2
```

**以下是上述方法的实施:**

## C++

```
// C++ program to find sum of first n terms
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the sum
int calculateSum(int n)
{

    return n * (n + 1) / 2
           + pow((n * (n + 1) / 2), 2);
}

// Driver code
int main()
{
    // number of terms to be
    // included in the sum
    int n = 3;

    // find the Sum
    cout << "Sum = " << calculateSum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of first n terms

public class GFG {

    // Function to calculate the sum
    static int calculateSum(int n)
    {

        return n * (n + 1) / 2 
               + (int)Math.pow((n * (n + 1) / 2), 2);
    }

    // Driver code
    public static void main(String args[])
    {
        // number of terms to be
        // included in the sum
        int n = 3;

        // find the Sum
        System.out.println("Sum = "+ calculateSum(n));
    }
    // This Code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python program to find sum
# of first n terms

# Function to calculate the sum
def calculateSum(n):
    return (n * (n + 1) // 2 +
        pow((n * (n + 1) // 2), 2))

# Driver code

# number of terms to be
# included in the sum
n = 3

# find the Sum
print("Sum = ", calculateSum(n))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to find sum of first n terms
using System;
class gfg
{
    // Function to calculate the sum
    public void calculateSum(int n)
    {
        double r = (n * (n + 1) / 2 +
                Math.Pow((n * (n + 1) / 2), 2));
        Console.WriteLine("Sum = " + r);
    }

    // Driver code
    public static int Main()
    {
        gfg g = new gfg();

        // number of terms to be
        // included in the sum
        int n = 3;

        // find the Sum
        g.calculateSum(n);
        Console.Read();
        return 0;
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum
// of first n terms

// Function to calculate the sum
function calculateSum($n)
{
    return $n * ($n + 1) / 2 +
      pow(($n * ($n + 1) / 2), 2);
}

// Driver code

// number of terms to be
// included in the sum
$n = 3;

// find the Sum
echo "Sum = " , calculateSum($n);

// This code is contributed
// by anuj_67
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum of first n terms

// Function to calculate the sum
function calculateSum(n)
{

    return n * (n + 1) / 2
        + Math.pow((n * (n + 1) / 2), 2);
}

// Driver code

    // number of terms to be
    // included in the sum
    let n = 3;

    // find the Sum
    document.write("Sum = " + calculateSum(n));

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
Sum = 42
```