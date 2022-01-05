# 最大数量 M，其比特数为 N，使得它们的“或”和“异或”值之间的差值最大化

> 原文:[https://www . geeksforgeeks . org/最大位数 m 具有 n 的位数，使得它们的或与异或值之间的差值最大化/](https://www.geeksforgeeks.org/largest-number-m-having-bit-count-of-n-such-that-difference-between-their-or-and-xor-value-is-maximized/)

给定一个自然数 **N** ，任务是找到最大的数 **M** ,该数在二进制表示中具有与 **N** 相同的长度，使得 **N |** **M** 和 **N ^ M** 之间的差值最大。

**示例:**

> **输入:** N = 6
> **输出:** 7
> **解释:**
> 二进制表示中与 N 长度相同的所有数字都是 4、5、6、7。
> (6 | 4)–(6 ^ 4)= 4
> (6 | 5)–(6 ^ 5)= 4
> (6 | 6)–(6 ^ 6)= 6
> (6 | 7)–(6 ^ 7)= 6
> 因此(n | m)–(n ^ m)最大的最大 m 为 7
> 
> **输入:** N = 10
> **输出:** 15
> **解释:**
> 在二进制表示中与 10 长度相同的最大数 M = 15， **N |** **M** 与 **N ^ M** 的差值最大。

**天真的方法:**的想法是简单地找出二进制表示中所有长度与 **N** 相同的数字，然后对每个数字进行迭代，找出最大的**t5**T7**(n | I)–(n ^ I)**最大值。****

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效方法:**思路是初始化 **M = 0** 并在 N(比如 **i** )中一点一点迭代，根据以下 2 个观察设置或取消设置 **M** 的**I<sup>th</sup>T9】位:**

*   当 n 的 i <sup>第</sup>位被**设置**时:在这种情况下，如果我们**取消设置**m 的 i <sup>第</sup>位，则 **N | M** 和 **N^M** 的 i <sup>第</sup>位都将被设置，而在设置 m 的该位时, **N|M** 的 i <sup>第</sup>位将被设置并且**因此，设置 **M** 的该位是最佳的。**
*   当 n 的 i <sup>第</sup>位被**取消设置时:**在这种情况下，如果我们**设置M 的这个位, **N|M** 和 N^M 都将设置这个位，或者在保持 m 的这个位不被设置时, **N|M** 和 **N^M** 都将设置这个位。因此，在这种情况下，我们不能增加它们之间的差异，但是由于要求是尽可能输出最大 **M** ，因此设置 **M** 的该位。**
*   从以上观察，很明显 **M** 将设置所有的位。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the largest number
// M having the same length in binary
// form as N such that the difference
// between N | M and N ^ M is maximum
int maxORminusXOR(int N)
{
    // Find the most significant
    // bit of N
    int MSB = log2(N);

    // Initialize M
    int M = 0;

    // Set all the bits of M
    for (int i = 0; i <= MSB; i++)
        M += (1 << i);

    // Return the answer
    return M;
}

// Driver Code
int main()
{
    // Given Number N
    int N = 10;

    // Function Call
    cout << maxORminusXOR(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the largest number
// M having the same length in binary
// form as N such that the difference
// between N | M and N ^ M is maximum
static int maxORminusXOR(int N)
{

    // Find the most significant
    // bit of N
    int MSB = (int)Math.ceil(Math.log(N));

    // Initialize M
    int M = 0;

    // Set all the bits of M
    for(int i = 0; i <= MSB; i++)
        M += (1 << i);

    // Return the answer
    return M;
}

// Driver Code
public static void main(String[] args)
{

    // Given number N
    int N = 10;

    // Function call
    System.out.print(maxORminusXOR(N));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to find the largest number
# M having the same length in binary
# form as N such that the difference
# between N | M and N ^ M is maximum
def maxORminusXOR(N):

    # Find the most significant
    # bit of N
    MSB = int(math.log2(N));

    # Initialize M
    M = 0

    # Set all the bits of M
    for i in range(MSB + 1):
        M += (1 << i)

    # Return the answer
    return M

# Driver code
if __name__ == '__main__':

    # Given Number N
    N = 10

    # Function call
    print(maxORminusXOR(N))

# This code is contributed by jana_sayantan
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the largest number
// M having the same length in binary
// form as N such that the difference
// between N | M and N ^ M is maximum
static int maxORminusXOR(int N)
{

    // Find the most significant
    // bit of N
    int MSB = (int)Math.Ceiling(Math.Log(N));

    // Initialize M
    int M = 0;

    // Set all the bits of M
    for(int i = 0; i <= MSB; i++)
        M += (1 << i);

    // Return the answer
    return M;
}

// Driver Code
public static void Main(String[] args)
{

    // Given number N
    int N = 10;

    // Function call
    Console.Write(maxORminusXOR(N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to find the largest number
// M having the same length in binary
// form as N such that the difference
// between N | M and N ^ M is maximum
function maxORminusXOR(N)
{

    // Find the most significant
    // bit of N
    let MSB = Math.ceil(Math.log(N));

    // Initialize M
    let M = 0;

    // Set all the bits of M
    for(let i = 0; i <= MSB; i++)
        M += (1 << i);

    // Return the answer
    return M;
}

// Driver code

    // Given number N
    let N = 10;

    // Function call
    document.write(maxORminusXOR(N));

  // This code is contributed by code_hunt.
</script>
```

**Output:** 

```
15
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*