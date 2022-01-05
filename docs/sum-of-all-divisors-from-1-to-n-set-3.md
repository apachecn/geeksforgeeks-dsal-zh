# 从 1 到 N 的所有除数之和|集合 3

> 原文:[https://www . geeksforgeeks . org/all-dividers 之和-从-1 到-n-set-3/](https://www.geeksforgeeks.org/sum-of-all-divisors-from-1-to-n-set-3/)

给定一个正整数 **N** ，任务是求从 **1** 到 **N** 的所有数的除数之和。
**示例:**

> **输入:** N = 5
> **输出:** 21
> **解释:**
> 1 到 5 所有数的除数之和= 21。
> 1->1 的除数
> 2->1、2 的除数
> 3->1、3 的除数
> 4->1、2、4 的除数
> 5->1、5 的除数，因此和= 21
> 
> **输入:** N = 6
> **输出:** 33
> **解释:**
> 1 到 6 所有数的除数之和= 33。
> 1->1 的除数
> 2->1、2 的除数
> 3->1、3 的除数
> 4->1、2、4 的除数
> 5->1、5 的除数
> 6->1、2、3、6 的除数，因此和= 33

**天真和线性方法:**天真和线性方法参考从 1 到 n 的所有因子的[和](https://www.geeksforgeeks.org/sum-divisors-1-n/)。
**对数法:**对数时间法参考从 1 到 N 的所有除数之和|集合 2 。

**高效方法:**
按照以下步骤解决问题:

*   我们可以观察到，对于从 **1** 到 **N** 的每个数字 ***x*** ，都出现在其最高倍数≤ **N** 的总和中。
*   因此，通过公式 **x *楼层(N / x)** 计算每个 ***x*** 的贡献，
*   可以观察到**楼层(N/i)** 对于一系列连续的数字 **l <sub>1</sub> ，l <sub>2</sub> ，l <sub>3</sub> …。l <sub>r</sub>** 。因此，与其计算每个 **i** 的 **l <sub>i</sub> *楼层(不适用)**，不如计算**(l<sub>1</sub>+l<sub>2</sub>+l<sub>3</sub>+…。+l<sub>r</sub>)* floor(N/l<sub>1</sub>)**，降低了计算复杂度。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

#define int long long int
#define m 1000000007

// Function to find the sum
// of all divisors of all
// numbers from 1 to N
void solve(long long n)
{

    // Stores the sum
    long long s = 0;

    for (int l = 1; l <= n;) {

        // Marks the last point of
        // occurence with same count
        int r = n / floor(n / l);

        int x = (((r % m) * ((r + 1)
                             % m))
                 / 2)
                % m;
        int y = (((l % m) * ((l - 1)
                             % m))
                 / 2)
                % m;
        int p = ((n / l) % m);

        // Calculate the sum
        s = (s + (((x - y) % m) * p) % m
             + m)
            % m;

        s %= m;
        l = r + 1;
    }

    // Return the result
    cout << (s + m) % m;
}

// Driver Code
signed main()
{
    long long n = 12;
    solve(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG{

static final int m = 1000000007;

// Function to find the sum
// of all divisors of all
// numbers from 1 to N
static void solve(long n)
{
  // Stores the sum
  long s = 0;

  for (int l = 1; l <= n;)
  {
    // Marks the last point of
    // occurence with same count
    int r = (int)(n /
             Math.floor(n / l));

    int x = (((r % m) *
             ((r + 1) %
               m)) / 2) % m;
    int y = (((l % m) *
             ((l - 1) %
               m)) / 2) % m;
    int p = (int)((n / l) % m);

    // Calculate the sum
    s = (s + (((x - y) %
                m) * p) %
                m + m) % m;

    s %= m;
    l = r + 1;
  }

  // Return the result
  System.out.print((s + m) % m);
}

// Driver Code
public static void main(String[] args)
{
  long n = 12;
  solve(n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach
import math
m = 1000000007

# Function to find the sum
# of all divisors of all
# numbers from 1 to N
def solve(n):

    # Stores the sum
    s = 0;
    l = 1;
    while(l < n + 1):

        # Marks the last point of
        # occurence with same count
        r = (int)(n /
             math.floor(n / l));

        x = ((((r % m) *
              ((r + 1) % m)) / 2) % m);
        y = ((((l % m) *
              ((l - 1) % m)) / 2) % m);
        p = (int)((n / l) % m);

        # Calculate the sum
        s = ((s + (((x - y) % m) *
                     p) % m + m) % m);

        s %= m;
        l = r + 1;

    # Return the result
    print (int((s + m) % m));

# Driver Code
if __name__ == '__main__':

    n = 12;
    solve(n);

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

static readonly int m = 1000000007;

// Function to find the sum
// of all divisors of all
// numbers from 1 to N
static void solve(long n)
{

  // Stores the sum
  long s = 0;

  for(int l = 1; l <= n;)
  {

    // Marks the last point of
    // occurence with same count
    int r = (int)(n /(Math.Floor((double)n/l)));

    int x = (((r % m) *
             ((r + 1) %
             m)) / 2) % m;
    int y = (((l % m) *
             ((l - 1) %
             m)) / 2) % m;
    int p = (int)((n / l) % m);

    // Calculate the sum
    s = (s + (((x - y) %
               m) * p) %
                m + m) % m;

    s %= m;
    l = r + 1;
  }

  // Return the result
  Console.Write((s + m) % m);
}

// Driver Code
public static void Main(String[] args)
{
  long n = 12;

  solve(n);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program implementation
// of the approach

let m = 1000000007;

// Function to find the sum
// of all divisors of all
// numbers from 1 to N
function solve(n)
{
  // Stores the sum
  let s = 0;

  for (let l = 1; l <= n;)
  {
    // Marks the last point of
    // occurence with same count
    let r = (n /
             Math.floor(n / l));

    let x = Math.floor(((r % m) *
             ((r + 1) %
               m)) / 2) % m;
    let y = Math.floor(((l % m) *
             ((l - 1) %
               m)) / 2) % m;
    let p = (Math.floor(n / l) % m);

    // Calculate the sum
    s = (s + (((x - y) %
                m) * p) %
                m + m) % m;

    s %= m;
    l = r + 1;
  }

  // Return the result
  document.write((s + m) % m);
}

// Driver Code

    let n = 12;
  solve(n);

 // This code is contributed by splevel62.
</script>
```

**Output**

```
127
```

***时间复杂度:** O(√N)*
***辅助空间:** O(1)*