# 与 N 共质数最多为 N 的所有数的和

> 原文:[https://www . geesforgeks . org/所有数字的总和-最多 n-与-n 同素/](https://www.geeksforgeeks.org/sum-of-all-numbers-up-to-n-that-are-co-prime-with-n/)

给定一个整数 **N** ，任务是找出范围**【1，N】**内与给定数 **N** 同素的所有数的和。

**示例:**

> ***输入:** N = 5*
> ***输出:** 10*
> ***解释:***
> *与 5 同素的数字为{1，2，3，4}。*
> *因此，总和由 1 + 2 + 3 + 4 = 10 给出。*
> 
> ***输入:** N = 6*
> ***输出:** 5*
> ***解释:***
> *与 6 同素的数字为{1，5}。*
> *因此，要求的总和等于 1 + 5 = 6*

**方法:**思路是迭代范围**【1，N】**，对于每一个数字，检查其带有 **N** 的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 是否等于 **1** 。如果发现是真的，那么对于任何数字，将该数字包括在结果和中。按照以下步骤解决问题:

*   将**和**初始化为 0。
*   迭代**【1，N】**的范围，如果 **i** 和 **N** 中的[T3T5】是 **1** ，则将 **i** 加到**和**上。](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)
*   完成上述步骤后，打印得到的**和**的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to return gcd of a and b
int gcd(int a, int b)
{
    // Base Case
    if (a == 0)
        return b;

    // Recursive GCD
    return gcd(b % a, a);
}

// Function to calculate the sum of all
// numbers till N that are coprime with N
int findSum(unsigned int N)
{
    // Stores the resultant sum
    unsigned int sum = 0;

    // Iterate over [1, N]
    for (int i = 1; i < N; i++) {

        // If gcd is 1
        if (gcd(i, N) == 1) {

            // Update sum
            sum += i;
        }
    }

    // Return the final sum
    return sum;
}

// Driver Code
int main()
{
    // Given N
    int N = 5;

    // Function Call
    cout << findSum(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to return gcd
// of a and b
static int gcd(int a,
               int b)
{
  // Base Case
  if (a == 0)
    return b;

  // Recursive GCD
  return gcd(b % a, a);
}

// Function to calculate the
// sum of all numbers till N
// that are coprime with N
static int findSum(int N)
{
  // Stores the resultant sum
  int sum = 0;

  // Iterate over [1, N]
  for (int i = 1; i < N; i++)
  {
    // If gcd is 1
    if (gcd(i, N) == 1)
    {
      // Update sum
      sum += i;
    }
  }

  // Return the final sum
  return sum;
}

// Driver Code
public static void main(String[] args)
{
  // Given N
  int N = 5;

  // Function Call
  System.out.print(findSum(N));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python program for
# the above approach

# Function to return gcd
# of a and b
def gcd(a, b):
    # Base Case
    if (a == 0):
        return b;

    # Recursive GCD
    return gcd(b % a, a);

# Function to calculate the
# sum of all numbers till N
# that are coprime with N
def findSum(N):
    # Stores the resultant sum
    sum = 0;

    # Iterate over [1, N]
    for i in range(1, N):
        # If gcd is 1
        if (gcd(i, N) == 1):
            # Update sum
            sum += i;

    # Return the final sum
    return sum;

# Driver Code
if __name__ == '__main__':
    # Given N
    N = 5;

    # Function Call
    print(findSum(N));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to return gcd
// of a and b
static int gcd(int a,
               int b)
{
  // Base Case
  if (a == 0)
    return b;

  // Recursive GCD
  return gcd(b % a, a);
}

// Function to calculate the
// sum of all numbers till N
// that are coprime with N
static int findSum(int N)
{
  // Stores the resultant sum
  int sum = 0;

  // Iterate over [1, N]
  for (int i = 1; i < N; i++)
  {
    // If gcd is 1
    if (gcd(i, N) == 1)
    {
      // Update sum
      sum += i;
    }
  }

  // Return the readonly sum
  return sum;
}

// Driver Code
public static void Main(String[] args)
{
  // Given N
  int N = 5;

  // Function Call
  Console.Write(findSum(N));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to return gcd of a and b
function gcd(a, b)
{
    // Base Case
    if (a == 0)
        return b;

    // Recursive GCD
    return gcd(b % a, a);
}

// Function to calculate the sum of all
// numbers till N that are coprime with N
function findSum(N)
{
    // Stores the resultant sum
    var sum = 0;

    // Iterate over [1, N]
    for (var i = 1; i < N; i++) {

        // If gcd is 1
        if (gcd(i, N) == 1) {

            // Update sum
            sum += i;
        }
    }

    // Return the final sum
    return sum;
}

// Driver Code
// Given N
var N = 5;

// Function Call
document.write(findSum(N));

</script>
```

**Output:** 

```
10
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)