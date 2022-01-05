# 检查通过 K 长度跳跃是否可以从循环队列中的另一个值到达给定值

> 原文:[https://www . geeksforgeeks . org/check-如果一个给定的值可以从另一个循环队列中的值通过 k 长度跳转到达/](https://www.geeksforgeeks.org/check-if-a-given-value-can-be-reached-from-another-value-in-a-circular-queue-by-k-length-jumps/)

给定整数 **N** 、 **K** 、 **A** 和 **B** ，检查从 **A** 到 **1** 到 **N** 依次放置的整数的[循环队列](https://www.geeksforgeeks.org/circular-queue-set-1-introduction-array-implementation/)中是否有可能通过 **K** 长度的跳跃到达 **B** 。在每一步棋中，如果可能，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** N = 5，A = 2，B = 1，K = 2
> **输出:**是
> **说明:** 2 - > 4 - > 1。因此，从 a 到 B 是可能的。
> 
> **输入:** N = 9，A = 6，B = 5，K = 3
> T3】输出:否

**方法:**解决问题的思路基于以下观察:

*   对于位置 **A** ，在 **t 步**后， **A** 的位置为 **(A + K*t)%N** 。
*   对于位置 **B** ，在 **t 步**后， **B** 的位置为 **(A + K*t)%N** 。
*   它可以写成:

> (A + K*t) = (N*q + B)，其中 q 为任意正整数
> (A–B)= N * q–K * t

观察上述等式**(N * q–K * t)**可被 **N** 和 **K** 的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 整除。因此**(A–B)**也可以被 **N** 和 **K** 的 GCD 整除。因此，要从 **A** 到达 **B** ，**(A–B)**必须能被 **GCD(N，K)** 整除。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return GCD of two
// numbers a and b
int GCD(int a, int b)
{
    // Base Case
    if (b == 0)
        return a;

    // Recursively Find the GCD
    return GCD(b, a % b);
}

// Function to check of B can be reaced
// from A with a jump of K elements in
// the circular queue
void canReach(int N, int A, int B, int K)
{

    // Find GCD of N and K
    int gcd = GCD(N, K);

    // If A - B is divisible by gcd
    // then print Yes
    if (abs(A - B) % gcd == 0) {
        cout << "Yes";
    }

    // Otherwise
    else {
        cout << "No";
    }
}

// Driver Code
int main()
{
    int N = 5, A = 2, B = 1, K = 2;

    // Function Call
    canReach(N, A, B, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class solution{

// Function to return GCD
// of two numbers a and b
static int GCD(int a, int b)
{
  // Base Case
  if (b == 0)
    return a;

  // Recursively Find
  // the GCD
  return GCD(b, a % b);
}

// Function to check of B can
// be reaced from A with a jump
// of K elements in the circular
// queue
static void canReach(int N, int A,
                     int B, int K)
{
  // Find GCD of N and K
  int gcd = GCD(N, K);

  // If A - B is divisible
  // by gcd then print Yes
  if (Math.abs(A - B) %
      gcd == 0)
  {
    System.out.println("Yes");
  }

  // Otherwise
  else
  {
    System.out.println("No");
  }
}

// Driver Code
public static void main(String args[])
{
  int N = 5, A = 2,
      B = 1, K = 2;
  // Function Call
  canReach(N, A, B, K);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to return GCD
# of two numbers a and b
def GCD(a, b):

    # Base Case
    if (b == 0):
        return a

    # Recursively Find
    # the GCD
    return GCD(b, a % b)

# Function to check of B
# can be reaced from A
# with a jump of K elements
# in the circular queue
def canReach(N, A, B, K):

    # Find GCD of N and K
    gcd = GCD(N, K)

    # If A - B is divisible
    # by gcd then prYes
    if (abs(A - B) %
        gcd == 0):
        print("Yes")

    # Otherwise   
    else:
        print("No")

# Driver Code
if __name__ == '__main__':

    N = 5
    A = 2
    B = 1
    K = 2

    # Function Call
    canReach(N, A, B, K)

# This code is contributed by Mohit Kumar 29
```

## C#

```
// C# program for the
// above approach
using System;

class GFG{

// Function to return GCD
// of two numbers a and b
static int GCD(int a, int b)
{

  // Base Case
  if (b == 0)
    return a;

  // Recursively Find
  // the GCD
  return GCD(b, a % b);
}

// Function to check of B can
// be reaced from A with a jump
// of K elements in the circular
// queue
static void canReach(int N, int A,
                     int B, int K)
{

  // Find GCD of N and K
  int gcd = GCD(N, K);

  // If A - B is divisible
  // by gcd then print Yes
  if (Math.Abs(A - B) % gcd == 0)
  {
    Console.WriteLine("Yes");
  }

  // Otherwise
  else
  {
    Console.WriteLine("No");
  }
}

// Driver Code
public static void Main()
{
  int N = 5, A = 2,
      B = 1, K = 2;

  // Function Call
  canReach(N, A, B, K);
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to return GCD of two
// numbers a and b
function GCD(a, b)
{
    // Base Case
    if (b == 0)
        return a;

    // Recursively Find the GCD
    return GCD(b, a % b);
}

// Function to check of B can be reaced
// from A with a jump of K elements in
// the circular queue
function canReach(N, A, B, K)
{

    // Find GCD of N and K
    var gcd = GCD(N, K);

    // If A - B is divisible by gcd
    // then print Yes
    if (Math.abs(A - B) % gcd == 0) {
        document.write( "Yes");
    }

    // Otherwise
    else {
        document.write( "No");
    }
}

// Driver Code
var N = 5, A = 2, B = 1, K = 2;

// Function Call
canReach(N, A, B, K);

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** *O(log(min(N，K))*
**辅助空间:** *O(1)*