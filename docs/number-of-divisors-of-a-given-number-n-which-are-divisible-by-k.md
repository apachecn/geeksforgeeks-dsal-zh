# 给定数 N 中可被 K 整除的除数

> 原文:[https://www . geeksforgeeks . org/给定数的除数 n 可被 k 整除/](https://www.geeksforgeeks.org/number-of-divisors-of-a-given-number-n-which-are-divisible-by-k/)

给定一个数 **N** 和一个数 K，任务是找出能被 K 整除的 N 的除数，这里 K 是一个总是小于或等于√(N)的数

**示例:**

```
Input: N = 12, K = 3
Output: 3

Input: N = 8, K = 2
Output: 3
```

**简单方法**:简单的方法是检查从 1 到 N 的所有数字，检查是否有任何数字是 N 的除数并且可以被 k 整除，计数这种小于 N 的满足两个条件的数字。
以下是上述办法的实施情况:

## C++

```
// C++ program to count number of divisors
// of N which are divisible by K

#include <iostream>
using namespace std;

// Function to count number of divisors
// of N which are divisible by K
int countDivisors(int n, int k)
{
    // Variable to store
    // count of divisors
    int count = 0, i;

    // Traverse from 1 to n
    for (i = 1; i <= n; i++) {

        // increase the count if both
        // the conditions are satisfied
        if (n % i == 0 && i % k == 0) {

            count++;
        }
    }

    return count;
}

// Driver code
int main()
{
    int n = 12, k = 3;

    cout << countDivisors(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of divisors
// of N which are divisible by K

import java.io.*;

class GFG {

// Function to count number of divisors
// of N which are divisible by K
 static int countDivisors(int n, int k)
{
    // Variable to store
    // count of divisors
    int count = 0, i;

    // Traverse from 1 to n
    for (i = 1; i <= n; i++) {

        // increase the count if both
        // the conditions are satisfied
        if (n % i == 0 && i % k == 0) {

            count++;
        }
    }

    return count;
}

// Driver code
    public static void main (String[] args) {
      int n = 12, k = 3;

    System.out.println(countDivisors(n, k));
    }
}
// This code is contributed by shashank..
```

## 蟒蛇 3

```
# Python program to count number
# of divisors of N which are
# divisible by K

# Function to count number of divisors
# of N which are divisible by K
def countDivisors(n, k) :

    # Variable to store
    # count of divisors
    count = 0

    # Traverse from 1 to n
    for i in range(1, n + 1) :

        # increase the count if both
        # the conditions are satisfied
        if (n % i == 0 and i % k == 0) :

            count += 1

    return count

# Driver code    
if __name__ == "__main__" :

    n, k = 12, 3
    print(countDivisors(n, k))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to count number
// of divisors of N which are
// divisible by K
using System;

class GFG
{

// Function to count number
// of divisors of N which
// are divisible by K
static int countDivisors(int n, int k)
{
    // Variable to store
    // count of divisors
    int count = 0, i;

    // Traverse from 1 to n
    for (i = 1; i <= n; i++)
    {

        // increase the count if both
        // the conditions are satisfied
        if (n % i == 0 && i % k == 0)
        {
            count++;
        }
    }

    return count;
}

// Driver code
public static void Main ()
{
    int n = 12, k = 3;

    Console.WriteLine(countDivisors(n, k));
}
}

// This code is contributed by Shashank
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number
// of divisors of N which are
// divisible by K

// Function to count number of divisors
// of N which are divisible by K
function countDivisors($n, $k)
{
    // Variable to store
    // count of divisors
    $count = 0;

    // Traverse from 1 to n
    for ($i = 1; $i <= $n; $i++)
    {

        // increase the count if both
        // the conditions are satisfied
        if ($n % $i == 0 && $i % $k == 0)
        {

            $count++;
        }
    }

    return $count;
}

// Driver code
$n = 12; $k = 3;

echo countDivisors($n, $k);

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

// Function to count number of divisors
// of N which are divisible by K
function countDivisors(n, k)
{
    // Variable to store
    // count of divisors
    var count = 0, i;

    // Traverse from 1 to n
    for (i = 1; i <= n; i++) {

        // increase the count if both
        // the conditions are satisfied
        if (n % i == 0 && i % k == 0) {

            count++;
        }
    }

    return count;
}

var n = 12, k = 3;
document.write(countDivisors(n, k));

// This code is contributed by SoumikMondal.
</script>
```

**Output**

```
3
```