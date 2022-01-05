# 1 到 N 之间可被 3 或 4 整除的数的和

> 原文:[https://www . geesforgeks . org/从 1 到 n 的可被 3 或 4 整除的数字总和/](https://www.geeksforgeeks.org/sum-of-numbers-from-1-to-n-which-are-divisible-by-3-or-4/)

给定一个数 N，任务是找出从 1 到 N 所有可被 3 或 4 整除的数的和。
**例** :

```
Input : N = 5
Output : 7
sum = 3 + 4

Input : N = 12 
Output : 42
sum = 3 + 4 + 6 + 8 + 9 + 12
```

**方法:**要解决问题，请按照以下步骤操作:

1.  找出能被 3 整除的数之和，用 S1 表示。
2.  求可被 4 整除的数的和，用 S2 表示。
3.  找出能被 12(3*4)整除的数之和，用 S3 表示。
4.  最终答案将是**S1+S2-S3**。

为了求和，我们可以用 A.P .的通式，即:

```
Sn = (n/2) * {2*a + (n-1)*d}

Where,
n -> total number of terms
a -> first term
d -> common difference
```

**对于 S1:** 能被 3 整除的总数将是 N/3，数列将是 **3，6，9，12，…。**

```
Hence, 
S1 = ((N/3)/2) * (2 * 3 + (N/3 - 1) * 3)
```

**对于 S2:** 能被 4 整除到 N 的总数是 N/4，数列是 **4，8，12，16，…..**。

```
Hence, 
S2 = ((N/4)/2) * (2 * 4 + (N/4 - 1) * 4)
```

**对于 S3:** 能被 12 整除到 N 的总数是 N/12。

```
Hence, 
S3 = ((N/12)/2) * (2 * 12 + (N/12 - 1) * 12)
```

因此，结果将是:

```
S = S1 + S2 - S3
```

以下是上述方法的实现:

## C++

```
// C++ program to find sum of numbers from 1 to N
// which are divisible by 3 or 4
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the sum
// of numbers divisible by 3 or 4
int sum(int N)
{
    int S1, S2, S3;

    S1 = ((N / 3)) * (2 * 3 + (N / 3 - 1) * 3) / 2;
    S2 = ((N / 4)) * (2 * 4 + (N / 4 - 1) * 4) / 2;
    S3 = ((N / 12)) * (2 * 12 + (N / 12 - 1) * 12) / 2;

    return S1 + S2 - S3;
}

// Driver code
int main()
{
    int N = 20;

    cout << sum(12);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of numbers from 1 to N
// which are divisible by 3 or 4
class GFG{

// Function to calculate the sum
// of numbers divisible by 3 or 4
static int sum(int N)
{
    int S1, S2, S3;

    S1 = ((N / 3)) * (2 * 3 + (N / 3 - 1) * 3) / 2;
    S2 = ((N / 4)) * (2 * 4 + (N / 4 - 1) * 4) / 2;
    S3 = ((N / 12)) * (2 * 12 + (N / 12 - 1) * 12) / 2;

    return S1 + S2 - S3;
}

// Driver code
 public static void main (String[] args) {
    int N = 20;

    System.out.print(sum(12));
}

}
```

## 蟒蛇 3

```
# Python3 program to find sum of numbers
# from 1 to N
# which are divisible by 3 or 4

# Function to calculate the sum
# of numbers divisible by 3 or 4
def sum(N):

    global S1,S2,S3

    S1 = (((N // 3)) *
         (2 * 3 + (N //3 - 1) * 3) //2)
    S2 = (((N // 4)) *
         (2 * 4 + (N // 4 - 1) * 4) // 2)
    S3 = (((N // 12)) *
         (2 * 12 + (N // 12 - 1) * 12) // 2)

    return int(S1 + S2 - S3)

if __name__=='__main__':
    N = 12
    print(sum(N))

# This code is contributed by Shrikant13
```

## C#

```
// C# program to find sum of
// numbers from 1 to N which
// are divisible by 3 or 4
using System;

class GFG
{

// Function to calculate the sum
// of numbers divisible by 3 or 4
static int sum(int N)
{
    int S1, S2, S3;

    S1 = ((N / 3)) * (2 * 3 +
          (N / 3 - 1) * 3) / 2;
    S2 = ((N / 4)) * (2 * 4 +
          (N / 4 - 1) * 4) / 2;
    S3 = ((N / 12)) * (2 * 12 +
          (N / 12 - 1) * 12) / 2;

    return S1 + S2 - S3;
}

// Driver code
public static void Main ()
{
    int N = 20;

    Console.WriteLine(sum(12));
}
}

// This code is contributed
// by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of
// numbers from 1 to N which
// are divisible by 3 or 4

// Function to calculate the sum
// of numbers divisible by 3 or 4
function sum($N)
{
    $S1; $S2; $S3;

    $S1 = (($N / 3)) * (2 * 3 +
           ($N / 3 - 1) * 3) / 2;
    $S2 = (($N / 4)) * (2 * 4 +
           ($N / 4 - 1) * 4) / 2;
    $S3 = (($N / 12)) * (2 * 12 +
           ($N / 12 - 1) * 12) / 2;

    return $S1 + $S2 - $S3;
}

// Driver Code
$N = 20;

echo sum(12);

// This code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum of numbers from 1 to N
// which are divisible by 3 or 4

// Function to calculate the sum
// of numbers divisible by 3 or 4
function sum(N)
{
    var S1, S2, S3;

    S1 = ((N / 3)) * (2 * 3 + (N / 3 - 1) * 3) / 2;
    S2 = ((N / 4)) * (2 * 4 + (N / 4 - 1) * 4) / 2;
    S3 = ((N / 12)) * (2 * 12 + (N / 12 - 1) * 12) / 2;

    return S1 + S2 - S3;
}

// Driver code
var N = 20;
document.write( sum(12));

</script>
```

**Output:** 

```
42
```