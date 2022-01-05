# 生成所有元素的欧拉全能函数之和等于 N 的数组

> 原文:[https://www . geesforgeks . org/generate-a-a-array-having-of-Euler-toitient-function-all-elements-equal-n/](https://www.geeksforgeeks.org/generate-an-array-having-sum-of-euler-totient-function-of-all-elements-equal-to-n/)

给定一个正整数 **N** ，任务是生成一个数组，使得每个元素的[欧拉全能函数](https://www.geeksforgeeks.org/eulers-totient-function/)之和等于 **N** 。

**示例:**

> **输入:**N = 6
> T3】输出: 1 6 2 3
> 
> **输入:**N = 12
> T3】输出: 1 12 2 6 3 4

**方法:**给定问题可以基于[欧拉全能函数](https://www.geeksforgeeks.org/eulers-totient-function/)的除数和性质求解，即，

*   [一个数 **N** <的欧拉全能性函数](https://www.geeksforgeeks.org/eulers-totient-function/)是从 **1** 到 **N** 的整数数，给出 **GCD(i，N)** 为 **1** ，一个数 **N** 可以表示为[的](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)[欧拉全能性函数](https://www.geeksforgeeks.org/eulers-totient-function/)的值与**N**T19 的所有除数之和
*   因此，想法是找到给定数 **N** 的[因子](https://www.geeksforgeeks.org/find-all-divisors-of-a-natural-number-set-2/)作为结果[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to construct the array such
// the sum of values of Euler Totient
// functions of all array elements is N
void constructArray(int N)
{
    // Stores the resultant array
    vector<int> ans;

    // Find divisors in sqrt(N)
    for (int i = 1; i * i <= N; i++) {

        // If N is divisible by i
        if (N % i == 0) {

            // Push the current divisor
            ans.push_back(i);

            // If N is not a
            // perfect square
            if (N != (i * i)) {

                // Push the second divisor
                ans.push_back(N / i);
            }
        }
    }

    // Print the resultant array
    for (auto it : ans) {
        cout << it << " ";
    }
}

// Driver Code
int main()
{
    int N = 12;

    // Function Call
    constructArray(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to construct the array such
// the sum of values of Euler Totient
// functions of all array elements is N
static void constructArray(int N)
{

    // Stores the resultant array
    ArrayList<Integer> ans = new ArrayList<Integer>();

    // Find divisors in sqrt(N)
    for(int i = 1; i * i <= N; i++)
    {

        // If N is divisible by i
        if (N % i == 0)
        {

            // Push the current divisor
            ans.add(i);

            // If N is not a
            // perfect square
            if (N != (i * i))
            {

                // Push the second divisor
                ans.add(N / i);
            }
        }
    }

    // Print the resultant array
    for(int it : ans)
    {
        System.out.print(it + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 12;

    // Function Call
    constructArray(N);
}
}

// This code is contributed by splevel62
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import sqrt

# Function to construct the array such
# the sum of values of Euler Totient
# functions of all array elements is N
def constructArray(N):

    # Stores the resultant array
    ans = []

    # Find divisors in sqrt(N)
    for i in range(1, int(sqrt(N)) + 1, 1):

        # If N is divisible by i
        if (N % i == 0):

            # Push the current divisor
            ans.append(i)

            # If N is not a
            # perfect square
            if (N != (i * i)):

                # Push the second divisor
                ans.append(N / i)

    # Print the resultant array
    for it in ans:
        print(int(it), end = " ")

# Driver Code
if __name__ == '__main__':

    N = 12

    # Function Call
    constructArray(N)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to construct the array such
// the sum of values of Euler Totient
// functions of all array elements is N
static void constructArray(int N)
{

    // Stores the resultant array
    List<int> ans = new List<int>();

    // Find divisors in sqrt(N)
    for(int i = 1; i * i <= N; i++)
    {

        // If N is divisible by i
        if (N % i == 0)
        {

            // Push the current divisor
            ans.Add(i);

            // If N is not a
            // perfect square
            if (N != (i * i))
            {

                // Push the second divisor
                ans.Add(N / i);
            }
        }
    }

    // Print the resultant array
    foreach(int it in ans)
    {
        Console.Write(it + " ");
    }
}

// Driver Code
public static void Main()
{
    int N = 12;

    // Function Call
    constructArray(N);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
// javascript program for the above approach

// Function to construct the array such
// the sum of values of Euler Totient
// functions of all array elements is N
function constructArray(N)
{

    // Stores the resultant array
    var ans = [];

    // Find divisors in sqrt(N)
    for(var i = 1; i * i <= N; i++)
    {

        // If N is divisible by i
        if (N % i == 0)
        {

            // Push the current divisor
            ans.push(i);

            // If N is not a
            // perfect square
            if (N != (i * i))
            {

                // Push the second divisor
                ans.push(N / i);
            }
        }
    }

    // Prvar the resultant array
    document.write(ans);
}

// Driver Code
var N = 12;

// Function Call
constructArray(N);

// This code contributed by shikhasingrajput
</script>
```

**Output:** 

```
1 12 2 6 3 4
```

***时间复杂度:** O(√N)*
***辅助空间:** O(N)*