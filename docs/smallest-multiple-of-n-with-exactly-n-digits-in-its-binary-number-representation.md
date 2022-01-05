# N 的最小倍数，其二进制数表示中正好有 N 个数字

> 原文:[https://www . geesforgeks . org/最小 n 倍数二进制数表示法/](https://www.geeksforgeeks.org/smallest-multiple-of-n-with-exactly-n-digits-in-its-binary-number-representation/)

给定一个正整数 **N** ，任务是找到 N 的最小倍数，在其[二进制数表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)中正好有 N 个数字。
**例:**

> **输入:** N = 3
> **输出:** 6
> **说明:**
> 6 是 3 的最小倍数，二进制中长度也是 3(110)。
> **输入:** N = 5
> **输出:** 20
> **说明:**
> 6 是 5 的最小倍数，在二进制中长度也是 5(10100)。

**进场:**思路是做一个观察。

*   如果我们仔细观察，一系列将形成 1，2，6，8，20，…
*   该系列的第 N 项将是:

> ![N*\lceil 2^\frac{N-1}{N} \rceil     ](img/315ab055fcb4b7d6bc00fd844646a6ff.png "Rendered by QuickLaTeX.com")

*   因此，以数字 N 为输入，实现上述公式。

以下是上述方法的实现:

## C++

```
// C++ program to find smallest
// multiple of n with exactly N
// digits in Binary number System.

#include <iostream>
#include <math.h>
using namespace std;

// Function to find smallest multiple
// of n with exactly n digits
// in Binary number representation.
void smallestNumber(int N)
{
    cout << N * ceil(pow(2,
                         (N - 1))
                     / N);
}

// Driver code
int main()
{
    int N = 3;
    smallestNumber(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find smallest
// multiple of n with exactly N
// digits in Binary Number System.
class GFG{

// Function to find smallest
// multiple of n with exactly N
// digits in Binary Number System.
static void smallestNumber(int N)
{
    System.out.print(N * Math.ceil
                        (Math.pow(2, (N - 1)) / N));
}

// Driver code
public static void main(String[] args)
{
    int N = 3;

    smallestNumber(N);
}
}

// This code is contributed by shubham
```

## 蟒蛇 3

```
# Python3 program to find smallest
# multiple of n with exactly N
# digits in Binary number System.
from math import ceil

# Function to find smallest multiple
# of n with exactly n digits
# in Binary number representation.
def smallestNumber(N):
    print(N * ceil(pow(2, (N - 1)) / N))

# Driver code
N = 3
smallestNumber(N)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to find smallest
// multiple of n with exactly N
// digits in Binary Number System.
using System;

class GFG{

// Function to find smallest
// multiple of n with exactly N
// digits in Binary Number System.
static void smallestNumber(int N)
{
    Console.Write(N * Math.Ceiling(
                      Math.Pow(2, (N - 1)) / N));
}

// Driver code
public static void Main(string[] args)
{
    int N = 3;

    smallestNumber(N);
}
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript program to find smallest
// multiple of n with exactly N
// digits in Binary number System.

// Function to find smallest multiple
// of n with exactly n digits
// in Binary number representation.
function smallestNumber(N)
{
    document.write(N * parseInt(Math.ceil(Math.pow(2,
                                 (N - 1))
                             / N)));
}

// Driver code
let N = 3;
smallestNumber(N);

// This code is contributed by rishavmahato348.
</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(n)*
T5**辅助空间:** O(1)