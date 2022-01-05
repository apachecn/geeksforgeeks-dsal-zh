# 没有任何乘法符号的最小字符串，表示两个给定数字的乘积

> 原文:[https://www . geesforgeks . org/不带任何乘法符号的最小字符串表示两个给定数字的乘积/](https://www.geeksforgeeks.org/smallest-string-without-any-multiplication-sign-that-represents-the-product-of-two-given-numbers/)

给定两个数字 **A** 和 **B** ，任务是打印最小可能长度的字符串，该字符串计算为两个给定数字的乘积[，即 **A*B** ，而不使用乘法符号。](https://www.geeksforgeeks.org/product-2-numbers-using-recursion/)

> 2 的任何[完美幂都可以用左移运算符的形式表示。
> **例如:**
> N = 2 = 1<<1 =<<1”
> N = 4 = 1<<2 =<<2】
> 利用上述思想，任何数字都可以用左移运算符而不是乘法符号来表示。
> **例如:**
> N = 24 = 6 * 4 = 6(1<<2)=“6<<2”](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)

**示例:**

> **输入:** A = 6，B = 10
> **输出:**6<<3+6<<1
> **说明:**
> 2 个数的乘积= 6 × 10 = 60。
> 上面给出的表达式计算结果为 6 × (2 × 2 × 2) + 6 × 2 = 60。
> 字符串“10 < < 2+10 < < 1”也评估为 60。
> 但是“6 < < 3+6 < < 1”是所需的输出，因为其长度较小。
> 
> **输入:** A = 5，B = 5
> **输出:** 5 < < 2+5
> **说明:**
> 2 个数的乘积= 5 × 5 = 25。
> 上面给出的表达式计算结果为 5 × (2 × 2) + 5 = 25。

**方法:**思路是用[左移符](https://www.geeksforgeeks.org/left-shift-right-shift-operators-c-cpp/)找产品。以下是步骤:

*   将 B 表示为 2 的[次方](https://www.geeksforgeeks.org/representation-number-powers/)。

> 让 B = 2<sup>k</sup><sub><sup>1</sup></sub>+2<sup>k</sup><sub><sup>2</sup></sub>+…+2<sup>k</sup><sub><sup>n</sup></sub>，其中 k<sub>1</sub>>k<sub>2</sub>>..> k <sub>n</sub>

*   因此，A 和 B 的乘积可以写成

> A * B = A *(2<sup>k</sup><sub><sup>1</sup></sub>+2<sup>k</sup><sub><sup>2</sup></sub>+…+2<sup>k</sup><sub><sup>n</sup></sub>)

*   使用**<<**(左移位运算符)将一个数乘以二的任意次方。
*   因此 A x B = A<< k<sub>1</sub>+A<T7】k<sub>2</sub>+…+A<T9】k<sub>n</sub>
*   要找到 **k <sub>i</sub>** ，我们使用 [log()函数](https://www.geeksforgeeks.org/log-function-cpp/)并用余数**B–2<sup>k</sup><sub><sup>I</sup></sub>**继续该过程，直到余数变为 **0** 或余数的 log 变为零。
*   同样，通过将 **A** 表示为 2 的幂，来表示 A * B = B<< k<sub>1</sub>+B<k<sub>2</sub>+…+B<T11】k<sub>n</sub>。
*   比较两种表示法，并打印长度较小的字符串。

下面是上述方法的实现:

## C++

```
// C++ program for
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the string
// which evaluates to the
// product of A and B
string len(long A, long B)
{
  // Stores the result
  string res = "";
  long Log = 0;

  do
  {   
    // 2 ^ log <= B &&
    // 2 ^ (log + 1) > B
    Log = (long)(log(B) / log(2));

    // Update res to
    // res+=A X 2^log
    if (Log != 0)
    {
      res = res + to_string(A) +
            "<<" + to_string(Log);
    }
    else
    {
      // Update res to
      // res+=A X 2^0
      res += A;
      break;
    }

    // Find the remainder
    B = B - (long)pow(2, Log);

    // If remainder is
    // not equal to 0
    if (B != 0)
    {
      res += "+";
    }
    else
      break;
  } while (Log != 0);

  // Return the
  // resultant string
  return res;
}

// Function to find the minimum
// length representation of A*B
void minimumString(long A, long B)
{
  // Find representation of form
  // A << k1 + A << k2 + ... + A << kn
  string res1 = len(A, B);

  // Find representation of form
  // B << k1 + B << k2 + ... + B << kn
  string res2 = len(B, A);

  // Compare the length of
  // the representations
  if (res1.length() > res2.length())
  {
    cout << res2 << endl;
  }
  else
  {
    cout << res1 << endl;
  }
}

// Driver code
int main()
{
  // Product A X B
  long A = 6;
  long B = 10;

  // Function Call
  minimumString(A, B);

  return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function to find the string
    // which evaluates to the
    // product of A and B
    public static String len(long A,
long B)
    {
        // Stores the result
        String res = "";
        long log = 0;

        do {

            // 2 ^ log <= B &&
            // 2 ^ (log + 1) > B
            log = (long)(Math.log(B)
                         / Math.log(2));

            // Update res to
            // res+=A X 2^log
            if (log != 0) {

                res += A + "<<" + log;
            }
            else {

                // Update res to res+=A X 2^0
                res += A;
                break;
            }

            // Find the remainder
            B = B - (long)Math.pow(2, log);

            // If remainder is not equal
            // to 0
            if (B != 0) {
                res += "+";
            }
            else
                break;
        } while (log != 0);

        // Return the resultant string
        return res;
    }

    // Function to find the minimum
    // length representation of A*B
    public static void
    minimumString(long A, long B)
    {
        // Find representation of form
        // A << k1 + A << k2 + ... + A << kn
        String res1 = len(A, B);

        // Find representation of form
        // B << k1 + B << k2 + ... + B << kn
        String res2 = len(B, A);

        // Compare the length of
        // the representations
        if (res1.length() > res2.length()) {
            System.out.println(res2);
        }
        else {
            System.out.println(res1);
        }
    }

    // Driver Code
    public static void main(String args[])
    {
        // Product A X B
        long A = 6;
        long B = 10;

        // Function Call
        minimumString(A, B);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import log

# Function to find the string
# which evaluates to the
# product of A and B
def lenn(A, B):

    # Stores the result
    res = ""
    logg = 0

    while True:

        # 2 ^ logg <= B &&
        # 2 ^ (logg + 1) > B
        logg =log(B) // log(2)

        # Update res to
        # res+=A X 2^logg
        if (logg != 0):
            res += (str(A) + "<<" +
                    str(int(logg)))
        else:

            # Update res to res+=A X 2^0
            res += A
            break

        # Find the remainder
        B = B - pow(2, logg)

        # If remainder is not equal
        # to 0
        if (B != 0):
            res += "+"
        else:
            break

        if logg == 0:
            break

    # Return the resultant string
    return res

# Function to find the minimum
# length representation of A*B
def minimumString(A, B):

    # Find representation of form
    # A << k1 + A << k2 + ... + A << kn
    res1 = lenn(A, B)

    # Find representation of form
    # B << k1 + B << k2 + ... + B << kn
    res2 = lenn(B, A)

    # Compare the length of
    # the representations
    if (len(res1) > len(res2)):
        print(res2)
    else:
        print(res1)

# Driver Code
if __name__ == '__main__':

    # Product A X B
    A = 6
    B = 10

    # Function call
    minimumString(A, B)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the string
// which evaluates to the
// product of A and B
public static string len(long A, long B)
{

    // Stores the result
    string res = "";
    long log = 0;

    do
    {

        // 2 ^ log <= B &&
        // 2 ^ (log + 1) > B
        log = (long)(Math.Log(B) /
                     Math.Log(2));

        // Update res to
        // res+=A X 2^log
        if (log != 0)
        {
            res += A + "<<" + log;
        }
        else
        {

            // Update res to res+=A X 2^0
            res += A;
            break;
        }

        // Find the remainder
        B = B - (long)Math.Pow(2, log);

        // If remainder is not equal
        // to 0
        if (B != 0)
        {
            res += "+";
        }
        else
            break;
    } while (log != 0);

    // Return the resultant string
    return res;
}

// Function to find the minimum
// length representation of A*B
public static void minimumString(long A,
                                 long B)
{

    // Find representation of form
    // A << k1 + A << k2 + ... + A << kn
    string res1 = len(A, B);

    // Find representation of form
    // B << k1 + B << k2 + ... + B << kn
    string res2 = len(B, A);

    // Compare the length of
    // the representations
    if (res1.Length > res2.Length)
    {
        Console.WriteLine(res2);
    }
    else
    {
        Console.WriteLine(res1);
    }
}

// Driver Code
public static void Main()
{

    // Product A X B
    long A = 6;
    long B = 10;

    // Function call
    minimumString(A, B);
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>
// Javascript program for
// the above approach

// Function to find the string
// which evaluates to the
// product of A and B
function len(A, B) {
    // Stores the result
    let res = "";
    let Log = 0;

    do {
        // 2 ^ log <= B &&
        // 2 ^ (log + 1) > B
        Log = Math.floor(Math.log(B) / Math.log(2));

        // Update res to
        // res+=A X 2^log
        if (Log != 0) {
            res = res + String(A) + "<<" + String(Log);
        }
        else {
            // Update res to
            // res+=A X 2^0
            res += A;
            break;
        }

        // Find the remainder
        B = B - Math.pow(2, Log);

        // If remainder is
        // not equal to 0
        if (B != 0) {
            res += "+";
        }
        else
            break;
    } while (Log != 0);

    // Return the
    // resultant string
    return res;
}

// Function to find the minimum
// length representation of A*B
function minimumString(A, B) {
    // Find representation of form
    // A << k1 + A << k2 + ... + A << kn
    let res1 = len(A, B);

    // Find representation of form
    // B << k1 + B << k2 + ... + B << kn
    let res2 = len(B, A);

    // Compare the length of
    // the representations
    if (res1.length > res2.length) {
        document.write(res2 + "<br>");
    }
    else {
        document.write(res1 + "<br>");
    }
}

// Driver code

// Product A X B
let A = 6;
let B = 10;

// Function Call
minimumString(A, B);

// This code is contributed by gfgking
</script>
```

**Output:** 

```
6<<3+6<<1
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*