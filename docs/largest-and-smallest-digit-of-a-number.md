# 一个数字的最大和最小数字

> 原文:[https://www . geeksforgeeks . org/数字的最大和最小位数/](https://www.geeksforgeeks.org/largest-and-smallest-digit-of-a-number/)

给定一个数字 **N** 。任务是找出数字的最大和最小的数字。
**例:**

> **输入:** N = 2346
> **输出:** 6 2
> 6 为最大数字，2 为最小
> **输入:** N = 5
> **输出:** 5 5

**方法**:一种有效的方法是找出给定数字中的所有数字，并找出最大和最小的数字。

## C++

```
// CPP program to largest and smallest digit of a number
#include <bits/stdc++.h>
using namespace std;

// Function to the largest and smallest digit of a number
void Digits(int n)
{
    int largest = 0;
    int smallest = 9;

    while (n) {
        int r = n % 10;

        // Find the largest digit
        largest = max(r, largest);

        // Find the smallest digit
        smallest = min(r, smallest);

        n = n / 10;
    }
    cout << largest << " " << smallest;
}

// Driver code
int main()
{
    int n = 2346;

    // Function call
    Digits(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to largest and smallest digit of a number
import java.util.*;
import java.lang.*;
import java.io.*;

class Gfg
{

// Function to the largest and smallest digit of a number
static void Digits(int n)
{
    int largest = 0;
    int smallest = 9;

    while(n != 0)
    {
        int r = n % 10;

        // Find the largest digit
        largest = Math.max(r, largest);

        // Find the smallest digit
        smallest = Math.min(r, smallest);

        n = n / 10;
    }
    System.out.println(largest + " " + smallest);
}

// Driver code
public static void main (String[] args) throws java.lang.Exception
{
    int n = 2346;

    // Function call
    Digits(n);

}
}

// This code is contributed by nidhiva
```

## 蟒蛇 3

```
# Python3 program to largest and smallest digit of a number

# Function to the largest and smallest digit of a number
def Digits(n):
    largest = 0
    smallest = 9

    while (n):
        r = n % 10

        # Find the largest digit
        largest = max(r, largest)

        # Find the smallest digit
        smallest = min(r, smallest)

        n = n // 10

    print(largest,smallest)

# Driver code

n = 2346

# Function call
Digits(n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to largest and
// smallest digit of a number
using System;

class GFG
{

// Function to the largest and
// smallest digit of a number
static void Digits(int n)
{
    int largest = 0;
    int smallest = 9;

    while(n != 0)
    {
        int r = n % 10;

        // Find the largest digit
        largest = Math.Max(r, largest);

        // Find the smallest digit
        smallest = Math.Min(r, smallest);

        n = n / 10;
    }
    Console.WriteLine(largest + " " + smallest);
}

// Driver code
public static void Main (String[] args)
{
    int n = 2346;

    // Function call
    Digits(n);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to largest and
// smallest digit of a number

// Function to the largest and smallest
// digit of a number
function Digits(n)
{
    let largest = 0;
    let smallest = 9;

    while (n) {
        let r = n % 10;

        // Find the largest digit
        largest = Math.max(r, largest);

        // Find the smallest digit
        smallest = Math.min(r, smallest);

        n = parseInt(n / 10);
    }
    document.write(largest + " " + smallest);
}

// Driver code
    let n = 2346;

    // Function call
    Digits(n);

</script>
```

**Output:** 

```
6 2
```