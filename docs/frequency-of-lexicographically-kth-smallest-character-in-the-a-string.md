# 一个字符串中按字典顺序排列的第 k 个最小字符的频率

> 原文:[https://www . geeksforgeeks . org/词频-kth-字符串中最小的字符/](https://www.geeksforgeeks.org/frequency-of-lexicographically-kth-smallest-character-in-the-a-string/)

给定一个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和一个整数 **K** ，任务是找到给定字符串中出现的词典上的 **K <sup>th</sup>** 最小字符的频率。

**示例:**

> **输入:**S =“geeks forgeeks”，K = 3
> **输出:** 4
> **解释:**S 中字典上最小的 3 <sup>rd</sup> 字符是‘e’。S = 4 中“e”的频率。
> 
> **输入:**S =“abcdabcd”，K = 4
> T3】输出:2
> T6】说明:S 中第 4 个<sup>最小的辞书字符为‘b’。S = 2 中“b”的频率。</sup>

**方法:**想法是[按照其](https://www.geeksforgeeks.org/sort-string-characters/) [ASCII 值](https://www.geeksforgeeks.org/program-print-ascii-value-character/)的升序对字符串进行排序。现在，在[排序字符串](https://www.geeksforgeeks.org/python-program-to-sort-a-string/)中找到**(K–1)<sup>第</sup>个字符**，并找到其出现频率。按照以下步骤解决问题:

*   [按照升序对给定的字符串](https://www.geeksforgeeks.org/sort-string-characters/) **S** 进行排序。
*   将**(K–1)<sup>第</sup>** 个字符存储在变量 **ch** 中，即**S【K–1】**。
*   [在 **S** 中找到字符 **ch**](https://www.geeksforgeeks.org/c-program-to-find-the-frequency-of-characters-in-a-string/) 的频率并打印该值。

以下是该方法的实施情况:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the frequency of
// the lexicographically Kth smallest
// character
void KthCharacter(
  string S, int N, int K)
{

  // Convert the string to
  // array of characters
  char strarray[N + 1];
  strcpy(strarray, S.c_str());

  // Sort the array in ascending order
  sort(strarray, strarray + N);

  // Store the Kth character
  char ch = strarray[K - 1];

  // Store the frequency of
  // the K-th character
  int count = 0;

  // Count the frequency of
  // the K-th character
  for (auto c : strarray)
  {
    if (c == ch)
      count++;
  }

  // Print the count
  cout << count;
}

// Driver Code
int main()
{
  string S = "geeksforgeeks";
  int N = S.length();
  int K = 3;

  KthCharacter(S, N, K);

  return 0;
}

// This code is contributed by sanjoy_62.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to find the frequency of
    // the lexicographically Kth smallest
    // character
    public static void KthCharacter(
        String S, int N, int K)
    {
        // Convert the string to
        // array of characters
        char strarray[] = S.toCharArray();

        // Sort the array in ascending order
        Arrays.sort(strarray);

        // Store the Kth character
        char ch = strarray[K - 1];

        // Store the frequency of
        // the K-th character
        int count = 0;

        // Count the frequency of
        // the K-th character
        for (char c : strarray) {
            if (c == ch)
                count++;
        }

        // Print the count
        System.out.println(count);
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "geeksforgeeks";
        int N = S.length();
        int K = 3;

        KthCharacter(S, N, K);
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the frequency of
# the lexicographically Kth smallest
# character
def KthCharacter(S, N, K):

    # Convert the string to
    # array of characters
    strarray = [char for char in S];

    # Sort the array in ascending order
    strarray.sort();

    # Store the Kth character
    ch = strarray[K - 1];

    # Store the frequency of
    # the K-th character
    count = 0;

    # Count the frequency of
    # the K-th character
    for c in strarray:
        if (c == ch):
            count += 1;

    # Prthe count
    print(count);

# Driver Code
if __name__ == '__main__':
    S = "geeksforgeeks";
    N = len(S);
    K = 3;

    KthCharacter(S, N, K);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

  // Function to find the frequency of
  // the lexicographically Kth smallest
  // character
  public static void KthCharacter(
    string S, int N, int K)
  {

    // Convert the string to
    // array of characters
    char[] strarray = S.ToCharArray();

    // Sort the array in ascending order
    Array.Sort(strarray);

    // Store the Kth character
    char ch = strarray[K - 1];

    // Store the frequency of
    // the K-th character
    int count = 0;

    // Count the frequency of
    // the K-th character
    foreach (char c in strarray)
    {
      if (c == ch)
        count++;
    }

    // Print the count
    Console.Write(count);
  }

  // Driver Code
  public static void Main()
  {
    string S = "geeksforgeeks";
    int N = S.Length;
    int K = 3;

    KthCharacter(S, N, K);
  }
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the frequency of
// the lexicographically Kth smallest
// character
function KthCharacter(S, N, K)
{

    // Convert the string to
    // array of characters
    var strarray = S.split('');

    strarray.sort();

    // Store the Kth character
    var ch = strarray[K - 1];

    // Store the frequency of
    // the K-th character
    var count = 0;

    // Count the frequency of
    // the K-th character
    strarray.forEach(c => {
        if (c == ch)
            count++;
    });

    // Print the count
    document.write(count);
}

// Driver Code
var S = "geeksforgeeks";
var N = S.length;
var K = 3;

KthCharacter(S, N, K);

// This code is contributed by famously

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*