# 检查一个数是否可以表示为 K 个正整数的和，其中至少有 K–1 个几乎是素数

> 原文:[https://www . geesforgeks . org/check-如果一个数可以表示为 k 个正整数的和，其中至少有 k-1 个几乎是素数/](https://www.geeksforgeeks.org/check-if-a-number-can-be-represented-as-sum-of-k-positive-integers-out-of-which-at-least-k-1-are-nearly-prime/)

给定两个整数 **N** 和 **K** ，任务是检查 **N** 是否可以表示为 **K** 个正整数的和，其中至少**K–1**个几乎是素数。

> [**【近素数】**](https://www.geeksforgeeks.org/almost-prime-numbers/) :指可以表示为任意一对[素数](https://www.geeksforgeeks.org/prime-numbers/)乘积的数。

**示例:**

> ***输入*** **:** N = 100，K = 6
> ***输出:*** 是
> ***说明:** 100 可以表示为* 4 + 6 + 9 + 10 + 14 + 57，其中 4 (= 2 * 2)、6 ( = 3 * 2)、9 ( = 3 * 3)、10 ( = 5 * 2)和 14 ( = 7 * 2)接近素数。
> 
> ***输入*** : N=19，K = 4
> ***输出:*** 否

**逼近:**思路是求第一个**K–1**个近素数之和，检查其值是否小于等于 **N** 。如果发现为真，则打印**是**。否则，打印**否**。
按照以下步骤解决问题:

*   将第一个**K–1**个接近质数的和存储在一个变量中，比如说 **S** 。
*   从 **2** 开始迭代，直到获得 **S** ，执行以下步骤:
    *   检查当前数字的质因数[计数是否等于 **2** 。](https://www.geeksforgeeks.org/print-all-prime-factors-and-their-powers/)
    *   如果发现为真，将当前数字的值加到 **S** 上。
    *   如果这些数字的计数等于**K–1**，[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   检查 **S > =N. I** f 的值是否为真，打印**是**。
*   否则，打印**号**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count all prime
// factors of a given number
int countPrimeFactors(int n)
{
    int count = 0;

    // Count the number of 2s
    // that divides n
    while (n % 2 == 0) {
        n = n / 2;
        count++;
    }

    // Since n is odd at this point,
    // skip one element
    for (int i = 3; i <= sqrt(n); i = i + 2) {

        // While i divides n, count
        // i and divide n
        while (n % i == 0) {
            n = n / i;
            count++;
        }
    }

    // If n is a prime number
    // greater than 2
    if (n > 2)
        count++;

    return (count);
}

// Function to find the sum of
// first n nearly prime numbers
int findSum(int n)
{
    // Store the required sum
    int sum = 0;

    for (int i = 1, num = 2; i <= n; num++) {

        // Add this number if it is
        // satisfies the condition
        if (countPrimeFactors(num) == 2) {
            sum += num;

            // Increment count of
            // nearly prime numbers
            i++;
        }
    }
    return sum;
}

// Function to check if N can be
// represented as sum of K different
// positive integers out of which at
// least K - 1 of them are nearly prime
void check(int n, int k)
{
    // Store the sum of first
    // K - 1 nearly prime numbers
    int s = findSum(k - 1);

    // If sum is greater
    // than or equal to n
    if (s >= n)
        cout << "No";

    // Otherwise, print Yes
    else
        cout << "Yes";
}

// Driver Code
int main()
{
    int n = 100, k = 6;
    check(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count all prime
// factors of a given number
static int countPrimeFactors(int n)
{
    int count = 0;

    // Count the number of 2s
    // that divides n
    while (n % 2 == 0)
    {
        n = n / 2;
        count++;
    }

    // Since n is odd at this point,
    // skip one element
    for(int i = 3;
            i <= (int)Math.sqrt(n);
            i = i + 2)
    {

        // While i divides n, count
        // i and divide n
        while (n % i == 0)
        {
            n = n / i;
            count++;
        }
    }

    // If n is a prime number
    // greater than 2
    if (n > 2)
        count++;

    return (count);
}

// Function to find the sum of
// first n nearly prime numbers
static int findSum(int n)
{

    // Store the required sum
    int sum = 0;

    for(int i = 1, num = 2; i <= n; num++)
    {

        // Add this number if it is
        // satisfies the condition
        if (countPrimeFactors(num) == 2)
        {
            sum += num;

            // Increment count of
            // nearly prime numbers
            i++;
        }
    }
    return sum;
}

// Function to check if N can be
// represented as sum of K different
// positive integers out of which at
// least K - 1 of them are nearly prime
static void check(int n, int k)
{

    // Store the sum of first
    // K - 1 nearly prime numbers
    int s = findSum(k - 1);

    // If sum is greater
    // than or equal to n
    if (s >= n)
        System.out.print("No");

    // Otherwise, print Yes
    else
        System.out.print("Yes");
}

// Driver Code
public static void main(String[] args)
{
    int n = 100, k = 6;

    check(n, k);
}
}

// This code is contributed by splevel62
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to count all prime
# factors of a given number
def countPrimeFactors(n) :

    count = 0

    # Count the number of 2s
    # that divides n
    while (n % 2 == 0) :
        n = n // 2
        count += 1

    # Since n is odd at this point,
    # skip one element
    for i in range(3, int(math.sqrt(n) + 1), 2) :

        # While i divides n, count
        # i and divide n
        while (n % i == 0) :
            n = n // i
            count += 1

    # If n is a prime number
    # greater than 2
    if (n > 2) :
        count += 1

    return (count)

# Function to find the sum of
# first n nearly prime numbers
def findSum(n) :

    # Store the required sum
    sum = 0

    i = 1
    num = 2
    while(i <= n) :

        # Add this number if it is
        # satisfies the condition
        if (countPrimeFactors(num) == 2) :
            sum += num

            # Increment count of
            # nearly prime numbers
            i += 1
        num += 1

    return sum

# Function to check if N can be
# represented as sum of K different
# positive integers out of which at
# least K - 1 of them are nearly prime
def check(n, k) :

    # Store the sum of first
    # K - 1 nearly prime numbers
    s = findSum(k - 1)

    # If sum is great
    # than or equal to n
    if (s >= n) :
        print("No")

    # Otherwise, prYes
    else :
        print("Yes")

# Driver Code

n = 100
k = 6

check(n, k)

 # This code is contributed by susmitakundugoaldanga.
```

## C#

```
// C# program for above approach
using System;

public class GFG
{
  // Function to count all prime
  // factors of a given number
  static int countPrimeFactors(int n)
  {
    int count = 0;

    // Count the number of 2s
    // that divides n
    while (n % 2 == 0)
    {
      n = n / 2;
      count++;
    }

    // Since n is odd at this point,
    // skip one element
    for(int i = 3;
        i <= (int)Math.Sqrt(n);
        i = i + 2)
    {

      // While i divides n, count
      // i and divide n
      while (n % i == 0)
      {
        n = n / i;
        count++;
      }
    }

    // If n is a prime number
    // greater than 2
    if (n > 2)
      count++;

    return (count);
  }

  // Function to find the sum of
  // first n nearly prime numbers
  static int findSum(int n)
  {

    // Store the required sum
    int sum = 0;

    for(int i = 1, num = 2; i <= n; num++)
    {

      // Add this number if it is
      // satisfies the condition
      if (countPrimeFactors(num) == 2)
      {
        sum += num;

        // Increment count of
        // nearly prime numbers
        i++;
      }
    }
    return sum;
  }

  // Function to check if N can be
  // represented as sum of K different
  // positive integers out of which at
  // least K - 1 of them are nearly prime
  static void check(int n, int k)
  {

    // Store the sum of first
    // K - 1 nearly prime numbers
    int s = findSum(k - 1);

    // If sum is greater
    // than or equal to n
    if (s >= n)
      Console.WriteLine("No");

    // Otherwise, print Yes
    else
      Console.WriteLine("Yes");
  }

  // Driver code
  public static void Main(String[] args)
  {
    int n = 100, k = 6;

    check(n, k);
  }
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count all prime
// factors of a given number
function countPrimeFactors(n)
{
    var count = 0;

    // Count the number of 2s
    // that divides n
    while (n % 2 == 0)
    {
        n = parseInt(n / 2);
        count++;
    }

    // Since n is odd at this point,
    // skip one element
    for(i = 3;
        i <= parseInt(Math.sqrt(n));
        i = i + 2)
    {

        // While i divides n, count
        // i and divide n
        while (n % i == 0)
        {
            n = parseInt(n / i);
            count++;
        }
    }

    // If n is a prime number
    // greater than 2
    if (n > 2)
        count++;

    return (count);
}

// Function to find the sum of
// first n nearly prime numbers
function findSum(n)
{

    // Store the required sum
    var sum = 0;

    for(i = 1, num = 2; i <= n; num++)
    {

        // Add this number if it is
        // satisfies the condition
        if (countPrimeFactors(num) == 2)
        {
            sum += num;

            // Increment count of
            // nearly prime numbers
            i++;
        }
    }
    return sum;
}

// Function to check if N can be
// represented as sum of K different
// positive integers out of which at
// least K - 1 of them are nearly prime
function check(n, k)
{

    // Store the sum of first
    // K - 1 nearly prime numbers
    var s = findSum(k - 1);

    // If sum is greater
    // than or equal to n
    if (s >= n)
        document.write("No");

    // Otherwise, print Yes
    else
        document.write("Yes");
}

// Driver Code
var n = 100, k = 6;

check(n, k);

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(K * √X)，其中 X 是第(K–1)<sup>次</sup>近素数。*
***辅助空间:** O(1)*