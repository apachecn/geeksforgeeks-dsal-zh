# 去掉 K 个数字后可能的最大数字

> 原文:[https://www . geeksforgeeks . org/k 位数去除后的最大可能数/](https://www.geeksforgeeks.org/largest-number-possible-after-removal-of-k-digits/)

给定一个正数 **N** ，目标是从 **N** 中去掉任意一个 **K** 数字后，找到能形成的最大数字。
**举例:**

> **输入:** N = 6358，K = 1
> **输出:** 658
> **输入:** N = 2589，K = 2
> **输出:** 89

**进场:**

*   重复一个循环 **K** 次。
*   在每次迭代过程中，从 **N** 的当前值中删除每个数字一次，并存储所获得的所有数字的最大值。
*   为了实现这一点，我们存储 **(N / (i * 10)) * i + (N % i)** 的最大值，其中 I 的范围为**【1，10<sup>l–1</sup>**其中 l 表示 **N** 当前值的位数。
*   将该最大值视为 **N** 的当前值，继续下一次迭代，重复上述步骤。
*   因此，在每次迭代之后，我们从 **N** 的当前值中移除最少的数字。在重复过程 **K** 次时，我们获得了可能的最大数量。

**例如:**

> 让我们针对 N = 6358，K = 1
> 来分析这种方法，去掉每个数字一次后的不同可能性如下:
> (6358/10)* 1+6358% 1 = 635+0 = 635
> (6358/100)* 10+6358% 10 = 630+8 = 638
> (6358/1000)* 100+6358% 100 = 638

以下是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the
// largest number possible
int maxnumber(int n, int k)
{
    // Generate the largest number
    // after removal of the least
    // K digits one by one
    for (int j = 0; j < k; j++) {

        int ans = 0;
        int i = 1;

        // Remove the least digit
        // after every iteration
        while (n / i > 0) {

            // Store the numbers formed after
            // removing every digit once
            int temp = (n / (i * 10))
                           * i
                       + (n % i);
            i *= 10;

            // Compare and store the maximum
            ans = max(ans, temp);
        }

        // Store the largest
        // number remaining
        n = ans;
    }

    // Return the remaining number
    // after K removals
    return n;
}

// Driver code
int main()
{
    int n = 6358;
    int k = 1;

    cout << maxnumber(n, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.util.*;
import java.math.*;

class GFG {

    // Function to return the
    // largest number possible
    static int maxnumber(int n, int k)
    {
        // Generate the largest number
        // after removal of the least
        // K digits one by one
        for (int j = 0; j < k; j++) {

            int ans = 0;
            int i = 1;

            // Remove the least digit
            // after every iteration
            while (n / i > 0) {

                // Store the numbers formed after
                // removing every digit once
                int temp = (n / (i * 10))
                               * i
                           + (n % i);
                i *= 10;

                // Compare and store the maximum
                ans = Math.max(ans, temp);
            }
            n = ans;
        }

        // Return the remaining number
        // after K removals
        return n;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 6358;
        int k = 1;

        System.out.println(maxnumber(n, k));
    }
}
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

def maxnumber(n, k):
# Function to return the
# largest number possible

    for i in range(0, k):
        # Generate the largest number
        # after removal of the least K digits
        # one by one
        ans = 0
        i = 1

        while n // i > 0:
        # Remove the least digit
        # after every iteration
            temp = (n//(i * 10))*i + (n % i)
            i *= 10
        # Store the numbers formed after
        # removing every digit once

        # Compare and store the maximum
            if temp > ans:
                ans = temp
        n = ans       

    # Return the remaining number
    # after K removals
    return ans;

n = 6358
k = 1
print(maxnumber(n, k))
```

## C#

```
// C# program to implement
// the above approach

using System;

class GFG {

    // Function to return the
    // largest number possible
    static int maxnumber(int n, int k)
    {
        // Generate the largest number
        // after removal of the least
        // K digits one by one
        for (int j = 0; j < k; j++) {

            int ans = 0;
            int i = 1;

            // Remove the least digit
            // after every iteration
            while (n / i > 0) {

                // Store the numbers formed after
                // removing every digit once
                int temp = (n / (i * 10))
                               * i
                           + (n % i);
                i *= 10;

                // Compare and store the maximum
                if (temp > ans)
                    ans = temp;
            }

            // Store the largest
            // number remaining
            n = ans;
        }

        // Return the remaining number
        // after K removals
        return n;
    }

    // Driver code
    static public void Main()
    {
        int n = 6358;
        int k = 1;
        Console.WriteLine(maxnumber(n, k));
    }
}
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to return the
// largest number possible
function maxnumber(n, k)
{
    // Generate the largest number
    // after removal of the least
    // K digits one by one
    for (var j = 0; j < k; j++) {

        var ans = 0;
        var i = 1;

        // Remove the least digit
        // after every iteration
        while (parseInt(n / i) > 0) {

            // Store the numbers formed after
            // removing every digit once
            var temp = parseInt(n / (i * 10))
                           * i
                       + (n % i);
            i *= 10;

            // Compare and store the maximum
            ans = Math.max(ans, temp);
        }

        // Store the largest
        // number remaining
        n = ans;
    }

    // Return the remaining number
    // after K removals
    return n;
}

// Driver code
var n = 6358;
var k = 1;
document.write( maxnumber(n, k));

</script>
```

**Output:** 

```
658
```

时间复杂度:0(对数 <sub>10</sub> N)

辅助空间:0(1)