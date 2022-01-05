# 可被两个给定字符串整除的最小字符串

> 原文:[https://www . geesforgeks . org/最小字符串可被两个给定字符串整除/](https://www.geeksforgeeks.org/smallest-string-divisible-by-two-given-strings/)

给定两个长度分别为 **N** 和 **M** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和 **T** ，任务是找到能被这两个字符串整除的最小字符串。如果不存在这样的字符串，则打印 **-1** 。

> 对于任意两个字符串 **A** 和 **B** ，当且仅当 **A** 是 **B** 的至少一次拼接时， **B** 将 **A** 相除。

**示例:**

> **输入:**S =“abab”，T =“ab”
> **输出:** abab
> **说明:**字符串“abab”与 S 相同，是字符串 T 的两倍串联(“abab”=“ab”+“ab”= T+T)
> 
> **输入:** S = "ccc "，T = "cc"
> **输出:** cccccc
> **说明:**字符串“cccccccc”分别是 S 和 T 的两次和三次拼接。
> (“cccccc”=“CCC”+“CCC”= S+S)
> (“cccccc”=“cc”+“cc”+“cc”= T+T+T)

**方法:**这个想法是基于这样的观察:所需字符串的长度，比如说 **L、**必须等于 **N** 和 **M** 的[最小公倍数。检查串 **S** 串接 **L / N** 的次数是否等于串 **T** 被串接 **L / M** 的次数。如果发现是真的，打印其中任何一个。否则，打印 **-1** 。按照以下步骤解决问题:](https://www.geeksforgeeks.org/program-to-find-lcm-of-two-numbers/)

*   将 **N** 和**M**T5 的[最小公倍数存储在一个变量中，比如 **L** 。](https://www.geeksforgeeks.org/program-to-find-lcm-of-two-numbers/)
*   初始化两个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S1** 和 **T1** 。
*   [串，S1 串， **S** ， **(L/N)** 次](https://www.geeksforgeeks.org/c-program-concatenate-string-given-number-times/)。
*   [串接串， **T1** 与串， **T** 、 **(L/M)** 次数](https://www.geeksforgeeks.org/c-program-concatenate-string-given-number-times/)。
*   如果[字符串 **S1** 和 **T1** 相等](https://www.geeksforgeeks.org/comparing-two-strings-cpp/)，则打印 **S1** 作为结果。
*   否则，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// GCD of two numbers
int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to calculate
// LCM of two numbers
int lcm(int a, int b)
{
    return (a / gcd(a, b)) * b;
}

// Function to find the smallest string
// which is divisible by strings S and T
void findSmallestString(string s, string t)
{
    // Store the length of both strings
    int n = s.length(), m = t.length();

    // Store LCM of n and m
    int l = lcm(n, m);

    // Temporary strings to store
    // concatenated strings
    string s1 = "", t1 = "";

    // Concatenate s1 (l / n) times
    for (int i = 0; i < l / n; i++) {
        s1 += s;
    }

    // Concatenate t1 (l / m) times
    for (int i = 0; i < l / m; i++) {
        t1 += t;
    }

    // If s1 and t1 are equal
    if (s1 == t1)
        cout << s1;

    // Otherwise, print -1
    else
        cout << -1;
}

// Driver Code
int main()
{
    string S = "baba", T = "ba";
    findSmallestString(S, T);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.io.*;

class GFG
{

  // Function to calculate
  // GCD of two numbers
  static int gcd(int a, int b)
  {
    if (b == 0)
      return a;
    return gcd(b, a % b);
  }

  // Function to calculate
  // LCM of two numbers
  static int lcm(int a, int b)
  {
    return (a / gcd(a, b)) * b;
  }

  // Function to find the smallest string
  // which is divisible by strings S and T
  static void findSmallestString(String s, String t)
  {
    // Store the length of both strings
    int n = s.length(), m = t.length();

    // Store LCM of n and m
    int l = lcm(n, m);

    // Temporary strings to store
    // concatenated strings
    String s1 = "", t1 = "";

    // Concatenate s1 (l / n) times
    for (int i = 0; i < l / n; i++) {
      s1 += s;
    }

    // Concatenate t1 (l / m) times
    for (int i = 0; i < l / m; i++) {
      t1 += t;
    }

    // If s1 and t1 are equal
    if (s1.equals(t1)){
      System.out.println(s1);
    }

    // Otherwise, print -1
    else{
      System.out.println(-1);
    }
  }

  // Driver code
  public static void main(String[] args)
  {

    String S = "baba", T = "ba";
    findSmallestString(S, T);
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate
# GCD of two numbers
def gcd(a, b):
    if (b == 0):
        return a
    return gcd(b, a % b)

# Function to calculate
# LCM of two numbers
def lcm(a, b):
    return (a // gcd(a, b)) * b

# Function to find the smallest string
# which is divisible by strings S and T
def findSmallestString(s, t):
    # Store the length of both strings
    n, m = len(s), len(t)

    # Store LCM of n and m
    l = lcm(n, m)

    # Temporary strings to store
    # concatenated strings
    s1, t1 = "", ""

    # Concatenate s1 (l / n) times
    for i in range(l//n):
        s1 += s

    # Concatenate t1 (l / m) times
    for i in range(l//m):
        t1 += t

    # If s1 and t1 are equal
    if (s1 == t1):
        print(s1)

    # Otherwise, pr-1
    else:
        print(-1)

# Driver Code
if __name__ == '__main__':
    S, T = "baba", "ba"
    findSmallestString(S, T)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for above approach
using System;

public class GFG
{

  // Function to calculate
  // GCD of two numbers
  static int gcd(int a, int b)
  {
    if (b == 0)
      return a;
    return gcd(b, a % b);
  }

  // Function to calculate
  // LCM of two numbers
  static int lcm(int a, int b)
  {
    return (a / gcd(a, b)) * b;
  }

  // Function to find the smallest string
  // which is divisible by strings S and T
  static void findSmallestString(string s, string t)
  {
    // Store the length of both strings
    int n = s.Length, m = t.Length;

    // Store LCM of n and m
    int l = lcm(n, m);

    // Temporary strings to store
    // concatenated strings
    string s1 = "", t1 = "";

    // Concatenate s1 (l / n) times
    for (int i = 0; i < l / n; i++) {
      s1 += s;
    }

    // Concatenate t1 (l / m) times
    for (int i = 0; i < l / m; i++) {
      t1 += t;
    }

    // If s1 and t1 are equal
    if (s1 == t1)
      Console.WriteLine(s1);

    // Otherwise, print -1
    else
      Console.WriteLine(-1);
  }

  // Driver code
  public static void Main(String[] args)
  {
    string S = "baba", T = "ba";
    findSmallestString(S, T);
  }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
// Javascript program for above approach

// Function to calculate
// GCD of two numbers
function gcd(a,b)
{
    if (b == 0)
      return a;
    return gcd(b, a % b);
}

// Function to calculate
// LCM of two numbers
function lcm(a,b)
{
    return (a / gcd(a, b)) * b;
}

// Function to find the smallest string
// which is divisible by strings S and T
function findSmallestString(s,t)
{
    // Store the length of both strings
    let n = s.length, m = t.length;

    // Store LCM of n and m
    let l = lcm(n, m);

    // Temporary strings to store
    // concatenated strings
    let s1 = "", t1 = "";

    // Concatenate s1 (l / n) times
    for (let i = 0; i < l / n; i++) {
      s1 += s;
    }

    // Concatenate t1 (l / m) times
    for (let i = 0; i < l / m; i++) {
      t1 += t;
    }

    // If s1 and t1 are equal
    if (s1 == (t1)){
      document.write(s1+"<br>");
    }

    // Otherwise, print -1
    else{
      document.write(-1+"<br>");
    }
}

 // Driver code
let  S = "baba", T = "ba";
findSmallestString(S, T);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
baba
```

***时间复杂度:** O(max(N，M))*
***辅助空间:** O(max(N，M))*