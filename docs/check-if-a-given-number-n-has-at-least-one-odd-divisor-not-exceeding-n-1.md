# 检查给定数字 N 是否至少有一个不超过 N–1 的奇数除数

> 原文:[https://www . geesforgeks . org/check-if-a-给定数字-n-有-至少-1 个奇数除数-不超过-n-1/](https://www.geeksforgeeks.org/check-if-a-given-number-n-has-at-least-one-odd-divisor-not-exceeding-n-1/)

给定一个正整数 **N** ，任务是检查给定的数字 **N** 是否在**【2，N–1】**范围内至少有 1 个奇数[除数](http://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)。如果发现是真的，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** N = 10
> **输出:**是
> **说明:**
> 10 有 5 为奇数除数。因此，打印“是”。
> 
> **输入:**N = 8
> T3】输出:否

**方法:**解决给定问题的思路是在**【3，sqrt(N)】**范围内迭代所有可能的[奇数除数](https://www.geeksforgeeks.org/find-sum-odd-factors-number/)，如果存在这样的[除数](https://www.geeksforgeeks.org/smallest-prime-divisor-of-a-number/)，则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether N
// has at least one odd divisor
// not exceeding N - 1 or not
string oddDivisor(int N)
{
    // Stores the value of N
    int X = N;

    // Reduce the given number
    // N by dividing it by 2
    while (N % 2 == 0) {
        N /= 2;
    }

    for (int i = 3; i * i <= X; i += 2) {

        // If N is divisible by
        // an odd divisor i
        if (N % i == 0) {
            return "Yes";
        }
    }

    // Check if N is an odd divisor after
    // reducing N by dividing it by 2
    if (N != X)
        return "Yes";

    // Otherwise
    return "No";
}

// Driver Code
int main()
{
    int N = 10;

    // Function Call
    cout << oddDivisor(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;

class GFG {

    // Function to check whether N
    // has at least one odd divisor
    // not exceeding N - 1 or not
    public static String oddDivisor(int N)
    {

        // Stores the value of N
        int X = N;

        // Reduce the given number
        // N by dividing it by 2
        while (N % 2 == 0) {
            N /= 2;
        }

        for (int i = 3; i * i <= X; i += 2) {

            // If N is divisible by
            // an odd divisor i
            if (N % i == 0) {
                return "Yes";
            }
        }

        // Check if N is an odd divisor after
        // reducing N by dividing it by 2
        if (N != X) {
            return "Yes";
        }

        // Otherwise
        return "No";
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 10;

        // Function Call
        System.out.println(oddDivisor(N));
    }
}

// This code is contributed by aditya7409.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to check whether N
# has at least one odd divisor
# not exceeding N - 1 or not
def oddDivisor(N):

    # Stores the value of N
    X = N

    # Reduce the given number
    # N by dividing it by 2
    while (N % 2 == 0):
        N //= 2

    i = 3
    while(i * i <= X):

        # If N is divisible by
        # an odd divisor i
        if (N % i == 0):
            return "Yes"
        i += 2

    # Check if N is an odd divisor after
    # reducing N by dividing it by 2
    if (N != X):
        return "Yes"

    # Otherwise
    return "No"

# Driver Code

N = 10
# Function Call
print(oddDivisor(N))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

  // Function to check whether N
  // has at least one odd divisor
  // not exceeding N - 1 or not
  public static string oddDivisor(int N)
  {

    // Stores the value of N
    int X = N;

    // Reduce the given number
    // N by dividing it by 2
    while (N % 2 == 0) {
      N /= 2;
    }

    for (int i = 3; i * i <= X; i += 2) {

      // If N is divisible by
      // an odd divisor i
      if (N % i == 0) {
        return "Yes";
      }
    }

    // Check if N is an odd divisor after
    // reducing N by dividing it by 2
    if (N != X) {
      return "Yes";
    }

    // Otherwise
    return "No";
  }

  // Driver Code
  static public void Main()
  {
    int N = 10;

    // Function Call
    Console.Write(oddDivisor(N));
  }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to check whether N
// has at least one odd divisor
// not exceeding N - 1 or not
function oddDivisor(N)
{

    // Stores the value of N
    var X = N;
    var i;

    // Reduce the given number
    // N by dividing it by 2
    while (N % 2 == 0) {
        N /= 2;
    }

    for (i = 3; i * i <= X; i += 2) {

        // If N is divisible by
        // an odd divisor i
        if (N % i == 0) {
            return "Yes";
        }
    }

    // Check if N is an odd divisor after
    // reducing N by dividing it by 2
    if (N != X)
        return "Yes";

    // Otherwise
    return "No";
}

// Driver Code
    var N = 10;

    // Function Call
    document.write(oddDivisor(N));

// This code is contributed by ipg2016107.
</script>
```

**Output**

```
Yes
```

***时间复杂度:** O(√N)*
***辅助空间:** O(1)*

***另一种方法:*** 任何数 n > 1 没有奇数除数的唯一可能是 n 是 2 的幂。

要检查二的幂，我们可以使用这种方法

n &(n-1)，只有当 n 是 2 的幂时，结果才为零。

## C++

```
#include <iostream>
using namespace std;

void oddDivisor(int n){
  //checking power of two or not
  if ((n & (n - 1)) == 0) {
        cout << "NO" << endl;
    } else {
        cout << "YES" << endl;
    }
}

int main() {
    int N = 10;

    // Function Call
    oddDivisor(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;

class GFG {

    public static void main (String[] args) {
      int N = 10;

    // Function Call
    oddDivisor(N);
    }

  static void oddDivisor(int n){
  //checking power of two or not
  if ((n & (n - 1)) == 0) {
        System.out.println("NO");
    } else {
        System.out.println("YES");
    }
}
}
```

**Output**

```
YES
```