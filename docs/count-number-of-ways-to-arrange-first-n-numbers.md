# 计数排列前 N 个数字的方式数量

> 原文:[https://www . geeksforgeeks . org/count-to-number-first-n-numbers/](https://www.geeksforgeeks.org/count-number-of-ways-to-arrange-first-n-numbers/)

数数排列一行中第一个 **N 个**自然数的方法，使得最左边的数总是 **1** ，并且没有两个连续的数具有大于 **2** 的绝对差。

**示例:**

> **输入:** N = 4
> **输出:** 4
> 唯一可能的排列是(1，2，3，4)
> (1，2，4，3)，(1，3，4，2)和(1，3，2，4)。
> 
> **输入:**N = 6
> T3】输出: 9

**天真的方法:**生成所有的排列，并计算它们中有多少满足给定的条件。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of required arrangements
int countWays(int n)
{

    // Create a vector
    vector<int> a;
    int i = 1;

    // Store numbers from 1 to n
    while (i <= n)
        a.push_back(i++);

    // To store the count of ways
    int ways = 0;

    // Generate all the permutations
    // using next_permutation in STL
    do {
        // Initialize flag to true if first
        // element is 1 else false
        bool flag = (a[0] == 1);

        // Checking if the current permutation
        // satisfies the given conditions
        for (int i = 1; i < n; i++) {

            // If the current permutation is invalid
            // then set the flag to false
            if (abs(a[i] - a[i - 1]) > 2)
                flag = 0;
        }

        // If valid arrangement
        if (flag)
            ways++;

        // Generate the next permutation
    } while (next_permutation(a.begin(), a.end()));

    return ways;
}

// Driver code
int main()
{
    int n = 6;

    cout << countWays(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.util.*;
class GFG{

// Function to return the count
// of required arrangements
static int countWays(int n)
{
  // Create a vector
  Vector<Integer> a =
         new Vector<>();
  int i = 1;

  // Store numbers from
  // 1 to n
  while (i <= n)
    a.add(i++);

  // To store the count
  // of ways
  int ways = 0;

  // Generate all the permutations
  // using next_permutation in STL
  do
  {
    // Initialize flag to true
    // if first element is 1
    // else false
    boolean flag = (a.get(0) == 1);

    // Checking if the current
    // permutation satisfies the
    // given conditions
    for (int j = 1; j < n; j++)
    {
      // If the current permutation
      // is invalid then set the
      // flag to false
      if (Math.abs(a.get(j) -
                   a.get(j - 1)) > 2)
        flag = false;
    }

    // If valid arrangement
    if (flag)
      ways++;

    // Generate the next permutation
  } while (next_permutation(a));

  return ways;
}

static boolean next_permutation(Vector<Integer> p)
{
  for (int a = p.size() - 2;
           a >= 0; --a)
    if (p.get(a) < p.get(a + 1))
      for (int b = p.size() - 1;; --b)
        if (p.get(b) > p.get(a))
        {
          int t = p.get(a);
          p.set(a, p.get(b));
          p.set(b, t);

          for (++a, b = p.size() - 1;
                 a < b; ++a, --b)
          {
            t = p.get(a);
            p.set(a, p.get(b));
            p.set(b, t);
          }
          return true;
        }
  return false;
}

// Driver code
public static void main(String[] args)
{
  int n = 6;
  System.out.print(countWays(n));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from itertools import permutations

# Function to return the count
# of required arrangements
def countWays(n):

    # Create a vector
    a = []
    i = 1

    # Store numbers from 1 to n
    while (i <= n):
        a.append(i)
        i += 1

    # To store the count of ways
    ways = 0

    # Generate the all permutation
    for per in list(permutations(a)):

        # Initialize flag to true if first
        # element is 1 else false
        flag = 1 if (per[0] == 1) else 0

        # Checking if the current permutation
        # satisfies the given conditions
        for i in range(1, n):

            # If the current permutation is invalid
            # then set the flag to false
            if (abs(per[i] - per[i - 1]) > 2):
                flag = 0

        # If valid arrangement
        if (flag):
            ways += 1

    return ways

# Driver code
n = 6

print(countWays(n))

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# implementation of the
// above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to return the count
// of required arrangements
static int countWays(int n)
{
  // Create a vector
  List<int> a =
       new List<int>();
  int i = 1;

  // Store numbers from
  // 1 to n
  while (i <= n)
    a.Add(i++);

  // To store the count
  // of ways
  int ways = 0;

  // Generate all the
  // permutations using
  // next_permutation in STL
  do
  {
    // Initialize flag to true
    // if first element is 1
    // else false
    bool flag = (a[0] == 1);

    // Checking if the current
    // permutation satisfies the
    // given conditions
    for (int j = 1; j < n; j++)
    {
      // If the current permutation
      // is invalid then set the
      // flag to false
      if (Math.Abs(a[j] -
                   a[j - 1]) > 2)
        flag = false;
    }

    // If valid arrangement
    if (flag)
      ways++;

    // Generate the next
    // permutation
  } while (next_permutation(a));

  return ways;
}

static bool next_permutation(List<int> p)
{
  for (int a = p.Count - 2;
           a >= 0; --a)
    if (p[a] < p[a + 1])
      for (int b = p.Count - 1;; --b)
        if (p[b] > p[a])
        {
          int t = p[a];
          p[a] = p[b];
          p[b]  =  t;

          for (++a, b = p.Count - 1;
                 a < b; ++a, --b)
          {
            t = p[a];
            p[a] = p[b];
            p[b] = t;
          }
          return true;
        }
  return false;
}

// Driver code
public static void Main(String[] args)
{
  int n = 6;
  Console.Write(countWays(n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation of the
// above approach

// Function to return the count
// of required arrangements
function countWays(n)
{
    // Create a vector
  let a =[];
  let i = 1;

  // Store numbers from
  // 1 to n
  while (i <= n)
    a.push(i++);

  // To store the count
  // of ways
  let ways = 0;

  // Generate all the permutations
  // using next_permutation in STL
  do
  {
    // Initialize flag to true
    // if first element is 1
    // else false
    let flag = (a[0] == 1);

    // Checking if the current
    // permutation satisfies the
    // given conditions
    for (let j = 1; j < n; j++)
    {
      // If the current permutation
      // is invalid then set the
      // flag to false
      if (Math.abs(a[j] -
                   a[j - 1]) > 2)
        flag = false;
    }

    // If valid arrangement
    if (flag)
      ways++;

    // Generate the next permutation
  } while (next_permutation(a));

  return ways;
}

function next_permutation(p)
{
    for (let a = p.length - 2;a >= 0; --a)
    {if (p[a] < p[a + 1])
      {for (let b = p.length - 1;; --b)
        {if (p[b] > p[a])
        {
          let t = p[a];
          p[a] = p[b];
          p[b] = t;

          for (++a, b = p.length - 1;
                 a < b; ++a, --b)
          {
            t = p[a];
            p[a] = p[b];
            p[b] = t;
          }
          return true;
        }
        }
        }
   }
  return false;
}

// Driver code
let n = 6;
document.write(countWays(n));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
9
```

**高效途径:**这个问题可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。
解决这个问题的更好的线性方法依赖于以下观察。寻找 2 的位置。设 a[i]为 n = i 的路数，有三种情况:

1.  **12 _ _ _ _ _**–“2”在第二位置。
2.  **1 * 2 _ _ _ _**–“2”在第三个位置。
    **1 * * 2 _ _**–“2”在第四个位置是不可能的，因为唯一可能的方式是(1342)，这和情况 3 一样。
    **1 * * * 2 _ _**–“2”在第五个位置是不可能的，因为 **1** 后面必须跟有 **3** 、 **3** 后面跟有 **5** 、 **2** 前面需要 **4** ，所以就变成了 **13542** ，还是跟例 3 一样。
3.  **最后一个位置的 1 _(I–2)术语 _ _ _ 2**–“2”(1357642 及类似)

对于每种情况，以下是子任务:
在[I–1]即(1 __(I–1)个术语 _ _)的每个术语上加 1。
关于 1_2_____ 只能有一个 1324 _ _(I–4)条款 ____，即 a[I–3]。

因此，循环关系将是，

> a[I]= a[I–1]+a[I–3]+1

基本情况是:

> a[0] = 0
> a[1] = 1
> a[2] = 1

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of required arrangements
int countWays(int n)
{
    // Create the dp array
    int dp[n + 1];

    // Initialize the base cases
    // as explained above
    dp[0] = 0;
    dp[1] = 1;

    // (12) as the only possibility
    dp[2] = 1;

    // Generate answer for greater values
    for (int i = 3; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 3] + 1;
    }

    // dp[n] contains the desired answer
    return dp[n];
}

// Driver code
int main()
{
    int n = 6;

    cout << countWays(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count
// of required arrangements
static int countWays(int n)
{
    // Create the dp array
    int []dp = new int[n + 1];

    // Initialize the base cases
    // as explained above
    dp[0] = 0;
    dp[1] = 1;

    // (12) as the only possibility
    dp[2] = 1;

    // Generate answer for greater values
    for (int i = 3; i <= n; i++)
    {
        dp[i] = dp[i - 1] + dp[i - 3] + 1;
    }

    // dp[n] contains the desired answer
    return dp[n];
}

// Driver code
public static void main(String args[])
{
    int n = 6;
    System.out.println(countWays(n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to return the count
# of required arrangements
def countWays(n):

    # Create the dp array
    dp = [0 for i in range(n + 1)]

    # Initialize the base cases
    # as explained above
    dp[0] = 0
    dp[1] = 1

    # (12) as the only possibility
    dp[2] = 1

    # Generate answer for greater values
    for i in range(3, n + 1):
        dp[i] = dp[i - 1] + dp[i - 3] + 1

    # dp[n] contains the desired answer
    return dp[n]

# Driver code
n = 6

print(countWays(n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

// Function to return the count
// of required arrangements
static int countWays(int n)
{
    // Create the dp array
    int []dp = new int[n + 1];

    // Initialize the base cases
    // as explained above
    dp[0] = 0;
    dp[1] = 1;

    // (12) as the only possibility
    dp[2] = 1;

    // Generate answer for greater values
    for (int i = 3; i <= n; i++)
    {
        dp[i] = dp[i - 1] + dp[i - 3] + 1;
    }

    // dp[n] contains the desired answer
    return dp[n];
}

// Driver code
public static void Main()
{
    int n = 6;
    Console.WriteLine(countWays(n));
}
}

// This code is contributed by Code@Mech.
```

## java 描述语言

```
<script>
// Function to return the count
// of required arrangements
function countWays( n)
{

    // Create the dp array
    let dp = new Array (n + 1);

    // Initialize the base cases
    // as explained above
    dp[0] = 0;
    dp[1] = 1;

    // (12) as the only possibility
    dp[2] = 1;

    // Generate answer for greater values
    for (let i = 3; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 3] + 1;
    }

    // dp[n] contains the desired answer
    return dp[n];
}

// Driver code
    let n = 6;

    document.write(countWays(n));

    // This code is contributed by shivanisinghss2110
</script>
```

**Output:** 

```
9
```