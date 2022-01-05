# 可被 2 和 7 整除的前 N 个自然数之和

> 原文:[https://www . geesforgeks . org/可被 2 和 7 整除的第 n 个自然数之和/](https://www.geeksforgeeks.org/sum-of-first-n-natural-numbers-which-are-divisible-by-2-and-7/)

给定一个数 N，任务是找出从 1 到 N 所有可被 2 或 7 整除的数的和。
**例** :

```
Input : N = 7
Output : 19
sum = 2 + 4 + 6 + 7

Input : N = 14 
Output : 63
sum = 2 + 4 + 6 + 7 + 8 + 10 + 12 + 14
```

**逼近**:解决问题，按照下面的步骤:
- >求可被 2 整除到 n 的数的和，用 S1 表示。
- >求可被 7 整除的数的和，用 S2 表示。
- >求可被 14(2*7)整除的数的和，用 S3 表示。
- >最终答案将是 S1+S2-S3。
为了求和，我们可以用 A.P .的通式，即:

```
Sn = (n/2) * {2*a + (n-1)*d}
```

对于 S1:能被 2 整除的总数将是 N/2，数列将是 2，4，6，8，…。

```
Hence, 
S1 = ((N/2)/2) * (2 * 2 + (N/2 - 1) * 2)
```

对于 S2:能被 7 整除到 N 的总数是 N/7，数列是 7，14，21，28，…

```
Hence, 
S2 = ((N/7)/2) * (2 * 7 + (N/7 - 1) * 7)
```

对于 S3:能被 14 整除的总数将是 N/14。

```
Hence, 
S3 = ((N/14)/2) * (2 * 14 + (N/14 - 1) * 14)
```

因此，结果将是:

```
S = S1 + S2 - S3
```

以下是上述方法的实现:

## C++

```
// C++ program to find sum of numbers from 1 to N
// which are divisible by 2 or 7
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the sum
// of numbers divisible by 2 or 7
int sum(int N)
{
    int S1, S2, S3;

    S1 = ((N / 2)) * (2 * 2 + (N / 2 - 1) * 2) / 2;
    S2 = ((N / 7)) * (2 * 7 + (N / 7 - 1) * 7) / 2;
    S3 = ((N / 14)) * (2 * 14 + (N / 14 - 1) * 14) / 2;

    return S1 + S2 - S3;
}

// Driver code
int main()
{
    int N = 20;

    cout << sum(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program to find sum of
// numbers from 1 to N which
// are divisible by 2 or 7

import java.io.*;

class GFG {
// Function to calculate the sum
// of numbers divisible by 2 or 7
public static int sum(int N)
{
    int S1, S2, S3;

    S1 = ((N / 2)) * (2 * 2 +
        (N / 2 - 1) * 2) / 2;
    S2 = ((N / 7)) * (2 * 7 +
        (N / 7 - 1) * 7) / 2;
    S3 = ((N / 14)) * (2 * 14 +
        (N / 14 - 1) * 14) / 2;

    return S1 + S2 - S3;
}

// Driver code
    public static void main (String[] args) {

    int N = 20;
    System.out.println( sum(N));
    }
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# Python3 implementation of
# above approach

# Function to calculate the sum
# of numbers divisible by 2 or 7
def sum(N):

    S1 = ((N // 2)) * (2 * 2 + (N // 2 - 1) * 2) // 2
    S2 = ((N // 7)) * (2 * 7 + (N // 7 - 1) * 7) // 2
    S3 = ((N // 14)) * (2 * 14 + (N // 14 - 1) * 14) // 2

    return S1 + S2 - S3

# Driver code
if __name__=='__main__':
    N = 20

    print(sum(N))

# This code is written by
# Sanjit_Prasad
```

## C#

```
// C# program to find sum of
// numbers from 1 to N which
// are divisible by 2 or 7
using System;

class GFG
{
// Function to calculate the sum
// of numbers divisible by 2 or 7
public static int sum(int N)
{
    int S1, S2, S3;

    S1 = ((N / 2)) * (2 * 2 +
          (N / 2 - 1) * 2) / 2;
    S2 = ((N / 7)) * (2 * 7 +
          (N / 7 - 1) * 7) / 2;
    S3 = ((N / 14)) * (2 * 14 +
          (N / 14 - 1) * 14) / 2;

    return S1 + S2 - S3;
}

// Driver code
public static int Main()
{
    int N = 20;
    Console.WriteLine( sum(N));
    return 0;
}
}

// This code is contributed
// by SoumikMondal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of numbers
// from 1 to N which are divisible by 2 or 7

// Function to calculate the sum
// of numbers divisible by 2 or 7
function sum($N)
{
    $S1 = (int)(($N / 2)) * (int)(2 * 2 +
           (int)($N / 2 - 1) * 2) / 2;
    $S2 = (int)(($N / 7)) * (int)(2 * 7 +
           (int)($N / 7 - 1) * 7) / 2;
    $S3 = (int)(($N / 14)) * (int)(2 * 14 +
           (int)($N / 14 - 1) * 14) / 2;

    return ($S1 + $S2) - $S3;
}

// Driver code
$N = 20;

echo sum($N);

// This Code is Contributed by akt_mit
?>
```

## java 描述语言

```
<script>
// javascript  program to find sum of
// numbers from 1 to N which
// are divisible by 2 or 7

// Function to calculate the sum
// of numbers divisible by 2 or 7
function sum(N)
{
    var S1, S2, S3;

    S1 = (((N / 2)) * parseInt(2 * 2 +
        parseInt(N / 2 - 1) * 2) / 2);
    S2 = (parseInt(parseInt(N / 7)) * (2 * 7 +
        parseInt(N / 7 - 1) * 7) / 2);
    S3 = (parseInt(parseInt(N / 14)) * (2 * 14 +
        parseInt(N / 14 - 1) * 14) / 2);

    return S1 + S2 - S3;
}

// Driver code
var N = 20;
document.write( sum(N));

// This code is contributed by shikhasingrajput
</script>
```

**Output:** 

```
117
```