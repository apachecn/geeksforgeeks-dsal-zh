# 求 K 的最大可能值，使得 K 模 X 为 Y

> 原文:[https://www . geeksforgeeks . org/find-最大可能值-k-这样-k-模-x-is-y/](https://www.geeksforgeeks.org/find-the-largest-possible-value-of-k-such-that-k-modulo-x-is-y/)

给定三个整数 **N** 、 **X** 和 **Y** ，任务是找出最大正整数 **K** ，使得 **K % X = Y** ，其中 **0 ≤ K ≤ N** 。如果不存在 **K** ，打印 **-1** 。

**示例:**

> **输入:** N = 15，X = 10，Y = 5
> **输出:** 15
> **说明:**
> As 15 % 10 = 5
> 
> **输入:** N = 187，X = 10，Y = 5
> T3】输出: 185

**天真法:**解决问题最简单的方法就是检查 **K** 在**【0，N】**范围内的每个可能值，是否满足条件 **K % X = Y** 。如果没有这样的 **K** ，打印 **-1** 。否则，从满足条件的范围打印最大可能值 **K** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the largest
// positive integer K such that K % x = y
int findMaxSoln(int n, int x, int y)
{
    // Stores the minimum solution
    int ans = INT_MIN;

    for (int k = 0; k <= n; k++) {
        if (k % x == y) {
            ans = max(ans, k);
        }
    }

    // Return the maximum possible value
    return ((ans >= 0
             && ans <= n)
                ? ans
                : -1);
}

// Driver Code
int main()
{
    int n = 15, x = 10, y = 5;
    cout << findMaxSoln(n, x, y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the largest
// positive integer K such that K % x = y
static int findMaxSoln(int n, int x, int y)
{

    // Stores the minimum solution
    int ans = Integer.MIN_VALUE;

    for(int k = 0; k <= n; k++)
    {
        if (k % x == y)
        {
            ans = Math.max(ans, k);
        }
    }

    // Return the maximum possible value
    return ((ans >= 0 && ans <= n) ?
             ans : -1);
}

// Driver Code
public static void main(String[] args)
{
    int n = 15, x = 10, y = 5;

    System.out.print(findMaxSoln(n, x, y));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find the largest
# positive integer K such that
# K % x = y
def findMaxSoln(n, x, y):

    # Stores the minimum solution
    ans = -sys.maxsize

    for k in range(n + 1):
        if (k % x == y):
            ans = max(ans, k)

    # Return the maximum possible value
    return (ans if (ans >= 0 and
                    ans <= n) else -1)

# Driver Code
if __name__ == '__main__':

    n = 15
    x = 10
    y = 5

    print(findMaxSoln(n, x, y))

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find the largest
// positive integer K such that
// K % x = y
static int findMaxSoln(int n,
                       int x, int y)
{   
  // Stores the minimum solution
  int ans = int.MinValue;

  for(int k = 0; k <= n; k++)
  {
    if (k % x == y)
    {
      ans = Math.Max(ans, k);
    }
  }

  // Return the maximum possible value
  return ((ans >= 0 && ans <= n) ?
           ans : -1);
}

// Driver Code
public static void Main(String[] args)
{
  int n = 15, x = 10, y = 5;   
  Console.Write(findMaxSoln(n, x, y));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the largest
// positive integer K such that K % x = y
function findMaxSoln(n, x, y)
{

    // Stores the minimum solution
    var ans = -1000000000;

    for (var k = 0; k <= n; k++) {
        if (k % x == y) {
            ans = Math.max(ans, k);
        }
    }

    // Return the maximum possible value
    return ((ans >= 0
             && ans <= n)
                ? ans
                : -1);
}

// Driver Code
var n = 15, x = 10, y = 5;
document.write( findMaxSoln(n, x, y));

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
15
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**有效方法:**上述方法可以基于观察到 **K** 可以获得以下值之一来满足等式而进行优化:

> **K = N–N % X+Y**
> 或
> **K = N–N % X+Y–X**

按照以下步骤解决问题:

1.  计算 **K1** 为**K = N–N % X+Y**， **K2** 为**K = N–N % X+Y–X**。
2.  如果 **K1** 在**【0，N】**范围内，打印 **K1** 。
3.  否则，如果 **K2** 在**【0，N】**范围内，打印 **K2** 。
4.  否则，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the largest positive
// integer K such that K % x = y
int findMaxSoln(int n, int x, int y)
{
    // Possible value of K as K1
    if (n - n % x + y <= n) {
        return n - n % x + y;
    }

    // Possible value of K as K2
    else {
        return n - n % x - (x - y);
    }
}

// Driver Code
int main()
{
    int n = 15, x = 10, y = 5;
    int ans = findMaxSoln(n, x, y);
    cout << ((ans >= 0 && ans <= n) ? ans : -1);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the largest positive
// integer K such that K % x = y
static int findMaxSoln(int n, int x, int y)
{

    // Possible value of K as K1
    if (n - n % x + y <= n)
    {
        return n - n % x + y;
    }

    // Possible value of K as K2
    else
    {
        return n - n % x - (x - y);
    }
}

// Driver Code
public static void main(String[] args)
{
    int n = 15, x = 10, y = 5;
    int ans = findMaxSoln(n, x, y);

    System.out.print(((ans >= 0 &&
                       ans <= n) ? ans : -1));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the largest positive
# integer K such that K % x = y
def findMaxSoln(n, x, y):

    # Possible value of K as K1
    if (n - n % x + y <= n):
        return n - n % x + y;

    # Possible value of K as K2
    else:
        return n - n % x - (x - y);

# Driver Code
if __name__ == '__main__':
    n = 15;
    x = 10;
    y = 5;
    ans = findMaxSoln(n, x, y);
    print(( ans if (ans >= 0 and ans <= n) else -1));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to find the largest
// positive integer K such that
// K % x = y
static int findMaxSoln(int n,
                       int x, int y)
{
  // Possible value of K as K1
  if (n - n % x + y <= n)
  {
    return n - n % x + y;
  }

  // Possible value of K as K2
  else
  {
    return n - n % x - (x - y);
  }
}

// Driver Code
public static void Main(String[] args)
{
  int n = 15, x = 10, y = 5;
  int ans = findMaxSoln(n, x, y);
  Console.Write(((ans >= 0 &&
                  ans <= n) ?
                  ans : -1));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

    // Function to find the largest positive
    // integer K such that K % x = y
    function findMaxSoln(n , x , y) {

        // Possible value of K as K1
        if (n - n % x + y <= n) {
            return n - n % x + y;
        }

        // Possible value of K as K2
        else {
            return n - n % x - (x - y);
        }
    }

    // Driver Code

        var n = 15, x = 10, y = 5;
        var ans = findMaxSoln(n, x, y);

        document.write(
        ((ans >= 0 && ans <= n) ? ans : -1)
        );

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
15
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)