# 检查 N 是否可以划分为 K 个连续的元素，其和等于 N

> 原文:[https://www . geesforgeks . org/check-if-n-can-division-k-in-continuous-elements-with-sum-equal-n/](https://www.geeksforgeeks.org/check-if-n-can-be-divided-into-k-consecutive-elements-with-a-sum-equal-to-n/)

给定一个整数 **N** ，我们的任务是检查 **N** 是否可以划分为 **K** 个和等于 N 的连续元素，如果不能这样划分，打印 **-1** ，否则打印值 **K** 。
**示例:**

> **输入:** N = 12
> **输出:** 3
> **说明:**
> 整数 N = 12 可以分为 3 个连续的元素{3，4，5}，其中 3 + 4 + 5 = 12。
> **输入:** N = 8
> **输出:** -1
> **说明:**
> 整数 8 不可能这样划分。

**方法:**为了解决上面提到的问题，让我们将整数 **N** 分成 *i* 个连续的数字。序列的术语看起来像 **(d+1)、(d+2)、(d+3)…..(d+i)** 其中 d 是每个整数中存在的公共差，该序列的和应等于 **N** 。
所以，这些数的和也可以表示为:

> ![Sum = \frac{i*(i+1)}{2} + (i*d) = N    ](img/c0f77a14760d83e422632254e267a8af.png "Rendered by QuickLaTeX.com")

随着**和= i * (i + 1) / 2** 的二次增长，我们有，**N–和= i * d** 。因此，为了解决方案的存在，整数的数量应该平均分配数量**N-sum。**以下是步骤:

1.  从 2 开始从索引(比如 **i** )迭代。
2.  [求第一个 I 数的和](https://www.geeksforgeeks.org/sum-of-first-n-natural-numbers/)(说**和**)。
3.  对于任何迭代，如果**(N-sum)**可以被 I 整除，那么打印 **i** 的值。
4.  对于任何迭代，如果 N 超过总和，则打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the K consecutive
// elements with a sum equal to N
void canBreakN(long long n)
{
    // Iterate over [2, INF]
    for (long long i = 2;; i++) {

        // Store the sum
        long long m = i * (i + 1) / 2;

        // If the sum exceeds N
        // then break the loop
        if (m > n)
            break;

        long long k = n - m;

        // Common difference should be
        // divisible by number of terms
        if (k % i)
            continue;

        // Print value of i & return
        cout << i << endl;
        return;
    }

    // Print "-1" if not possible
    // to break N
    cout << "-1";
}

// Driver Code
int main()
{
    // Given N
    long long N = 12;

    // Function Call
    canBreakN(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the K consecutive
// elements with a sum equal to N
public static void canBreakN(long n)
{

    // Iterate over [2, INF]
    for(long i = 2;; i++)
    {

        // Store the sum
        long m = i * (i + 1) / 2;

        // If the sum exceeds N
        // then break the loop
        if (m > n)
            break;

        long k = n - m;

        // Common difference should be
        // divisible by number of terms
        if (k % i != 0)
            continue;

        // Print value of i & return
        System.out.println(i);
        return;
    }

    // Print "-1" if not possible
    // to break N
    System.out.println("-1");
}

// Driver Code
public static void main(String[] args)
{

    // Given N
    long N = 12;

    // Function call
    canBreakN(N);
}
}

// This code is contributed by jrishabh99
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the K consecutive
# elements with a sum equal to N
def canBreakN(n):

    # Iterate over [2, INF]
    for i in range(2, n):

        # Store the sum
        m = i * (i + 1) // 2

        # If the sum exceeds N
        # then break the loop
        if (m > n):
            break

        k = n - m

        # Common difference should be
        # divisible by number of terms
        if (k % i):
            continue

        # Print value of i & return
        print(i)
        return

    # Print "-1" if not possible
    # to break N
    print("-1")

# Driver Code

# Given N
N = 12

# Function call
canBreakN(N)

# This code is contributed by code_hunt
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find the K consecutive
// elements with a sum equal to N
public static void canBreakN(long n)
{

    // Iterate over [2, INF]
    for(long i = 2;; i++)
    {

        // Store the sum
        long m = i * (i + 1) / 2;

        // If the sum exceeds N
        // then break the loop
        if (m > n)
            break;

        long k = n - m;

        // Common difference should be
        // divisible by number of terms
        if (k % i != 0)
            continue;

        // Print value of i & return
        Console.Write(i);
        return;
    }

    // Print "-1" if not possible
    // to break N
    Console.Write("-1");
}

// Driver Code
public static void Main(string[] args)
{

    // Given N
    long N = 12;

    // Function call
    canBreakN(N);
}
}

// This code is contributed by rock_cool
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to find the K consecutive
    // elements with a sum equal to N
    function canBreakN(n)
    {

        // Iterate over [2, INF]
        for(let i = 2;; i++)
        {

            // Store the sum
            let m = parseInt(i * (i + 1) / 2, 10);

            // If the sum exceeds N
            // then break the loop
            if (m > n)
                break;

            let k = n - m;

            // Common difference should be
            // divisible by number of terms
            if (k % i != 0)
                continue;

            // Print value of i & return
            document.write(i);
            return;
        }

        // Print "-1" if not possible
        // to break N
        document.write("-1");
    }

    // Given N
    let N = 12;

    // Function call
    canBreakN(N);

// This code is contributed by sureh07.
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(K)，其中 K 为和为 K 的元素个数*
***辅助空间:** O(1)*