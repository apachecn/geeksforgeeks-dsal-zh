# 将前 N 个自然数分成两组，使得它们的和不是互质

> 原文:[https://www . geeksforgeeks . org/partition-first-n-自然数-in-two-set-这样-它们的和就不是互质/](https://www.geeksforgeeks.org/partition-first-n-natural-number-into-two-sets-such-that-their-sum-is-not-coprime/)

给定一个整数 **N** ，任务是将第一个 **N** 个自然数划分为两个非空集合，使得这些集合的和互不互质。如果可能，找到可能的分区，然后打印 **-1** 否则打印两组元素的总和。
**举例:**

> **输入:** N = 5
> **输出:** 10 5
> {1，2，3，4}和{5}是有效分区。
> **输入:** N = 2
> **输出:** -1

**进场:**

*   如果 **N ≤ 2** 那么打印 **-1** 作为唯一可能的分区是 **{1}** 和 **{2}** ，其中两个集合的和是互质的。
*   现在如果 **N 是奇数**，那么我们将 **N** 放在一组中，首先将**(N–1)**号放在其他组中。所以这两组的总和将是 **N** 和**N *(N–1)/2**，并且由于它们的 gcd 是 **N** ，所以它们彼此不会互质。
*   如果 **N 是偶数**，那么我们做和前面一样的事情，两组之和就是 **N** 和**N *(N–1)/2**。由于 **N** 为偶数，**(N–1)**不能被 2 整除，但 **N** 可整除，其和为**(N/2)*(N–1)**，其 gcd 为 **N / 2** 。由于 **N / 2** 是 **N** 的一个因子，所以它们互不互质。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the required sets
void find_set(int n)
{

    // Impossible case
    if (n <= 2) {
        cout << "-1";
        return;
    }

    // Sum of first n-1 natural numbers
    int sum1 = (n * (n - 1)) / 2;
    int sum2 = n;
    cout << sum1 << " " << sum2;
}

// Driver code
int main()
{
    int n = 8;
    find_set(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to find the required sets
static void find_set(int n)
{

    // Impossible case
    if (n <= 2)
    {
        System.out.println ("-1");
        return;
    }

    // Sum of first n-1 natural numbers
    int sum1 = (n * (n - 1)) / 2;
    int sum2 = n;
        System.out.println (sum1 + " " +sum2 );
}

// Driver code
public static void main (String[] args)
{

    int n = 8;
    find_set(n);
}
}

// This code is contributed by jit_t.
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to find the required sets
def find_set(n):

    # Impossible case
    if (n <= 2):
        print("-1");
        return;

    # Sum of first n-1 natural numbers
    sum1 = (n * (n - 1)) / 2;
    sum2 = n;
    print(sum1, " ", sum2);

# Driver code
n = 8;
find_set(n);

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find the required sets
static void find_set(int n)
{

    // Impossible case
    if (n <= 2)
    {
        Console.WriteLine("-1");
        return;
    }

    // Sum of first n-1 natural numbers
    int sum1 = (n * (n - 1)) / 2;
    int sum2 = n;
        Console.WriteLine(sum1 + " " +sum2 );
}

// Driver code
public static void Main ()
{

    int n = 8;
    find_set(n);
}
}

// This code is contributed by anuj_67...
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to find the required sets
    function find_set(n)
    {

        // Impossible case
        if (n <= 2)
        {
            document.write("-1");
            return;
        }

        // Sum of first n-1 natural numbers
        let sum1 = parseInt((n * (n - 1)) / 2, 10);
        let sum2 = n;
          document.write(sum1 + " " +sum2 + "</br>");
    }

    let n = 8;
    find_set(n);

</script>
```

**Output:** 

```
28 8
```

**时间复杂度:** O(1)