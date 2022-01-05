# 使用按位运算符

生成 N 的前 K 倍

> 原文:[https://www . geesforgeks . org/generate-first-k-倍数-n-use-bitwise-operator/](https://www.geeksforgeeks.org/generate-first-k-multiples-of-n-using-bitwise-operators/)

给定一个整数 **N** ，任务是使用[按位运算符](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)打印 **N** 的前 K 倍。

**示例:**

> **输入:** N = 16，K = 7
> T3】输出:T5】16 * 1 = 16
> 16 * 2 = 32
> 16 * 3 = 48
> 16 * 4 = 64
> 16 * 5 = 80
> 16 * 6 = 96
> 16 * 7 = 112
> **输入:** N = 7， K = 10
> **输出:**
> 7 * 1 = 7
> 7 * 2 = 14
> 7 * 3 = 21
> 7 * 4 = 28
> 7 * 5 = 35
> 7 * 6 = 42
> 7 * 7 = 49
> 7 * 8 = 56
> 7 * 9 = 63
> 7 * 10 = 70

**进场:**

按照以下步骤解决问题:

*   迭代到 **K** 。
*   每次迭代，打印 **N** 的当前值。
*   然后，计算 **N** 的每一个 **i <sup>第</sup>组位**的**2<sup>I</sup>T3】之和。将此总和加到 **N** 上，重复上述步骤。**

以下是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the first K
// multiples of N
void Kmultiples(int n, int k)
{
    int a = n;

    for (int i = 1; i <= k; i++) {

        // Print the value of N*i
        cout << n << " * " << i << " = "
             << a << endl;
        int j = 0;

        // Iterate each bit of N and add
        // pow(2, pos), where pos is the
        // index of each set bit
        while (n >= (1 << j)) {

            // Check if current bit at
            // pos j is fixed or not
            a += n & (1 << j);

            // For next set bit
            j++;
        }
    }
}

// Driver Code
int main()
{
    int N = 16, K = 7;

    Kmultiples(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to print the first K
// multiples of N
static void Kmultiples(int n, int k)
{
    int a = n;

    for (int i = 1; i <= k; i++)
    {

        // Print the value of N*i
        System.out.print(n+ " * " +  i+ " = "
             + a +"\n");
        int j = 0;

        // Iterate each bit of N and add
        // Math.pow(2, pos), where pos is the
        // index of each set bit
        while (n >= (1 << j))
        {

            // Check if current bit at
            // pos j is fixed or not
            a += n & (1 << j);

            // For next set bit
            j++;
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 16, K = 7;

    Kmultiples(N, K);
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to print the first K
# multiples of N
def Kmultiples(n, k):

    a = n

    for i in range(1, k + 1):

        # Print the value of N*i
        print("{} * {} = {}".format(n, i, a))
        j = 0

        # Iterate each bit of N and add
        # pow(2, pos), where pos is the
        # index of each set bit
        while(n >= (1 << j)):

            # Check if current bit at
            # pos j is fixed or not
            a += n & (1 << j)

            # For next set bit
            j += 1

# Driver Code
N = 16
K = 7

Kmultiples(N, K)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to print the first K
// multiples of N
static void Kmultiples(int n, int k)
{
    int a = n;

    for(int i = 1; i <= k; i++)
    {

        // Print the value of N*i
        Console.Write(n + " * " + i +
                          " = " + a + "\n");
        int j = 0;

        // Iterate each bit of N and add
        // Math.Pow(2, pos), where pos is
        //  the index of each set bit
        while (n >= (1 << j))
        {

            // Check if current bit at
            // pos j is fixed or not
            a += n & (1 << j);

            // For next set bit
            j++;
        }
    }
}

// Driver Code
public static void Main(String[] args)
{
    int N = 16, K = 7;

    Kmultiples(N, K);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach
// Function to print the first K
// multiples of N
function Kmultiples(n , k)
{
    var a = n;

    for (i = 1; i <= k; i++)
    {

        // Print the value of N*i
        document.write(n+ " * " +  i+ " = "
             + a +"<br>");
        var j = 0;

        // Iterate each bit of N and add
        // Math.pow(2, pos), where pos is the
        // index of each set bit
        while (n >= (1 << j))
        {

            // Check if current bit at
            // pos j is fixed or not
            a += n & (1 << j);

            // For next set bit
            j++;
        }
    }
}

// Driver Code
var N = 16, K = 7;

Kmultiples(N, K);

// This code contributed by Princi Singh
</script>
```

**Output:** 

```
16 * 1 = 16
16 * 2 = 32
16 * 3 = 48
16 * 4 = 64
16 * 5 = 80
16 * 6 = 96
16 * 7 = 112
```

***时间复杂度:**O(Klog<sub>2</sub>N)*
***辅助空间:** O(1)*