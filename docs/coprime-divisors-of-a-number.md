# 一个数的互质因子

> 原文:[https://www.geeksforgeeks.org/coprime-divisors-of-a-number/](https://www.geeksforgeeks.org/coprime-divisors-of-a-number/)

给定一个整数 **N** 。任务是找到一对大于 1 的 N 的共质因数。如果这样的除数不存在，那么打印“-1”。

**示例:**

> **输入:** N = 45
> **输出:** 3 5
> **说明:**因为 3 和 5 是 45 的除数，gcd( 3，5 ) = 1。
> 因此，它们满足条件。
> 
> **输入:** N = 25
> **输出:** -1
> **说明:**没有一对 25 的除数满足其 gcd 为 1 的条件
> 。

**进场:**

1.  从 x = 2 迭代到 sqrt(N)，求 N 的所有除数
2.  对于任何值 x，检查它是否除以 N
3.  如果它除了，那么只要它能被除，就继续用 x 除 N。
4.  现在，检查 N 是否> 1，那么除数对(x，N)将具有
    gcd(x，N) == 1，因为‘x’的所有因子已经从 N 中消除
5.  同样，检查 x 的所有值。

下面是上述方法的实现:

## C++

```
// C++ program to find two coprime
// divisors of a given number
// such that both are greater
// than 1

#include <bits/stdc++.h>
using namespace std;

// Function which finds the
// required pair of divisors
// of N
void findCoprimePair(int N)
{
    // We iterate upto sqrt(N)
    // as we can find all the
    // divisors of N in this
    // time
    for (int x = 2; x <= sqrt(N); x++) {
        if (N % x == 0) {
            // If x is a divisor of N
            // keep dividing as long
            // as possible
            while (N % x == 0) {
                N /= x;
            }
            if (N > 1) {
                // We have found a
                // required pair
                cout << x << " "
                     << N << endl;
                return;
            }
        }
    }
    // No such pair of divisors
    // of N was found, hence
    // print -1
    cout << -1 << endl;
}

// Driver Code
int main()
{
    // Sample example 1
    int N = 45;
    findCoprimePair(N);

    // Sample example 2
    N = 25;
    findCoprimePair(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find two coprime
// divisors of a given number
// such that both are greater
// than 1
import java.util.*;

class GFG{

// Function which finds the
// required pair of divisors
// of N
public static void findCoprimePair(int N)
{

    // We iterate upto sqrt(N)
    // as we can find all the
    // divisors of N in this
    // time
    for(int x = 2; x <= Math.sqrt(N); x++)
    {
        if (N % x == 0)
        {

            // If x is a divisor of N
            // keep dividing as long
            // as possible
            while (N % x == 0)
            {
                N /= x;
            }
            if (N > 1)
            {

                // We have found a
                // required pair
                System.out.println(x + " " + N);
                return;
            }
        }
    }

    // No such pair of divisors
    // of N was found, hence
    // print -1
    System.out.println(-1);
}

// Driver code
public static void main(String[] args)
{

    // Sample example 1
    int N = 45;
    findCoprimePair(N);

    // Sample example 2
    N = 25;
    findCoprimePair(N);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to find two coprime
# divisors of a given number such that
# both are greater than 1
import math

# Function which finds the
# required pair of divisors
# of N
def findCoprimePair(N):

    # We iterate upto sqrt(N)
    # as we can find all the
    # divisors of N in this
    # time
    for x in range(2, int(math.sqrt(N)) + 1):
        if (N % x == 0):

            # If x is a divisor of N
            # keep dividing as long
            # as possible
            while (N % x == 0):
                N //= x

            if (N > 1):

                # We have found a
                # required pair
                print(x, N)
                return;

    # No such pair of divisors
    # of N was found, hence
    # print -1
    print("-1")

# Driver Code

# Sample example 1
N = 45
findCoprimePair(N)

# Sample example 2
N = 25
findCoprimePair(N)

# This code is contributed by Vishal Maurya.
```

## C#

```
// C# program to find two coprime
// divisors of a given number
// such that both are greater
// than 1
using System;
class GFG{

// Function which finds the
// required pair of divisors
// of N
public static void findCoprimePair(int N)
{
  // We iterate upto sqrt(N)
  // as we can find all the
  // divisors of N in this
  // time
  for(int x = 2;
          x <= Math.Sqrt(N); x++)
  {
    if (N % x == 0)
    {
      // If x is a divisor of N
      // keep dividing as long
      // as possible
      while (N % x == 0)
      {
        N /= x;
      }
      if (N > 1)
      {
        // We have found a
        // required pair
        Console.WriteLine(x +
                          " " + N);
        return;
      }
    }
  }

  // No such pair of divisors
  // of N was found, hence
  // print -1
  Console.WriteLine(-1);
}

// Driver code
public static void Main(String[] args)
{   
  // Sample example 1
  int N = 45;
  findCoprimePair(N);

  // Sample example 2
  N = 25;
  findCoprimePair(N);
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>

// JavaScript program to find two coprime
// divisors of a given number
// such that both are greater
// than 1

// Function which finds the
// required pair of divisors
// of N
function findCoprimePair(N)
{
    // We iterate upto sqrt(N)
    // as we can find all the
    // divisors of N in this
    // time
    for (let x = 2; x <= Math.sqrt(N); x++) {
        if (N % x == 0) {
            // If x is a divisor of N
            // keep dividing as long
            // as possible
            while (N % x == 0) {
                N = Math.floor(N / x);
            }
            if (N > 1) {
                // We have found a
                // required pair
                document.write(x + " "
                    + N + "<br>");
                return;
            }
        }
    }
    // No such pair of divisors
    // of N was found, hence
    // print -1
    document.write(-1 + "<br>");
}

// Driver Code
    // Sample example 1
    let N = 45;
    findCoprimePair(N);

    // Sample example 2
    N = 25;
    findCoprimePair(N);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
3 5
-1
```

**时间复杂度** : O( **sqrt(N)** )