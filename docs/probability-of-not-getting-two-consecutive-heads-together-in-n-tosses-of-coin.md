# N 次抛硬币没有连续两个头像在一起的概率

> 原文:[https://www . geeksforgeeks . org/连续两次掷硬币不中头概率/](https://www.geeksforgeeks.org/probability-of-not-getting-two-consecutive-heads-together-in-n-tosses-of-coin/)

给定一枚投掷 **N** 次的公平硬币，任务是确定没有两个头像连续出现的概率。

**示例:**

> **输入:** N = 2
> **输出:** 0.75
> **说明:**
> 硬币掷 2 次，可能的结果是{TH，HT，TT，HH}。
> 因为在四分之三的结果中，头部不会同时出现。
> 因此，所需概率为(3/4)或 0.75
> 
> **输入:** N = 3
> **输出:** 0.62
> **说明:**
> 硬币掷 3 次，可能的结果是{TTT、HTT、THT、TTH、HHT、HTH、THH、HHH}。
> 因为八分之五的结果中，头部不会同时出现。
> 因此，所需概率为(5/8)或 0.62

**方法:**必须对有利结果的数量进行以下观察。

*   **N = 1 时:**可能的结果是{T，H}。两者中有**两个**有利的结果。
*   **N = 2 时:**可能的结果是{TH，HT，TT，HH}。四个中有**三个**有利结果。
*   **N = 3 时:**同样，可能的结果是{TTT、HTT、THT、TTH、HHT、HTH、THH、HHH}。八个中有**五个**有利结果。
*   **N = 4 时:**同样，可能的结果有{TTTT、TTTH、TTHT、THTT、HTTT、TTHH、THTH、HTHT、HHTT、THHT、HTTH、THHH、HTHH、HHTH、HHHT、hhhhhh }。十六个中有**八个**有利结果。

显然，有利结果的数量遵循斐波那契数列，其中 Fn(1) = 2，Fn(2) = 3，依此类推。因此，想法是实现斐波那契序列，以便找到有利案例的数量。显然，病例总数为 2 <sup>N</sup> 。
为了计算概率，使用以下公式:

> P =有利案例/案例总数

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// probability of not getting two
// consecutive heads together when
// N coins are tossed
#include <bits/stdc++.h>
using namespace std;

float round(float var,int digit)
{
  float value = (int)(var *
                 pow(10, digit) + .5);
  return (float)value /
          pow(10, digit);
}

// Function to compute the N-th
// Fibonacci number in the
// sequence where a = 2
// and b = 3
int probability(int N)
{
  // The first two numbers in
  // the sequence are initialized
  int a = 2;
  int b = 3;

  //  Base cases
  if (N == 1)
  {
    return a;
  }
  else if(N == 2)
  {
    return b;
  }
  else
  {
    // Loop to compute the fibonacci
    // sequence based on the first
    // two initialized numbers
    for(int i = 3; i <= N; i++)
    {
      int c = a + b;
      a = b;
      b = c;
    }
    return b;
  }
}

// Function to find the probability
// of not getting two consecutive
// heads when N coins are tossed
float operations(int N)
 {
  // Computing the number of
  // favourable cases
  int x = probability(N);

  // Computing the number of
  // all possible outcomes for
  // N tosses
  int y = pow(2, N);

  return round((float)x /
               (float)y, 2);
}

// Driver code
int main()
{
  int N = 10;
  cout << (operations(N));
}

// Thus code is contributed by Rutvik_56
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// probability of not getting two
// consecutive heads together when
// N coins are tossed
class GFG{

public static float round(float var, int digit)
{
    float value = (int)(var *
                   Math.pow(10, digit) + .5);
    return (float)value /
           (float)Math.pow(10, digit);
}

// Function to compute the N-th
// Fibonacci number in the
// sequence where a = 2
// and b = 3
public static int probability(int N)
{

    // The first two numbers in
    // the sequence are initialized
    int a = 2;
    int b = 3;

    //  Base cases
    if (N == 1)
    {
        return a;
    }
    else if (N == 2)
    {
        return b;
    }
    else
    {

        // Loop to compute the fibonacci
        // sequence based on the first
        // two initialized numbers
        for(int i = 3; i <= N; i++)
        {
            int c = a + b;
            a = b;
            b = c;
        }
        return b;
    }
}

// Function to find the probability
// of not getting two consecutive
// heads when N coins are tossed
public static float operations(int N)
{

    // Computing the number of
    // favourable cases
    int x = probability(N);

    // Computing the number of
    // all possible outcomes for
    // N tosses
    int y = (int)Math.pow(2, N);

    return round((float)x /
                 (float)y, 2);
}

// Driver code
public static void main(String[] args)
{
    int N = 10;

    System.out.println((operations(N)));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 implementation to find the
# probability of not getting two
# consecutive heads together when
# N coins are tossed

import math

# Function to compute the N-th
# Fibonacci number in the
# sequence where a = 2
# and b = 3
def probability(N):

    # The first two numbers in
    # the sequence are initialized
    a = 2
    b = 3

    # Base cases
    if N == 1:
        return a
    elif N == 2:
        return b
    else:

        # Loop to compute the fibonacci
        # sequence based on the first
        # two initialized numbers
        for i in range(3, N + 1):
            c = a + b
            a = b
            b = c
        return b

# Function to find the probability
# of not getting two consecutive
# heads when N coins are tossed
def operations(N):

    # Computing the number of
    # favourable cases
    x = probability (N)

    # Computing the number of
    # all possible outcomes for
    # N tosses
    y = math.pow(2, N)

    return round(x / y, 2)

# Driver code
if __name__ == '__main__':

    N = 10

    print(operations(N))

```

## C#

```
// C# implementation to find the
// probability of not getting two
// consecutive heads together when
// N coins are tossed
using System;

class GFG{

public static float round(float var, int digit)
{
    float value = (int)(var *
                   Math.Pow(10, digit) + .5);
    return (float)value /
           (float)Math.Pow(10, digit);
}

// Function to compute the N-th
// Fibonacci number in the
// sequence where a = 2
// and b = 3
public static int probability(int N)
{

    // The first two numbers in
    // the sequence are initialized
    int a = 2;
    int b = 3;

    //  Base cases
    if (N == 1)
    {
        return a;
    }
    else if (N == 2)
    {
        return b;
    }
    else
    {

        // Loop to compute the fibonacci
        // sequence based on the first
        // two initialized numbers
        for(int i = 3; i <= N; i++)
        {
            int c = a + b;
            a = b;
            b = c;
        }
        return b;
    }
}

// Function to find the probability
// of not getting two consecutive
// heads when N coins are tossed
public static float operations(int N)
{

    // Computing the number of
    // favourable cases
    int x = probability(N);

    // Computing the number of
    // all possible outcomes for
    // N tosses
    int y = (int)Math.Pow(2, N);

    return round((float)x /
                 (float)y, 2);
}

// Driver code
public static void Main(string[] args)
{
    int N = 10;

    Console.WriteLine((operations(N)));
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>
// javascript implementation to find the
// probability of not getting two
// consecutive heads together when
// N coins are tossed   
function round(vr, digit) {
        var value = parseInt( (vr* Math.pow(10, digit) + .5));
        return  value /  Math.pow(10, digit);
    }

    // Function to compute the N-th
    // Fibonacci number in the
    // sequence where a = 2
    // and b = 3
    function probability(N) {

        // The first two numbers in
        // the sequence are initialized
        var a = 2;
        var b = 3;

        // Base cases
        if (N == 1) {
            return a;
        } else if (N == 2) {
            return b;
        } else {

            // Loop to compute the fibonacci
            // sequence based on the first
            // two initialized numbers
            for (i = 3; i <= N; i++) {
                var c = a + b;
                a = b;
                b = c;
            }
            return b;
        }
    }

    // Function to find the probability
    // of not getting two consecutive
    // heads when N coins are tossed
    function operations(N) {

        // Computing the number of
        // favourable cases
        var x = probability(N);

        // Computing the number of
        // all possible outcomes for
        // N tosses
        var y = parseInt( Math.pow(2, N));

        return round(x /  y, 2);
    }

    // Driver code
    var N = 10;
    document.write((operations(N)));

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
0.14
```

时间复杂度:0(N)

辅助空间:0(1)