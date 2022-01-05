# 所有 2 的幂相加两次的前 N 个自然数之和

> 原文:[https://www . geeksforgeeks . org/第一个 n 个自然数之和加 2 的所有幂次/](https://www.geeksforgeeks.org/sum-of-first-n-natural-numbers-with-all-powers-of-2-added-twice/)

给定一个整数 **N** ，任务是计算前 N 个自然数的[和，将 2](https://www.geeksforgeeks.org/program-find-sum-first-n-natural-numbers/) 的所有[次幂相加。
**举例:**](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/) 

> **输入:** N = 4
> **输出:** 17
> **说明:**
> 和=**2**+**4**+3+**8**= 17
> 由于 1、2、4 分别是 2 <sup>0</sup> ，2 <sup>1</sup> 和 2 <sup>2</sup> 的和，所以加起来是两次。
> **输入:** N = 5
> **输出:** 22
> **解释:**
> 之和等于**2**+**4**+3+**8**+5 = 22、
> 因为 1、2、4 是 2 <sup>0</sup> ，2 <sup>1</sup> 和 2

**天真法:**
解决这个问题最简单的方法就是迭代到 **N** ，除了 **2** 的次方需要相加两次之外，每加一次，继续计算总和。
***时间复杂度:** O(N)*
***辅助空间:** O(1)*
**高效途径:**
按照以下步骤优化上述途径:

1.  用公式 **(N * (N + 1)) / 2** 计算[前 N 个自然数之和](https://www.geeksforgeeks.org/program-find-sum-first-n-natural-numbers/)。
2.  现在，2 的所有幂需要再加一次。[2 到 N 的所有幂之和](https://www.geeksforgeeks.org/sum-of-the-series-20-21-22-2n/)可以计算为 **2 <sup>对数</sup>T5<sup>2</sup>T8<sup>(N)+1</sup>–1**。

3.  因此，所需的总和为:

> (N *(N+1))/2+2<sup>log</sup><sub><sup>2</sup></sub><sup>(N)+1</sup>–1

以下是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to raise N to the
// power P and return the value
double power(int N, int P)
{
    return pow(N, P);
}

// Function to calculate the
// log base 2 of an integer
int Log2(int N)
{

    // Calculate log2(N) indirectly
    // using log() method
    int result = (int)(log(N) / log(2));
    return result;
}

// Function to calculate and
// return the required sum
double specialSum(int n)
{

    // Sum of first N natural
    // numbers
    double sum = n * (n + 1) / 2;

    // Sum of all powers of 2
    // up to N
    int a = Log2(n);
    sum = sum + power(2, a + 1) - 1;

    return sum;
}

// Driver code
int main()
{
    int n = 4;

    cout << (specialSum(n)) << endl;

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
import java.lang.Math;

class GFG {

    // Function to raise N to the
    // power P and return the value
    static double power(int N, int P)
    {
        return Math.pow(N, P);
    }

    // Function to calculate the
    // log base 2 of an integer
    public static int log2(int N)
    {

        // Calculate log2(N) indirectly
        // using log() method
        int result = (int)(Math.log(N)
                        / Math.log(2));
        return result;
    }

    // Function to calculate and
    // return the required sum
    static double specialSum(int n)
    {

        // Sum of first N natural
        // numbers
        double sum = n * (n + 1) / 2;

        // Sum of all powers of 2
        // up to N
        int a = log2(n);
        sum = sum + power(2, a + 1) - 1;

        return sum;
    }

    // Driver Code
    public static void main(String[] args)
    {

        int n = 4;

        System.out.println(specialSum(n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import math

# Function to raise N to the
# power P and return the value
def power(N, P):

    return math.pow(N, P)

# Function to calculate the
# log base 2 of an integer
def Log2(N):

    # Calculate log2(N) indirectly
    # using log() method
    result = (math.log(N) // math.log(2))

    return result

# Function to calculate and
# return the required sum
def specialSum(n):

    # Sum of first N natural
    # numbers
    sum = n * (n + 1) // 2

    # Sum of all powers of 2
    # up to N
    a = Log2(n)
    sum = sum + power(2, a + 1) - 1

    return sum

# Driver code   
if __name__=="__main__":

    n = 4
    print(specialSum(n))

# This code is contributed by rutvik_56
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

    // Function to raise N to the
    // power P and return the value
    static double power(int N, int P)
    {
        return Math.Pow(N, P);
    }

    // Function to calculate the
    // log base 2 of an integer
    public static int log2(int N)
    {

        // Calculate log2(N) indirectly
        // using log() method
        int result = (int)(Math.Log(N) /
                        Math.Log(2));
        return result;
    }

    // Function to calculate and
    // return the required sum
    static double specialSum(int n)
    {

        // Sum of first N natural
        // numbers
        double sum = (double)(n) * (n + 1) / 2;

        // Sum of all powers of 2
        // up to N
        int a = log2(n);
        sum = (sum) + power(2, a + 1) - 1;

        return sum;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int n = 4;

        Console.Write(specialSum(n));
    }
}

// This code is contributed by Ritik Bansal
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to raise N to the
// power P and return the value
function power(N, P)
{
    return Math.pow(N, P);
}

// Function to calculate the
// log base 2 of an integer
function Log2(N)
{

    // Calculate log2(N) indirectly
    // using log() method
    let result = (Math.floor(Math.log(N) / Math.log(2)));
    return result;
}

// Function to calculate and
// return the required sum
function specialSum(n)
{

    // Sum of first N natural
    // numbers
    let sum = n * (n + 1) / 2;

    // Sum of all powers of 2
    // up to N
    let a = Log2(n);
    sum = sum + power(2, a + 1) - 1;

    return sum;
}

// Driver Code

    let n = 4;

    document.write(specialSum(n) + "<br>");

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
17.0
```

***时间复杂度:**O(log<sub>2</sub>(N))*
***辅助空间:** O(1)*