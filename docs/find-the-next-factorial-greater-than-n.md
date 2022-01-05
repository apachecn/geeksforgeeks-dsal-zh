# 求下一个大于 N 的阶乘

> 原文:[https://www . geesforgeks . org/find-下一个因子-大于-n/](https://www.geeksforgeeks.org/find-the-next-factorial-greater-than-n/)

给定一个数 **N** (≤ 10 <sup>18</sup> ，任务是找到下一个大于 **N** 的[阶乘数](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/)。
**举例:**

> **输入:** N = 24
> **输出:** 120
> **解释:**
> As 4！= 24.所以下一个阶乘大于 24 的数是 5！，即 120
> **输入:** N = 150
> **输出:** 720
> **解释:**
> As 5！= 120.所以下一个阶乘大于 150 的数是 6！，也就是 720。

**进场:**

1.  在一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中将所有数字的[因子](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/)预先计算到 **20** 为 **20！> 10 <sup>18</sup>** 。
2.  遍历阶乘数组，找到刚好大于 **N** 的值作为所需的下一个阶乘数。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include "bits/stdc++.h"
using namespace std;

// Array that stores the factorial
// till 20
long long fact[21];

// Function to pre-compute
// the factorial till 20
void preCompute()
{

    // Precomputing factorials
    fact[0] = 1;

    for (int i = 1; i < 18; i++)
        fact[i] = (fact[i - 1] * i);
}

// Function to return the next
// factorial number greater than N
void nextFactorial(int N)
{
    // Traverse the factorial array
    for (int i = 0; i < 21; i++) {

// Find the next just greater
// factorial than N
        if (N < fact[i]) {

            cout << fact[i];
            break;
        }
    }
}

// Driver Code
int main()
{
    // Function to precalculate
    // the factorial till 20
    preCompute();

    int N = 120;

    // Function call
    nextFactorial(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG {

// Array that stores the factorial
// till 20
final static int fact[] = new int[21];

    // Function to pre-compute
    // the factorial till 20
    static void preCompute()
    {

        // Precomputing factorials
        fact[0] = 1;

        for (int i = 1; i < 18; i++)
            fact[i] = (fact[i - 1] * i);
    }

    // Function to return the next
    // factorial number greater than N
    static void nextFactorial(int N)
    {
        // Traverse the factorial array
        for (int i = 0; i < 21; i++) {

            // Find the next just greater
            // factorial than N
            if (N < fact[i]) {

                System.out.println(fact[i]);
                break;
            }
        }
    }

    // Driver Code
    public static void main (String[] args)
    {
        // Function to precalculate
        // the factorial till 20
        preCompute();

        int N = 120;

        // Function call
        nextFactorial(N);
    }

}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Array that stores the factorial
# till 20
fact = [0] * 21

# Function to pre-compute
# the factorial till 20
def preCompute():

    # Precomputing factorials
    fact[0] = 1

    for i in range(1, 18):
        fact[i] = (fact[i - 1] * i)

# Function to return the next
# factorial number greater than N
def nextFactorial(N):

    # Traverse the factorial array
    for i in range(21):

# Find the next just greater
# factorial than N
        if N < fact[i]:

            print(fact[i])
            break

# Driver Code
# Function to precalculate
# the factorial till 20
preCompute()

N = 120

# Function call
nextFactorial(N)

# This code is contributed by divyamohan123
```

## C#

```
// C# implementation of the above approach
using System;

class GFG {

    // Array that stores the factorial
    // till 20
    static int []fact = new int[21];

    // Function to pre-compute
    // the factorial till 20
    static void preCompute()
    {

        // Precomputing factorials
        fact[0] = 1;

        for (int i = 1; i < 18; i++)
            fact[i] = (fact[i - 1] * i);
    }

    // Function to return the next
    // factorial number greater than N
    static void nextFactorial(int N)
    {
        // Traverse the factorial array
        for (int i = 0; i < 21; i++) {

            // Find the next just greater
            // factorial than N
            if (N < fact[i]) {

                Console.WriteLine(fact[i]);
                break;
            }
        }
    }

    // Driver Code
    public static void Main (string[] args)
    {
        // Function to precalculate
        // the factorial till 20
        preCompute();

        int N = 120;

        // Function call
        nextFactorial(N);
    }

}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Array that stores the factorial
// till 20
fact = Array(21).fill(0);

// Function to pre-compute
// the factorial till 20
function preCompute()
{

    // Precomputing factorials
    fact[0] = 1;

    for (var i = 1; i < 18; i++)
        fact[i] = (fact[i - 1] * i);
}

// Function to return the next
// factorial number greater than N
function nextFactorial(N)
{
    // Traverse the factorial array
    for (var i = 0; i < 21; i++) {

    // Find the next just greater
    // factorial than N
        if (N < fact[i]) {

            document.write(fact[i]);
            break;
        }
    }
}

// Driver Code

// Function to precalculate
// the factorial till 20
preCompute();
var N = 120;

// Function call
nextFactorial(N);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
720
```

时间复杂性:O(21)

辅助空间:O(21)