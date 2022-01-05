# 计算到达数组末尾所需的最小因子跳跃

> 原文:[https://www . geeksforgeeks . org/count-最小因子跳跃-到达阵列末端所需的时间/](https://www.geeksforgeeks.org/count-minimum-factor-jumps-required-to-reach-the-end-of-an-array/)

给定一个正整数数组 **arr[]** ，任务是计算到达数组末尾所需的最小因子跳跃。从任何特定指数 **i** 来看，只能对 **K** 指数进行跳跃，其中 **K** 是**arr【I】**的一个因素。

**示例:**

> **输入:** arr[] = {2，8，16，55，99，100}
> **输出:** 2
> **说明:**
> 最优跳跃为:
> a)从 2 开始。
> b)因为因子 2 是[1，2]。因此只有 1 或 2 个索引跳转可用。因此，跳 1 指数达到 8。
> c)因为因子 8 是[1，2，4，8]。因此只有 1、2、4 或 8 个索引跳转可用。因此，他们跳了 4 个指数达到 100。
> d)我们已经到了终点，不需要再跳了。
> 所以需要 **2** 跳。
> 
> **输入:** arr[] = {2，4，6 }
> T3】输出: 1

**方法:**这个问题可以用[递归](https://www.geeksforgeeks.org/recursion/)解决。

*   首先，我们需要预先计算从 1 到 1000000 的每个数字的[因子，这样我们就可以在 O(1)时间内得到不同的跳跃选择。](https://www.geeksforgeeks.org/efficient-program-print-number-factors-n-numbers/)
*   然后，**递归**计算到达数组末尾所需的最小跳转并打印出来。

## C++

```
// C++ code to count minimum factor jumps
// to reach the end of array
#include <bits/stdc++.h>
using namespace std;

// vector to store factors of each integer
vector<int> factors[100005];

// Precomputing all factors of integers
// from 1 to 100000
void precompute()
{
    for (int i = 1; i <= 100000; i++) {
        for (int j = i; j <= 100000; j += i) {
            factors[j].push_back(i);
        }
    }
}

// Recursive function to count the minimum jumps
int solve(int arr[], int k, int n)
{
    // If we reach the end of array,
    // no more jumps are required
    if (k == n - 1) {
        return 0;
    }

    // If the jump results in out of index,
    // return INT_MAX
    if (k >= n) {
        return INT_MAX;
    }

    // Else compute the answer
    // using the recurrence relation
    int ans = INT_MAX;

    // Iterating over all choices of jumps
    for (auto j : factors[arr[k]]) {

        // Considering current factor as a jump
        int res = solve(arr, k + j, n);

        // Jump leads to the destination
        if (res != INT_MAX) {
            ans = min(ans, res + 1);
        }
    }

    // Return ans
    return ans;
}

// Driver code
int main()
{
    // pre-calculating the factors
    precompute();

    int arr[] = { 2, 8, 16, 55, 99, 100 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << solve(arr, 0, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to count minimum
// factor jumps to reach the
// end of array
import java.util.*;
public class GFG{

// vector to store factors
// of each integer
static Vector<Integer> []factors =
              new Vector[100005];

// Precomputing all factors
// of integers from 1 to 100000
static void precompute()
{
  for (int i = 0; i < factors.length; i++)
    factors[i] = new Vector<Integer>();
  for (int i = 1; i <= 100000; i++)
  {
    for (int j = i; j <= 100000; j += i)
    {
      factors[j].add(i);
    }
  }
}

// Function to count the
// minimum jumps
static int solve(int arr[],
                 int k, int n)
{
  // If we reach the end of
  // array, no more jumps
  // are required
  if (k == n - 1)
  {
    return 0;
  }

  // If the jump results in
  // out of index, return
  // Integer.MAX_VALUE
  if (k >= n)
  {
    return Integer.MAX_VALUE;
  }

  // Else compute the answer
  // using the recurrence relation
  int ans = Integer.MAX_VALUE;

  // Iterating over all choices
  // of jumps
  for (int j : factors[arr[k]])
  {
    // Considering current factor
    // as a jump
    int res = solve(arr, k + j, n);

    // Jump leads to the destination
    if (res != Integer.MAX_VALUE)
    {
      ans = Math.min(ans, res + 1);
    }
  }

  // Return ans
  return ans;
}

// Driver code
public static void main(String[] args)
{
  // pre-calculating
  // the factors
  precompute();

  int arr[] = {2, 8, 16,
               55, 99, 100};
  int n = arr.length;
  System.out.print(solve(arr, 0, n));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## C#

```
// C# code to count minimum
// factor jumps to reach the
// end of array
using System;
using System.Collections.Generic;
class GFG{

// vector to store factors
// of each integer
static List<int> []factors =
            new List<int>[100005];

// Precomputing all factors
// of integers from 1 to 100000
static void precompute()
{
  for (int i = 0;
           i < factors.Length; i++)
    factors[i] = new List<int>();
  for (int i = 1; i <= 100000; i++)
  {
    for (int j = i;
             j <= 100000; j += i)
    {
      factors[j].Add(i);
    }
  }
}

// Function to count the
// minimum jumps
static int solve(int []arr,
                 int k, int n)
{
  // If we reach the end of
  // array, no more jumps
  // are required
  if (k == n - 1)
  {
    return 0;
  }

  // If the jump results in
  // out of index, return
  // int.MaxValue
  if (k >= n)
  {
    return int.MaxValue;
  }

  // Else compute the answer
  // using the recurrence relation
  int ans = int.MaxValue;

  // Iterating over all choices
  // of jumps
  foreach (int j in factors[arr[k]])
  {
    // Considering current 
    // factor as a jump
    int res = solve(arr, k + j, n);

    // Jump leads to the
    // destination
    if (res != int.MaxValue)
    {
      ans = Math.Min(ans, res + 1);
    }
  }

  // Return ans
  return ans;
}

// Driver code
public static void Main(String[] args)
{
  // pre-calculating
  // the factors
  precompute();

  int []arr = {2, 8, 16,
               55, 99, 100};
  int n = arr.Length;
  Console.Write(solve(arr, 0, n));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## 计算机编程语言

```
# Python3 code to count minimum factor jumps
# to reach the end of array

# vector to store factors of each integer
factors = [[] for i in range(100005)]

# Precomputing all factors of integers
# from 1 to 100000
def precompute():

    for i in range(1, 100001):
        for j in range(i, 100001, i):

            factors[j].append(i)

# Function to count the minimum jumps
def solve(arr, k, n):

    # If we reach the end of array,
    # no more jumps are required
    if (k == n - 1):
        return 0

    # If the jump results in out of index,
    # return INT_MAX
    if (k >= n):
        return 1000000000

    # Else compute the answer
    # using the recurrence relation
    ans = 1000000000

    # Iterating over all choices of jumps
    for j in factors[arr[k]]:

        # Considering current factor as a jump
        res = solve(arr, k + j, n)

        # Jump leads to the destination
        if (res != 1000000000):
            ans = min(ans, res + 1)

    # Return ans
    return ans

# Driver code
if __name__ == '__main__':

    # pre-calculating the factors
    precompute()

    arr = [2, 8, 16, 55, 99, 100]
    n = len(arr)

    print(solve(arr, 0, n))

# This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript code to count minimum factor jumps
// to reach the end of array

// vector to store factors of each integer
let factors = new Array();

for (let i = 0; i < 100005; i++) {
    factors.push(new Array());
}

// Precomputing all factors of integers
// from 1 to 100000
function precompute() {
    for (let i = 1; i <= 100000; i++) {
        for (let j = i; j <= 100000; j += i) {
            factors[j].push(i);
        }
    }
}

// Function to count the minimum jumps
function solve(arr, k, n) {

    // If we reach the end of array,
    // no more jumps are required
    if (k == n - 1) {
        return 0;
    }

    // If the jump results in out of index,
    // return INT_MAX
    if (k >= n) {
        return Number.MAX_SAFE_INTEGER;
    }

    // Else compute the answer
    // using the recurrence relation
    let ans = Number.MAX_SAFE_INTEGER;

    // Iterating over all choices of jumps
    for (let j of factors[arr[k]]) {

        // Considering current factor as a jump
        let res = solve(arr, k + j, n);

        // Jump leads to the destination
        if (res != Number.MAX_SAFE_INTEGER) {
            ans = Math.min(ans, res + 1);
        }
    }

    // Return ans
    return ans;
}

// Driver code

// pre-calculating the factors
precompute();

let arr = [2, 8, 16, 55, 99, 100];
let n = arr.length;

document.write(solve(arr, 0, n));

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
2
```

**时间复杂度:** O(100005*2 <sup>N</sup>

**辅助空间:** O(100005)

**另一种方法:** [使用](http://www.geeksforgeeks.org/dynamic-programming/)[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)进行动态编程。

*   首先，我们需要预先计算从 1 到 1000000 的每个数字的[因子，这样我们就可以在 O(1)时间内得到不同的跳跃选择。](https://www.geeksforgeeks.org/efficient-program-print-number-factors-n-numbers/)
*   然后，让 **dp[i]** 成为到达 I 所需的最小跳跃，我们需要找到 **dp[n-1]** 。
*   所以，循环关系变成:

> ![dp[i] = min(dp[i], 1 + solve(i+j))                               ](img/8032725a0837140168817b140b695e0a.png "Rendered by QuickLaTeX.com")
> 
> 其中 j 是 arr[i]的因子之一，solve()是递归函数

*   使用这个循环关系找到最小跳跃并打印出来。

下面是上述方法的递归实现:

## C++

```
// C++ code to count minimum factor jumps
// to reach the end of array

#include <bits/stdc++.h>
using namespace std;

// vector to store factors of each integer
vector<int> factors[100005];

// dp array
int dp[100005];

// Precomputing all factors of integers
// from 1 to 100000
void precompute()
{
    for (int i = 1; i <= 100000; i++) {
        for (int j = i; j <= 100000; j += i) {
            factors[j].push_back(i);
        }
    }
}

// Function to count the minimum jumps
int solve(int arr[], int k, int n)
{

    // If we reach the end of array,
    // no more jumps are required
    if (k == n - 1) {
        return 0;
    }

    // If the jump results in out of index,
    // return INT_MAX
    if (k >= n) {
        return INT_MAX;
    }

    // If the answer has been already computed,
    // return it directly
    if (dp[k]) {
        return dp[k];
    }

    // Else compute the answer
    // using the recurrence relation
    int ans = INT_MAX;

    // Iterating over all choices of jumps
    for (auto j : factors[arr[k]]) {

        // Considering current factor as a jump
        int res = solve(arr, k + j, n);

        // Jump leads to the destination
        if (res != INT_MAX) {
            ans = min(ans, res + 1);
        }
    }

    // Return ans and memorize it
    return dp[k] = ans;
}

// Driver code
int main()
{

    // pre-calculating the factors
    precompute();

    int arr[] = { 2, 8, 16, 55, 99, 100 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << solve(arr, 0, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to count minimum
// factor jumps to reach the
// end of array
import java.util.*;
class GFG{

// vector to store factors
// of each integer
static Vector<Integer> []factors =
              new Vector[100005];

// dp array
static int []dp = new int[100005];

// Precomputing all factors
// of integers from 1 to 100000
static void precompute()
{
  for (int i = 0; i < factors.length; i++)
    factors[i] = new Vector<Integer>();
  for (int i = 1; i <= 100000; i++)
  {
    for (int j = i; j <= 100000; j += i)
    {
      factors[j].add(i);
    }
  }
}

// Function to count the
// minimum jumps
static int solve(int arr[],
                 int k, int n)
{
  // If we reach the end of
  // array, no more jumps
  // are required
  if (k == n - 1)
  {
    return 0;
  }

  // If the jump results in
  // out of index, return
  // Integer.MAX_VALUE
  if (k >= n)
  {
    return Integer.MAX_VALUE;
  }

  // If the answer has been
  // already computed, return
  // it directly
  if (dp[k] != 0)
  {
    return dp[k];
  }

  // Else compute the answer
  // using the recurrence relation
  int ans = Integer.MAX_VALUE;

  // Iterating over all choices
  // of jumps
  for (int j : factors[arr[k]])
  {
    // Considering current factor
    // as a jump
    int res = solve(arr, k + j, n);

    // Jump leads to the destination
    if (res != Integer.MAX_VALUE)
    {
      ans = Math.min(ans, res + 1);
    }
  }

  // Return ans and memorize it
  return dp[k] = ans;
}

// Driver code
public static void main(String[] args)
{
  // pre-calculating
  // the factors
  precompute();

  int arr[] = {2, 8, 16,
               55, 99, 100};
  int n = arr.length;
  System.out.print(solve(arr, 0, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 code to count minimum factor jumps
# to reach the end of array

# vector to store factors of each integer
factors= [[] for i in range(100005)];

# dp array
dp = [0 for i in range(100005)];

# Precomputing all factors of integers
# from 1 to 100000
def precompute():

    for i in range(1, 100001):
        for j in range(i, 100001, i):

            factors[j].append(i);

# Function to count the minimum jumps
def solve(arr, k, n):

    # If we reach the end of array,
    # no more jumps are required
    if (k == n - 1):
        return 0;

    # If the jump results in out of index,
    # return INT_MAX
    if (k >= n):
        return 1000000000

    # If the answer has been already computed,
    # return it directly
    if (dp[k]):
        return dp[k];

    # Else compute the answer
    # using the recurrence relation
    ans = 1000000000

    # Iterating over all choices of jumps
    for j in factors[arr[k]]:

        # Considering current factor as a jump
        res = solve(arr, k + j, n);

        # Jump leads to the destination
        if (res != 1000000000):
            ans = min(ans, res + 1);

    # Return ans and memorize it
    dp[k] = ans;
    return ans

# Driver code
if __name__=='__main__':

    # pre-calculating the factors
    precompute()

    arr = [ 2, 8, 16, 55, 99, 100 ]
    n = len(arr)

    print(solve(arr, 0, n))

# This code is contributed by rutvik_56
```

## C#

```
// C# code to count minimum
// factor jumps to reach the
// end of array
using System;
using System.Collections.Generic;
class GFG{

// vector to store factors
// of each integer
static List<int> []factors =
            new List<int>[100005];

// dp array
static int []dp = new int[100005];

// Precomputing all factors
// of integers from 1 to 100000
static void precompute()
{
  for (int i = 0;
           i < factors.Length; i++)
    factors[i] = new List<int>();
  for (int i = 1; i <= 100000; i++)
  {
    for (int j = i;
             j <= 100000; j += i)
    {
      factors[j].Add(i);
    }
  }
}

// Function to count the
// minimum jumps
static int solve(int []arr,
                 int k, int n)
{
  // If we reach the end of
  // array, no more jumps
  // are required
  if (k == n - 1)
  {
    return 0;
  }

  // If the jump results in
  // out of index, return
  // int.MaxValue
  if (k >= n)
  {
    return int.MaxValue;
  }

  // If the answer has been
  // already computed, return
  // it directly
  if (dp[k] != 0)
  {
    return dp[k];
  }

  // Else compute the answer
  // using the recurrence relation
  int ans = int.MaxValue;

  // Iterating over all choices
  // of jumps
  foreach (int j in factors[arr[k]])
  {
    // Considering current 
    // factor as a jump
    int res = solve(arr, k + j, n);

    // Jump leads to the
    // destination
    if (res != int.MaxValue)
    {
      ans = Math.Min(ans, res + 1);
    }
  }

  // Return ans and
  // memorize it
  return dp[k] = ans;
}

// Driver code
public static void Main(String[] args)
{
  // pre-calculating
  // the factors
  precompute();

  int []arr = {2, 8, 16,
               55, 99, 100};
  int n = arr.Length;
  Console.Write(solve(arr, 0, n));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript code to count minimum factor jumps
// to reach the end of array

// vector to store factors of each integer
let factors = new Array();

// dp array
let dp = new Array(100005);

for (let i = 0; i < 100005; i++) {
    factors.push(new Array());
}

// Precomputing all factors of integers
// from 1 to 100000
function precompute() {
    for (let i = 1; i <= 100000; i++) {
        for (let j = i; j <= 100000; j += i) {
            factors[j].push(i);
        }
    }
}

// Function to count the minimum jumps
function solve(arr, k, n) {

    // If we reach the end of array,
    // no more jumps are required
    if (k == n - 1) {
        return 0;
    }

    // If the jump results in out of index,
    // return INT_MAX
    if (k >= n) {
        return Number.MAX_SAFE_INTEGER;
    }

    // If the answer has been already computed,
    // return it directly
    if (dp[k]) {
        return dp[k];
    }

    // Else compute the answer
    // using the recurrence relation
    let ans = Number.MAX_SAFE_INTEGER;

    // Iterating over all choices of jumps
    for (let j of factors[arr[k]]) {

        // Considering current factor as a jump
        let res = solve(arr, k + j, n);

        // Jump leads to the destination
        if (res != Number.MAX_SAFE_INTEGER) {
            ans = Math.min(ans, res + 1);
        }
    }

    // Return ans and memorize it
    return dp[k] = ans;
}

// Driver code

// pre-calculating the factors
precompute();

let arr = [2, 8, 16, 55, 99, 100];
let n = arr.length;

document.write(solve(arr, 0, n));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output**

```
2
```

**时间复杂度:** O(100000*N)

**辅助空间:** O(100005)

**下面给出的是自下而上的迭代方法:**

## C++

```
// C++ program for bottom up approach
#include <bits/stdc++.h>
using namespace std;

// Vector to store factors of each integer
vector<int> factors[100005];

// Initialize the dp array
int dp[100005];

// Precompute all the
// factors of every integer
void precompute()
{
    for (int i = 1; i <= 100000; i++) {
        for (int j = i; j <= 100000; j += i)
            factors[j].push_back(i);
    }
}

// Function to count the
// minimum factor jump
int solve(int arr[], int n)
{

    // Initialise minimum jumps to
    // reach each cell as INT_MAX
    for (int i = 0; i <= 100005; i++) {
        dp[i] = INT_MAX;
    }

    // 0 jumps required to
    // reach the first cell
    dp[0] = 0;

    // Iterate over all cells
    for (int i = 0; i < n; i++) {
        // calculating for each jump
        for (auto j : factors[arr[i]]) {
            // If a cell is in bound
            if (i + j < n)
                dp[i + j] = min(dp[i + j], 1 + dp[i]);
        }
    }
    // Return minimum jumps
    // to reach last cell
    return dp[n - 1];
}

// Driver code
int main()
{
    // Pre-calculating the factors
    precompute();
    int arr[] = { 2, 8, 16, 55, 99, 100 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << solve(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for bottom up approach
import java.util.*;

class GFG{

// Vector to store factors of each integer
@SuppressWarnings("unchecked")
static Vector<Integer> []factors = new Vector[100005];

// Initialize the dp array
static int []dp = new int[100005];

// Precompute all the
// factors of every integer
static void precompute()
{
    for(int i = 1; i <= 100000; i++)
    {
        for(int j = i; j <= 100000; j += i)
            factors[j].add(i);
    }
}

// Function to count the
// minimum factor jump
static int solve(int arr[], int n)
{

    // Initialise minimum jumps to
    // reach each cell as Integer.MAX_VALUE
    for(int i = 0; i < 100005; i++)
    {
        dp[i] = Integer.MAX_VALUE;
    }

    // 0 jumps required to
    // reach the first cell
    dp[0] = 0;

    // Iterate over all cells
    for(int i = 0; i < n; i++)
    {

        // Calculating for each jump
        for(int j : factors[arr[i]])
        {

            // If a cell is in bound
            if (i + j < n)
                dp[i + j] = Math.min(dp[i + j],
                                        1 + dp[i]);
        }
    }

    // Return minimum jumps
    // to reach last cell
    return dp[n - 1];
}

// Driver code
public static void main(String[] args)
{
    for(int i = 0; i < factors.length; i++)
        factors[i] = new Vector<Integer>();

    // Pre-calculating the factors
    precompute();
    int arr[] = { 2, 8, 16, 55, 99, 100 };
    int n = arr.length;

    // Function call
    System.out.print(solve(arr, n));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for bottom up approach

# Vector to store factors of each integer
factors=[[] for i in range(100005)];

# Initialize the dp array
dp=[1000000000 for i in range(100005)];

# Precompute all the
# factors of every integer
def precompute():

    for i in range(1, 100001):

        for j in range(i, 100001, i):

            factors[j].append(i);

# Function to count the
# minimum factor jump
def solve(arr, n):

    # 0 jumps required to
    # reach the first cell
    dp[0] = 0;

    # Iterate over all cells
    for i in range(n):

        # calculating for each jump
        for j in factors[arr[i]]:

            # If a cell is in bound
            if (i + j < n):
                dp[i + j] = min(dp[i + j], 1 + dp[i]);

    # Return minimum jumps
    # to reach last cell
    return dp[n - 1];

# Driver code
if __name__=='__main__':

    # Pre-calculating the factors
    precompute();
    arr = [ 2, 8, 16, 55, 99, 100 ]
    n=len(arr)

    # Function call
    print(solve(arr,n))

    # This code is contributed by pratham76
```

## C#

```
// C# program for bottom up approach
using System;
using System.Collections.Generic;

class GFG{

// Vector to store factors of each integer
static List<List<int>> factors = new List<List<int>>();

// Initialize the dp array
static int[] dp;

// Precompute all the
// factors of every integer
static void precompute()
{
    for(int i = 1; i <= 100000; i++)
    {
        for(int j = i; j <= 100000; j += i)
            factors[j].Add(i);
    }
}

// Function to count the
// minimum factor jump
static int solve(int[] arr, int n)
{

    // Initialise minimum jumps to
    // reach each cell as Integer.MAX_VALUE
    for(int i = 0; i < 100005; i++)
    {
        dp[i] = int.MaxValue;
    }

    // 0 jumps required to
    // reach the first cell
    dp[0] = 0;

    // Iterate over all cells
    for(int i = 0; i < n; i++)
    {

        // Calculating for each jump
        foreach(int j in factors[arr[i]])
        {

            // If a cell is in bound
            if (i + j < n)
                dp[i + j] = Math.Min(dp[i + j],
                                        1 + dp[i]);
        }
    }

    // Return minimum jumps
    // to reach last cell
    return dp[n - 1];
}

// Driver code
static public void Main ()
{
    for(int i = 0; i < 100005; i++)
        factors.Add(new List<int>());

    dp = new int[100005];

    // Pre-calculating the factors
    precompute();
    int[] arr = { 2, 8, 16, 55, 99, 100 };
    int n = arr.Length;

    // Function call
    Console.Write(solve(arr, n));
}
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>

// Javascript program for bottom up approach

// Vector to store factors of each integer
var factors = Array.from(Array(100005), ()=>Array());

// Initialize the dp array
var dp = Array(100005);

// Precompute all the
// factors of every integer
function precompute()
{
    for (var i = 1; i <= 100000; i++) {
        for (var j = i; j <= 100000; j += i)
            factors[j].push(i);
    }
}

// Function to count the
// minimum factor jump
function solve(arr, n)
{

    // Initialise minimum jumps to
    // reach each cell as INT_MAX
    for (var i = 0; i <= 100005; i++) {
        dp[i] = 1000000000;
    }

    // 0 jumps required to
    // reach the first cell
    dp[0] = 0;

    // Iterate over all cells
    for (var i = 0; i < n; i++) {
        // calculating for each jump
        for (var j of factors[arr[i]]) {
            // If a cell is in bound
            if (i + j < n)
                dp[i + j] = Math.min(dp[i + j], 1 + dp[i]);
        }
    }
    // Return minimum jumps
    // to reach last cell
    return dp[n - 1];
}

 // Driver code
 // Pre-calculating the factors
 precompute();
 var arr = [2, 8, 16, 55, 99, 100];
 var n = arr.length
 // Function call
 document.write( solve(arr, n));

</script>
```

**Output**

```
2
```

**时间复杂度:** O(N <sup>2</sup> )

**辅助空间:** O(100005)