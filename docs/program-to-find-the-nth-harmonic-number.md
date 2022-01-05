# 计算第 n 次谐波数的程序

> 原文:[https://www . geesforgeks . org/program-to-find-n 次谐波数/](https://www.geeksforgeeks.org/program-to-find-the-nth-harmonic-number/)

给定一个数 n，任务是找到第 n 个调和数。
让第 n 次谐波数为 H <sub>n</sub> 。
谐波系列如下:

> **h<sub><sub>= 1</sub></sub>**
> **【h】<sub>【2】</sub>= h<sub>【1】</sub>+1/2
> **【h】**
> **。**
> **。**
> **h<sub>= h<sub>【n-1】</sub>+1/n</sub>****

**示例** :

```
Input : N = 5
Output : 2.45

Input : N = 9
Output : 2.71786
```

这个想法是从 H1 穿越，然后连续不断地从 H1 找到 H2，从 H2 找到 H3…..等等。
下面是寻找第 N 次谐波数的程序:

## C++

```
// CPP program to find N-th Harmonic Number

#include <iostream>
using namespace std;

// Function to find N-th Harmonic Number
double nthHarmonic(int N)
{
    // H1 = 1
    float harmonic = 1.00;

    // loop to apply the formula
    // Hn = H1 + H2 + H3 ... + Hn-1 + Hn-1 + 1/n
    for (int i = 2; i <= N; i++) {
        harmonic += (float)1 / i;
    }

    return harmonic;
}

// Driver Code
int main()
{
    int N = 8;

    cout<<nthHarmonic(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find N-th Harmonic Number

import java.io.*;

class GFG {

// Function to find N-th Harmonic Number
static double nthHarmonic(int N)
{
    // H1 = 1
    float harmonic = 1;

    // loop to apply the formula
    // Hn = H1 + H2 + H3 ... + Hn-1 + Hn-1 + 1/n
    for (int i = 2; i <= N; i++) {
        harmonic += (float)1 / i;
    }

    return harmonic;
}

// Driver Code

    public static void main (String[] args) {
            int N = 8;

    System.out.print(nthHarmonic(N));

    }
}
// This code is contributed
// by ajit
```

## 蟒蛇 3

```
# Python3 program to find
# N-th Harmonic Number

# Function to find N-th Harmonic Number
def nthHarmonic(N) :

    # H1 = 1
    harmonic = 1.00

    # loop to apply the formula
    # Hn = H1 + H2 + H3 ... +
    # Hn-1 + Hn-1 + 1/n
    for i in range(2, N + 1) :
        harmonic += 1 / i

    return harmonic

# Driver code    
if __name__ == "__main__" :

    N = 8
    print(round(nthHarmonic(N),5))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find N-th Harmonic Number
using System;

class GFG
{

// Function to find N-th Harmonic Number
static double nthHarmonic(int N)
{
    // H1 = 1
    float harmonic = 1;

    // loop to apply the formula
    // Hn = H1 + H2 + H3 ... +
    // Hn-1 + Hn-1 + 1/n
    for (int i = 2; i <= N; i++)
    {
        harmonic += (float)1 / i;
    }

    return harmonic;
}

// Driver Code
static public void Main ()
{
    int N = 8;

    Console.Write(nthHarmonic(N));
}
}

// This code is contributed
// by Raj
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// N-th Harmonic Number

// Function to find N-th
// Harmonic Number
function nthHarmonic($N)
{
    // H1 = 1
    $harmonic = 1.00;

    // loop to apply the formula
    // Hn = H1 + H2 + H3 ... +
    // Hn-1 + Hn-1 + 1/n
    for ($i = 2; $i <= $N; $i++)
    {
        $harmonic += (float)1 / $i;
    }

    return $harmonic;
}

// Driver Code
$N = 8;
echo nthHarmonic($N);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// N-th Harmonic Number

// Function to find N-th
// Harmonic Number
function nthHarmonic(N)
{
    // H1 = 1
    let harmonic = 1.00;

    // loop to apply the formula
    // Hn = H1 + H2 + H3 ... +
    // Hn-1 + Hn-1 + 1/n
    for (let i = 2; i <= N; i++)
    {
        harmonic += parseFloat(1) / i;
    }

    return harmonic;
}

// Driver Code

let N = 8;
document.write( nthHarmonic(N).toFixed(5));

// This code is contributed by bobby

</script>
```

**Output:** 

```
2.71786
```

**时间复杂度** : O(N)