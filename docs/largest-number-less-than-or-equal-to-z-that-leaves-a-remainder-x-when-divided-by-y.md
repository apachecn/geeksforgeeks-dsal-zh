# 小于或等于 Z 的最大数字，除以 Y 后剩余 X

> 原文:[https://www . geeksforgeeks . org/最大数字小于或等于 z，当除以 y 时会留下余数 x/](https://www.geeksforgeeks.org/largest-number-less-than-or-equal-to-z-that-leaves-a-remainder-x-when-divided-by-y/)

给定三个整数 **x，y，z** ，任务是找到小于或等于 z 的最大非负数，当除以 y 时剩下余数 x(给定 x < y)。如果不存在这样的数字，那么输出将是-1。

**示例:**

```
Input: x = 1, y = 5, z = 8
Output: 6
Explanation:
6 is the largest number less than 8 
which when divided by 5 
leaves a remainder 1.

Input: x = 4, y = 6, z = 3
Output: -1
Explanation:
Since no such number exists the output is -1
```

**方法:**要解决上面提到的问题，第一个观察是如果 **x > z** 那么答案是不可能的，所以输出将是-1。
要求的数字为 **p** 。下面是解决这个问题的两个公式:

*   p * y + x = 0
*   p * y < =(z–x)

为了找到答案，我们需要找到 **p** 的值。所以，

```
p = (z - x) / y
```

在计算 **p** 之后，我们可以简单地找到答案，即

```
p * y + x
```

**以下是上述方法的实现:**

## C++

```
// C++ implementation to Find the
// largest non-negative number that
// is less than or equal to integer Z
// and leaves a remainder X when divided by Y

#include <bits/stdc++.h>
using namespace std;

// Function to get the number
int get(int x, int y, int z)
{

    // remainder can't be larger
    // than the largest number,
    // if so then answer doesn't exist.
    if (x > z)
        return -1;

    // reduce number by x
    int val = z - x;

    // finding the possible
    // number that is divisible by y
    int div = (z - x) / y;

    // this number is always <= x
    // as we calculated over z - x
    int ans = div * y + x;

    return ans;
}

// Driver Code
int main()
{
    // initialise the three integers
    int x = 1, y = 5, z = 8;

    cout << get(x, y, z) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to Find the
// largest non-negative number that
// is less than or equal to integer Z
// and leaves a remainder X when divided by Y
class GFG{

// Function to get the number
static int get(int x, int y, int z)
{

    // remainder can't be larger
    // than the largest number,
    // if so then answer doesn't exist.
    if (x > z)
        return -1;

    // reduce number by x
    int val = z - x;

    // finding the possible
    // number that is divisible by y
    int div = (z - x) / y;

    // this number is always <= x
    // as we calculated over z - x
    int ans = div * y + x;

    return ans;
}

// Driver Code
public static void main(String[] args)
{
    // initialise the three integers
    int x = 1, y = 5, z = 8;

    System.out.print(get(x, y, z)+ "\n");
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python implementation to Find the
# largest non-negative number that
# is less than or equal to integer Z
# and leaves a remainder X when divided by Y

# Function to get the number
def get(x, y, z):

    # remainder can't be larger
    # than the largest number,
    # if so then answer doesn't exist.
    if (x > z):
        return -1

    # reduce number by x
    val = z - x

    # finding the possible
    # number that is divisible by y
    div = (z - x) // y

    # this number is always <= x
    # as we calculated over z - x
    ans = div * y + x

    return ans

# Driver Code
# initialise the three integers
x = 1
y = 5
z = 8

print(get(x, y, z))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# implementation to Find the
// largest non-negative number that
// is less than or equal to integer Z
// and leaves a remainder X when divided by Y
using System;

class GFG{

// Function to get the number
static int get(int x, int y, int z)
{

    // remainder can't be larger
    // than the largest number,
    // if so then answer doesn't exist.
    if (x > z)
        return -1;

    // reduce number by x
    int val = z - x;

    // finding the possible
    // number that is divisible by y
    int div = (z - x) / y;

    // this number is always <= x
    // as we calculated over z - x
    int ans = div * y + x;

    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    // initialise the three integers
    int x = 1, y = 5, z = 8;

    Console.Write(get(x, y, z)+ "\n");
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript implementation to Find the
// largest non-negative number that
// is less than or equal to integer Z
// and leaves a remainder X when divided by Y

// Function to get the number
function get(x, y, z)
{

    // remainder can't be larger
    // than the largest number,
    // if so then answer doesn't exist.
    if (x > z)
        return -1;

    // reduce number by x
    let val = z - x;

    // finding the possible
    // number that is divisible by y
    let div = Math.floor((z - x) / y);

    // this number is always <= x
    // as we calculated over z - x
    let ans = div * y + x;

    return ans;
}

// Driver Code

    // initialise the three integers
    let x = 1, y = 5, z = 8;

    document.write(get(x, y, z)+ "\n");

</script>
```

**Output:** 

```
6
```

**时间复杂度:** O(1)

**辅助空间:** O(1)