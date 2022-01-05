# 从包含给定数字作为后缀的给定范围中计数数字

> 原文:[https://www . geesforgeks . org/count-numbers-from-a-给定范围-包含给定数字作为后缀/](https://www.geeksforgeeks.org/count-numbers-from-a-given-range-that-contains-a-given-number-as-the-suffix/)

给定三个整数 **A、L** 和 **R** ，任务是从范围 **L** 到包含 **A** 作为后缀的 **R** 对数字进行计数。

**示例:**

> **输入:** A = 2，L = 2，R = 20
> **输出:** 2
> **说明:**
> 满足条件的给定范围内只有两个可能的数是 **2** 和 **12** 。
> 
> **输入:** A = 25，L = 25，R = 273
> **输出:** 3
> **说明:**
> 给定范围内满足条件的三个数分别为 25，125，225。

**天真法:**解决问题最简单的方法是遍历 **L** 到 **R** 范围内的数字，检查数字是否以 **A** 结尾。对于所有被发现为真的数字，将这些数字的计数增加 1。最后，打印最终计数。

***时间复杂度:** O(B)*
***辅助空间:** O(log <sub>2</sub> R)*

**高效方法:**要优化上述方法，请执行以下步骤:

*   计数并存储 **A** 的位数，并将其存储在一个变量中，比如说**计数。**
*   将 10 提升到 **A** 的位数的幂，即 10 <sup>计数</sup>。
*   检查每 10 个<sup>周期的计数</sup>是否在**【左，右】**范围内。如果发现为真，则将计数增加 1。
*   打印**计数**的最终值。

下面是上述方法的实现:

## C++

```
// C++ Program of the
// above approach

#include <bits/stdc++.h>

using namespace std;

// Function to count the number
// ends with given number in range
void countNumEnds(int A, int L, int R)
{
    int temp, count = 0, digits;
    int cycle;

    // Find number of digits in A
    digits = log10(A) + 1;

    // Find the power of 10
    temp = pow(10, digits);
    cycle = temp;

    while (temp <= R) {

        if (temp >= L)
            count++;

        // Incrementing the A
        temp += cycle;
    }

    cout << count;
}

// Driver Code
int main()
{
    int A = 2, L = 2, R = 20;

    // Function Call
    countNumEnds(A, L, R);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program of the
// above approach
class GFG{

// Function to count the number
// ends with given number in range
static void countNumEnds(int A,
                         int L, int R)
{
  int temp, count = 0, digits;
  int cycle;

  // Find number of digits in A
  digits = (int) (Math.log10(A) + 1);

  // Find the power of 10
  temp = (int) Math.pow(10, digits);
  cycle = temp;

  while (temp <= R)
  {
    if (temp >= L)
      count++;

    // Incrementing the A
    temp += cycle;
  }
  System.out.print(count);
}

// Driver Code
public static void main(String[] args)
{
  int A = 2, L = 2, R = 20;

  // Function Call
  countNumEnds(A, L, R);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program of the
# above approach
from math import log10

# Function to count the number
# ends with given number in range
def countNumEnds(A, L, R):

    count = 0

    # Find number of digits in A
    digits = int(log10(A) + 1)

    # Find the power of 10
    temp = int(pow(10, digits))
    cycle = temp

    while(temp <= R):
        if(temp >= L):
            count += 1

        # Incrementing the A
        temp += cycle

    print(count)

# Driver Code
A = 2
L = 2
R = 20

# Function call
countNumEnds(A, L, R)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program of the
// above approach
using System;

class GFG{

// Function to count the number
// ends with given number in range
static void countNumEnds(int A, int L,
                         int R)
{
    int temp, count = 0, digits;
    int cycle;

    // Find number of digits in A
    digits = (int)(Math.Log10(A) + 1);

    // Find the power of 10
    temp = (int)Math.Pow(10, digits);
    cycle = temp;

    while (temp <= R)
    {
        if (temp >= L)
        count++;

        // Incrementing the A
        temp += cycle;
    }
    Console.Write(count);
}

// Driver Code
public static void Main(String[] args)
{
    int A = 2, L = 2, R = 20;

    // Function call
    countNumEnds(A, L, R);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program for
// the above approach

// Function to count the number
// ends with given number in range
function countNumEnds(A, L, R)
{
  let temp = 0, count = 0, digits = 0;
  let cycle = 0;

  // Find number of digits in A
  digits = Math.round(Math.log10(A)) + 1;

  // Find the power of 10
  temp = Math.round(Math.pow(10, digits));
  cycle = temp;

  while (temp <= R)
  {
    if (temp >= L)
      count++;

    // Incrementing the A
    temp += cycle;
  }
  document.write(count);
}

// Driver code

  let A = 2, L = 2, R = 20;

  // Function Call
  countNumEnds(A, L, R);

  // This code is contributed by splevel62.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N)，其中 N 为范围。*
***辅助空间:** O(1)*