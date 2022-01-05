# 找到一个数字的最高有效设定位

> 原文:[https://www . geeksforgeeks . org/find-有效位集-位数/](https://www.geeksforgeeks.org/find-significant-set-bit-number/)

给定一个数，找出比给定的 2 的幂的数小的最大数，或者找出最高有效位数。

**例:**

```
Input : 10
Output : 8
Greatest number which is a Power of 2 less than 10 is 8
Binary representation of 10 is 1010
The most significant bit corresponds
to decimal number 8.

Input : 18
Output : 16 
```

一个**简单的解决方案**是一个接一个地将 n 除以 2，直到它变成 0，并在此过程中增加一个计数。这个计数实际上代表了 MSB 的位置。

## c++

```
// Simple CPP program to find MSB number
// for given n.
#include <iostream>
using namespace std;

int setBitNumber(int n)
{
    if (n == 0)
        return 0;

    int msb = 0;
    n = n / 2;
    while (n != 0) {
        n = n / 2;
        msb++;
    }

    return (1 << msb);
}

// Driver code
int main()
{
    int n = 0;
    cout << setBitNumber(n);
    return 0;
}
```

## Java

```
// Simple Java program to find
// MSB number for given n.
import java.io.*;

class GFG {
    static int setBitNumber(int n)
    {
        if (n == 0)
            return 0;

        int msb = 0;
        n = n / 2;

        while (n != 0) {
            n = n / 2;
            msb++;
        }

        return (1 << msb);
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 0;
        System.out.println(setBitNumber(n));
    }
}

// This code is contributed by ajit
```

## python 3

```
# Simple Python3 program
# to find MSB number
# for given n.
def setBitNumber(n):
    if (n == 0):
        return 0;

    msb = 0;
    n = int(n / 2);

    while (n > 0):
        n = int(n / 2);
        msb += 1;

    return (1 << msb);

# Driver code
n = 0;
print(setBitNumber(n));

# This code is contributed
# by mits
```

## c#

```
// Simple C# program to find
// MSB number for given n.
using System;

class GFG {
    static int setBitNumber(int n)
    {
        if (n == 0)
            return 0;

        int msb = 0;
        n = n / 2;

        while (n != 0) {
            n = n / 2;
            msb++;
        }

        return (1 << msb);
    }

    // Driver code
    static public void Main()
    {
        int n = 0;
        Console.WriteLine(setBitNumber(n));
    }
}

// This code is contributed
// by akt_mit
```

## PHP

```
<?php
// Simple PhP program
// to find MSB number
// for given n.

function setBitNumber($n)
{
    if ($n == 0)
        return 0;

    $msb = 0;
        $n = $n / 2;

    while ($n != 0)
    {
        $n = $n / 2;
        $msb++;
    }

    return (1 << $msb);
}

// Driver code
$n = 0;
echo setBitNumber($n);

// This code is contributed
// by akt_mit
?>
```

## Javascript

```
<script>

// Javascript  program
// to find MSB number
// for given n.

function setBitNumber(n)
{
    if (n == 0)
        return 0;

    let msb = 0;
        n = n / 2;

    while (n != 0)
    {
        n = $n / 2;
        msb++;
    }

    return (1 << msb);
}

// Driver code
let n = 0;
document.write (setBitNumber(n));

// This code is contributed by Bobby

</script>
```

**输出:**

```
0
```