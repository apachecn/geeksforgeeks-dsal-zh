# 打印任意一对 GCD 和 LCM 之和等于 N 的整数

> 原文:[https://www . geesforgeks . org/print-任意整数对加 gcd 和 lcm 之和等于 n/](https://www.geeksforgeeks.org/print-any-pair-of-integers-with-sum-of-gcd-and-lcm-equals-to-n/)

给定一个**整数 N** ，任务是打印任意一对 GCD 和 LCM 之和等于 N 的整数。
**示例:**

> **输入:** N = 14
> **输出:** 1，13
> **解释** :
> 对于给定的对，我们有 GCD(1，13) = 1 和 LCM (1，13) = 13。GCD 和 LCM 之和= 1 + 13 = 14。
> 
> **输入:** 2
> **输出:** 1 1
> **解释** :
> 对于给定的对，我们有 GCD(1，1) = 1 和 LCM (1，1) = 1。GCD 和 LCM 之和= 1 + 1 = 2。

**方法:**
为了解决上面提到的问题，让我们考虑这一对是(1，n-1)。 **GCD 为(1，n-1) = 1，LCM 为(1，n-1)= n–1**。因此，GCD 和 LCM 之和= 1+(n–1)= n。因此，对(1，n–1)将是 GCD 和 LCM 之和等于 n 的对。
下面是上述方法的实现:

## C++

```
// C++ implementation to Print any pair of integers
// whose summation of GCD and LCM is equal to integer N

#include <bits/stdc++.h>
using namespace std;

// Function to print the required pair
void printPair(int n)
{
    // print the pair
    cout << 1 << " " << n - 1;
}

// Driver code
int main()
{
    int n = 14;

    printPair(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print any pair of integers
// whose summation of GCD and LCM is equal to integer N
class GFG{

// Function to print the required pair
static void printPair(int n)
{
    // Print the pair
    System.out.print(1 + " " + (n - 1));
}

// Driver code
public static void main(String[] args)
{
    int n = 14;
    printPair(n);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 implementation to print any
# pair of integers whose summation of
# GCD and LCM is equal to integer N

# Function to print the required pair
def printPair(n):

    # Print the pair
    print("1", end = " ")
    print(n - 1)

# Driver code
n = 14
printPair(n)

# This code is contributed by PratikBasu
```

## C#

```
// C# implementation to print any pair
// of integers whose summation of
// GCD and LCM is equal to integer N
using System;

public class GFG{

// Function to print the required pair
static void printPair(int n)
{

    // Print the pair
    Console.Write(1 + " " + (n - 1));
}

// Driver code
public static void Main(String[] args)
{
    int n = 14;
    printPair(n);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// javascript implementation to print any pair of integers
// whose summation of GCD and LCM is equal to integer N
// Function to print the required pair
    function printPair(n)
    {

        // Print the pair
        document.write(1 + " " + (n - 1));
    }

    // Driver code
        var n = 14;
        printPair(n);

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
1 13
```

**时间复杂度:** O(1)

**辅助空间:** O(1)