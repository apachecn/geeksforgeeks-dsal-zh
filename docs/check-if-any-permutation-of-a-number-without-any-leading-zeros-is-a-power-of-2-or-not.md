# 检查没有任何前导零的数字的任何排列是否是 2 的幂

> 原文:[https://www . geesforgeks . org/check-if-any-replacement-of-number-不带任何前导零是 2 的幂或不是/](https://www.geeksforgeeks.org/check-if-any-permutation-of-a-number-without-any-leading-zeros-is-a-power-of-2-or-not/)

给定一个整数 **N，**的任务是检查没有任何前导零的 **N** 的任何排列是否是 2 的幂。如果给定数字存在任何这样的排列，那么打印该排列。否则，打印**否**。

**示例:**

> **输入:** N = 46
> **输出:** 64
> **解释:**
> 46 的完美 2 次方的排列是 64( = 2 <sup>6</sup>
> 
> **输入:** N = 75
> **输出:**否
> **解释:**
> 75 不可能排列成 2 的完美幂。

**天真方法:**一个简单的解决方案是[生成数字 N](https://www.geeksforgeeks.org/print-all-permutations-of-a-number-n-greater-than-itself/) 的所有排列，对于每个排列，检查它是否是 2 的[次方](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)。如果发现是真的，打印**是**。否则，打印**否**。
***时间复杂度:**O(*(log<sub>10</sub>*N*)！*(log <sub>10</sub> *N))，其中 N 为给定数字 N.*
***辅助空间:** O(1)*

**有效方法:**给定数字和给定数字的任何排列的位数总是相同的。因此，要优化上述方法，只需检查给定数字的[位数是否等于任何 2 的完美幂。如果发现是真的，打印 2 的幂。否则，打印**否**。](https://www.geeksforgeeks.org/program-count-digits-integer-3-different-methods/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

const int TEN = 10;

// Function to update the frequency
// array  such that freq[i] stores
// the frequency of digit i to n
void updateFreq(int n, int freq[])
{
    // While there are digits
    // left to process
    while (n) {

        int digit = n % TEN;

        // Update the frequency of
        // the current digit
        freq[digit]++;

        // Remove the last digit
        n /= TEN;
    }
}

// Function that returns true if a
// and b are anagrams of each other
bool areAnagrams(int a, int b)
{
    // To store the frequencies of
    // the digits in a and b
    int freqA[TEN] = { 0 };
    int freqB[TEN] = { 0 };

    // Update the frequency of
    // the digits in a
    updateFreq(a, freqA);

    // Update the frequency of
    // the digits in b
    updateFreq(b, freqB);

    // Match the frequencies of
    // the common digits
    for (int i = 0; i < TEN; i++) {

        // If frequency differs for any
        // digit then the numbers are
        // not anagrams of each other
        if (freqA[i] != freqB[i])
            return false;
    }

    return true;
}

// Function to check if any permutation
// of a number is a power of 2 or not
bool isPowerOf2(int N)
{
    // Iterate over all possible perfect
    // power of 2
    for (int i = 0; i < 32; i++) {

        if (areAnagrams(1 << i, N)) {

            // Print that number
            cout << (1 << i);
            return true;
        }
    }
    return false;
}

// Driver Code
int main()
{
    // Given Number N
    int N = 46;

    // Function Call
    if (!isPowerOf2(N)) {
        cout << "No";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static int TEN = 10;

// Function to update the frequency
// array such that freq[i] stores
// the frequency of digit i to n
static void updateFreq(int n, int freq[])
{

    // While there are digits
    // left to process
    while (n > 0)
    {
        int digit = n % TEN;

        // Update the frequency of
        // the current digit
        freq[digit]++;

        // Remove the last digit
        n /= TEN;
    }
}

// Function that returns true if a
// and b are anagrams of each other
static boolean areAnagrams(int a, int b)
{

    // To store the frequencies of
    // the digits in a and b
    int freqA[] = new int[TEN];
    int freqB[] = new int[TEN];

    // Update the frequency of
    // the digits in a
    updateFreq(a, freqA);

    // Update the frequency of
    // the digits in b
    updateFreq(b, freqB);

    // Match the frequencies of
    // the common digits
    for(int i = 0; i < TEN; i++)
    {

        // If frequency differs for any
        // digit then the numbers are
        // not anagrams of each other
        if (freqA[i] != freqB[i])
            return false;
    }
    return true;
}

// Function to check if any permutation
// of a number is a power of 2 or not
static boolean isPowerOf2(int N)
{

    // Iterate over all possible perfect
    // power of 2
    for(int i = 0; i < 32; i++)
    {
        if (areAnagrams(1 << i, N))
        {

            // Print that number
            System.out.print((1 << i));
            return true;
        }
    }
    return false;
}

// Driver Code
public static void main(String[] args)
{

    // Given number N
    int N = 46;

    // Function call
    if (!isPowerOf2(N))
    {
        System.out.print("No");
    }
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach
TEN = 10

# Function to update the frequency
# array such that freq[i] stores
# the frequency of digit i to n
def updateFreq(n, freq):

    # While there are digits
    # left to process
    while (n):
        digit = n % TEN

        # Update the frequency of
        # the current digit
        freq[digit] += 1

        # Remove the last digit
        n //= TEN

# Function that returns true if a
# and b are anagrams of each other
def areAnagrams(a, b):

    # To store the frequencies of
    # the digits in a and b
    freqA = [0] * (TEN)
    freqB = [0] * (TEN)

    # Update the frequency of
    # the digits in a
    updateFreq(a, freqA)

    # Update the frequency of
    # the digits in b
    updateFreq(b, freqB)

    # Match the frequencies of
    # the common digits
    for i in range(TEN):

        # If frequency differs for any
        # digit then the numbers are
        # not anagrams of each other
        if (freqA[i] != freqB[i]):
            return False

    return True

# Function to check if any permutation
# of a number is a power of 2 or not
def isPowerOf2(N):

    # Iterate over all possible perfect
    # power of 2
    for i in range(32):
        if (areAnagrams(1 << i, N)):

            # Print that number
            print(1 << i)
            return True

    return False

# Driver Code

# Given number N
N = 46

# Function call
if (isPowerOf2(N) == 0):
    print("No")

# This code is contributed by code_hunt
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

static int TEN = 10;

// Function to update the frequency
// array such that freq[i] stores
// the frequency of digit i to n
static void updateFreq(int n,
                       int []freq)
{
  // While there are digits
  // left to process
  while (n > 0)
  {
    int digit = n % TEN;

    // Update the frequency of
    // the current digit
    freq[digit]++;

    // Remove the last digit
    n /= TEN;
  }
}

// Function that returns true if a
// and b are anagrams of each other
static bool areAnagrams(int a, int b)
{
  // To store the frequencies of
  // the digits in a and b
  int []freqA = new int[TEN];
  int []freqB = new int[TEN];

  // Update the frequency of
  // the digits in a
  updateFreq(a, freqA);

  // Update the frequency of
  // the digits in b
  updateFreq(b, freqB);

  // Match the frequencies of
  // the common digits
  for(int i = 0; i < TEN; i++)
  {
    // If frequency differs for any
    // digit then the numbers are
    // not anagrams of each other
    if (freqA[i] != freqB[i])
      return false;
  }
  return true;
}

// Function to check if any
// permutation of a number
// is a power of 2 or not
static bool isPowerOf2(int N)
{
  // Iterate over all
  // possible perfect power of 2
  for(int i = 0; i < 32; i++)
  {
    if (areAnagrams(1 << i, N))
    {
      // Print that number
      Console.Write((1 << i));
      return true;
    }
  }
  return false;
}

// Driver Code
public static void Main(String[] args)
{
  // Given number N
  int N = 46;

  // Function call
  if (!isPowerOf2(N))
  {
    Console.Write("No");
  }
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

var TEN = 10;

// Function to update the frequency
// array  such that freq[i] stores
// the frequency of digit i to n
function updateFreq(n, freq)
{
    // While there are digits
    // left to process
    while (n) {

        var digit = n % TEN;

        // Update the frequency of
        // the current digit
        freq[digit]++;

        // Remove the last digit
        n = parseInt(n/TEN);
    }
}

// Function that returns true if a
// and b are anagrams of each other
function areAnagrams(a, b)
{
    // To store the frequencies of
    // the digits in a and b
    var freqA = Array(TEN).fill(0);
    var freqB = Array(TEN).fill(0);

    // Update the frequency of
    // the digits in a
    updateFreq(a, freqA);

    // Update the frequency of
    // the digits in b
    updateFreq(b, freqB);

    // Match the frequencies of
    // the common digits
    for (var i = 0; i < TEN; i++) {

        // If frequency differs for any
        // digit then the numbers are
        // not anagrams of each other
        if (freqA[i] != freqB[i])
            return false;
    }

    return true;
}

// Function to check if any permutation
// of a number is a power of 2 or not
function isPowerOf2(N)
{
    // Iterate over all possible perfect
    // power of 2
    for (var i = 0; i < 32; i++) {

        if (areAnagrams(1 << i, N)) {

            // Print that number
            document.write( (1 << i));
            return true;
        }
    }
    return false;
}

// Driver Code
// Given Number N
var N = 46;
// Function Call
if (!isPowerOf2(N)) {
    document.write( "No");
}

</script>
```

**Output:** 

```
64
```

***时间复杂度:**O((log<sub>10</sub>N)<sup>2</sup>)*
***辅助空间:** O(log <sub>10</sub> N)*