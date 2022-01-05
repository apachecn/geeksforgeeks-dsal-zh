# 可被 X 或 Y 整除的前 N 个自然数之和

> 原文:[https://www . geeksforgeeks . org/可被 x 或 y 整除的第一 n 个自然数之和/](https://www.geeksforgeeks.org/sum-of-first-n-natural-numbers-which-are-divisible-by-x-or-y/)

给定一个数字 **N** 。给定两个数字 **X** 和 **Y** ，任务是找出从 1 到 N 的所有可被 X 或 Y 整除的数字的和。
**示例** :

```
Input : N = 20
Output : 98

Input : N = 14 
Output : 45
```

**逼近**:解决问题，按照下面的步骤:
- >求 X 到 n 整除的数的和，用 S1 表示。
- >求可被 Y 整除的数的和，用 S2 表示。
- >求可被 X 和 Y (X*Y)整除的数的和，用 S3 表示。
- >最终答案为**S1+S2-S3**。
为了求和，我们可以用 A.P .的通式，即:

```
Sn = (n/2) * {2*a + (n-1)*d}
```

**对于 S1** :能被 X 整除的总数为 N/X，总和为:

```
Hence, 
S1 = ((N/X)/2) * (2 * X + (N/X - 1) * X)
```

**对于 S2** :可被 Y 整除的总数为 N/Y，总和为:

```
Hence, 
S2 = ((N/Y)/2) * (2 * Y + (N/Y - 1) * Y)
```

**对于 S3** :能被 X 和 Y 整除的总数为 N/(X*Y)，和为:

```
Hence, 
S2 = ((N/(X*Y))/2) * (2 * Y + (N/(X*Y) - 1) * (X*Y))
```

因此，结果将是:

```
S = S1 + S2 - S3
```

以下是上述方法的实现:

## C++

```
// C++ program to find sum of numbers from
// 1 to N which are divisible by X or Y
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the sum
// of numbers divisible by X or Y
int sum(int N, int X, int Y)
{
    int S1, S2, S3;

    S1 = ((N / X)) * (2 * X + (N / X - 1) * X) / 2;
    S2 = ((N / Y)) * (2 * Y + (N / Y - 1) * Y) / 2;
    S3 = ((N / (X * Y))) * (2 * (X * Y)
                      + (N / (X * Y) - 1) * (X * Y))/ 2;

    return S1 + S2 - S3;
}

// Driver code
int main()
{
    int N = 14;
    int X = 3, Y = 5;

    cout << sum(N, X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of numbers from
// 1 to N which are divisible by X or Y

public class GFG{

    // Function to calculate the sum
    // of numbers divisible by X or Y
    static int sum(int N, int X, int Y)
    {
        int S1, S2, S3;

        S1 = ((N / X)) * (2 * X + (N / X - 1) * X) / 2;
        S2 = ((N / Y)) * (2 * Y + (N / Y - 1) * Y) / 2;
        S3 = ((N / (X * Y))) * (2 * (X * Y)
                          + (N / (X * Y) - 1) * (X * Y))/ 2;

        return S1 + S2 - S3;
    }

    // Driver code
    public static void main(String []args)
    {
        int N = 14;
        int X = 3, Y = 5;

        System.out.println(sum(N, X, Y));

    }
    // This code is contributed by Ryuga
}
```

## 蟒蛇 3

```
# Python 3 program to find sum of numbers from
# 1 to N which are divisible by X or Y
from math import ceil, floor

# Function to calculate the sum
# of numbers divisible by X or Y
def sum(N, X, Y):
    S1 = floor(floor(N / X) * floor(2 * X +
               floor(N / X - 1) * X) / 2)
    S2 = floor(floor(N / Y)) * floor(2 * Y +
               floor(N / Y - 1) * Y) / 2
    S3 = floor(floor(N / (X * Y))) * floor (2 * (X * Y) +
               floor(N / (X * Y) - 1) * (X * Y))/ 2

    return S1 + S2 - S3

# Driver code
if __name__ == '__main__':
    N = 14
    X = 3
    Y = 5

    print(int(sum(N, X, Y)))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find sum of numbers from
// 1 to N which are divisible by X or Y

using System;
public class GFG{

    // Function to calculate the sum
    // of numbers divisible by X or Y
    static int sum(int N, int X, int Y)
    {
        int S1, S2, S3;

        S1 = ((N / X)) * (2 * X + (N / X - 1) * X) / 2;
        S2 = ((N / Y)) * (2 * Y + (N / Y - 1) * Y) / 2;
        S3 = ((N / (X * Y))) * (2 * (X * Y)
                          + (N / (X * Y) - 1) * (X * Y))/ 2;

        return S1 + S2 - S3;
    }

    // Driver code
    public static void Main()
    {
        int N = 14;
        int X = 3, Y = 5;

        Console.Write(sum(N, X, Y));

    }

}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of numbers from
// 1 to N which are divisible by X or Y
// Function to calculate the sum
// of numbers divisible by X or Y
function sum($N, $X, $Y)
{
    $S1; $S2; $S3;

    $S1 = floor(((int)$N / $X)) * (2 * $X + (int)((int)$N / $X - 1) * $X) / 2;
    $S2 = floor(((int)$N / $Y)) * (2 * $Y + (int)((int)$N / $Y - 1) * $Y) / 2;
    $S3 = floor(((int)$N / ($X * $Y))) * (2 * ($X * $Y)
                    + ((int)$N / ($X * $Y) - 1) * (int)($X * $Y))/ 2;

    return ceil($S1 + ($S2 - $S3));
}

// Driver code
    $N = 14;
    $X = 3;
    $Y = 5;

    echo  sum($N, $X, $Y);

#This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
// javascript program to find sum of numbers from
// 1 to N which are divisible by X or Y

// Function to calculate the sum
// of numbers divisible by X or Y
function sum(N , X , Y)
{
    var S1, S2, S3;

    S1 = (parseInt(N / X)) * (2 * X + parseInt(N / X - 1) * X) / 2;
    S2 = (parseInt(N / Y)) * (2 * Y + parseInt(N / Y - 1) * Y) / 2;
    S3 = (parseInt(N / (X * Y))) * (2 * (X * Y)
                      + parseInt(N / (X * Y) - 1) * (X * Y))/ 2;

    return S1 + S2 - S3;
}

// Driver code
var N = 14;
var X = 3, Y = 5;

document.write(sum(N, X, Y));

// This code is contributed by Princi Singh
</script>
```

**Output:** 

```
45
```

**时间复杂度:** O(1)