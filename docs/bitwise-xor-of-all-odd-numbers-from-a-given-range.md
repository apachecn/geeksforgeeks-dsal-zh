# 给定范围内所有奇数的逐位异或

> 原文:[https://www . geeksforgeeks . org/给定范围内所有奇数的按位异或/](https://www.geeksforgeeks.org/bitwise-xor-of-all-odd-numbers-from-a-given-range/)

给定一个整数 **N** ，任务是在**【1，N】**范围内找到所有[奇数](https://www.geeksforgeeks.org/sum-first-n-odd-numbers-o1-complexity/)的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。

**例:**

> **输入:** 11
> **输出:** 2
> **解释:**对所有奇数进行按位异或运算，直到 11 = 1 ^ 3 ^ 5 ^ 7 ^ 9 ^ 11 = 2。
> 
> **输入:** 10
> **输出:** 9
> **解释:**对所有奇数进行按位异或运算，直到 10 = 1 ^ 3 ^ 5 ^ 7 ^ 9 = 9。

**天真方法:**解决问题最简单的方法是迭代范围**【1，N】**，对于每个值，[检查是否为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)。计算找到的每个奇数元素的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)，并将其打印为所需结果。
***时间复杂度:** O(N)*
***辅助空间:** O(1)*

**高效法:**对上述方法进行优化，思路是用以下公式计算所有小于等于 **N** 的奇数的**按位异或**:

> 设 f(n)= 2 ^ 4 ^ 6 ^…^(n-2)^ n 和 g(n)= 1 ^ 2 ^ 3 ^…(n-2)/2(n/2)
> =>f(n)= 2 * g(n)
> 
> 现在，让 k(n)= 1 ^ 2 ^ 3 ^…^(n-2)^ n
> 
> 所有小于或等于 N = k(N) ^ f(N)的奇数的异或运算[因为所有偶数都取消自己的位，只留下奇数]。
> 代入 f(N) = 2 * g(N)的值，对所有奇数进行异或运算，直到 N = k(N) ^ (2 * g(N))

按照以下步骤解决问题:

*   将**【1，N】**范围内的数字的[异或存储在一个变量中，比如 **K** 。](https://www.geeksforgeeks.org/calculate-xor-1-n/)
*   [如果 N 为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，将**【1)、(N–1)/2】**范围内的数字的[异或存储在一个变量中，比如 **g** 。否则，将**【1，N/2】**](https://www.geeksforgeeks.org/calculate-xor-1-n/)范围内的数字的[异或存储在 **g** 中。](https://www.geeksforgeeks.org/calculate-xor-1-n/)
*   使用导出的公式，将**结果**更新为 **K ^ (2 & g)** 。
*   完成以上步骤后，打印**结果**的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate Bitwise
// XOR of odd numbers in the range [1, N]
int findXOR(int n)
{
    // N & 3 is equivalent to n % 4
    switch (n & 3) {

    // If n is multiple of 4
    case 0:
        return n;

    // If n % 4 gives remainder 1
    case 1:
        return 1;

    // If n % 4 gives remainder 2
    case 2:
        return n + 1;

    // If n % 4 gives remainder 3
    case 3:
        return 0;
    }
}

// Function to find the XOR of odd
// numbers less than or equal to N
void findOddXOR(int n)
{

    // If number is even
    if (n % 2 == 0)

        // Print the answer
        cout << ((findXOR(n))
                 ^ (2 * findXOR(n / 2)));

    // If number is odd
    else

        // Print the answer
        cout << ((findXOR(n))
                 ^ (2 * findXOR((n - 1) / 2)));
}

// Driver Code
int main()
{
    int N = 11;

    // Function Call
    findOddXOR(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Function to calculate Bitwise
  // XOR of odd numbers in the range [1, N]
  static int findXOR(int n)
  {

    // N & 3 is equivalent to n % 4
    switch (n & 3)
    {

        // If n is multiple of 4
      case 0:
        return n;

        // If n % 4 gives remainder 1
      case 1:
        return 1;

        // If n % 4 gives remainder 2
      case 2:
        return n + 1;
    }
    // If n % 4 gives remainder 3
    return 0;

  }

  // Function to find the XOR of odd
  // numbers less than or equal to N
  static void findOddXOR(int n)
  {

    // If number is even
    if (n % 2 == 0)

      // Print the answer
      System.out.print(((findXOR(n))
                        ^ (2 * findXOR(n / 2))));

    // If number is odd
    else

      // Print the answer
      System.out.print(((findXOR(n))
                        ^ (2 * findXOR((n - 1) / 2))));
  }

  // Driver Code
  public static void main(String[] args)
  {
    int N = 11;

    // Function Call
    findOddXOR(N);
  }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to calculate Bitwise
# XOR of odd numbers in the range [1, N]
def findXOR(n):

    # N & 3 is equivalent to n % 4
    if (n % 4 == 0):

        # If n is multiple of 4
        return n;
    elif (n % 4 == 1):

        # If n % 4 gives remainder 1
        return 1;

    # If n % 4 gives remainder 2
    elif (n % 4 == 2):
        return n + 1;

    # If n % 4 gives remainder 3
    elif (n % 4 == 3):
        return 0;

# Function to find the XOR of odd
# numbers less than or equal to N
def findOddXOR(n):

    # If number is even
    if (n % 2 == 0):

        # Print the answer
        print(((findXOR(n)) ^ (2 * findXOR(n // 2))));

    # If number is odd
    else:

        # Print the answer
        print(((findXOR(n)) ^ (2 * findXOR((n - 1) // 2))));

# Driver Code
if __name__ == '__main__':
    N = 11;

    # Function Call
    findOddXOR(N);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to calculate Bitwise
  // XOR of odd numbers in the range [1, N]
  static int findXOR(int n)
  {

    // N & 3 is equivalent to n % 4
    switch (n & 3)
    {

        // If n is multiple of 4
      case 0:
        return n;

        // If n % 4 gives remainder 1
      case 1:
        return 1;

        // If n % 4 gives remainder 2
      case 2:
        return n + 1;
    }
    // If n % 4 gives remainder 3
    return 0;

  }

  // Function to find the XOR of odd
  // numbers less than or equal to N
  static void findOddXOR(int n)
  {

    // If number is even
    if (n % 2 == 0)

      // Print the answer
      Console.Write(((findXOR(n))
                     ^ (2 * findXOR(n / 2))));

    // If number is odd
    else

      // Print the answer
      Console.Write(((findXOR(n))
                     ^ (2 * findXOR((n - 1) / 2))));
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int N = 11;

    // Function Call
    findOddXOR(N);
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to calculate Bitwise
// XOR of odd numbers in the range [1, N]
function findXOR(n)
{
    // N & 3 is equivalent to n % 4
    switch (n & 3) {

    // If n is multiple of 4
    case 0:
        return n;

    // If n % 4 gives remainder 1
    case 1:
        return 1;

    // If n % 4 gives remainder 2
    case 2:
        return n + 1;

    // If n % 4 gives remainder 3
    case 3:
        return 0;
    }
}

// Function to find the XOR of odd
// numbers less than or equal to N
function findOddXOR(n)
{

    // If number is even
    if (n % 2 == 0)

        // Print the answer
        document.write((findXOR(n))
                ^ (2 * findXOR(n / 2)));

    // If number is odd
    else

        // Print the answer
        document.write((findXOR(n))
                ^ (2 * findXOR((n - 1) / 2)));
}

// Driver Code
    let N = 11;

    // Function Call
    findOddXOR(N);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)