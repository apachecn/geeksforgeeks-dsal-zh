# 通过将其最小的正除数加正好 K 倍来修改 N

> 原文:[https://www . geeksforgeeks . org/modify-n-by-adding-its-minist-正除数-just-k-times/](https://www.geeksforgeeks.org/modify-n-by-adding-its-smallest-positive-divisor-exactly-k-times/)

给定两个正整数 **N** 和 **K** ，任务是将每次操作中 **N** 的值递增其最小除数超过 **N** ( *超过 1* )次后，求 **N** 的值，正好是 **K** 次。

**示例:**

> **输入:** N = 5，K = 2
> **输出:** 12
> **说明:**
> N(= 5)的最小除数为 5。因此，N = 5 + 5 = 10。
> N(= 10)的最小除数为 2。因此，N = 5 + 2 = 12。
> 因此，所需输出为 12。
> 
> **输入:** N = 6，K = 4
> T3】输出: 14

**天真法:**解决这个问题最简单的方法是使用变量 **i** 迭代范围**【1，K】**，在每次运算中，[找到大于 N](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/) 的 **1** 的最小除数，并将 **N** 的值增加大于 **N** 的 **1** 的最小除数。最后打印 **N** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest
// divisor of N greater than 1
int smallestDivisorGr1(int N)
{
    for (int i = 2; i <= sqrt(N);
         i++) {

        // If i is a divisor
        // of N
        if (N % i == 0) {
            return i;
        }
    }

    // If N is a prime number
    return N;
}

// Function to find the value of N by
// performing the operations K times
int findValOfNWithOperat(int N, int K)
{

    // Iterate over the range [1, K]
    for (int i = 1; i <= K; i++) {

        // Update N
        N += smallestDivisorGr1(N);
    }

    return N;
}

// Driver Code
int main()
{
    int N = 6, K = 4;

    cout << findValOfNWithOperat(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

class GFG{

// Function to find the smallest
// divisor of N greater than 1
static int smallestDivisorGr1(int N)
{
    for (int i = 2; i <= Math.sqrt(N);
         i++) {

        // If i is a divisor
        // of N
        if (N % i == 0) {
            return i;
        }
    }

    // If N is a prime number
    return N;
}

// Function to find the value of N by
// performing the operations K times
static int findValOfNWithOperat(int N, int K)
{

    // Iterate over the range [1, K]
    for (int i = 1; i <= K; i++)
    {

        // Update N
        N += smallestDivisorGr1(N);
    }

    return N;
}

// Driver Code
public static void main(String[] args)
{
    int N = 6, K = 4;

    System.out.print(findValOfNWithOperat(N, K));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python 3 program to implement
# the above approach
import math

# Function to find the smallest
# divisor of N greater than 1
def smallestDivisorGr1(N):
    for i in range(2, int(math.sqrt(N))+1):

        # If i is a divisor
        # of N
        if (N % i == 0):
            return i

    # If N is a prime number
    return N

# Function to find the value of N by
# performing the operations K times
def findValOfNWithOperat(N, K):

    # Iterate over the range [1, K]
    for i in range(1, K + 1):

        # Update N
        N += smallestDivisorGr1(N)

    return N

# Driver Code
if __name__ == "__main__":

    N = 6
    K = 4

    print(findValOfNWithOperat(N, K))

    # This code is contributed by ukasp.
```

## C#

```
// C# program to implement
// the above approach
using System;
public class GFG
{

  // Function to find the smallest
  // divisor of N greater than 1
  static int smallestDivisorGr1(int N)
  {
    for (int i = 2; i <= Math.Sqrt(N);
         i++) {

      // If i is a divisor
      // of N
      if (N % i == 0) {
        return i;
      }
    }

    // If N is a prime number
    return N;
  }

  // Function to find the value of N by
  // performing the operations K times
  static int findValOfNWithOperat(int N, int K)
  {

    // Iterate over the range [1, K]
    for (int i = 1; i <= K; i++)
    {

      // Update N
      N += smallestDivisorGr1(N);
    }

    return N;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int N = 6, K = 4;

    Console.Write(findValOfNWithOperat(N, K));
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// JavaScript program to implement
// the above approach

// Function to find the smallest
// divisor of N greater than 1
function smallestDivisorGr1(N)
{
    for (let i = 2; i <= Math.sqrt(N);
        i++) {

        // If i is a divisor
        // of N
        if (N % i == 0)
        {
            return i;
        }
    }

    // If N is a prime number
    return N;
}

// Function to find the value of N by
// performing the operations K times
function findValOfNWithOperat(N, K)
{

    // Iterate over the range [1, K]
    for (let i = 1; i <= K; i++)
    {

        // Update N
        N += smallestDivisorGr1(N);
    }
    return N;
}

// Driver Code
let N = 6, K = 4;
document.write(findValOfNWithOperat(N, K));

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
14
```

***时间复杂度:** O(K * √N)*
***辅助空间:** O(1)*

**高效方法:**按照以下步骤解决问题:

*   如果 [N 是偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则将 **N** 的值更新为 **(N + K * 2)** 。
*   否则，找到大于 **N** 的 **1** 的最小正除数，说 **smDiv** 并将值 **N** 更新为**(N+smDiv+(K–1)* 2)**
*   最后，打印 **N** 的值。

下面是上述方法的实现:

## C++14

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest
// divisor of N greater than 1
int smallestDivisorGr1(int N)
{
    for (int i = 2; i <= sqrt(N);
         i++) {

        // If i is a divisor
        // of N
        if (N % i == 0) {
            return i;
        }
    }

    // If N is a prime number
    return N;
}

// Function to find the value of N by
// performing the operations K times
int findValOfNWithOperat(int N, int K)
{
    // If N is an even number
    if (N % 2 == 0) {

        // Update N
        N += K * 2;
    }

    // If N is an odd number
    else {

        // Update N
        N += smallestDivisorGr1(N)
             + (K - 1) * 2;
    }

    return N;
}

// Driver Code
int main()
{
    int N = 6, K = 4;

    cout << findValOfNWithOperat(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to find the smallest
// divisor of N greater than 1
static int smallestDivisorGr1(int N)
{
    for(int i = 2; i <= Math.sqrt(N); i++)
    {

        // If i is a divisor
        // of N
        if (N % i == 0)
        {
            return i;
        }
    }

    // If N is a prime number
    return N;
}

// Function to find the value of N by
// performing the operations K times
static int findValOfNWithOperat(int N, int K)
{

    // If N is an even number
    if (N % 2 == 0)
    {

        // Update N
        N += K * 2;
    }

    // If N is an odd number
    else
    {

        // Update N
        N += smallestDivisorGr1(N) + (K - 1) * 2;
    }
    return N;
}

// Driver Code
public static void main(String[] args)
{
    int N = 6, K = 4;

    System.out.print(findValOfNWithOperat(N, K));
}
}

// This code is contributed by target_2
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to find the smallest
# divisor of N greater than 1
def smallestDivisorGr1(N):
    for i in range (sqrt(N)):
         i += 1

        # If i is a divisor
        # of N
    if(N % i == 0):
            return i

    # If N is a prime number
    return N

# Function to find the value of N by
# performing the operations K times
def findValOfNWithOperat(N, K):

  # If N is an even number
  if (N % 2 == 0):

    # Update N
    N += K * 2

  # If N is an odd number
  else:
    # Update N
    N += smallestDivisorGr1(N) + (K - 1) * 2

  return N

# Driver Code
N = 6
K = 4
print(findValOfNWithOperat(N, K))

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find the smallest
// divisor of N greater than 1
static int smallestDivisorGr1(int N)
{
    for(int i = 2; i <= Math.Sqrt(N); i++)
    {

        // If i is a divisor
        // of N
        if (N % i == 0)
        {
            return i;
        }
    }

    // If N is a prime number
    return N;
}

// Function to find the value of N by
// performing the operations K times
static int findValOfNWithOperat(int N, int K)
{

    // If N is an even number
    if (N % 2 == 0)
    {

        // Update N
        N += K * 2;
    }

    // If N is an odd number
    else
    {

        // Update N
        N += smallestDivisorGr1(N) + (K - 1) * 2;
    }
    return N;
}

// Driver code
static public void Main()
{
    int N = 6, K = 4;

    Console.Write(findValOfNWithOperat(N, K));
}
}

// This code is contributed by Khushboogoyal499
```

## java 描述语言

```
<script>

// Function to find the smallest
// divisor of N greater than 1
function smallestDivisorGr1( N)
{
    for (var i = 2; i <= Math.sqrt(N);
        i++) {

        // If i is a divisor
        // of N
        if (N % i == 0) {
            return i;
        }
    }

    // If N is a prime number
    return N;
}

// Function to find the value of N by
// performing the operations K times
function findValOfNWithOperat(N, K)
{
    // If N is an even number
    if (N % 2 == 0) {

        // Update N
        N += K * 2;
    }

    // If N is an odd number
    else {

        // Update N
        N += smallestDivisorGr1(N)
            + (K - 1) * 2;
    }

    return N;
}

// Driver Code
var N = 6, K = 4;

    document.write(findValOfNWithOperat(N, K));

</script>
```

**Output:** 

```
14
```

***时间复杂度:** O(√N)*
***辅助空间:** O(1)*