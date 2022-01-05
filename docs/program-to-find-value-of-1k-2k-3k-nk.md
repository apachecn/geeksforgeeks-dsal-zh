# 程序寻找 1^k + 2^k + 3^k + … + n^k 的价值

> 原文:[https://www . geesforgeks . org/program-to-find-value-1k-2k-3k-NK/](https://www.geeksforgeeks.org/program-to-find-value-of-1k-2k-3k-nk/)

给定两个正整数 **N** 和 **K** 。任务是评估 1<sup>K</sup>+2<sup>K</sup>+3<sup>K</sup>+…+N<sup>K</sup>的值。
**示例**

> **输入:** N = 3，K = 4
> **输出:** 98
> **解释:**
> ∑(x<sup>4</sup>)= 1<sup>4</sup>+2<sup>4</sup>+3<sup>4</sup>，其中 1≤x≤N
> ∑(x<sup>4</sup>)= 1+16+81【t21

**进场:**

1.  想法是利用 [pow()](https://www.geeksforgeeks.org/power-function-cc/) 函数求**x<sup>K</sup>T3】的值。(其中 x 为 1 至 N)。**
2.  所需的总和是上面计算的所有值的总和。

以下是上述方法的实现:

## C++

```
// C++ Program to find the value
// 1^K + 2^K + 3^K + .. + N^K
#include <bits/stdc++.h>
using namespace std;

// Function to find value of
// 1^K + 2^K + 3^K + .. + N^K
int findSum(int N, int k)
{
    // Initialise sum to 0
    int sum = 0;
    for (int i = 1; i <= N; i++) {

        // Find the value of
        // pow(i, 4) and then
        // add it to the sum
        sum += pow(i, k);
    }

    // Return the sum
    return sum;
}

// Drivers Code
int main()
{
    int N = 8, k = 4;

    // Function call to
    // find the sum
    cout << findSum(N, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the value
// 1^K + 2^K + 3^K + .. + N^K
class GFG {

    // Function to find value of
    // 1^K + 2^K + 3^K + .. + N^K
    static int findSum(int N, int k)
    {
        // Initialise sum to 0
        int sum = 0;
        for (int i = 1; i <= N; i++) {

            // Find the value of
            // pow(i, 4) and then
            // add it to the sum
            sum += (int)Math.pow(i, k);
        }

        // Return the sum
        return sum;
    }

    // Drivers Code
    public static void main (String[] args)
    {
        int N = 8, k = 4;

        // Function call to
        // find the sum
        System.out.println(findSum(N, k));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python 3 Program to find the value
# 1^K + 2^K + 3^K + .. + N^K
from math import pow

# Function to find value of
# 1^K + 2^K + 3^K + .. + N^K
def findSum(N, k):

    # Initialise sum to 0
    sum = 0
    for i in range(1, N + 1, 1):

        # Find the value of
        # pow(i, 4) and then
        # add it to the sum
        sum += pow(i, k)

    # Return the sum
    return sum

# Drives Code
if __name__ == '__main__':
    N = 8
    k = 4

    # Function call to
    # find the sum
    print(int(findSum(N, k)))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# Program to find the value
// 1^K + 2^K + 3^K + .. + N^K

using System;

public class GFG {

    // Function to find value of
    // 1^K + 2^K + 3^K + .. + N^K
    static int findSum(int N, int k)
    {
        // Initialise sum to 0
        int sum = 0;
        for (int i = 1; i <= N; i++) {

            // Find the value of
            // pow(i, 4) and then
            // add it to the sum
            sum += (int)Math.Pow(i, k);
        }

        // Return the sum
        return sum;
    }

    // Drivers Code
    public static void Main (string[] args)
    {
        int N = 8, k = 4;

        // Function call to
        // find the sum
        Console.WriteLine(findSum(N, k));
    }

}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
    // Javascript Program to find the value
    // 1^K + 2^K + 3^K + .. + N^K

    // Function to find value of
    // 1^K + 2^K + 3^K + .. + N^K
    function findSum(N, k)
    {
        // Initialise sum to 0
        let sum = 0;
        for (let i = 1; i <= N; i++) {

            // Find the value of
            // pow(i, 4) and then
            // add it to the sum
            sum += Math.pow(i, k);
        }

        // Return the sum
        return sum;
    }

    let N = 8, k = 4;

    // Function call to
    // find the sum
    document.write(findSum(N, k));

// This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
8772
```

**时间复杂度:** O(N)