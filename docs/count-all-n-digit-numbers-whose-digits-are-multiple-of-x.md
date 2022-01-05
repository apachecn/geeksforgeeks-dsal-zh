# 统计所有 N 位数为 X 倍数的数字

> 原文:[https://www . geesforgeks . org/count-all-n-digits-numbers-其位数是 x 的倍数/](https://www.geeksforgeeks.org/count-all-n-digit-numbers-whose-digits-are-multiple-of-x/)

给定两个整数 **N** 和 **X** ，任务是找出所有可能的 **N** 位数的计数，其每一个位数都是 **X.** 的倍数

**示例:**

> **输入:** N = 1，X = 3
> **输出:** 4
> **说明:**
> 位数为 3 的倍数的一位数为 0、3、6、9。
> 所以答案会是 4。
> **输入:** N = 2，X = 4
> **输出:** 6
> **说明:**
> 数字为 4 的倍数的两位数是 40、44、48、80、84、88。
> 所以答案会是 6。

**天真法:**最简单的方法是迭代所有 [**N 位数字**](https://www.geeksforgeeks.org/print-all-n-digit-strictly-increasing-numbers/) ，即在**【10<sup>N–1</sup>、10<sup>N</sup>–1】**的范围内，对于每个数字，检查该数字的每个数字是否为 **X** 的倍数。增加此类数字的计数并打印最终计数。

***时间复杂度:**O((10<sup>N</sup>–10<sup>N–1</sup>)* N)*
***辅助空间:** O(1)*

**高效方法:**按照以下步骤解决问题:

1.  计算 **X** 的倍数的总位数，表示为 **total_Multiples** 。
2.  通过将以上所有数字排列在不同的位置，形成一个 **N 位**数字，就可以得到所需的计数。

    > **图解:**
    > 例如 N = 2，X = 3
    > 3 的倍数为 S = { 0，3，6，9 }
    > 
    > *   要查找所有 **2 位数字**的数字，将 **X** 的所有倍数排列成一个 **2 位数字**的数字并进行计数。
    > *   排列集合 **S** 中的数字。取 **0** 为最高有效位会得到 1 位数，所以一个数的最高有效位有 3 种排列方式，位数是 **3** 倍数的数的最后一位有 4 种排列方式。
    >     所以总途径= 3*4 = 12 所以答案会是 12。

3.  从上图可知，如果 **M** 是 **X** 的所有倍数的计数，那么 **N** 位数(对于 **N > 1** )所需的计数等于**(M–1)* M<sup>N–1</sup>**)。
4.  对于一位数，答案是 **M** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <stdio.h>
#define ll long long

// Function to calculate x^n
// using binary-exponentiation
ll power(ll x, ll n)
{
    // Stores the resultant power
    ll temp;

    if (n == 0)
        return 1;

    // Stores the value of x^(n/2)
    temp = power(x, n / 2);
    if (n % 2 == 0)
        return temp * temp;
    else
        return x * temp * temp;
}

// Function to count all N-digit numbers
// whose digits are multiples of x
ll count_Total_Numbers(ll n, ll x)
{
    ll total, multiples = 0;

    // Count all digits which
    // are multiples of x
    for (int i = 0; i < 10; i++) {

        // Check if current number
        // is a multiple of X
        if (i % x == 0)

            // Increase count of multiples
            multiples++;
    }

    // Check if it's a 1 digit number
    if (n == 1)
        return multiples;

    // Count the total numbers
    total = (multiples - 1)
            * power(multiples, n - 1);

    // Return the total numbers
    return total;
}

// Driver Code
int main()
{
    // Given N and X
    ll N = 1, X = 3;

    // Function Call
    printf("%lld ",
           count_Total_Numbers(N, X));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for 
// the above approach
class GFG{

// Function to calculate x^n
// using binary-exponentiation
static int power(int x, int n)
{

  // Stores the resultant power
  int temp;

  if (n == 0)
    return 1;

  // Stores the value of x^(n/2)
  temp = power(x, n / 2);
  if (n % 2 == 0)
    return temp * temp;
  else
    return x * temp * temp;
}

// Function to count aint N-digit 
// numbers whose digits are multiples 
// of x
static int count_Total_Numbers(int n, 
                               int x)
{
  int total, multiples = 0;

  // Count aint digits which
  // are multiples of x
  for (int i = 0; i < 10; i++) 
  {

    // Check if current number
    // is a multiple of X
    if (i % x == 0)

      // Increase count of multiples
      multiples++;
  }

  // Check if it's a 1 digit number
  if (n == 1)
    return multiples;

  // Count the total numbers
  total = (multiples - 1) * 
           power(multiples, n - 1);

  // Return the total numbers
  return total;
}

// Driver Code
public static void main(String[] args)
{
  // Given N and X
  int N = 1, X = 3;

  // Function Call
  System.out.printf("%d ", 
                    count_Total_Numbers(N, X));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate x^n
# using binary-exponentiation
def power(x, n):

    # Stores the resultant power
    temp = []

    if (n == 0):
        return 1

    # Stores the value of x^(n/2)
    temp = power(x, n // 2)
    if (n % 2 == 0):
        return temp * temp
    else:
        return x * temp * temp

# Function to count aN-digit numbers
# whose digits are multiples of x
def count_Total_Numbers(n, x):

    total, multiples = 0, 0

    # Count adigits which
    # are multiples of x
    for i in range(10):

        # Check if current number
        # is a multiple of X
        if (i % x == 0):

            # Increase count of multiples
            multiples += 1

    # Check if it's a 1 digit number
    if (n == 1):
        return multiples

    # Count the total numbers
    total = ((multiples - 1) * 
     power(multiples, n - 1))

    # Return the total numbers
    return total

# Driver Code
if __name__ == '__main__':

    # Given N and X
    N = 1
    X = 3

    # Function call
    print(count_Total_Numbers(N, X))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach 
using System;

class GFG{

// Function to calculate x^n
// using binary-exponentiation
static int power(int x, int n)
{

    // Stores the resultant power
    int temp;

    if (n == 0)
        return 1;

    // Stores the value of x^(n/2)
    temp = power(x, n / 2);

    if (n % 2 == 0)
        return temp * temp;
    else
        return x * temp * temp;
}

// Function to count aint N-digit 
// numbers whose digits are multiples 
// of x
static int count_Total_Numbers(int n, 
                               int x)
{
    int total, multiples = 0;

    // Count aint digits which
    // are multiples of x
    for(int i = 0; i < 10; i++) 
    {

        // Check if current number
        // is a multiple of X
        if (i % x == 0)

        // Increase count of multiples
        multiples++;
    }

    // Check if it's a 1 digit number
    if (n == 1)
        return multiples;

    // Count the total numbers
    total = (multiples - 1) * 
             power(multiples, n - 1);

    // Return the total numbers
    return total;
}

// Driver Code
public static void Main()
{

    // Given N and X
    int N = 1, X = 3;

    // Function call
    Console.Write(count_Total_Numbers(N, X));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to calculate x^n
// using binary-exponentiation
function power(x, n)
{

    // Stores the resultant power
    let temp;

    if (n == 0)
        return 1;

    // Stores the value of x^(n/2)
    temp = power(x, parseInt(n / 2));
    if (n % 2 == 0)
        return temp * temp;
    else
        return x * temp * temp;
}

// Function to count all N-digit numbers
// whose digits are multiples of x
function count_Total_Numbers(n, x)
{
    let total, multiples = 0;

    // Count all digits which
    // are multiples of x
    for (let i = 0; i < 10; i++)
    {

        // Check if current number
        // is a multiple of X
        if (i % x == 0)

            // Increase count of multiples
            multiples++;
    }

    // Check if it's a 1 digit number
    if (n == 1)
        return multiples;

    // Count the total numbers
    total = (multiples - 1)
            * power(multiples, n - 1);

    // Return the total numbers
    return total;
}

// Driver Code

    // Given N and X
    let N = 1, X = 3;

    // Function Call
    document.write(
           count_Total_Numbers(N, X));

// This code is contributed by subhammahato348.
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(Log N)*
***辅助空间:** O(1)*