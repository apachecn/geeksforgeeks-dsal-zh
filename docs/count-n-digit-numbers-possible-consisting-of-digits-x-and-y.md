# 计算可能由数字 X 和 Y 组成的 N 位数

> 原文:[https://www . geesforgeks . org/count-n-digits-numbers-可能-由-digits-x-and-y 组成/](https://www.geeksforgeeks.org/count-n-digit-numbers-possible-consisting-of-digits-x-and-y/)

给定三个整数 **N** 、 **X** 和 **Y** ，任务是找出满足以下条件的数字 **0** 到 **9** 可以构成的 **N** 位数的个数:

*   数字 **X** 和 **Y** 必须出现在其中。
*   该数字可能包含前导 **0** s

**注意:**由于答案可以很大，所以打印答案取模 **10 <sup>9</sup> + 7** 。

**示例:**

> **输入:** *N = 2，X = 1，Y = 2*
> ***输出:** 2*
> ***解释:***
> *只有两个可能的数字 12 和 21。*
> 
> ***输入:** N = 10，X = 3，Y = 4*
> T5**输出:** 100172994

**做法:**思路是用[排列组合](https://www.geeksforgeeks.org/permutation-and-combination/)的手法解决问题。按照以下步骤解决问题:

*   使用数字**{ 0–9 }**可能得到的总数 **N-** 数字为**10<sup>N</sup>T7】**
*   可以使用数字**{ 0–9 } –{ X }**形成的总计 **N-** 位数是**9<sup>N</sup>T7】**
*   总计**N**-可以使用数字**{ 0–9 }–{ X，Y}** 形成的数字是 **8 <sup>N</sup>**
*   total**N**-包含数字 **X** 和 **Y** 的数字是所有可能的数字与不包含数字 **X** 或 **Y** 的数字之间的差值，后跟包含除 **X** 和 **Y** 之外的所有数字的数字总和。因此，答案是**10<sup>N</sup>–2 * 9<sup>N</sup>+8<sup>N</sup>。**

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach
#include <bits/stdc++.h>
using namespace std;

const int mod = 1e9 + 7;

// Function for calculate
// (x ^ y) % mod in O(log y)
long long power(int x, int y)
{

    // Base Condition
    if (y == 0)
        return 1;

    // Transition state of
    // power Function
    long long int p
        = power(x, y / 2) % mod;

    p = (p * p) % mod;

    if (y & 1) {
        p = (x * p) % mod;
    }

    return p;
}

// Function for counting total numbers
// that can be formed such that digits
// X, Y are present in each number
int TotalNumber(int N)
{

    // Calculate the given expression
    int ans = (power(10, N)
               - 2 * power(9, N)
               + power(8, N) + 2 * mod)
              % mod;

    // Return the final answer
    return ans;
}

// Driver Code
int main()
{

    int N = 10, X = 3, Y = 4;
    cout << TotalNumber(N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static int mod = (int)(1e9 + 7);

// Function for calculate
// (x ^ y) % mod in O(log y)
static long power(int x, int y)
{

    // Base Condition
    if (y == 0)
        return 1;

    // Transition state of
    // power Function
    int p = (int)(power(x, y / 2) % mod);

    p = (p * p) % mod;

    if (y % 2 == 1)
    {
        p = (x * p) % mod;
    }
    return p;
}

// Function for counting total numbers
// that can be formed such that digits
// X, Y are present in each number
static int TotalNumber(int N)
{

    // Calculate the given expression
    int ans = (int)((power(10, N) - 2 *
                     power(9, N) +
                     power(8, N) +
                        2 * mod) % mod);

    // Return the final answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int N = 10, X = 3, Y = 4;

    System.out.print(TotalNumber(N) + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach
mod = 1e9 + 7

# Function for calculate
# (x ^ y) % mod in O(log y)
def power(x, y):

    # Base Condition
    if (y == 0):
        return 1

    # Transition state of
    # power Function
    p = power(x, y // 2) % mod

    p = (p * p) % mod

    if (y & 1):
        p = (x * p) % mod

    return p

# Function for counting total numbers
# that can be formed such that digits
# X, Y are present in each number
def TotalNumber(N):

    # Calculate the given expression
    ans = (power(10, N) - 2 *
           power(9, N) +
           power(8, N) + 2 * mod) % mod

    # Return the final answer
    return ans

# Driver Code
if __name__ == '__main__':

    N = 10
    X = 3
    Y = 4

    print(TotalNumber(N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG{

static int mod = (int)(1e9 + 7);

// Function for calculate
// (x ^ y) % mod in O(log y)
static long power(int x, int y)
{
  // Base Condition
  if (y == 0)
    return 1;

  // Transition state of
  // power Function
  int p = (int)(power(x,
           y / 2) % mod);

  p = (p * p) % mod;

  if (y % 2 == 1)
  {
    p = (x * p) % mod;
  }
  return p;
}

// Function for counting
// total numbers that can be
// formed such that digits
// X, Y are present in each number
static int TotalNumber(int N)
{   
  // Calculate the given expression
  int ans = (int)((power(10, N) - 2 *
                   power(9, N) +
                   power(8, N) +
                   2 * mod) % mod);

  // Return the
  // readonly answer
  return ans;
}

// Driver Code
public static void Main(String[] args)
{
  int N = 10;
  Console.Write(TotalNumber(N) + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript Program for the above approach

var mod = 1000000007;

// Function for calculate
// (x ^ y) % mod in O(log y)
function power(x, y)
{

    // Base Condition
    if (y == 0)
        return 1;

    // Transition state of
    // power Function
    var p
        = power(x, y / 2) % mod;

    p = (p * p) % mod;

    if (y & 1) {
        p = (x * p) % mod;
    }

    return p;
}

// Function for counting total numbers
// that can be formed such that digits
// X, Y are present in each number
function TotalNumber(N)
{

    // Calculate the given expression
    var ans = (power(10, N)
               - 2 * power(9, N)
               + power(8, N) + 2 * mod)
              % mod;

    // Return the final answer
    return ans;
}

// Driver Code
var N = 10, X = 3, Y = 4;
document.write( TotalNumber(N));

</script>
```

**Output**

```
100172994
```

***时间复杂度:**T3】O(*log N)*
T7**辅助空间:** O(1)*