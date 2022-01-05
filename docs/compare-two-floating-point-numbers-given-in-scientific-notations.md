# 比较科学符号

中给出的两个浮点数

> 原文:[https://www . geeksforgeeks . org/compare-two-floating-point-numbers-in-scientific-entrepreneurs/](https://www.geeksforgeeks.org/compare-two-floating-point-numbers-given-in-scientific-notations/)

给定两根弦 **N** 和 **M** 以**a * 10<sup>b</sup>T7】的形式。任务是比较给定的两个浮点数，并打印出**较小的数字**，如果两个数字相等，则打印相等。**

> 0

**示例:**

> n 和 M 是由两部分组成的两个数字:
> 
> 1.  **a1 为 N 的尾数，a2 为 m 的尾数**
> 2.  **b1 是 N 的指数，b2 是 m 的指数**
> 
> **输入:** N = 3*10^2，M = 299*10^0
> **输出:** M
> **解释:**
> a1 = 3，b1 = 2
> a2 = 299，B2 = 0
> n = 3*10^2 = 300
> m = 299*10^0 = 299。
> 我们知道 299 比 300 小。
> 
> **输入:** N = -5*10^3，M = -50*10^2
> **输出:**相等
> **解释:**t8】a1 =-5，b1 = 3
> a2 = -50，B2 = 2
> n = -5*10^3 =-5000
> m = -50*10^2 =-5000
> 因此，n 和 m 相等。
> 
> **输入:** N = -2*10^1，M = -3*10^1
> **输出:** M
> **解释:**
> a1 = -2，b1 = 1
> a2 = -3，B2 = 1
> n =-20
> m =-30
> -30 小于-20，因此 m 是较小的数字。

**天真方法:**我们将计算从字符串 N 和 M 中提取的数字的值，然后比较哪一个更好。[大整数](https://www.geeksforgeeks.org/biginteger-class-in-java/)类将用于存储和计算 [Java](https://www.geeksforgeeks.org/java/) 中的 N 和 M 的值。对于较大的测试用例，这种方法会产生超过时间限制的错误。

**最佳方法:**

*   从字符串 N 和 m 中提取尾数和指数
*   找到' * '的索引(假设**穆林)，那么穆林之前的子串就是尾数(a1)。**
*   找到'^'的指数，假设 **powInd** ，那么 powInd 之后的子串就是指数(b1)。
*   同样，找出 a2 和 b2。
*   **如果(a1 > 0 & & a2 < 0)** ，则打印 **M** ( M 始终较小)。
*   同样的，**如果(a2 > 0 & & a1 < 0)** ，打印 **N** 。
*   否则将需要使用日志进行比较。
*   以下公式将用于计算日志，并得出一个比较结果，以确定哪个数字更大。

> N = a1 * 10 ^ b1
> 
> 从两侧取原木底座 10
> 
> 对数 N =对数(a1)+B1 ——-(1)
> 
> 同样，log(M)= log(a2)+B2 ——( 2)
> 
> 从等式(2)中减去等式(1)
> ans =(2)–(1)
> ans = log(a1/a2)+B1–B2
> 
> 因此:int ans = log(a1/a2)+B1–B2

*   **如果 a1 < 0** ，那么 **ans = -ans** 。这是因为 a1 和 a2 都是负的。
    *   如果**年< 0** ，打印 **N** 。
    *   else if**年> 0** ，打印 **M** 。
*   否则打印平等。

下面是实现上述方法的 Jave 程序:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;
import java.math.*;
import java.lang.*;

class GFG
{
  // Function to extract mantissa
  static int[] extract_mantissa(String N,
                                String M)
  {
    int mantissa[] = new int [2];
    int mulInd1 = N.indexOf('*');
    int a1 = Integer.parseInt(
             N.substring(0, mulInd1));
    mantissa[0] = a1;

    int mulInd2 = M.indexOf('*');
    int a2 = Integer.parseInt(
             M.substring(0, mulInd2));
    mantissa[1] = a2;
    return mantissa;
  }

  // Function to extract exponent
  static int[] extract_exponent(String N,
                                String M)
  {
    int exponent[] = new int [2];
    int powInd1 = N.indexOf('^');
    int b1 = Integer.parseInt(
             N.substring(powInd1 + 1));
    exponent[0] = b1;

    int powInd2 = M.indexOf('^');        
    int b2 = Integer.parseInt(
             M.substring(powInd2 + 1));
    exponent[1] = b2;
    return exponent;
  }

  // Function to find smaller number
  static void solution(int a1, int b1,
                       int a2, int b2)
  { 
    double x = ((double)(a1) /
                (double)(a2));
    double ans = (b1 - b2 +
                  Math.log10(x));

    // If both are negative
    if(a1 < 0)
      ans = -ans;
    if(ans < 0)
      System.out.println("N");
    else if(ans > 0)
      System.out.println("M");
    else
      System.out.println("Equal");
  }

  static void solve(String N, String M)
  {
    // Extract mantissa(a1) and mantissa(a2)
    // from num1 and num2
    int mantissa[] = extract_mantissa(N, M);

    // Extract exponent(b1) and exponent(b2)
    // from num1 and num2
    int exponent[] = extract_exponent(N, M);

    if(mantissa[0] > 0 && mantissa[1] < 0)
      System.out.println("M");
    else if(mantissa[0] < 0 && mantissa[1] > 0)
      System.out.println("N");
    else
    {
      // if mantissa of both num1 and num2
      // are positive or both are negative
      solution(mantissa[0], exponent[0],
               mantissa[1], exponent[1]);
    }
  }

  // Driver code
  public static void main (String[] args)
  {
    // Mantissa is negative and
    // exponenent is positive
    String N = "-5*10^3";
    String M = "-50*10^2";
    solve(N, M);

    // Mantissa is negative and
    // exponent is negative
    N = "-5*10^-3";
    M = "-50*10^-2";
    solve(N, M);

    // Mantissa is positive and
    // exponent is negative
    N = "5*10^-3";
    M = "50*10^-2";
    solve(N, M);

    // Mantissa is positive and
    // exponent is positive
    N = "5*10^3";
    M = "50*10^2";
    solve(N, M);
  }
}
```

## 蟒蛇 3

```
# Python 3 program to implement
# the above approach
import math

# Function to extract mantissa
def extract_mantissa(N,  M):

    mantissa = [0]*2
    mulInd1 = list(N).index('*')
    a1 = N[0: mulInd1]
    mantissa[0] = a1

    mulInd2 = list(M).index('*')
    a2 = M[0: mulInd2]
    mantissa[1] = a2
    return mantissa

# Function to extract exponent
def extract_exponent(N,  M):

    exponent = [0]*2
    powInd1 = list(N).index('^')
    b1 = N[powInd1 + 1:]
    exponent[0] = b1

    powInd2 = list(M).index('^')
    b2 = M[powInd2 + 1:]
    exponent[1] = b2
    return exponent

# Function to find smaller number
def solution(a1,  b1,
             a2,  b2):

    x = int(a1) / int(a2)
    ans = (int(b1) - int(b2) + math.log10(x))

    # If both are negative
    if(int(a1) < 0):
        ans = -ans
    if(ans < 0):
        print("N")
    elif(ans > 0):
        print("M")
    else:
        print("Equal")

def solve(N,  M):

    # Extract mantissa(a1) and mantissa(a2)
    # from num1 and num2
    mantissa = extract_mantissa(N, M)

    # Extract exponent(b1) and exponent(b2)
    # from num1 and num2
    exponent = extract_exponent(N, M)

    if(int(mantissa[0]) > 0 and int(mantissa[1]) < 0):
        print("M")
    elif(int(mantissa[0]) < 0 and int(mantissa[1]) > 0):
        print("N")
    else:

        # if mantissa of both num1 and num2
        # are positive or both are negative
        solution(mantissa[0], exponent[0],
                 mantissa[1], exponent[1])

# Driver code
if __name__ == "__main__":

    # Mantissa is negative and
    # exponenent is positive
    N = "-5*10^3"
    M = "-50*10^2"
    solve(N, M)

    # Mantissa is negative and
    # exponent is negative
    N = "-5*10^-3"
    M = "-50*10^-2"
    solve(N, M)

    # Mantissa is positive and
    # exponent is negative
    N = "5*10^-3"
    M = "50*10^-2"
    solve(N, M)

    # Mantissa is positive and
    # exponent is positive
    N = "5*10^3"
    M = "50*10^2"
    solve(N, M)

    # This code is contributed by ukasp.
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{
  // Function to extract mantissa
  public static int[] extract_mantissa(String N, String M)
  {
    int[] mantissa = new int [2];
    int mulInd1 = N.IndexOf('*');
    int a1 = int.Parse(N.Substring(0, mulInd1));
    mantissa[0] = a1;

    int mulInd2 = M.IndexOf('*');
    int a2 = int.Parse(M.Substring(0, mulInd2));
    mantissa[1] = a2;
    return mantissa;
  }

  // Function to extract exponent
  public static int[] extract_exponent(String N,  String M)
  {
    int[] exponent = new int [2];
    int powInd1 = N.IndexOf('^');
    int b1 = int.Parse(N.Substring(powInd1 + 1));
    exponent[0] = b1;

    int powInd2 = M.IndexOf('^');        
    int b2 = int.Parse(
             M.Substring(powInd2 + 1));
    exponent[1] = b2;
    return exponent;
  }

  // Function to find smaller number
  static void solution(int a1, int b1,
                       int a2, int b2)
  { 
    double x = ((double)(a1) /
                (double)(a2));
    double ans = (b1 - b2 +
                  Math.Log10(x));

    // If both are negative
    if(a1 < 0)
      ans = -ans;
    if(ans < 0)
      Console.WriteLine("N");
    else if(ans > 0)
      Console.WriteLine("M");
    else
      Console.WriteLine("Equal");
  }

  static void solve(String N, String M)
  {
    // Extract mantissa(a1) and mantissa(a2)
    // from num1 and num2
    int[] mantissa = extract_mantissa(N, M);

    // Extract exponent(b1) and exponent(b2)
    // from num1 and num2
    int[] exponent = extract_exponent(N, M);

    if(mantissa[0] > 0 && mantissa[1] < 0)
      Console.WriteLine("M");
    else if(mantissa[0] < 0 && mantissa[1] > 0)
      Console.WriteLine("N");
    else
    {
      // if mantissa of both num1 and num2
      // are positive or both are negative
      solution(mantissa[0], exponent[0],
               mantissa[1], exponent[1]);
    }
  }

  // Driver code
  public static void Main ()
  {
    // Mantissa is negative and
    // exponenent is positive
    String N = "-5*10^3";
    String M = "-50*10^2";
    solve(N, M);

    // Mantissa is negative and
    // exponent is negative
    N = "-5*10^-3";
    M = "-50*10^-2";
    solve(N, M);

    // Mantissa is positive and
    // exponent is negative
    N = "5*10^-3";
    M = "50*10^-2";
    solve(N, M);

    // Mantissa is positive and
    // exponent is positive
    N = "5*10^3";
    M = "50*10^2";
    solve(N, M);
  }
}

// This code is contributed by saurabh_jaiswal.
```

**输出:**

> 相等
> M
> N
> 相等

**时间复杂度:** O ( 1 )
根据给定的约束|a|最多可以是 10 个长度的字符串，如果是负数，那么它可以是 11 个长度，同样 b 也可以是 11 位数。字符串的最大长度可以是 25 (11 +3+11)，所以我们可以考虑提取 a 和 b 的恒定时间操作。

**辅助空间:** O ( 1)