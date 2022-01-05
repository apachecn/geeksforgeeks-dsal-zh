# 通过执行给定的操作将数字减少到 1 |设置 3

> 原文:[https://www . geesforgeks . org/通过执行给定的操作将一个数字减少到 1-set-3/](https://www.geeksforgeeks.org/reduce-a-number-to-1-by-performing-given-operations-set-3/)

给定一个整数 **N** ，任务是通过执行以下操作，找到将给定数 **N** 减少到 **1** 所需的步数:

1.  [如果数字是 2 的幂](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)，那么将数字除以 **2** 。
2.  否则，从 **N** 中减去比**N**T3】小 2 的最大幂[。](https://www.geeksforgeeks.org/highest-power-2-less-equal-given-number/)

**示例:**

> **输入:** N = 2
> **输出:** *1*
> **说明:**给定的数可以通过以下步骤减为 1:
> 将数除以 2，因为 N 是 2 的幂，将 N 修改为 1。
> 因此，N 只需 1 步就可以减少到 1。
> 
> **输入:** N = 7
> **输出:** 2
> **说明:**给定的数可以通过以下步骤减 1:
> 减去 4 小于 N 的 2 的最大幂，步骤后 N 修改为 N = 7-4 = 3。
> 减去 2 小于 N 的 2 的最大幂。步骤之后，N 修改为 N = 3-2 = 1。
> 因此，N 可以 2 步降 1。

**方法 1–**

**方法:**思路是递归计算所需的最小步数。

*   如果[数是 2 的幂](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)，那么只允许我们用 **2** 除这个数。
*   否则我们可以从 **N** 中减去小于 N 的 2 的[最大幂。](https://www.geeksforgeeks.org/highest-power-2-less-equal-given-number/)
*   因此，我们将对有效的操作和返回的操作数都使用递归。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to check
// if n is power of 2
int highestPowerof2(int n)
{
   int p = (int)log2(n);
   return (int)pow(2, p);
}

// Utility function to find highest
// power of 2 less than or equal
// to given number
bool isPowerOfTwo(int n)
{
   if(n==0)
   return false;

   return (ceil(log2(n)) == floor(log2(n)));
}

// Recursive function to find
// steps needed to reduce
// a given integer to 1
int reduceToOne(int N)
{
    // Base Condition
    if(N == 1){
        return 0;
    }
    // If the number is a power of 2
    if(isPowerOfTwo(N) == true){
        return 1 + reduceToOne(N/2);
    }
    // Else subtract the greatest
    //power of 2 smaller than N
    //from N
    else{
        return 1 + reduceToOne(N - highestPowerof2(N));
    }
}

// Driver Code
int main()
{
    // Input
    int N = 7;
    // Function call
    cout << reduceToOne(N) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach

class GFG {

  // Utility function to check
  // if n is power of 2
  static int highestPowerof2(int n)
  {
     int p = (int)(Math.log(n) / Math.log(2));
     return (int)Math.pow(2, p);
  }

  // Utility function to find highest
  // power of 2 less than or equal
  // to given number
  static boolean isPowerOfTwo(int n)
  {
     if(n==0)
     return false;

     return (int)(Math.ceil((Math.log(n) / Math.log(2)))) ==
       (int)(Math.floor(((Math.log(n) / Math.log(2)))));
  }

  // Recursive function to find
  // steps needed to reduce
  // a given integer to 1
  static int reduceToOne(int N)
  {
      // Base Condition
      if(N == 1){
          return 0;
      }
      // If the number is a power of 2
      if(isPowerOfTwo(N) == true){
          return 1 + reduceToOne(N/2);
      }
      // Else subtract the greatest
      //power of 2 smaller than N
      //from N
      else{
          return 1 + reduceToOne(N - highestPowerof2(N));
      }
  }

  // Driver Code
  public static void main(String [] args)
  {
      // Input
      int N = 7;
      // Function call
      System.out.println(reduceToOne(N));
  }

}

// This code is contributed by ihritik
```

## 计算机编程语言

```
# Python program for the above approach
import math

# Utility function to check
# Log base 2
def Log2(x):
    if x == 0:
        return false;

    return (math.log10(x) /
            math.log10(2));

# Utility function to check
# if x is power of 2
def isPowerOfTwo(n):
    return (math.ceil(Log2(n)) ==
            math.floor(Log2(n)));

# Utility function to find highest
# power of 2 less than or equal
# to given number
def highestPowerof2(n):

    p = int(math.log(n, 2));
    return int(pow(2, p));

# Recursive function to find
# steps needed to reduce
# a given integer to 1
def reduceToOne(N):

    # Base Condition
    if(N == 1):
        return 0

    # If the number is a power of 2
    if(isPowerOfTwo(N) == True):
        return 1 + reduceToOne(N/2)

    # Else subtract the greatest
    # power of 2 smaller than N
    # from N
    else:
        return 1 + reduceToOne(N - highestPowerof2(N))

# Driver Code

# Input
N = 7;

#Function call
print(reduceToOne(N))

# This code is contributed by Samim Hossain Mondal.
```

## C#

```
// C# program for the above approach
using System;

class GFG {

  // Utility function to check
  // if n is power of 2
  static int highestPowerof2(int n)
  {
     int p = (int)(Math.Log(n) / Math.Log(2));
     return (int)Math.Pow(2, p);
  }

  // Utility function to find highest
  // power of 2 less than or equal
  // to given number
  static bool isPowerOfTwo(int n)
  {
     if(n == 0)
     return false;

     return (int)(Math.Ceiling((Math.Log(n) / Math.Log(2)))) ==
       (int)(Math.Floor(((Math.Log(n) / Math.Log(2)))));
  }

  // Recursive function to find
  // steps needed to reduce
  // a given integer to 1
  static int reduceToOne(int N)
  {

      // Base Condition
      if(N == 1){
          return 0;
      }

      // If the number is a power of 2
      if(isPowerOfTwo(N) == true){
          return 1 + reduceToOne(N/2);
      }

      // Else subtract the greatest
      //power of 2 smaller than N
      //from N
      else{
          return 1 + reduceToOne(N - highestPowerof2(N));
      }
  }

  // Driver Code
  public static void Main()
  {

      // Input
      int N = 7;

      // Function call
      Console.Write(reduceToOne(N));
  }
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Utility function to check
// if n is power of 2
function isPowerOfTwo(n)
{
    if (n == 0)
        return false;

    return parseInt( (Math.ceil((Math.log(n) / Math.log(2))))) == parseInt( (Math.floor(((Math.log(n) / Math.log(2))))));
}

// Utility function to find highest
// power of 2 less than or equal
// to given number
function highestPowerof2(n)
{
    let p = parseInt(Math.log(n) / Math.log(2), 10);
    return Math.pow(2, p);
}

// Recursive function to find
// steps needed to reduce
// a given integer to 1
function reduceToOne(N)
{
    // Base Condition
    if(N == 1){
        return 0;
    }
    // If the number is a power of 2
    if(isPowerOfTwo(N) == true){
        return 1 + reduceToOne(N/2);
    }
    // Else subtract the greatest
    //power of 2 smaller than N
    //from N
    else{
        return 1 + reduceToOne(N - highestPowerof2(N));
    }
}

// Driver Code

// Input
let N = 7;

// Function call
document.write(reduceToOne(N));

// This code is contributed by Samim Hossain Mondal
</script>
```

**Output**

```
2
```

**方法 2–**

**方法:**给定的问题可以使用[按位运算符](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)来解决。按照以下步骤解决问题:

*   初始化两个变量，表示 **res** 值为 **0** 和 **MSB** 值为 **log <sub>2</sub> (N)** 以存储将该数减少到 **1** 所需的步数和 **N** 的[最高有效位](https://www.geeksforgeeks.org/find-significant-set-bit-number/)。
*   [迭代而](https://www.geeksforgeeks.org/java-while-loop-with-examples/) **N** 不等于 **1:**
    *   C [检查数字是否为 2 的幂](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)，然后将 **N** 除以 **2** 。
    *   否则，从 **N** 中减去[小于 N 的 2 的最大幂](https://www.geeksforgeeks.org/highest-power-of-2-less-than-or-equal-to-given-integer/)，即更新 **N** 为 **N=N-2 <sup>MSB</sup> 。**
    *   将 **res** 增加 **1** ，将 **MSB** 减少 **1** 。
*   最后，打印 **res** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find steps needed to
// reduce a given integer to 1
int reduceToOne(int N)
{
    // Stores the most
    // significant bit of N
    int MSB = log2(N);

    // Stores the number of steps
    // required to reduce N to 1
    int res = 0;

    // Iterates while N
    // is not equal 1
    while (N != 1) {

        // Increment res by 1
        res++;

        // If N is power of 2
        if (N & (N - 1) == 0) {

            // Divide N by 2
            N /= 2;
        }
        // Otherwise
        else {

            // Subtract 2 ^ MSB
            // from N
            N -= (1 << MSB);
        }
        // Decrement MSB by 1
        MSB--;
    }
    // Returns res
    return res;
}

// Driver code
int main()
{
    // Input
    int N = 7;
    // Function call
    cout << reduceToOne(N) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;

class GFG {
    public static int logarithm(int number, int base)
    {
        int res = (int)(Math.log(number) / Math.log(base));
        return res;
    }
    public static int reduceToOne(int N)
    {

        // Stores the most
        // significant bit of N
        int MSB = logarithm(N, 2);

        // Stores the number of steps
        // required to reduce N to 1
        int res = 0;

        // Iterates while N
        // is not equal 1
        while (N != 1) {

            // Increment res by 1
            res++;

            // If N is power of 2
            if ((N & (N - 1)) == 0) {

                // Divide N by 2
                N /= 2;
            }
            // Otherwise
            else {

                // Subtract 2 ^ MSB
                // from N
                N -= (1 << MSB);
            }
            // Decrement MSB by 1
            MSB--;
        }
        // Returns res
        return res;
    }

    public static void main(String[] args)
    {
        int N = 7;
        int res = reduceToOne(N);
        System.out.println(res);
    }
}

// This code is contributed by lokeshpotta20.
```

## 蟒蛇 3

```
# Python program for the above approach
import math

# Function to find steps needed to
# reduce a given integer to 1
def reduceToOne(N):

    # Stores the most
    # significant bit of N
    MSB = math.floor(math.log2(N))

    # Stores the number of steps
    # required to reduce N to 1
    res = 0

    # Iterates while N
    # is not equal 1
    while (N != 1):

        # Increment res by 1
        res += 1

        # If N is power of 2
        if (N & (N - 1) == 0):

            # Divide N by 2
            N //= 2

        # Otherwise
        else:
            # Subtract 2 ^ MSB
            # from N
            N -= (1 << MSB)

        # Decrement MSB by 1
        MSB-=1

    # Returns res
    return res

# Driver code
# Input
N = 7
# Function call
print(reduceToOne(N))

# This code is contributed by shubham Singh
```

## C#

```
// C# program for the above approach

using System;
using System.Collections.Generic;

class GFG{

// Function to find steps needed to
// reduce a given integer to 1
static int reduceToOne(int N)
{

    // Stores the most
    // significant bit of N
    int MSB = (int)(Math.Log(N)/Math.Log(2));

    // Stores the number of steps
    // required to reduce N to 1
    int res = 0;

    // Iterates while N
    // is not equal 1
    while (N != 1) {

        // Increment res by 1
        res++;

        // If N is power of 2
        if ((N & (N - 1)) == 0) {

            // Divide N by 2
            N /= 2;
        }
        // Otherwise
        else {

            // Subtract 2 ^ MSB
            // from N
            N -= (1 << MSB);
        }

        // Decrement MSB by 1
        MSB--;
    }

    // Returns res
    return res;
}

// Driver code
public static void Main()
{
    // Input
    int N = 7;

    // Function call
    Console.Write(reduceToOne(N));
}
}

// This code is contributed by bgangwar59.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    function logarithm(number, base)
    {
        let res = (Math.log(number) / Math.log(base));
        return res;
    }
    function reduceToOne(N)
    {

        // Stores the most
        // significant bit of N
        let MSB = logarithm(N, 2);

        // Stores the number of steps
        // required to reduce N to 1
        let res = 0;

        // Iterates while N
        // is not equal 1
        while (N != 1) {

            // Increment res by 1
            res++;

            // If N is power of 2
            if ((N & (N - 1)) == 0) {

                // Divide N by 2
                N /= 2;
            }
            // Otherwise
            else {

                // Subtract 2 ^ MSB
                // from N
                N -= (1 << MSB);
            }
            // Decrement MSB by 1
            MSB--;
        }
        // Returns res
        return res;
    }

        // Driver Code

        let N = 7;
        let res = reduceToOne(N);
        document.write(res);

</script>
```

**Output**

```
2
```

**时间复杂度:** O(log(N))
**辅助空间:** O(1)