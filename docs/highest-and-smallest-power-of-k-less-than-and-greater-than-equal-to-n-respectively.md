# K 的最高和最低幂分别小于和大于等于 N

> 原文:[https://www . geesforgeks . org/k 的最高和最低幂分别小于和大于等于 n/](https://www.geeksforgeeks.org/highest-and-smallest-power-of-k-less-than-and-greater-than-equal-to-n-respectively/)

给定正整数 **N** 和 **K** ，任务是分别求大于等于 N 和小于等于 N 的 K 的最高幂和最低幂。

**示例:**

> **输入:** N = 3，K = 2
> T3】输出:2 4
> 2 小于 3 的最大功率= 2
> 2 大于 3 的最小功率= 4
> 
> **输入:** N = 6，K = 3
> T3】输出:3 9
> 3 小于 6 的最大功率= 3
> 3 大于 6 的最小功率= 9

**进场:**

1.  计算以 K 为基数的 N 的[对数(**对数 <sub>K</sub> N** )得到指数幂，使 K 上升到这个指数就是 K 小于等于 N 的最高幂](https://www.geeksforgeeks.org/logarithm/)
2.  对于小于等于 N 的 K 的最小幂，求从上一步计算出的 K 的下一次幂

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the highest power
// of k less than or equal to n
int prevPowerofK(int n, int k)
{
    int p = (int)(log(n) / log(k));
    return (int)pow(k, p);
}

// Function to return the smallest power
// of k greater than or equal to n
int nextPowerOfK(int n, int k)
{
    return prevPowerofK(n, k) * k;
}

// Function to print the result
void printResult(int n, int k)
{
    cout << prevPowerofK(n, k)
         << " " << nextPowerOfK(n, k)
         << endl;
}

// Driver code
int main()
{
    int n = 25, k = 3;

    printResult(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG{

// Function to return the highest power
// of k less than or equal to n
static int prevPowerofK(int n, int k)
{
    int p = (int)(Math.log(n) / Math.log(k));
    return (int) Math.pow(k, p);
}

// Function to return the smallest power
// of k greater than or equal to n
static int nextPowerOfK(int n, int k)
{
    return prevPowerofK(n, k) * k;
}

// Function to print the result
static void printResult(int n, int k)
{
    System.out.println(prevPowerofK(n, k) + " " +
                       nextPowerOfK(n, k));
}

// Driver Code
public static void main (String args[])
{
    int n = 25, k = 3;
    printResult(n, k);
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math

# Function to return the highest power
# of k less than or equal to n
def prevPowerofK(n, k):

    p = int(math.log(n) / math.log(k))
    return int(math.pow(k, p))

# Function to return the smallest power
# of k greater than or equal to n
def nextPowerOfK(n, k):

    return prevPowerofK(n, k) * k

# Function to print the result
def printResult(n, k):

    print(prevPowerofK(n, k), nextPowerOfK(n, k))

# Driver code
n = 6
k = 3

printResult(n, k)

# This code is contributed by divyamohan123
```

## C#

```
// C# implementation of the approach
using System;
class GFG{

// Function to return the highest power
// of k less than or equal to n
static int prevPowerofK(int n, int k)
{
    int p = (int)(Math.Log(n) / Math.Log(k));
    return (int) Math.Pow(k, p);
}

// Function to return the smallest power
// of k greater than or equal to n
static int nextPowerOfK(int n, int k)
{
    return prevPowerofK(n, k) * k;
}

// Function to print the result
static void printResult(int n, int k)
{
    Console.WriteLine(prevPowerofK(n, k) + " " +
                      nextPowerOfK(n, k));
}

// Driver Code
public static void Main(String []args)
{
    int n = 25, k = 3;
    printResult(n, k);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the highest power
// of k less than or equal to n
function prevPowerofK(n, k)
{
    var p = parseInt(Math.log(n) / Math.log(k));
    return parseInt(Math.pow(k, p));
}

// Function to return the smallest power
// of k greater than or equal to n
function nextPowerOfK(n, k)
{
    return prevPowerofK(n, k) * k;
}

// Function to print the result
function printResult(n, k)
{
    document.write(prevPowerofK(n, k)
         + " " + nextPowerOfK(n, k) + "<br>");

}

// Driver code
var n = 25, k = 3;
printResult(n, k);

</script>
```

**Output:** 

```
9 27
```