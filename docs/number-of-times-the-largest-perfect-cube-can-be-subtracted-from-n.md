# 从 N 中减去最大完美立方体的次数

> 原文:[https://www . geeksforgeeks . org/最大完美立方体可从 n 中减去的次数/](https://www.geeksforgeeks.org/number-of-times-the-largest-perfect-cube-can-be-subtracted-from-n/)

给定一个数字 **N** ，在每一步中，从 N 中减去最大的完美立方体(≤ N)。当 **N > 0** 时，重复这一步。任务是计算可以执行的步骤数。

**示例:**

> **输入:** N = 100
> **输出:** 4
> 第一步，100 –( 4 * 4 * 4)= 100–64 = 36
> 第二步，36 –( 3 * 3 * 3)= 36–27 = 9
> 第三步，9–(2 * 2 * 2)= 9–8 = 1
> 第四步，1–(1 * 1 * 1)= 1–1 = 0
> 
> **输入:** N = 150
> **输出:** 5
> 第一步，150 –( 5 * 5 * 5)= 150–125 = 25
> 第二步，25 –( 2 * 2 * 2)= 25–8 = 17
> 第三步，17–(2 * 2 * 2)= 17–8 = 9
> 第四步，9–(2 * 2 * 2)= 9–8 = 1
> 第五步

**接近**:

*   得到一个数，从这个数中最大的完美立方体必须被缩小。
*   找到数字的立方根，并将结果转换为整数。数字的立方根可能在小数之后包含一些分数部分，这需要避免。
*   减去上一步中找到的整数的立方。这将从上面步骤中的数字中移除最大可能的完美立方体。

```
N = N - ((int) ∛N)3
```

*   用减少的数字重复上述两个步骤，直到它大于 0。
*   打印一个完美立方体从 n 减少的次数。这是最终结果。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the count of steps
int countSteps(int n)
{

    // Variable to store the count of steps
    int steps = 0;

    // Iterate while N > 0
    while (n) {

        // Get the largest perfect cube
        // and subtract it from N
        int largest = cbrt(n);
        n -= (largest * largest * largest);

        // Increment steps
        steps++;
    }

    // Return the required count
    return steps;
}

// Driver code
int main()
{
    int n = 150;
    cout << countSteps(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG{

// Function to return the count of steps
static int countSteps(int n)
{

    // Variable to store the count of steps
    int steps = 0;

    // Iterate while N > 0
    while (n > 0) {

        // Get the largest perfect cube
        // and subtract it from N
        int largest = (int) Math.cbrt(n);
        n -= (largest * largest * largest);

        // Increment steps
        steps++;
    }

    // Return the required count
    return steps;
}

// Driver code
public static void main(String[] args)
{
    int n = 150;
    System.out.print(countSteps(n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import floor

# Function to return the count of steps
def countSteps(n):

    # Variable to store the count of steps
    steps = 0

    # Iterate while N > 0
    while (n):

        # Get the largest perfect cube
        # and subtract it from N
        largest = floor(n**(1/3))
        n -= (largest * largest * largest)

        # Increment steps
        steps += 1

    # Return the required count
    return steps

# Driver code
n = 150
print(countSteps(n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

// Function to return the count of steps
static int countSteps(int n)
{

    // Variable to store the count of steps
    int steps = 0;

    // Iterate while N > 0
    while (n > 0) {

        // Get the largest perfect cube
        // and subtract it from N
        int largest = (int) Math.Pow(n,(double)1/3);
        n -= (largest * largest * largest);

        // Increment steps
        steps++;
    }

    // Return the required count
    return steps;
}

// Driver code
public static void Main(String[] args)
{
    int n = 150;
    Console.Write(countSteps(n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the count of steps
function countSteps(n)
{

    // Variable to store the count of steps
    let steps = 0;

    // Iterate while N > 0
    while (n)
    {

        // Get the largest perfect cube
        // and subtract it from N
        let largest = Math.floor(Math.cbrt(n));
        n -= (largest * largest * largest);

        // Increment steps
        steps++;
    }

    // Return the required count
    return steps;
}

// Driver code
let n = 150;

document.write(countSteps(n));

// This code is contributed by Manoj.

</script>
```

**Output:** 

```
5
```