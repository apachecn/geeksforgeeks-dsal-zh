# 计算连续 N 天后价格 P 预期涨幅的程序

> 原文:[https://www . geesforgeks . org/program-to-compute-预计连续 n 天涨价/p/](https://www.geeksforgeeks.org/program-to-calculate-expected-increase-in-price-p-after-n-consecutive-days/)

给定一个整数 **P** ，在接下来的连续 **N** 天内，分别以 **50%** 的概率增加 **A** 或 **B** ，任务是在 **N** 天后找到[期望值](https://www.geeksforgeeks.org/expectation-expected-value-array/)。

**示例:**

> **输入:** P = 1000，A = 5，B = 10，N = 10
> **输出:** 1075
> **说明:**
> 连续 N 天后预期增加值等于:
> P+N *(A+B)/2 = 1000+10×7.5 = 1000+75 = 1075。
> 
> **输入:** P = 2000，a = 10，b = 20，N = 30
> T3】输出: 2450

**方法:**按照步骤解决问题:

1.  每天增加的期望值=(增加 A 的概率)* A +(增加 B 的概率)* B = **(1 / 2) * A + (1 / 2) * B** 。
2.  因此，一天后的增值= **(a + b) / 2。**
3.  因此， **N** 天后的数值增加= **N * (a + b) / 2。**
4.  因此， **N** 天后增加值= **P + N * (a + b) / 2。**
5.  将增加的值打印为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the increased
// value of P after N days
void expectedValue(int P, int a,
                   int b, int N)
{
    // Expected value of the
    // number P after N days
    double expValue
        = P + (N * 0.5 * (a + b));

    // Print the expected value
    cout << expValue;
}

// Driver Code
int main()
{
    int P = 3000, a = 20, b = 10, N = 30;
    expectedValue(P, a, b, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the increased
// value of P after N days
static void expectedValue(int P, int a,
                          int b, int N)
{

    // Expected value of the
    // number P after N days
    double expValue = P + (N * 0.5 * (a + b));

    // Print the expected value
    System.out.print(expValue);
}

// Driver code
public static void main(String[] args)
{
    int P = 3000, a = 20, b = 10, N = 30;
    expectedValue(P, a, b, N);
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to find the increased
# value of P after N days
def expectedValue(P, a, b, N):

    # Expected value of the
    # number P after N days
    expValue = P + (N * 0.5 * (a + b))

    # Print the expected value
    print(int(expValue))

# Driver Code
if __name__ == '__main__':

    P = 3000
    a = 20
    b = 10
    N = 30

    expectedValue(P, a, b, N)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the increased
// value of P after N days
static void expectedValue(int P, int a,
                          int b, int N)
{

    // Expected value of the
    // number P after N days
    double expValue = P + (N * 0.5 * (a + b));

    // Print the expected value
    Console.Write(expValue);
}

// Driver code
static void Main()
{
    int P = 3000, a = 20, b = 10, N = 30;
    expectedValue(P, a, b, N);
}
}

// This code is contributed by abhinavjain194
```

## java 描述语言

```
<script>

// Javascript program for
// the above approach

// Function to find the increased
// value of P after N days

    function expectedValue(P, a, b, N)
    {

       // Expected value of the
       // number P after N day

       var expValue = P + (N * 0.5 * (a + b)) ;

       return expValue;
      }

    // Driver code

      var P = 3000
      var a = 20
      var b = 10
      var N = 30

     document.write(expectedValue(P, a, b, N));

</script>
```

**Output:** 

```
3450
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)