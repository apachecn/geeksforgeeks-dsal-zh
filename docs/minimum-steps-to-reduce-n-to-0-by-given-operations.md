# 通过给定操作将 N 减少到 0 的最小步骤

> 原文:[https://www . geesforgeks . org/按给定操作将 n 减少到 0 的最小步骤/](https://www.geeksforgeeks.org/minimum-steps-to-reduce-n-to-0-by-given-operations/)

给定一个整数 **N** ，任务是通过以下操作之一找到将 **N** 减少到 **0** 的最小移动次数:

*   N 减 1。
*   如果 N 能被 2 整除，把 N 减少到(N/2)。
*   如果 N 能被 3 整除，把 N 减少到(N/3)。

**示例:**

> **输入:** N = 10
> **输出:** 4
> **说明:**
> 这里 N = 10
> 第一步:减 N 1，即 10–1 = 9。
> 第二步:既然 9 能被 3 整除，那就化简为 N/3 = 9/3 = 3
> 第三步:既然 3 又能被 3 整除，那就再次重复第二步，即 3/3 = 1。
> 步骤 4: 1 可以通过步骤 1 来减少，即 1-1 = 0
> 因此，需要 4 个步骤来将 N 减少到 0。
> 
> **输入:** N = 6
> **输出:** 3
> **解释:**
> 这里 N = 6
> 步骤 1:既然 6 能被 2 整除，那么 6/2 =3
> 步骤 2:既然 3 能被 3 整除，那么 3/3 = 1。
> 第三步:将 N 减 1 为 N-1，1-1 = 0。
> 因此，需要 3 个步骤将氮减少到 0。

**天真方法:**想法是对所有可能的移动使用[递归](https://www.geeksforgeeks.org/recursion/)。以下是步骤:

1.  观察问题的基本情况，如果 **N < 2** 那么对于所有情况，答案将是 N 本身。
2.  在 **N** 的每个值下，从两种可能的情况中进行选择:
    *   减少 n 直到 n % 2 == 0，然后用 count = 1 + n%2 + f(n/2)更新 n /= 2
    *   减少 n 直到 n % 3 == 0，然后用计数= 1 + n%3 + f(n/3)更新 n /= 3
3.  计算结果在[递推关系](https://www.geeksforgeeks.org/different-types-recurrence-relations-solutions/)中均为:

> 计数= 1 +分钟(n%2 + f(n/2)，n%3 + f(n/3))
> 其中，f(n)是将 N 减少到 0 的最小移动次数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// number to steps to reduce N to 0
int minDays(int n)
{

    // Base case
    if (n < 1)
        return n;

    // Recursive call to count the
    // minimum steps needed
    int cnt = 1 + min(n % 2 + minDays(n / 2),
                      n % 3 + minDays(n / 3));

    // Return the answer
    return cnt;
}

// Driver Code
int main()
{

    // Given number N
    int N = 6;

    // Function call
    cout << minDays(N);

    return 0;
}

// This code is contributed by 29AjayKumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

    // Function to find the minimum
    // number to steps to reduce N to 0
    static int minDays(int n)
    {

        // Base case
        if (n < 1)
            return n;

        // Recursive Call to count the
        // minimum steps needed
        int cnt = 1 + Math.min(n % 2 + minDays(n / 2),
                               n % 3 + minDays(n / 3));

        // Return the answer
        return cnt;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given Number N
        int N = 6;

        // Function Call
        System.out.print(minDays(N));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum
# number to steps to reduce N to 0
def minDays(n):

    # Base case
    if n < 1:
        return n

    # Recursive Call to count the
    # minimum steps needed
    cnt = 1 + min(n % 2 + minDays(n // 2),
                  n % 3 + minDays(n // 3))

    # Return the answer
    return cnt

# Driver Code

# Given Number N
N = 6

# Function Call
print(str(minDays(N)))
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find the minimum
// number to steps to reduce N to 0
static int minDays(int n)
{   
    // Base case
    if (n < 1)
        return n;

    // Recursive call to count the
    // minimum steps needed
    int cnt = 1 + Math.Min(n % 2 + minDays(n / 2),
                           n % 3 + minDays(n / 3));

    // Return the answer
    return cnt;
}

// Driver Code
public static void Main(String[] args)
{   
    // Given number N
    int N = 6;

    // Function call
    Console.Write(minDays(N));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the minimum
// number to steps to reduce N to 0
function minDays(n)
{

    // Base case
    if (n < 1)
        return n;

    // Recursive call to count the
    // minimum steps needed
    var cnt = 1 + Math.min(n % 2 + minDays(parseInt(n / 2)),
                      n % 3 + minDays(parseInt(n / 3)));

    // Return the answer
    return cnt;
}

// Driver Code
// Given number N
var N = 6;

// Function call
document.write( minDays(N));

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。由于重复子问题的数量，上述递归方法产生了 [TLE](https://www.geeksforgeeks.org/overcome-time-limit-exceedtle/) 。使用[字典](https://www.geeksforgeeks.org/python-dictionary/)来优化上述方法，以跟踪已经执行递归调用的值，以减少进一步的计算，从而可以更快地访问值。

下面是上述方法的实现:

## C++

```
// C++ program for
// the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find the minimum
// number to steps to reduce N to 0
int count(int n)
{
  // Dictionary for storing
  // the precomputed sum
  map<int, int> dp;

  // Bases Cases
  dp[0] = 0;
  dp[1] = 1;

  // Check if n is not in dp then
  // only call the function so as
  // to reduce no of recursive calls
  if ((dp.find(n) == dp.end()))
    dp[n] = 1 + min(n % 2 +
                    count(n / 2), n % 3 +
                    count(n / 3));

  // Return the answer
  return dp[n];
}

// Driver Code
int main()
{   
  // Given number N
  int N = 6;

  // Function call
  cout << count(N);
}

// This code is contributed by gauravrajput1
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.HashMap;

class GFG{

// Function to find the minimum
// number to steps to reduce N to 0
static int count(int n)
{

    // Dictionary for storing
    // the precomputed sum
    HashMap<Integer,
            Integer> dp = new HashMap<Integer,
                                      Integer>();

    // Bases Cases
    dp.put(0, 0);
    dp.put(1, 1);

    // Check if n is not in dp then
    // only call the function so as
    // to reduce no of recursive calls
    if (!dp.containsKey(n))
        dp.put(n, 1 + Math.min(n % 2 +
                 count(n / 2), n % 3 +
                 count(n / 3)));

    // Return the answer
    return dp.get(n);
}

// Driver Code
public static void main(String[] args)
{

    // Given number N
    int N = 6;

    // Function call
    System.out.println(String.valueOf((count(N))));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum
# number to steps to reduce N to 0
def count(n):

    # Dictionary for storing
    # the precomputed sum
    dp = dict()

    # Bases Cases
    dp[0] = 0
    dp[1] = 1

    # Check if n is not in dp then
    # only call the function so as
    # to reduce no of recursive calls
    if n not in dp:
        dp[n] = 1 + min(n % 2 + count(n//2), n % 3 + count(n//3))

    # Return the answer
    return dp[n]

# Driver Code

# Given Number N
N = 6

# Function Call
print(str(count(N)))
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
public class GFG{

// Function to find the minimum
// number to steps to reduce N to 0
static int count(int n)
{   
    // Dictionary for storing
    // the precomputed sum
    Dictionary<int,
               int> dp = new Dictionary<int,
                                        int>();

    // Bases Cases
    dp.Add(0, 0);
    dp.Add(1, 1);

    // Check if n is not in dp then
    // only call the function so as
    // to reduce no of recursive calls
    if (!dp.ContainsKey(n))
        dp.Add(n, 1 + Math.Min(n % 2 + count(n / 2),
                               n % 3 + count(n / 3)));

    // Return the answer
    return dp[n];
}

// Driver Code
public static void Main(String[] args)
{   
    // Given number N
    int N = 6;

    // Function call
    Console.WriteLine(String.Join("",
                                  (count(N))));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program for
// the above approach

// Function to find the minimum
// number to steps to reduce N to 0
function count(n)
{
  // Dictionary for storing
  // the precomputed sum
  var dp = new Map();

  // Bases Cases
  dp.set(0, 0);
  dp.set(1, 1);

  // Check if n is not in dp then
  // only call the function so as
  // to reduce no of recursive calls
  if (!dp.has(n))
    dp.set(n, 1 + Math.min(n % 2 +
                    count(parseInt(n / 2)), n % 3 +
                    count(parseInt(n / 3))));

  // Return the answer
  return dp.get(n);
}

// Driver Code

// Given number N
var N = 6;

// Function call
document.write( count(N));

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*