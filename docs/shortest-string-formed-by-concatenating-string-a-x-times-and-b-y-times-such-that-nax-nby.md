# 通过串联字符串 A x 倍和 by 倍形成的最短字符串，使得 n(A)*x = n(B)*y

> 原文:[https://www . geeksforgeeks . org/通过连接字符串-a-x-times-和-b-y-times-so-nax-nby 形成的最短字符串/](https://www.geeksforgeeks.org/shortest-string-formed-by-concatenating-string-a-x-times-and-b-y-times-such-that-nax-nby/)

给定两个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **A** 和 **B** ，任务是找到最短的字符串，该字符串是 **A** 和 **B** 的倍数。一个字符串 **X** 如果字符串 **X** 可以由字符串 **Y** 的多次出现串联而成，则称该字符串为字符串 **Y** 的倍数。

**示例:**

> **输入**:A =【aaa】，B =【aa】
> **输出**:AAA
> **说明:**A 乘以二，B 乘以三，会得到 AAA
> 
> **输入:** A=“冷”，B =“老”
> T3】输出: -1

**方法:**给定的问题可以基于这样的观察来解决，即可以是弦 **A** 和 **B** 的倍数的最小弦的长度必须等于 **A** 的长度和 **B** 的长度的 [LCM](http://www.geeksforgeeks.org/lcm-gq/) 。因此，可以使用以下步骤解决给定的问题:

*   创建一个变量 **lcm** ，该变量存储 **A** 长度和 **B** 长度的 [LCM](http://www.geeksforgeeks.org/lcm-gq/) 值。
*   创建一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **C** ，它是由[将字符串](https://www.geeksforgeeks.org/methods-to-concatenate-string-in-c-c-with-examples/) **A** 、 **lcm /(长度为 A)** 次串联而成。
*   同样，创建一个字符串 **D** ，该字符串由字符串 **B** 、**LCM/(B 的长度)**次串联而成。
*   检查字符串 **C** 和 **D** 是否相等。如果是，打印其中任何一个，否则打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find GCD of two numbers
int gcd(int a, int b)
{
    if (a == 0) {
        return b;
    }
    return gcd(b % a, a);
}

// Function to find shortest string that
// is a multiple of string A and B
void ShortestString(string A, string B)
{
    int n1 = A.length();
    int n2 = B.length();
    int g = gcd(n1, n2);

    // Stores the Lcm of length
    // of string A and B
    int lcm = (n1 * n2) / g;

    // Stores multiple of string A
    string C = "";

    // Stores multiple of string B
    string D = "";

    // Concatenate A, lcm / n1 times
    for (int i = 0; i < (lcm / n1); i++) {
        C = C + A;
    }

    // Concatenate B, lcm / n2 times
    for (int i = 0; i < (lcm / n2); i++) {
        D = D + B;
    }

    // If both strings are equal
    // to each other
    if (C == D) {
        cout << C;
    }
    else {
        cout << -1;
    }
}

// Driver Code
int main()
{
    string A = "aaa";
    string B = "aa";
    ShortestString(A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find GCD of two numbers
static int gcd(int a, int b)
{
    if (a == 0) {
        return b;
    }
    return gcd(b % a, a);
}

// Function to find shortest String that
// is a multiple of String A and B
static void ShortestString(String A, String B)
{
    int n1 = A.length();
    int n2 = B.length();
    int g = gcd(n1, n2);

    // Stores the Lcm of length
    // of String A and B
    int lcm = (n1 * n2) / g;

    // Stores multiple of String A
    String C = "";

    // Stores multiple of String B
    String D = "";

    // Concatenate A, lcm / n1 times
    for (int i = 0; i < (lcm / n1); i++) {
        C = C + A;
    }

    // Concatenate B, lcm / n2 times
    for (int i = 0; i < (lcm / n2); i++) {
        D = D + B;
    }

    // If both Strings are equal
    // to each other
    if (C.equals(D)) {
        System.out.print(C);
    }
    else {
        System.out.print(-1);
    }
}

// Driver Code
public static void main(String[] args)
{
    String A = "aaa";
    String B = "aa";
    ShortestString(A, B);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to find GCD of two numbers
def gcd(a, b):
    if (a == 0):
        return b
    return gcd(b % a, a)

# Function to find shortest string that
# is a multiple of string A and B
def ShortestString(A, B):
    n1 = len(A)
    n2 = len(B)
    g = gcd(n1, n2)

    # Stores the Lcm of length
    # of string A and B
    lcm = (n1 * n2) / g

    # Stores multiple of string A
    C = ""

    # Stores multiple of string B
    D = ""

    # Concatenate A, lcm / n1 times
    for i in range(0, (int)(lcm//n1)):
        C = C + A

    # Concatenate B, lcm / n2 times
    for i in range((int)(lcm // n2)):
        D = D + B

    # If both strings are equal
    # to each other
    if (C == D):
        print(C)
    else:
        print(-1)

# Driver Code
A = "aaa"
B = "aa"
ShortestString(A, B)

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find GCD of two numbers
static int gcd(int a, int b)
{
    if (a == 0) {
        return b;
    }
    return gcd(b % a, a);
}

// Function to find shortest String that
// is a multiple of String A and B
static void ShortestString(string A, string B)
{
    int n1 = A.Length;
    int n2 = B.Length;
    int g = gcd(n1, n2);

    // Stores the Lcm of length
    // of String A and B
    int lcm = (n1 * n2) / g;

    // Stores multiple of String A
    string C = "";

    // Stores multiple of String B
    string D = "";

    // Concatenate A, lcm / n1 times
    for (int i = 0; i < (lcm / n1); i++) {
        C = C + A;
    }

    // Concatenate B, lcm / n2 times
    for (int i = 0; i < (lcm / n2); i++) {
        D = D + B;
    }

    // If both Strings are equal
    // to each other
    if (C.Equals(D)) {
        Console.Write(C);
    }
    else {
        Console.Write(-1);
    }
}

// Driver Code
public static void Main()
{
    string A = "aaa";
    string B = "aa";
    ShortestString(A, B);
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
      // JavaScript code for the above approach

      // Function to find GCD of two numbers
      function gcd(a, b) {
          if (a == 0) {
              return b;
          }
          return gcd(b % a, a);
      }

      // Function to find shortest string that
      // is a multiple of string A and B
      function ShortestString(A, B) {
          let n1 = A.length;
          let n2 = B.length;
          let g = gcd(n1, n2);

          // Stores the Lcm of length
          // of string A and B
          let lcm = (n1 * n2) / g;

          // Stores multiple of string A
          let C = "";

          // Stores multiple of string B
          let D = "";

          // Concatenate A, lcm / n1 times
          for (let i = 0; i < (lcm / n1); i++) {
              C = C + A;
          }

          // Concatenate B, lcm / n2 times
          for (let i = 0; i < (lcm / n2); i++) {
              D = D + B;
          }

          // If both strings are equal
          // to each other
          if (C == D) {
              document.write(C);
          }
          else {
              document.write(-1);
          }
      }

      // Driver Code
      let A = "aaa";
      let B = "aa";
      ShortestString(A, B);

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
aaaaaa
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)