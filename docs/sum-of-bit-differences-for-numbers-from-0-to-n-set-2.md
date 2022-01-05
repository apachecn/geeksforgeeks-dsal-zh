# 从 0 到 N 的数字的位差之和|集合 2

> 原文:[https://www . geesforgeks . org/0 到 n-set-2 数字的位差总和/](https://www.geeksforgeeks.org/sum-of-bit-differences-for-numbers-from-0-to-n-set-2/)

给定一个数字 **N** ，任务是为从 **0 到 N** 的每个连续数字计算二进制表示中对应不同位的[总数。](https://www.geeksforgeeks.org/number-of-mismatching-bits-in-the-binary-representation-of-two-integers/)

**示例:**

> **输入:** N = 5
> **输出:** 8
> **解释:**
> 数字的二进制表示为:
> 0 - > 000、
> 1 - > 001、
> 2 - > 010、
> 3 - > 011、
> 4 - > 100、
> 5->101
> 1 和 0 之间- > 1 位不同
> 2 和 1 之间- > 2 位不同
> 3 和 2 之间- > 1 位不同
> 4 和 3 之间- > 3 位不同
> 5 和 4 之间- > 1 位不同
> T21 总计= 1+2+1+3+1 = 8
> T24

关于天真高效的方法，请参考本文[之前的帖子](https://www.geeksforgeeks.org/sum-of-bit-differences-for-numbers-from-0-to-n/)。
**更高效的方法:**为了优化上述方法，我们可以使用[递归](https://www.geeksforgeeks.org/recursion/)。要解决这个问题，需要进行以下观察

```
Number:     0 1 2 3 4  5  6  7
Difference: 1 2 1 3 1  2  1  4
Sum:        1 3 4 7 8 10 11 15
```

我们可以观察到对于**N =【1，2，3，4，…..】**，连续元素中不同位的和形成序列**【1，3，4，7，8，…】**。因此，本系列的 **N <sup>第</sup>** 项将是我们需要的答案，可计算为:

> a(n)= a(n/2)+n；基本情况为 a(1) = 1

以下是上述递归方法的实现:

## C++

```
// C++ program to find the sum
// of bit differences between
// consecutive numbers
// from 0 to N using recursion

#include <bits/stdc++.h>
using namespace std;

// Recursive function to find sum
// of different bits between
// consecutive numbers from 0 to N
int totalCountDifference(int n)
{

    // Base case
    if (n == 1)
        return 1;

    // Calculate the Nth term
    return n
           + totalCountDifference(n / 2);
}

// Driver Code
int main()
{
    // Given Number
    int N = 5;

    // Function Call
    cout << totalCountDifference(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum
// of bit differences between
// consecutive numbers from
// 0 to N using recursion
class GFG{

// Recursive function to find sum
// of different bits between
// consecutive numbers from 0 to N
static int totalCountDifference(int n)
{

    // Base case
    if (n == 1)
        return 1;

    // Calculate the Nth term
    return n + totalCountDifference(n / 2);
}

// Driver Code
public static void main(String[] args)
{

    // Given number
    int N = 5;

    // Function call
    System.out.println(totalCountDifference(N));
}
}

// This code is contributed by himanshu77
```

## 蟒蛇 3

```
# Python3 program to find the sum
# of bit differences between
# consecutive numbers from
# 0 to N using recursion

# Recursive function to find sum
# of different bits between
# consecutive numbers from 0 to N
def totalCountDifference (n):

    # Base case
    if (n == 1):
        return 1

    # Calculate the Nth term
    return n + totalCountDifference(n // 2)

# Driver code

# Given number
N = 5

# Function call
print(totalCountDifference(N))

# This code is contributed by himanshu77
```

## C#

```
// C# program to find the sum
// of bit differences between
// consecutive numbers from
// 0 to N using recursion
using System;

class GFG{

// Recursive function to find sum
// of different bits between
// consecutive numbers from 0 to N
static int totalCountDifference(int n)
{

    // Base case
    if (n == 1)
        return 1;

    // Calculate the Nth term
    return n + totalCountDifference(n / 2);
}

// Driver Code
public static void Main()
{

    // Given number
    int N = 5;

    // Function call
    Console.WriteLine(totalCountDifference(N));
}
}

// This code is contributed by himanshu77
```

## java 描述语言

```
<script>
// JavaScript program to find the sum
// of bit differences between
// consecutive numbers from
// 0 to N using recursion

// Recursive function to find sum
// of different bits between
// consecutive numbers from 0 to N
function totalCountDifference(n)
{

    // Base case
    if (n == 1)
        return 1;

    // Calculate the Nth term
    return n + totalCountDifference(Math.floor(n / 2));
}

// Driver Code

           // Given number
    let N = 5;

    // Function call
    document.write(totalCountDifference(N));

</script>
```

**Output:** 

```
8
```

***时间复杂度:**O(log<sub>2</sub>N)*
***辅助空间:** O(1)*