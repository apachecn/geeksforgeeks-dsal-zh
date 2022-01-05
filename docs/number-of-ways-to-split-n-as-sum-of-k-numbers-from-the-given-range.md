# 从给定范围内将 N 拆分为 K 个数之和的方式数

> 原文:[https://www . geeksforgeeks . org/从给定范围内将 n 拆分为 k 个数字之和的方式数/](https://www.geeksforgeeks.org/number-of-ways-to-split-n-as-sum-of-k-numbers-from-the-given-range/)

给定四个正整数 **N，K，L，**和 **R** ，任务是将 N 拆分为位于范围**【L，R】**内的 K 个数之和。
**注意:**既然途径的数量可以很大。输出答案模 **1000000007** 。
**示例:**

> **输入:** N = 12，K = 3，L = 1，R = 5
> **输出:** 10
> {2，5，5}
> {3，4，5}
> {3，5，4}
> {4，3，5}
> {4，4，4}
> {4，5，3}
> {5，2，5}
> {5，3，4}
> 
> **输入:** N = 23，K = 4，L = 2，R = 10
> T3】输出: 480

**天真的方法**
我们可以使用[递归](https://www.geeksforgeeks.org/recursion/)来解决问题。在递归的每一步，试着做一组大小为 L 到 R 的所有
在递归中将有两个变化的参数:

*   pos–组号
*   左侧–还剩多少氮有待分配

下面是上述方法的实现:

## C++

```
// C++ implementation to count the
// number of ways to divide N in K
// groups such that each group
// has elements in range [L, R]

#include <bits/stdc++.h>

using namespace std;

const int mod = 1000000007;

// Function to count the number
// of ways to divide the number N
// in K groups such that each group
// has number of elements in range [L, R]
int calculate(int pos, int left,
              int k, int L, int R)
{
    // Base Case
    if (pos == k) {
        if (left == 0)
            return 1;
        else
            return 0;
    }

    // if N is divides completely
    // into less than k groups
    if (left == 0)
        return 0;

    int answer = 0;

    // put all possible values
    // greater equal to prev
    for (int i = L; i <= R; i++) {
        if (i > left)
            break;
        answer = (answer + calculate(pos + 1,
                                     left - i, k, L, R))
                 % mod;
    }
    return answer;
}

// Function to count the number of
// ways to divide the number N
int countWaystoDivide(int n, int k,
                      int L, int R)
{
    return calculate(0, n, k, L, R);
}

// Driver Code
int main()
{
    int N = 12;
    int K = 3;
    int L = 1;
    int R = 5;

    cout << countWaystoDivide(N, K, L, R);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count the
// number of ways to divide N in K
// groups such that each group
// has elements in range [L, R]
class GFG{

static int mod = 1000000007;

// Function to count the number
// of ways to divide the number N
// in K groups such that each group
// has number of elements in range [L, R]
static int calculate(int pos, int left,
                     int k, int L, int R)
{
    // Base Case
    if (pos == k)
    {
        if (left == 0)
            return 1;
        else
            return 0;
    }

    // If N is divides completely
    // into less than k groups
    if (left == 0)
        return 0;

    int answer = 0;

    // Put all possible values
    // greater equal to prev
    for(int i = L; i <= R; i++)
    {
       if (i > left)
           break;
       answer = ((answer +
                  calculate(pos + 1,left - i,
                            k, L, R)) % mod);
    }
    return answer;
}

// Function to count the number of
// ways to divide the number N
static int countWaystoDivide(int n, int k,
                             int L, int R)
{
    return calculate(0, n, k, L, R);
}

// Driver Code
public static void main(String[] args)
{
    int N = 12;
    int K = 3;
    int L = 1;
    int R = 5;

    System.out.print(countWaystoDivide(N, K, L, R));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 implementation to count the
# number of ways to divide N in K
# groups such that each group
# has elements in range [L, R]

mod = 1000000007

# Function to count the number
# of ways to divide the number N
# in K groups such that each group
# has number of elements in range [L, R]
def calculate(pos, left, k, L, R):

    # Base Case
    if (pos == k):
        if (left == 0):
            return 1
        else:
            return 0

    # If N is divides completely
    # into less than k groups
    if (left == 0):
        return 0

    answer = 0

    # Put all possible values
    # greater equal to prev
    for i in range(L, R + 1):
        if (i > left):
            break
        answer = (answer +
                  calculate(pos + 1,
                            left - i, k, L, R)) % mod
    return answer

# Function to count the number of
# ways to divide the number N
def countWaystoDivide(n, k, L, R):
    return calculate(0, n, k, L, R)

# Driver Code
N = 12
K = 3
L = 1
R = 5

print(countWaystoDivide(N, K, L, R))

# This code is contributed by divyamohan123
```

## C#

```
// C# implementation to count the
// number of ways to divide N in K
// groups such that each group
// has elements in range [L, R]
using System;

class GFG{

static int mod = 1000000007;

// Function to count the number
// of ways to divide the number N
// in K groups such that each group
// has number of elements in range [L, R]
static int calculate(int pos, int left,
                     int k, int L, int R)
{

    // Base Case
    if (pos == k)
    {
        if (left == 0)
            return 1;
        else
            return 0;
    }

    // If N is divides completely
    // into less than k groups
    if (left == 0)
        return 0;

    int answer = 0;

    // Put all possible values
    // greater equal to prev
    for(int i = L; i <= R; i++)
    {
       if (i > left)
           break;
       answer = ((answer +
                  calculate(pos + 1,left - i,
                            k, L, R)) % mod);
    }
    return answer;
}

// Function to count the number of
// ways to divide the number N
static int countWaystoDivide(int n, int k,
                             int L, int R)
{
    return calculate(0, n, k, L, R);
}

// Driver Code
public static void Main(String[] args)
{
    int N = 12;
    int K = 3;
    int L = 1;
    int R = 5;

    Console.Write(countWaystoDivide(N, K, L, R));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript implementation to count the
// number of ways to divide N in K
// groups such that each group
// has elements in range [L, R]

var mod = 1000000007;

// Function to count the number
// of ways to divide the number N
// in K groups such that each group
// has number of elements in range [L, R]
function calculate(pos, left, k, L, R)
{
    // Base Case
    if (pos == k) {
        if (left == 0)
            return 1;
        else
            return 0;
    }

    // if N is divides completely
    // into less than k groups
    if (left == 0)
        return 0;

    var answer = 0;

    // put all possible values
    // greater equal to prev
    for (var i = L; i <= R; i++) {
        if (i > left)
            break;
        answer = (answer + calculate(pos + 1,
                                     left - i, k, L, R))
                 % mod;
    }
    return answer;
}

// Function to count the number of
// ways to divide the number N
function countWaystoDivide(n, k, L, R)
{
    return calculate(0, n, k, L, R);
}

// Driver Code
var N = 12;
var K = 3;
var L = 1;
var R = 5;
document.write( countWaystoDivide(N, K, L, R));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
10
```

**时间复杂度:** *O(N <sup>K</sup> )* 。

**高效方法:**在前面的方法中我们可以看到，我们是在重复求解子问题，即遵循[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)的性质。所以我们可以用 DP 表[记住同样的事情。](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)

下面是上述方法的实现:

## C++

```
// C++ implementation to count the
// number of ways to divide N in K
// groups such that each group
// has elements in range [L, R]

#include <bits/stdc++.h>

using namespace std;

const int mod = 1000000007;

// DP Table
int dp[1000][1000];

// Function to count the number
// of ways to divide the number N
// in K groups such that each group
// has number of elements in range [L, R]
int calculate(int pos, int left,
              int k, int L, int R)
{
    // Base Case
    if (pos == k) {
        if (left == 0)
            return 1;
        else
            return 0;
    }

    // if N is divides completely
    // into less than k groups
    if (left == 0)
        return 0;

    // If the subproblem has been
    // solved, use the value
    if (dp[pos][left] != -1)
        return dp[pos][left];

    int answer = 0;

    // put all possible values
    // greater equal to prev
    for (int i = L; i <= R; i++) {
        if (i > left)
            break;
        answer = (answer + calculate(pos + 1,
                                     left - i, k, L, R))
                 % mod;
    }
    return dp[pos][left] = answer;
}

// Function to count the number of
// ways to divide the number N
int countWaystoDivide(int n, int k,
                      int L, int R)
{
    // Initialize DP Table as -1
    memset(dp, -1, sizeof(dp));
    return calculate(0, n, k, L, R);
}

// Driver Code
int main()
{
    int N = 12;
    int K = 3;
    int L = 1;
    int R = 5;

    cout << countWaystoDivide(N, K, L, R);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count the
// number of ways to divide N in K
// groups such that each group
// has elements in range [L, R]
class GFG{

static int mod = 1000000007;

// DP Table
static int [][]dp = new int[1000][1000];

// Function to count the number
// of ways to divide the number N
// in K groups such that each group
// has number of elements in range [L, R]
static int calculate(int pos, int left,
                     int k, int L, int R)
{

    // Base Case
    if (pos == k)
    {
        if (left == 0)
            return 1;
        else
            return 0;
    }

    // If N is divides completely
    // into less than k groups
    if (left == 0)
        return 0;

    // If the subproblem has been
    // solved, use the value
    if (dp[pos][left] != -1)
        return dp[pos][left];

    int answer = 0;

    // Put all possible values
    // greater equal to prev
    for(int i = L; i <= R; i++)
    {
       if (i > left)
           break;
       answer = (answer + calculate(pos + 1, left - i,
                                      k, L, R)) % mod;
    }
    return dp[pos][left] = answer;
}

// Function to count the number of
// ways to divide the number N
static int countWaystoDivide(int n, int k,
                             int L, int R)
{

    // Initialize DP Table as -1
    for(int i = 0; i < 1000; i++)
    {
       for(int j = 0; j < 1000; j++)
       {
          dp[i][j] = -1;
       }
    }
    return calculate(0, n, k, L, R);
}

// Driver Code
public static void main(String[] args)
{
    int N = 12;
    int K = 3;
    int L = 1;
    int R = 5;

    System.out.print(countWaystoDivide(N, K, L, R));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to count the
# number of ways to divide N in K
# groups such that each group
# has elements in range [L, R]
mod = 1000000007

# DP Table
dp = [[-1 for j in range(1000)]
          for i in range(1000)]

# Function to count the number
# of ways to divide the number N
# in K groups such that each group
# has number of elements in range [L, R]
def calculate(pos, left, k, L, R):

    # Base Case
    if (pos == k):
        if (left == 0):
            return 1
        else:
            return 0

    # if N is divides completely
    # into less than k groups
    if (left == 0):
        return 0

    # If the subproblem has been
    # solved, use the value
    if (dp[pos][left] != -1):
        return dp[pos][left]

    answer = 0

    # put all possible values
    # greater equal to prev
    for i in range(L, R + 1):
        if (i > left):
            break

        answer = (answer +
                  calculate(pos + 1,
                           left - i,
                           k, L, R)) % mod

    dp[pos][left] = answer

    return answer

# Function to count the number of
# ways to divide the number N
def countWaystoDivide(n, k, L, R):

    return calculate(0, n, k, L, R)

# Driver code
if __name__=="__main__":

    N = 12
    K = 3
    L = 1
    R = 5

    print(countWaystoDivide(N, K, L, R))

# This code is contributed by rutvik_56
```

## C#

```
// C# implementation to count the
// number of ways to divide N in K
// groups such that each group
// has elements in range [L, R]
using System;
class GFG{

static int mod = 1000000007;

// DP Table
static int [,]dp = new int[1000, 1000];

// Function to count the number
// of ways to divide the number N
// in K groups such that each group
// has number of elements in range [L, R]
static int calculate(int pos, int left,
                     int k, int L, int R)
{

    // Base Case
    if (pos == k)
    {
        if (left == 0)
            return 1;
        else
            return 0;
    }

    // If N is divides completely
    // into less than k groups
    if (left == 0)
        return 0;

    // If the subproblem has been
    // solved, use the value
    if (dp[pos, left] != -1)
        return dp[pos, left];

    int answer = 0;

    // Put all possible values
    // greater equal to prev
    for(int i = L; i <= R; i++)
    {
        if (i > left)
            break;
        answer = (answer + calculate(pos + 1, left - i,
                                       k, L, R)) % mod;
    }
    return dp[pos, left] = answer;
}

// Function to count the number of
// ways to divide the number N
static int countWaystoDivide(int n, int k,
                             int L, int R)
{

    // Initialize DP Table as -1
    for(int i = 0; i < 1000; i++)
    {
        for(int j = 0; j < 1000; j++)
        {
            dp[i, j] = -1;
        }
    }
    return calculate(0, n, k, L, R);
}

// Driver Code
public static void Main()
{
    int N = 12;
    int K = 3;
    int L = 1;
    int R = 5;

    Console.Write(countWaystoDivide(N, K, L, R));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// JavaScript implementation to count the
// number of ways to divide N in K
// groups such that each group
// has elements in range [L, R]

var mod = 1000000007;

// DP Table
var dp = Array.from(Array(1000), ()=>Array(1000));

// Function to count the number
// of ways to divide the number N
// in K groups such that each group
// has number of elements in range [L, R]
function calculate(pos, left, k, L, R)
{
    // Base Case
    if (pos == k) {
        if (left == 0)
            return 1;
        else
            return 0;
    }

    // if N is divides completely
    // into less than k groups
    if (left == 0)
        return 0;

    // If the subproblem has been
    // solved, use the value
    if (dp[pos][left] != -1)
        return dp[pos][left];

    var answer = 0;

    // put all possible values
    // greater equal to prev
    for (var i = L; i <= R; i++) {
        if (i > left)
            break;
        answer = (answer + calculate(pos + 1,
                                     left - i, k, L, R))
                 % mod;
    }
    return dp[pos][left] = answer;
}

// Function to count the number of
// ways to divide the number N
function countWaystoDivide(n, k, L, R)
{
    // Initialize DP Table as -1
    dp = Array.from(Array(1000), ()=>Array(1000).fill(-1));
    return calculate(0, n, k, L, R);
}

// Driver Code
var N = 12;
var K = 3;
var L = 1;
var R = 5;
document.write( countWaystoDivide(N, K, L, R));

</script>
```

**Output:** 

```
10
```

**时间复杂度:** *O(N*K)* 。
**辅助空间:** *O(N*K)。*