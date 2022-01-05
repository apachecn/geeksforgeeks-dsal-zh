# 从 1 到 N 的所有完美平方因子的和

> 原文:[https://www . geeksforgeeks . org/从 1 到 n 的所有完美平方数之和/](https://www.geeksforgeeks.org/sum-of-all-perfect-square-divisors-of-numbers-from-1-to-n/)

给定一个数 **N** ，任务是找出从 **1** 到 **N** 的所有完美平方因子的和。
**示例:**

> **输入:** N = 5
> **输出:** 9
> **解释:**N = 5
> 1 = 1 的完美平方因子。
> 同样，2，3 = 1 的完美平方因子。
> 4 的完美平方因子= 1，4。
> 5 = 1 的完美平方除数(当然对于任何质数，只有 1 才是完美平方除数)
> 所以，总和= 1+1+1+(1+4)+1 = 9。
> 
> **输入:**N = 30
> T3】输出: 126
> 
> **输入:**N = 100
> T3】输出: 910

**天真法:**这种方法是基于[本文](https://www.geeksforgeeks.org/sum-divisors-1-n/)
中实现的方法，上述问题可以在 **O(N <sup>1/k</sup> )** 中解决，对于任何 **K <sup>th</sup>** 幂除数，其中 **N** 是我们要求其和的数。这是因为，在这个总和中，每个数字将贡献**下限(N/p)** 或 **int(N/p)** 次。因此，在迭代这些完美幂的时候，我们只需要将**【p * int(N/p)】**加到和上。

***时间复杂度:** O(√N)*

**有效方法:**

*   让我们从 start = 2 开始，找到哪个楼层(N/(start<sup>2</sup>)=楼层(N/(end <sup>2</sup> )的最大范围(开始到结束)
*   区间[开始，结束]中所有完美方块的贡献将贡献地板(N/(开始 <sup>2</sup> )次，因此我们可以立即对该范围进行更新。
*   范围[开始、结束]的贡献可以表示为:

> *楼层(N/(开始<sup>2</sup>)*(结束-开始-1)*

*   如何找到范围？
    对于给定的起始值，可以通过以下方式找到结束

> *sqrt(N/K)，其中 K = floor(N/(start^2))*

*   现在可以通过代入 start = end+1 找到下一个范围。

**时间复杂度:** *O(N <sup>1/3</sup> )* 作为 **N/(x <sup>2</sup> )** 不能取大于 **N <sup>1/3</sup>** 的不同值为 **N** 。

下面是上述方法的实现:

## C++

```
// C++ Program to find the
// sum of all perfect square
// divisors of numbers from 1 to N

#include <bits/stdc++.h>
using namespace std;

#define MOD 1000000007
#define int unsigned long long

// Function for finding inverse
// of a number iteratively
// Here we will find the inverse
// of 6, since it appears as
// denominator in the formula of
// sum of squares from 1 to N
int inv(int a)
{
    int o = 1;
    for (int p = MOD - 2;
         p > 0; p >>= 1) {

        if ((p & 1) == 1)
            o = (o * a) % MOD;
        a = (a * a) % MOD;
    }
    return o;
}

// Store the value of the inverse
// of 6 once as we don't need to call
// the function again and again
int inv6 = inv(6);

// Formula for finding the sum
// of first n squares
int sumOfSquares(int n)
{

    n %= MOD;
    return (((n * (n + 1))
             % MOD * (2 * n + 1))
            % MOD * inv6)
           % MOD;
}

int sums(int n)
{

    // No perfect square
    // exists which is
    // less than 4
    if (n < 4)
        return 0;

    // Starting from 2, present value
    // of start is denoted here as
    // curStart
    int curStart = 2, ans = 0;

    int sqrtN = sqrt(n);
    while (curStart <= n / curStart) {

        int V = n / (curStart * curStart);

        // Finding end of the segment
        // for which the contribution
        // will be same
        int end = sqrt(n / V);

        // Using the above mentioned
        // formula to find ans % MOD
        ans += (n / (curStart * curStart)
                % MOD * (sumOfSquares(end)
                         + MOD
                         - sumOfSquares(curStart - 1)))
               % MOD;

        if (ans >= MOD)
            ans -= MOD;

        // Now for mthe next iteration
        // start will become end+1
        curStart = end + 1;
    }

    // Finally returning the answer
    return ans;
}

// Driver Code
int32_t main()
{
    int input[] = { 5 };
    for (auto x : input) {
        cout << "sum of all perfect"
             << " square divisors from"
             << " 1 to " << x
             << " is: ";

        // Here we are adding x
        // because we have not
        // counted 1 as perfect
        // squares so if u want to
        // add it you can just add
        // that number to the ans
        cout << x + sums(x) << endl;
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// sum of all perfect square
// divisors of numbers from 1 to N
import java.util.*;

class GFG{

static final int MOD = 7;

// Function for finding inverse
// of a number iteratively
// Here we will find the inverse
// of 6, since it appears as
// denominator in the formula of
// sum of squares from 1 to N
static int inv(int a)
{
    int o = 1;
    for(int p = MOD - 2;
            p > 0; p >>= 1)
    {
        if ((p & 1) == 1)
            o = (o * a) % MOD;

        a = (a * a) % MOD;
    }
    return o;
}

// Store the value of the inverse
// of 6 once as we don't need to call
// the function again and again
static int inv6 = inv(6);

// Formula for finding the sum
// of first n squares
static int sumOfSquares(int n)
{
    n %= MOD;
    return (((n * (n + 1)) %
            MOD * (2 * n + 1)) %
            MOD * inv6) % MOD;
}

static int sums(int n)
{

    // No perfect square
    // exists which is
    // less than 4
    if (n < 4)
        return 0;

    // Starting from 2, present value
    // of start is denoted here as
    // curStart
    int curStart = 2, ans = 0;

    int sqrtN = (int)Math.sqrt(n);
    while (curStart <= n / curStart)
    {
        int V = n / (curStart * curStart);

        // Finding end of the segment
        // for which the contribution
        // will be same
        int end = (int)Math.sqrt(n / V);

        // Using the above mentioned
        // formula to find ans % MOD
        ans += (n / (curStart * curStart) %
              MOD * (sumOfSquares(end) + MOD -
                     sumOfSquares(curStart - 1))) % MOD;

        if (ans >= MOD)
            ans -= MOD;

        // Now for mthe next iteration
        // start will become end+1
        curStart = end + 1;
    }

    // Finally returning the answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int input[] = {5};
    for(int x : input)
    {
        System.out.print("sum of all perfect " +
                         "square divisors from " +
                         "1 to " +  x + " is: ");

        // Here we are adding x
        // because we have not
        // counted 1 as perfect
        // squares so if u want to
        // add it you can just add
        // that number to the ans
        System.out.print(x + sums(x) + "\n");
    }
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to find the
# sum of all perfect square
# divisors of numbers from 1 to N
from math import *
MOD = 1000000007

# Function for finding inverse
# of a number iteratively
# Here we will find the inverse
# of 6, since it appears as
# denominator in the formula of
# sum of squares from 1 to N
def inv (a):

    o = 1
    p = MOD - 2
    while (p > 0):

        if (p % 2 == 1):
            o = (o * a) % MOD

        a = (a * a) % MOD
        p >>= 1

    return o

# Store the value of the inverse
# of 6 once as we don't need to call
# the function again and again
inv6 = inv(6)

# Formula for finding the sum
# of first n squares
def sumOfSquares (n):

    n %= MOD
    return (((n * (n + 1)) %
            MOD * (2 * n + 1)) %
            MOD * inv6) % MOD

def sums (n):

    # No perfect square exists which
    # is less than 4
    if (n < 4):
        return 0

    # Starting from 2, present value
    # of start is denoted here as curStart
    curStart = 2
    ans = 0

    sqrtN = int(sqrt(n))
    while (curStart <= n // curStart):
        V = n // (curStart * curStart)

        # Finding end of the segment for
        # which the contribution will be same
        end = int(sqrt(n // V))

        # Using the above mentioned
        # formula to find ans % MOD
        ans += ((n // (curStart * curStart) %
                MOD * (sumOfSquares(end) +
                MOD - sumOfSquares(curStart - 1))) % MOD)

        if (ans >= MOD):
            ans -= MOD

        # Now for mthe next iteration
        # start will become end+1
        curStart = end + 1

    # Finally return the answer
    return ans

# Driver Code
if __name__ == '__main__':

    Input = [5]
    for x in Input:
        print("sum of all perfect "\
              "square " , end = '')
        print("divisors from 1 to", x,
              "is: ", end = '')

        # Here we are adding x because we have
        # not counted 1 as perfect squares so if u
        # want to add it you can just add that
        # number to the ans
        print(x + sums(x))

# This code is contributed by himanshu77
```

## C#

```
// C# program to find the
// sum of all perfect square
// divisors of numbers from 1 to N
using System;
class GFG{

static readonly int MOD = 7;

// Function for finding inverse
// of a number iteratively
// Here we will find the inverse
// of 6, since it appears as
// denominator in the formula of
// sum of squares from 1 to N
static int inv(int a)
{
  int o = 1;
  for(int p = MOD - 2;
          p > 0; p >>= 1)
  {
    if ((p & 1) == 1)
      o = (o * a) % MOD;

    a = (a * a) % MOD;
  }

  return o;
}

// Store the value of the inverse
// of 6 once as we don't need to call
// the function again and again
static int inv6 = inv(6);

// Formula for finding the sum
// of first n squares
static int sumOfSquares(int n)
{
  n %= MOD;
  return (((n * (n + 1)) %
            MOD * (2 * n + 1)) %
            MOD * inv6) % MOD;
}

static int sums(int n)
{
  // No perfect square
  // exists which is
  // less than 4
  if (n < 4)
    return 0;

  // Starting from 2, present
  // value of start is denoted
  // here as curStart
  int curStart = 2, ans = 0;

  int sqrtN = (int)Math.Sqrt(n);
  while (curStart <= n / curStart)
  {
    int V = n / (curStart * curStart);

    // Finding end of the segment
    // for which the contribution
    // will be same
    int end = (int)Math.Sqrt(n / V);

    // Using the above mentioned
    // formula to find ans % MOD
    ans += (n / (curStart * curStart) %
            MOD * (sumOfSquares(end) + MOD -
                   sumOfSquares(curStart -
                                1))) % MOD;

    if (ans >= MOD)
      ans -= MOD;

    // Now for mthe next iteration
    // start will become end+1
    curStart = end + 1;
  }

  // Finally returning
  // the answer
  return ans;
}

// Driver Code
public static void Main(String[] args)
{
  int []input = {5};
  foreach(int x in input)
  {
    Console.Write("sum of all perfect " +
                  "square divisors from " +
                  "1 to " + x + " is: ");

    // Here we are adding x
    // because we have not
    // counted 1 as perfect
    // squares so if u want to
    // add it you can just add
    // that number to the ans
    Console.Write(x + sums(x) + "\n");
  }
}
}

// This code is contributed by Rajput-Ji
```

**Output:** 

```
sum of all perfect square divisors from 1 to 5 is: 9

```

***时间复杂度:** O(N <sup>1/3</sup> )*