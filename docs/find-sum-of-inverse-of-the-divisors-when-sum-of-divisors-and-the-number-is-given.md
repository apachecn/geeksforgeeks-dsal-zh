# 给定除数和数时求除数的倒数之和

> 原文:[https://www . geesforgeks . org/find-除数的倒数之和-当除数之和和被给定时/](https://www.geeksforgeeks.org/find-sum-of-inverse-of-the-divisors-when-sum-of-divisors-and-the-number-is-given/)

给定一个整数 **N** 及其除数之和。任务是求 **N** 的除数的倒数之和。
**例:**

> **输入:** N = 6，和= 12
> **输出:**2.00
> N 的除数为{1，2，3，6}
> 除数的倒数之和等于(1/1 + 1/2 + 1/3 + 1/6) = 2.0
> **输入:** N = 9，和= 13
> **输出:** 1.44

**天真法:**计算给定整数的所有除数 **N** 。然后计算所计算除数的倒数之和。当 **N** 的值较大时，这种方法将给出 TLE。
**时间复杂度:** O(sqrt(N))
**高效途径:**让数 **N** 有 **K** 除数说 **d <sub>1</sub> ，d <sub>2</sub> ，…，d <sub>K</sub>** 。给出**d<sub>1</sub>+d<sub>2</sub>+…+d<sub>K</sub>= Sum**
任务是计算**(1/d<sub>1</sub>)+(1/d<sub>2</sub>)+…+(1/d<sub>K</sub>)**。
用 **N** 乘除上述方程。等式变成**[(N/d<sub>1</sub>)+(N/d<sub>2</sub>)+…+(N/d<sub>K</sub>)]/N**T52】现在很容易看出**N/d<sub>I</sub>T56】将代表所有 **1 ≤ i ≤ K** 的 **N** 的另一个除数。分子等于除数之和。因此，除数的倒数之和等于**和/ N** 。
以下是上述方法的实施:** 

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// sum of inverse of divisors
double SumofInverseDivisors(int N, int Sum)
{

    // Calculating the answer
    double ans = (double)(Sum)*1.0 / (double)(N);

    // Return the answer
    return ans;
}

// Driver code
int main()
{
    int N = 9;

    int Sum = 13;

    // Function call
    cout << setprecision(2) << fixed
         << SumofInverseDivisors(N, Sum);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.math.*;
import java.io.*;

class GFG
{

// Function to return the
// sum of inverse of divisors
static double SumofInverseDivisors(int N, int Sum)
{

    // Calculating the answer
    double ans = (double)(Sum)*1.0 / (double)(N);

    // Return the answer
    return ans;
}

// Driver code
public static void main (String[] args)
{

    int N = 9;
    int Sum = 13;

    // Function call
    System.out.println (SumofInverseDivisors(N, Sum));
}
}

// This code is contributed by jit_t.
```

## 计算机编程语言

```
# Python implementation of above approach

# Function to return the
# sum of inverse of divisors
def SumofInverseDivisors( N, Sum):

    # Calculating the answer
    ans = float(Sum)*1.0 /float(N);

    # Return the answer
    return round(ans,2);

# Driver code
N = 9;
Sum = 13;
print SumofInverseDivisors(N, Sum);

# This code is contributed by CrazyPro
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to return the
// sum of inverse of divisors
static double SumofInverseDivisors(int N, int Sum)
{

    // Calculating the answer
    double ans = (double)(Sum)*1.0 / (double)(N);

    // Return the answer
    return ans;
}

// Driver code
static public void Main ()
{

    int N = 9;
    int Sum = 13;

    // Function call
    Console.Write(SumofInverseDivisors(N, Sum));
}
}

// This code is contributed by ajit
```

## java 描述语言

```
<script>

// JavaScript implementation of above approach

// Function to return the
// sum of inverse of divisors
function SumofInverseDivisors(N, Sum)
{

    // Calculating the answer
    let ans = (Sum)*1.0 / (N);

    // Return the answer
    return ans;
}

// Driver code

    let N = 9;

    let Sum = 13;

    // Function call
    document.write(SumofInverseDivisors(N, Sum).toFixed(2));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
1.44
```

**时间复杂度:** O(1)