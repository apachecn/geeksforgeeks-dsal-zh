# 通过移除非空子字符串获得的所有可能字符串的总和

> 原文:[https://www . geesforgeks . org/所有可能字符串的总和-通过移除非空子字符串获得/](https://www.geeksforgeeks.org/sum-of-all-possible-strings-obtained-by-removal-of-non-empty-substrings/)

给定由 **N 个**整数组成的**数值** [**字符串**](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **字符串**，任务是在移除非空的[子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)后，找到所有可能的结果[字符串的和。](https://www.geeksforgeeks.org/string-data-structure/)

**示例:**

> **输入:** str = "205"
> **输出:** 57
> **说明:**可以去掉的子串有“2”、“0”、“5”、“20”、“05”、“205”。结果字符串分别是“05”、“25”、“20”、“5”、“2”、“0”。因此，总和将是 57。
> 
> **输入:** str = "1234"
> **输出:** 680
> **说明:**可删除的子串有“1”、“2”、“3”、“4”、“12”、“23”、“34”、“123”、“234”、“1234”、“1234”。结果字符串分别是“234”、“134”、“124”、“123”、“34”、“14”、“12”、“4”、“1”、“0”。因此，总和将是 680。

**方法:**要解决问题，需要进行以下观察:

> **插图:**
> Let str = "1234"
> 通过删除非空子字符串和这些字符串中每个字符的位置，所有可能的字符串如下:
> 
> <figure class="table">
> 
> |   | **100** | **10** | **1** |
> | **234** | Two | three | four |
> | **134** | one | three | four |
> | **124** | one | Two | four |
> | **123** | one | Two | three |
> | **34** |   | three | four |
> | **14** |   | one | four |
> | **12** |   | one | Two |
> | **4** |   |   | four |
> | **1** |   |   | one |
> | **0** |   |   | Zero |
> 
> 从上表中，获取每个索引处的贡献，例如 1 -> ((1 + 2 + 3) * 1 + 4 * 6) * 1 处的贡献
> 
> 10 时的贡献-> ((1 + 2) * 2 + 3 * 3) * 10
> 
> 100 时的贡献-> ((1) * 3 + 2 * 1) * 100
> 
> 因此，为每个索引生成一个通用公式，即
> 
> **10<sup>x</sup>=(∑(n–x–2)*(x+1)+str[n–x–1]*(n–x–1)第** [**项三角数**](https://en.wikipedia.org/wiki/Triangular_number) **) * 10 <sup>x</sup>**
> 
> </figure>

按照以下步骤解决问题:

*   预先计算 10 的幂并存储在数组中**幂[]** 。
*   将给定数值串的数字的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)存储在数组**pref【】**中。
*   应用上面得到的公式，从 **0** 到**N–1**的每 **x** 计算总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

const int N = 10;

int pref[N], power[N];

// Function to convert a character
// to its equivalent digit
int toDigit(char ch)
{
    return (ch - '0');
}

// Function to precompute powers of 10
void powerOf10()
{
    power[0] = 1;
    for (int i = 1; i < N; i++)
        power[i] = power[i - 1] * 10;
}

// Function to precompute prefix sum
// of numerical strings
void precomputePrefix(string str, int n)
{
    pref[0] = str[0] - '0';
    for (int i = 1; i < n; i++)
        pref[i] = pref[i - 1]
                  + toDigit(str[i]);
}

// Function to return the i-th
// term of Triangular Number
int triangularNumber(int i)
{
    int res = i * (i + 1) / 2;
    return res;
}

// Function to return the sum
// of all resulting strings
int sumOfSubstrings(string str)
{
    int n = str.size();

    // Precompute powers of 10
    powerOf10();

    // Precompute prefix sum
    precomputePrefix(str, n);

    // Initialize result
    int ans = 0;

    for (int i = 0; i < n - 1; i++) {

        // Apply the above general
        // formula for every i
        ans += (pref[n - i - 2] * (i + 1)
                + toDigit(str[n - i - 1])
                      * triangularNumber(
                            n - i - 1))
               * power[i];
    }

    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    string str = "1234";

    // Function Call
    cout << sumOfSubstrings(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

static int N = 10;
static int []pref = new int[N];
static int[] power = new int[N];

// Function to convert a
// character to its equivalent
// digit
static int toDigit(char ch)
{
  return (ch - '0');
}

// Function to precompute
// powers of 10
static void powerOf10()
{
  power[0] = 1;

  for (int i = 1; i < N; i++)
    power[i] = power[i - 1] * 10;
}

// Function to precompute prefix sum
// of numerical Strings
static void precomputePrefix(char[] str,
                             int n)
{
  pref[0] = str[0] - '0';

  for (int i = 1; i < n; i++)
    pref[i] = pref[i - 1] +
              toDigit(str[i]);
}

// Function to return the i-th
// term of Triangular Number
static int triangularNumber(int i)
{
  int res = i * (i + 1) / 2;
  return res;
}

// Function to return the sum
// of all resulting Strings
static int sumOfSubStrings(String str)
{
  int n = str.length();

  // Precompute powers of 10
  powerOf10();

  // Precompute prefix sum
  precomputePrefix(
  str.toCharArray(), n);

  // Initialize result
  int ans = 0;

  for (int i = 0; i < n - 1; i++)
  {
    // Apply the above general
    // formula for every i
    ans += (pref[n - i - 2] * (i + 1) +
            toDigit(str.charAt(n - i - 1)) *
            triangularNumber(n - i - 1)) *
            power[i];
  }

  // Return the answer
  return ans;
}

// Driver Code
public static void main(String[] args)
{
  String str = "1234";

  // Function Call
  System.out.print(sumOfSubStrings(str));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program for the
# above approach
N = 10
pref = [0] * N
power = [0] * N

# Function to convert a
# character to its equivalent
# digit
def toDigit(ch):

    return (ord(ch) -
            ord('0'))

# Function to precompute
# powers of 10
def powerOf10():

    power[0] = 1
    for i in range(1, N):
        power[i] = power[i - 1] * 10

# Function to precompute prefix sum
# of numerical strings
def precomputePrefix(st, n):

    pref[0] = (ord(st[0]) -
               ord('0'))
    for i in range(1, n):
        pref[i] = (pref[i - 1] +
                   toDigit(st[i]))

# Function to return the i-th
# term of Triangular Number
def triangularNumber(i):

    res = i * (i + 1) // 2
    return res

# Function to return the sum
# of all resulting strings
def sumOfSubstrings(st):

    n = len(st)

    # Precompute powers
    # of 10
    powerOf10()

    # Precompute prefix
    # sum
    precomputePrefix(st, n)

    # Initialize result
    ans = 0

    for i in range(n - 1):

        # Apply the above general
        # formula for every i
        ans += ((pref[n - i - 2] * (i + 1) +
                 toDigit(st[n - i - 1]) *
                 triangularNumber(n - i - 1)) *
                 power[i])

    # Return the answer
    return ans

# Driver Code
if __name__ == "__main__":

    st = "1234"

    # Function Call
    print(sumOfSubstrings(st))

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

static int N = 10;
static int []pref = new int[N];
static int[] power = new int[N];

// Function to convert a
// character to its equivalent
// digit
static int toDigit(char ch)
{
  return (ch - '0');
}

// Function to precompute
// powers of 10
static void powerOf10()
{
  power[0] = 1;

  for (int i = 1; i < N; i++)
    power[i] = power[i - 1] * 10;
}

// Function to precompute prefix sum
// of numerical Strings
static void precomputePrefix(char[] str,
                             int n)
{
  pref[0] = str[0] - '0';

  for (int i = 1; i < n; i++)
    pref[i] = pref[i - 1] +
              toDigit(str[i]);
}

// Function to return the i-th
// term of Triangular Number
static int triangularNumber(int i)
{
  int res = i * (i + 1) / 2;
  return res;
}

// Function to return the sum
// of all resulting Strings
static int sumOfSubStrings(String str)
{
  int n = str.Length;

  // Precompute powers of 10
  powerOf10();

  // Precompute prefix sum
  precomputePrefix(str.ToCharArray(), n);

  // Initialize result
  int ans = 0;

  for (int i = 0; i < n - 1; i++)
  {
    // Apply the above general
    // formula for every i
    ans += (pref[n - i - 2] * (i + 1) +
            toDigit(str[n - i - 1]) *
            triangularNumber(n - i - 1)) *
            power[i];
  }

  // Return the answer
  return ans;
}

// Driver Code
public static void Main(String[] args)
{
  String str = "1234";

  // Function Call
  Console.Write(sumOfSubStrings(str));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

      // JavaScript program for the
      // above approach
      var N = 10;
      var pref = new Array(N).fill(0);
      var power = new Array(N).fill(0);

      // Function to convert a
      // character to its equivalent
      // digit
      function toDigit(ch) {
        return ch - "0";
      }

      // Function to precompute
      // powers of 10
      function powerOf10() {
        power[0] = 1;

        for (var i = 1; i < N; i++)
        power[i] = power[i - 1] * 10;
      }

      // Function to precompute prefix sum
      // of numerical Strings
      function precomputePrefix(str, n) {
        pref[0] = str[0] - "0";

        for (var i = 1; i < n; i++)
        pref[i] = pref[i - 1] + toDigit(str[i]);
      }

      // Function to return the i-th
      // term of Triangular Number
      function triangularNumber(i) {
        var res = parseInt((i * (i + 1)) / 2);
        return res;
      }

      // Function to return the sum
      // of all resulting Strings
      function sumOfSubStrings(str) {
        var n = str.length;

        // Precompute powers of 10
        powerOf10();

        // Precompute prefix sum
        precomputePrefix(str.split(""), n);

        // Initialize result
        var ans = 0;

        for (var i = 0; i < n - 1; i++) {
          // Apply the above general
          // formula for every i
          ans +=
            (pref[n - i - 2] * (i + 1) +
              toDigit(str[n - i - 1]) *
              triangularNumber(n - i - 1)) *
              power[i];
        }

        // Return the answer
        return ans;
      }

      // Driver Code
      var str = "1234";

      // Function Call
      document.write(sumOfSubStrings(str));

</script>
```

**Output:** 

```
680
```

***时间复杂度:** O(N)，其中 **N** 为弦的长度。*
***辅助空间:** O(1)*