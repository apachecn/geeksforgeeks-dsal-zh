# 小于 N 的最大数 M，使得 M 和 N 的异或为偶数

> 原文:[https://www . geesforgeks . org/最大数-m-小于-n-这样-m 和-n 的异或为偶数/](https://www.geeksforgeeks.org/largest-number-m-less-than-n-such-that-xor-of-m-and-n-is-even/)

给定一个正整数 **N** ，任务是找到最大的整数 **M** ，使得 **0 < = M < N** 和 **XOR(M，N)** 为偶数。如果给定的 **N** 不能得到这样的 M 值，打印 **-1** 。

**示例:**

> **输入:** N = 10
> **输出:** 8
> **解释:**
> (10 XOR 9) = 3，所以 M = 9 是不可能的，因为 3 不是偶数。
> (10 异或 8) = 2，所以 M = 8 是可能的，因为它是满足必要条件的 M 的最大可能值。
> 
> **输入:** N = 5
> **输出:** 3
> (5 异或 4) = 1，所以 M = 4 是不可能的，因为 1 不是偶数。
> (5 异或 3) = 6，所以 M = 3 是可能的，因为 6 是偶数，3 是 M 的最大可能值(小于 N)。

**方法:**
解决问题时需要进行以下观察:

*   以二进制形式表示的奇数的最低有效位为 1，而以二进制形式表示的偶数的最低有效位为 0。
*   执行**异或**运算时，如果设置的位数为奇数，则异或值为 1。如果设置的位数是偶数，那么异或值将是 0。
*   因此，我们需要对两个奇数或两个偶数进行异或运算，从而得到一个偶数。

根据以上解释，可以通过以下步骤解决问题:

1.  如果 N 为奇数，小于 N 的最大奇数为**N–2**。
2.  如果 N 为偶数，小于 N 的最大偶数为**N–2**。
3.  因此，如果 N = 1，在这种情况下不能获得作为合适 M 的 print -1。对于所有其他情况，打印**N–2**作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above problem.
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// possible value of M
int getM(int n)
{
    // Edge case
    if (n == 1)
        return -1;

    // M = N - 2 is maximum
    // possible value
    else
        return n - 2;
}

// Driver Code
int main()
{
    int n = 10;

    int ans = getM(n);
    cout << ans;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above problem.
import java.util.*;

class GFG{

// Function to find the maximum
// possible value of M
static int getM(int n)
{

    // Edge case
    if (n == 1)
        return -1;

    // M = N - 2 is maximum
    // possible value
    else
        return n - 2;
}

// Driver code
public static void main(String[] args)
{
    int n = 10;

    System.out.print(getM(n));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above problem

# Function to find the maximum
# possible value of M
def getM(n):

    # Edge case
    if (n == 1):
        return -1;

    # M = N - 2 is maximum
    # possible value
    else:
        return n - 2;                

# Driver code
n = 10

print(getM(n))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above problem.
using System;
class GFG{

// Function to find the maximum
// possible value of M
static int getM(int n)
{

    // Edge case
    if (n == 1)
        return -1;

    // M = N - 2 is maximum
    // possible value
    else
        return n - 2;
}

// Driver code
static void Main()
{
    int n = 10;

    Console.Write(getM(n));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program for the above problem.

// Function to find the maximum
// possible value of M
function getM(n)
{
        // Edge case
    if (n == 1)
        return -1;

    // M = N - 2 is maximum
    // possible value
    else
        return n - 2;
}

// Driver code
var n = 10;

document.write(getM(n));

// This code is contributed by Khushboogoyal499

</script>
```

**Output:** 

```
8
```

***时间复杂度:** O(1)*
***辅助空间:** O(1)*