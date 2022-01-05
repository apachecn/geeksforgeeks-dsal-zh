# 由 N 位数字组成的 2 的最小幂

> 原文:[https://www . geeksforgeeks . org/由 n 位数组成的 2 的最小幂/](https://www.geeksforgeeks.org/smallest-power-of-2-consisting-of-n-digits/)

给定一个整数 **N** ，任务是找到 2 的最小[次方，由 **N** 位数组成。](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)

**示例:**

> **输入:** N = 3
> **输出:** 7
> **说明:**
> 2 <sup>7</sup> = 128，有三位数。
> 
> **输入:** N = 4
> **输出:** 10
> **说明:**
> 2 <sup>10</sup> = 1024，有四位数字。

**天真法**:简单的解决方法是从**2<sup>0</sup>T5】开始遍历 2 的所有幂，检查每个 2 的幂，是否包含 **N** 个数字。打印包含 **N** 位数字的二的一次幂。**

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return smallest
// power of 2 with N digits
int smallestNum(int n)
{
    int res = 1;

    // Iterate through all
    // powers of 2
    for (int i = 2;; i *= 2) {
        int length = log10(i) + 1;
        if (length == n)
            return log(i) / log(2);
    }
}

// Driver Code
int main()
{
    int n = 4;
    cout << smallestNum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG{

// Function to return smallest
// power of 2 with N digits
static int smallestNum(int n)
{
    int res = 1;

    // Iterate through all
    // powers of 2
    for(int i = 2;; i *= 2)
    {
        int length = (int)(Math.log10(i)) + 1;

        if (length == n)
            return (int)(Math.log(i) /
                         Math.log(2));
    }
}

// Driver Code
public static void main (String[] args)
{
    int n = 4;

    System.out.print(smallestNum(n));
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from math import log10, log

# Function to return smallest
# power of 2 with N digits
def smallestNum(n):

    res = 1

    # Iterate through all
    # powers of 2
    i = 2
    while (True):
        length = int(log10(i) + 1)

        if (length == n):
            return int(log(i) // log(2))

        i *= 2

# Driver Code
n = 4

print(smallestNum(n))

# This code is contributed by SHIVAMSINGH67
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to return smallest
// power of 2 with N digits
static int smallestNum(int n)
{
    //int res = 1;

    // Iterate through all
    // powers of 2
    for(int i = 2;; i *= 2)
    {
        int length = (int)(Math.Log10(i)) + 1;

        if (length == n)
            return (int)(Math.Log(i) /
                         Math.Log(2));
    }
}

// Driver Code
public static void Main ()
{
    int n = 4;

    Console.Write(smallestNum(n));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function to return smallest
// power of 2 with N digits
function smallestNum(n)
{
    res = 1;

    // Iterate through all
    // powers of 2
    for (var i = 2;; i *= 2) {
        var length = parseInt(Math.log(i)/Math.log(10)) + 1;
        if (length == n)
            return parseInt(Math.log(i) / Math.log(2));
    }
}

// Driver Code
n = 4;
document.write(smallestNum(n));

</script>
```

**Output:** 

```
10
```

**高效逼近**:优化上述逼近的关键观察点是:用 **N** 位数的 2 的最小幂可以通过下式得到:

![\lceil (N-1)*\log_2 10 \rceil          ](img/21b2421bf8149c175ef31a43b7fa35eb.png "Rendered by QuickLaTeX.com")

下面是上述方法的实现:

## C++

```
// C++ Program of the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return smallest
// power of 2 consisting of N digits
int smallestNum(int n)
{
    float power = log2(10);
  cout<<power;
    return ceil((n - 1) * power);
}

// Driver Code
int main()
{
    int n = 4;
    cout << smallestNum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program of the
// above approach
class GFG{

  // Function to return smallest
  // power of 2 consisting of N digits
  static int smallestNum(int n)
  {
    double power = log2(10);
    return (int) Math.ceil((n - 1) * power);
  }

  static double log2(int N)
  {
    // calculate log2 N indirectly
    // using log() method
    return (Math.log(N) / Math.log(2));
}

// Driver Code
public static void main(String[] args)
{
  int n = 4;
  System.out.print(smallestNum(n));

}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program of the
# above approach
from math import log2, ceil

# Function to return smallest
# power of 2 with N digits
def smallestNum(n):

    power = log2(10)
    print(power);
    return ceil((n - 1) * power)

# Driver Code
n = 4

print(smallestNum(n))

# This code is contributed by SHIVAMSINGH67
```

## C#

```
// C# program of the
// above approach
using System;
class GFG{

// Function to return smallest
// power of 2 consisting of N digits
static int smallestNum(int n)
{
  double power = log2(10);
  return (int) Math.Ceiling((n - 1) * power);
}

static double log2(int N)
{
  // calculate log2 N indirectly
  // using log() method
  return (Math.Log(N) / Math.Log(2));
}

// Driver Code
public static void Main()
{
  int n = 4;
  Console.Write(smallestNum(n));
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>

// JavaScript program for
// the above approach

 // Function to return smallest
  // power of 2 consisting of N digits
  function smallestNum(n)
  {
    let power = log2(10);
    return Math.ceil((n - 1) * power);
  }

  function log2(N)
  {

    // calculate log2 N indirectly
    // using log() method
    return (Math.log(N) / Math.log(2));
    }

// Driver code
    let n = 4;
   document.write(smallestNum(n));

   // This code is contributed by splevel62.
</script>
```

**Output:** 

```
10
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)