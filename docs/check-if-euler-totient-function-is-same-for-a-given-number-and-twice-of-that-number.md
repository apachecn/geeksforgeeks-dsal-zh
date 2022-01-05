# 检查欧拉全能性函数对于给定的数和该数的两倍是否相同

> 原文:[https://www . geeksforgeeks . org/check-if-Euler-toitient-function-is-for-同一个给定的数字和该数字的两倍/](https://www.geeksforgeeks.org/check-if-euler-totient-function-is-same-for-a-given-number-and-twice-of-that-number/)

给定一个整数 **N** ，任务是检查 **N** 和 **2 * N** 的[欧拉全能性函数](https://www.geeksforgeeks.org/eulers-totient-function/)是否相同。如果发现它们相同，则打印“**是”**。否则，打印“**否”**。

**示例:**

> **输入:** N = 9
> **输出:**是
> **解释:**
> 让φ()成为欧拉全图函数
> 因为 1、2、4、5、7、8 都有带 9 的 GCD 1。因此，φ(9)= 6。
> 从 1、5、7、11、13、17 开始有 GCD 1 带 18。因此，φ(18)= 6。
> 因此，φ(9)和φ(18)相等。
> 
> **输入:** N = 14
> **输出:**否
> **说明:**
> 设φ()为欧拉全图函数，那么
> 既然 1、3 有 GCD 1 加 4。因此，φ(4)= 2。
> 自 1、3、5、7 有 GCD 1 带 8。因此，φ(8)= 4。
> 所以，φ(4)和φ(8)不一样。

**天真法:**最简单的方法就是找到 **N** 和 **2 * N** 的[欧拉全能性函数](https://www.geeksforgeeks.org/eulers-totient-function/)。如果相同，则打印“是”。否则，打印“否”。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the Euler's
// Totient Function
int phi(int n)
{
    // Initialize result as N
    int result = 1;

    // Consider all prime factors
    // of n and subtract their
    // multiples from result
    for (int p = 2; p < n; p++) {
        if (__gcd(p, n) == 1) {
            result++;
        }
    }

    // Return the count
    return result;
}

// Function to check if phi(n)
// is equals phi(2*n)
bool sameEulerTotient(int n)
{

    return phi(n) == phi(2 * n);
}

// Driver Code
int main()
{
    int N = 13;
    if (sameEulerTotient(N))
        cout << "Yes";
    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of
// the above approach
import java.util.*;
class GFG{

// Function to find the Euler's
// Totient Function
static int phi(int n)
{
  // Initialize result as N
  int result = 1;

  // Consider all prime factors
  // of n and subtract their
  // multiples from result
  for (int p = 2; p < n; p++)
  {
    if (__gcd(p, n) == 1)
    {
      result++;
    }
  }

  // Return the count
  return result;
}

// Function to check if phi(n)
// is equals phi(2*n)
static boolean sameEulerTotient(int n)
{
  return phi(n) == phi(2 * n);
}

static int __gcd(int a, int b) 
{ 
  return b == 0 ? a :__gcd(b, a % b);    
}

// Driver Code
public static void main(String[] args)
{
  int N = 13;
  if (sameEulerTotient(N))
    System.out.print("Yes");
  else
    System.out.print("No");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program of the
# above approach

# Function to find the Euler's
# Totient Function
def phi(n):

    # Initialize result as N
    result = 1

    # Consider all prime factors
    # of n and subtract their
    # multiples from result
    for p in range(2, n):
        if (__gcd(p, n) == 1):
            result += 1

    # Return the count
    return result

# Function to check if phi(n)
# is equals phi(2*n)
def sameEulerTotient(n):

    return phi(n) == phi(2 * n)

def __gcd(a, b):

    return a if b == 0 else __gcd(b, a % b)

# Driver Code
if __name__ == '__main__':

    N = 13

    if (sameEulerTotient(N)):
        print("Yes")
    else:
        print("No")

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program of
// the above approach
using System;
class GFG{

// Function to find the Euler's
// Totient Function
static int phi(int n)
{
  // Initialize result as N
  int result = 1;

  // Consider all prime factors
  // of n and subtract their
  // multiples from result
  for (int p = 2; p < n; p++)
  {
    if (__gcd(p, n) == 1)
    {
      result++;
    }
  }

  // Return the count
  return result;
}

// Function to check if phi(n)
// is equals phi(2*n)
static bool sameEulerTotient(int n)
{
  return phi(n) == phi(2 * n);
}

static int __gcd(int a, int b) 
{ 
  return b == 0 ? a : __gcd(b, a % b);    
}

// Driver Code
public static void Main(String[] args)
{
  int N = 13;
  if (sameEulerTotient(N))
    Console.Write("Yes");
  else
    Console.Write("No");
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript  program for
//the above approach

// Function to find the Euler's
// Totient Function
function phi(n)
{
  // Initialize result as N
  let result = 1;

  // Consider all prime factors
  // of n and subtract their
  // multiples from result
  for (let p = 2; p < n; p++)
  {
    if (__gcd(p, n) == 1)
    {
      result++;
    }
  }

  // Return the count
  return result;
}

// Function to check if phi(n)
// is equals phi(2*n)
function sameEulerTotient(n)
{
  return phi(n) == phi(2 * n);
}

function __gcd( a, b)
{
  return b == 0 ? a :__gcd(b, a % b);   
}

// Driver Code

    let N = 13;
  if (sameEulerTotient(N))
    document.write("Yes");
  else
    document.write("No");

// This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效方法:**要优化上述方法，关键的观察是不需要计算[欧拉全能性函数](https://www.geeksforgeeks.org/eulers-totient-function/)，因为只有奇数遵循属性**φ(N)=φ(2 * N)**，其中**φ()**是欧拉全能性函数。

所以思路是检查 **N** 是不是奇数。如果发现是真的，打印“是”。否则，打印“否”。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if phi(n)
// is equals phi(2*n)
bool sameEulerTotient(int N)
{
    // Return if N is odd
    return (N & 1);
}

// Driver Code
int main()
{
    int N = 13;

    // Function Call
    if (sameEulerTotient(N))
        cout << "Yes";
    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
class GFG{

// Function to check if phi(n)
// is equals phi(2*n)
static int sameEulerTotient(int N)
{

    // Return if N is odd
    return (N & 1);
}

// Driver code
public static void main(String[] args)
{
    int N = 13;

    // Function call
    if (sameEulerTotient(N) == 1)
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Dewanti
```

## 蟒蛇 3

```
# Python3 program of the above approach

# Function to check if phi(n)
# is equals phi(2*n)
def sameEulerTotient(N):

    # Return if N is odd
    return (N & 1);

# Driver code
if __name__ == '__main__':

    N = 13;

    # Function call
    if (sameEulerTotient(N) == 1):
        print("Yes");
    else:
        print("No");

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program of
// the above approach
using System;
class GFG{

// Function to check if phi(n)
// is equals phi(2*n)
static int sameEulerTotient(int N)
{
  // Return if N is odd
  return (N & 1);
}

// Driver code
public static void Main(String[] args)
{
  int N = 13;

  // Function call
  if (sameEulerTotient(N) == 1)
    Console.Write("Yes");
  else
    Console.Write("No");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

//Javascript program of the above approach

// Function to check if phi(n)
// is equals phi(2*n)
function sameEulerTotient(N)
{
    // Return if N is odd
    return (N & 1);
}

// Driver Code
var N = 13;
// Function Call
if (sameEulerTotient(N))
    document.write( "Yes");
else
    document.write("No");

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)