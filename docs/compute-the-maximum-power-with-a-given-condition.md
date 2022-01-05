# 计算给定条件下的最大功率

> 原文:[https://www . geeksforgeeks . org/计算给定条件下的最大功率/](https://www.geeksforgeeks.org/compute-the-maximum-power-with-a-given-condition/)

给定 3 个整数 **N，M** ，**和 K** 。任务是找到最大 **P** 使得 **N * K <sup>P</sup> ≤ M** 。

**示例:**

> **输入:** N = 1，K = 2，M = 5
> **输出:** 2
> **输入:** N = 5，K = 25，M = 100
> **输出:** 0

**逼近:**
在该算法中，只需将 **N** 与 **K** 相乘，并用结果更新 **N** 的当前值，并将可变功率(初始为 0)增加 **1** 。
为了实现这一点，定义了一个递归函数，它有两种基本情况。

1.  最初，N 大于要求，因此，返回 **0** 。
2.  否则，返回**电源–1**。

*   如果当前 N 值等于 M，则返回**功率**。
*   **递归条件**如果当前 **N < M** :
    更新 **N** 为 **(N * k)** ，**功率**为当前**功率+ 1** 。

以下是上述方法的实现:

## C++

```
// Compute maximum power to which K can be raised so
// that given condition remains true
#include <bits/stdc++.h>
using namespace std;

#define ll long long

// Function to return the largest
// power
int calculate(ll int n, ll int k,
              ll int m, ll int power)
{

    // If n is greater than given M
    if (n > m) {
        if (power == 0)
            return 0;
        else
            return power - 1;
    }

    // If n == m
    else if (n == m)
        return power;

    else
        // Checking for the next power
        return calculate(n * k, k, m, power + 1);
}

// Driver Code
int main()
{
    ll N = 1, K = 2, M = 5;

    cout << calculate(N, K, M, 0);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Compute maximum power
// to which K can be raised so that
// given condition remains true
class GFG
{

// Function to return the largest
// power
static int calculate(int n, int k,
                     int m, int power)
{

    // If n is greater than given M
    if (n > m)
    {
        if (power == 0)
            return 0;
        else
            return power - 1;
    }

    // If n == m
    else if (n == m)
        return power;

    else
        // Checking for the next power
        return calculate(n * k, k, m,
                          power + 1);
}

// Driver Code
public static void main (String[] args)
{
    int N = 1, K = 2, M = 5;

    System.out.println(calculate(N, K, M, 0));
}
}

// This code is contributed by AnkitRai01
```

## 计算机编程语言

```
# Compute maximum power to
# which K can be raised so
# that given condition
# remains true

# Function to return the largest
# power
def calculate(n, k, m, power):    

    # If n is greater than given M                        
    if n > m:
        if power == 0:
            return 0
        else:
            return power-1

    # If n == m
    elif n == m:
        return power
    else:
        # Checking for the next power
        return calculate(n * k, k, m, power + 1)

# Driver's code    
if __name__=="__main__":

    N = 1
    K = 2
    M = 5

    print(calculate(N, K, M, 0))
```

## C#

```
// C# program for Compute maximum power
// to which K can be raised so that
// given condition remains true
using System;
class GFG
{

// Function to return the largest
// power
static int calculate(int n, int k,
                     int m, int power)
{

    // If n is greater than given M
    if (n > m)
    {
        if (power == 0)
            return 0;
        else
            return power - 1;
    }

    // If n == m
    else if (n == m)
        return power;

    else
        // Checking for the next power
        return calculate(n * k, k, m,
                         power + 1);
}

// Driver Code
public static void Main (String[] args)
{
    int N = 1, K = 2, M = 5;

    Console.WriteLine(calculate(N, K, M, 0));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// javascript program for Compute maximum power
// to which K can be raised so that
// given condition remains true    
// Function to return the largest
    // power
    function calculate(n , k , m , power) {

        // If n is greater than given M
        if (n > m) {
            if (power == 0)
                return 0;
            else
                return power - 1;
        }

        // If n == m
        else if (n == m)
            return power;

        else
            // Checking for the next power
            return calculate(n * k, k, m, power + 1);
    }

    // Driver Code

        var N = 1, K = 2, M = 5;

        document.write(calculate(N, K, M, 0));

// This code contributed by aashish1995
</script>
```

**Output:** 

```
2
```