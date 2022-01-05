# 通过乘以任意数或取平方根来减少 N 的最小运算

> 原文:[https://www . geesforgeks . org/min-operations-to-reduce-n-by-乘以任意数或取平方根/](https://www.geeksforgeeks.org/min-operations-to-reduce-n-by-multiplying-by-any-number-or-taking-square-root/)

给定一个数字 **N** ，任务是通过多次应用以下操作来找到 **N** 的最小值:

*   将 **N** 乘以任意正整数
*   将 **N** 替换为 **sqrt(N)** ，只有[N 是一个完美的正方形](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)。

**例:**

> **输入:** N = 20
> **输出:** 10
> **解释:**
> 乘- > 20 * 5 = 100
> sqrt(100) = 10，这是可获得的最小值。
> 
> **输入:** N = 5184
> **输出:** 6
> **解释:**
> sqrt(5184) = 72。
> 乘->72 * 18 = 1296
> sqrt(1296)= 6，这是可获得的最小值。

**进场**:这个问题可以用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。以下是步骤:

1.  继续将 **N** 替换为 **sqrt(N)** ，直到 **N** 成为一个完美的正方形。
2.  完成上述步骤后，从 **sqrt(N)** 迭代到 **2** ，每次，如果 **N 可以被 i <sup>2</sup>** 整除，我会继续用 **N / i** 替换 **N** 。
3.  上述步骤后 **N** 的值将是最小可能值。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to reduce N to its minimum
// possible value by the given operations
void minValue(int n)
{
    // Keep replacing n until is
    // an integer
    while (int(sqrt(n)) == sqrt(n)
        && n > 1) {
        n = sqrt(n);
    }

    // Keep replacing n until n
    // is divisible by i * i
    for (int i = sqrt(n);
        i > 1; i--) {

        while (n % (i * i) == 0)
            n /= i;
    }

    // Print the answer
    cout << n;
}

// Driver Code
int main()
{
    // Given N
    int N = 20;

    // Function Call
    minValue(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.lang.Math;

class GFG{

// Function to reduce N to its minimum
// possible value by the given operations
static void minValue(int n)
{

    // Keep replacing n until is
    // an integer
    while ((int)Math.sqrt(n) ==
                Math.sqrt(n) && n > 1)
    {
        n = (int)(Math.sqrt(n));
    }

    // Keep replacing n until n
    // is divisible by i * i
    for(int i = (int)(Math.sqrt(n));
            i > 1; i--)
    {
        while (n % (i * i) == 0)
            n /= i;
    }

    // Print the answer
    System.out.println(n);
}

// Driver code
public static void main(String args[])
{

    // Given N
    int N = 20;

    // Function call
    minValue(N);
}
}

// This code is contributed by vikas_g
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to reduce N to its minimum
# possible value by the given operations
def MinValue(n):

    # Keep replacing n until is
    # an integer
    while(int(math.sqrt(n)) ==
              math.sqrt(n) and n > 1):
        n = math.sqrt(n)

    # Keep replacing n until n
    # is divisible by i * i
    for i in range(int(math.sqrt(n)), 1, -1):
        while (n % (i * i) == 0):
            n /= i

    # Print the answer
    print(n)

# Driver code
n = 20

# Function call
MinValue(n)

# This code is contributed by virusbuddah_
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

// Function to reduce N to its minimum
// possible value by the given operations
static void minValue(int n)
{

    // Keep replacing n until is
    // an integer
    while ((int)Math.Sqrt(n) ==
                Math.Sqrt(n) && n > 1)
    {
        n = (int)(Math.Sqrt(n));
    }

    // Keep replacing n until n
    // is divisible by i * i
    for (int i = (int)(Math.Sqrt(n));
             i > 1; i--)
    {
        while (n % (i * i) == 0)
            n /= i;
    }

    // Print the answer
    Console.Write(n);
}

// Driver code
public static void Main()
{

    // Given N
    int N = 20;

    // Function call
    minValue(N);
}
}

// This code is contributed by vikas_g
```

## java 描述语言

```
<script>

// Javascript program for above approach

// Function to reduce N to its minimum
// possible value by the given operations
function minValue(n)
{

    // Keep replacing n until is
    // an integer
    while (parseInt(Math.sqrt(n)) == Math.sqrt(n)
        && n > 1)
    {
        n = parseInt(Math.sqrt(n));
    }

    // Keep replacing n until n
    // is divisible by i * i
    for (var i = parseInt(Math.sqrt(n));
        i > 1; i--) {

        while (n % (i * i) == 0)
            n /= i;
    }

    // Print the answer
    document.write(n);
}

// Driver Code

// Given N
var N = 20;

// Function Call
minValue(N);

// This code is contributed by rutvik_56.
</script>
```

**Output:**

```
10
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*