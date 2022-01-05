# 计数具有与数字本身相等的 GCD 的数字

> 原文:[https://www . geesforgeks . org/count-numbers-having-gcd-with-n-等于数字本身/](https://www.geeksforgeeks.org/count-numbers-having-gcd-with-n-equal-to-the-number-itself/)

给定一个正整数 **N** ，任务是找出正整数的个数，其 [GCD 与给定的整数**N**T5】就是这个数本身。](https://www.geeksforgeeks.org/gcd-two-array-numbers/)

**示例:**

> **输入:** N = 5
> **输出:** 2
> **说明:**
> 以下是 GCD 以 N 为数字本身的数字:
> 
> 1.  数字 1: GCD(1，5) = 1。
> 2.  数字 1: GCD(5，5) = 5。
> 
> 因此，总计数为 2。
> 
> **输入:**N = 10
> T3】输出: 4

**方法:**给定的问题可以基于以下观察来解决:任意数量的 GCD(比如说 **K** )与 **N** 的必要条件是 **K** 当且仅当 **K** 是 **N** 的因子。所以思路是找到 **N** 的[因子个数。按照以下步骤解决问题:](https://www.geeksforgeeks.org/program-to-find-all-factors-of-a-number-using-recursion/)

*   初始化一个变量，说**计数**为 **0** ，计数 **N** 的因子数。
*   迭代范围**【1，sqrt(N)】**，并执行以下步骤:
    *   如果当前数字 **i** 除以给定的整数 **N** ，那么将**计数**增加 **1** 。
    *   如果 **i** 和 **N / i** 的值不相同，则按 **1** 递增**计数**。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count numbers whose
// GCD with N is the number itself
int countNumbers(int N)
{
    // Stores the count of factors of N
    int count = 0;

    // Iterate over the range [1, sqrt(N)]
    for (int i = 1; i * i <= N; i++) {

        // If i is divisible by i
        if (N % i == 0) {

            // Increment count
            count++;

            // Avoid counting the
            // same factor twice
            if (N / i != i) {
                count++;
            }
        }
    }

    // Return the resultant count
    return count;
}

// Driver Code
int main()
{
    int N = 10;
    cout << countNumbers(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function to count numbers whose
    // GCD with N is the number itself
    static int countNumbers(int N)
    {
        // Stores the count of factors of N
        int count = 0;

        // Iterate over the range [1, sqrt(N)]
        for (int i = 1; i * i <= N; i++) {

            // If i is divisible by i
            if (N % i == 0) {

                // Increment count
                count++;

                // Avoid counting the
                // same factor twice
                if (N / i != i) {
                    count++;
                }
            }
        }

        // Return the resultant count
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 10;
        System.out.println(countNumbers(N));
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count numbers whose
# GCD with N is the number itself
def countNumbers(N):

    # Stores the count of factors of N
    count = 0

    # Iterate over the range [1, sqrt(N)]
    for i in range(1, N + 1):
        if i * i > N:
            break

        # If i is divisible by i
        if (N % i == 0):

            # Increment count
            count += 1

            # Avoid counting the
            # same factor twice
            if (N // i != i):
                count += 1

    # Return the resultant count
    return count

# Driver Code
if __name__ == '__main__':

    N = 10
    print(countNumbers(N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
public class GFG {

    // Function to count numbers whose
    // GCD with N is the number itself
    static int countNumbers(int N)
    {
        // Stores the count of factors of N
        int count = 0;

        // Iterate over the range [1, sqrt(N)]
        for (int i = 1; i * i <= N; i++) {

            // If i is divisible by i
            if (N % i == 0) {

                // Increment count
                count++;

                // Avoid counting the
                // same factor twice
                if (N / i != i) {
                    count++;
                }
            }
        }

        // Return the resultant count
        return count;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int N = 10;
        Console.WriteLine(countNumbers(N));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count numbers whose
// GCD with N is the number itself
function countNumbers(N)
{
    // Stores the count of factors of N
    var count = 0;

    // Iterate over the range [1, sqrt(N)]
    for (i = 1; i * i <= N; i++) {

        // If i is divisible by i
        if (N % i == 0) {

            // Increment count
            count++;

            // Avoid counting the
            // same factor twice
            if (parseInt(N / i) != i) {
                count++;
            }
        }
    }

    // Return the resultant count
    return count;
}

// Driver Code
var N = 10;
document.write(countNumbers(N));

// This code is contributed by Amit Katiyar

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N<sup>1/2</sup>)*
***辅助空间:** O(1)*