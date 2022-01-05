# 计算一个字符串中恰好出现 K 次的 M 长度子字符串

> 原文:[https://www . geeksforgeeks . org/count-m-length-substrings-occurrency-k-times-in-a-string/](https://www.geeksforgeeks.org/count-m-length-substrings-occurring-exactly-k-times-in-a-string/)

给定一个长度为 **N** 的**S**和两个整数 **M** 和 **K** ，任务是计算长度为 **M** 的[子串](https://www.geeksforgeeks.org/substring-in-cpp/)在字符串 **S** 中精确出现 **K** 次的数量。

**示例:**

> **输入:**S =“abacaba”，M = 3，K = 2
> **输出:** 1
> **解释:**长度为 3 的所有不同子串都是“aba”、“bac”、“aca”、“cab”。
> 在所有这些子字符串中，只有“aba”在字符串 s 中出现两次。
> 因此，计数为 1。
> 
> **输入:** S = "geeksforgeeks "，M = 2，K = 1
> **输出:** 4
> **解释:**
> 长度为 2 的所有不同子串都是“ge”、“ee”、“ek”、“ks”、“sf”、“fo”、“or”、“rg”。
> 在所有这些字符串中，“sf”、“fo”、“or”、“rg”在字符串 s 中出现一次。
> 因此，计数为 4。

**朴素方法:**最简单的方法是[生成所有长度为**M**T5】的子串，并将串中每个子串的](https://www.geeksforgeeks.org/program-print-substrings-given-string/)[频率](https://www.geeksforgeeks.org/frequency-substring-string/)T8】S 存储在[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。现在，[遍历地图](https://www.geeksforgeeks.org/iterate-map-java/)，如果频率等于 **K** ，那么将**计数**增加 **1** 。完成上述步骤后，打印**计数**作为结果。
***时间复杂度:**O((N–M)* N * M)*
***辅助空间:**O(N–M)*

**高效方法:**上述方法可以通过使用 [KMP 算法](https://www.geeksforgeeks.org/kmp-algorithm-for-pattern-searching/)[来寻找字符串中子串的频率](https://www.geeksforgeeks.org/frequency-substring-string/)来优化。按照以下步骤解决问题:

*   初始化一个变量，说**把**计数为 **0** ，存储所需子串的个数。
*   [从字符串 **S** 生成长度为 M](https://www.geeksforgeeks.org/program-print-substrings-given-string/) 的所有子字符串，并将它们插入到[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中，比如说 **arr[]。**
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**，对于数组中的每个字符串，使用 [**KMP** 算法计算其在字符串 **S** 中的频率。](https://www.geeksforgeeks.org/kmp-algorithm-for-pattern-searching/)
*   如果弦的频率等于 **P** ，那么将**计数**增加 **1** 。
*   完成上述步骤后，打印**计数**的值作为子串的结果计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to compute the LPS array
void computeLPSArray(string pat, int M,
                     int lps[])
{
    // Length of the previous
    // longest prefix suffix
    int len = 0;
    int i = 1;
    lps[0] = 0;

    // Iterate from [1, M - 1] to find lps[i]
    while (i < M) {

        // If the characters match
        if (pat[i] == pat[len]) {

            len++;
            lps[i] = len;
            i++;
        }

        // If pat[i] != pat[len]
        else {

            // If length is non-zero
            if (len != 0) {
                len = lps[len - 1];

                // Also, note that i is
                // not incremented here
            }

            // Otherwise
            else {
                lps[i] = len;
                i++;
            }
        }
    }
}

// Function to find the frequency of
// pat in the string txt
int KMPSearch(string pat, string txt)
{
    // Stores length of both strings
    int M = pat.length();
    int N = txt.length();

    // Initialize lps[] to store the
    // longest prefix suffix values
    // for the string pattern
    int lps[M];

    // Store the index for pat[]
    int j = 0;

    // Preprocess the pattern
    // (calculate lps[] array)
    computeLPSArray(pat, M, lps);

    // Store the index for txt[]
    int i = 0;
    int res = 0;
    int next_i = 0;

    while (i < N) {
        if (pat[j] == txt[i]) {
            j++;
            i++;
        }
        if (j == M) {

            // If pattern is found the
            // first time, iterate again
            // to check for more patterns
            j = lps[j - 1];
            res++;

            // Start i to check for more
            // than once occurrence
            // of pattern, reset i to
            // previous start + 1
            if (lps[j] != 0)
                i = ++next_i;
            j = 0;
        }

        // Mismatch after j matches
        else if (i < N
                 && pat[j] != txt[i]) {

            // Do not match lps[0..lps[j-1]]
            // characters, they will
            // match anyway
            if (j != 0)
                j = lps[j - 1];
            else
                i = i + 1;
        }
    }

    // Return the required frequency
    return res;
}

// Function to find count of substrings
// of length M occurring exactly P times
// in the string, S
void findCount(string& S, int M, int P)
{

    // Store all substrings of length M
    set<string> vec;

    // Store the size of the string, S
    int n = S.length();

    // Pick starting point
    for (int i = 0; i < n; i++) {

        // Pick ending point
        for (int len = 1;
             len <= n - i; len++) {

            // If the substring is of
            // length M, insert it in vec
            string s = S.substr(i, len);
            if (s.length() == M) {
                vec.insert(s);
            }
        }
    }

    // Initialise count as 0 to store
    // the required count of substrings
    int count = 0;

    // Iterate through the set of
    // substrings
    for (auto it : vec) {

        // Store its frequency
        int ans = KMPSearch(it, S);

        // If frequency is equal to P
        if (ans == P) {

            // Increment count by 1
            count++;
        }
    }

    // Print the answer
    cout << count;
}

// Driver Code
int main()
{
    string S = "abacaba";
    int M = 3, P = 2;

    // Function Call
    findCount(S, M, P);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to compute the LPS array
    static void computeLPSArray(String pat, int M,
                                int lps[])
    {
        // Length of the previous
        // longest prefix suffix
        int len = 0;
        int i = 1;
        lps[0] = 0;

        // Iterate from [1, M - 1] to find lps[i]
        while (i < M) {

            // If the characters match
            if (pat.charAt(i) == pat.charAt(len)) {

                len++;
                lps[i] = len;
                i++;
            }

            // If pat[i] != pat[len]
            else {

                // If length is non-zero
                if (len != 0) {
                    len = lps[len - 1];

                    // Also, note that i is
                    // not incremented here
                }

                // Otherwise
                else {
                    lps[i] = len;
                    i++;
                }
            }
        }
    }

    // Function to find the frequency of
    // pat in the string txt
    static int KMPSearch(String pat, String txt)
    {
        // Stores length of both strings
        int M = pat.length();
        int N = txt.length();

        // Initialize lps[] to store the
        // longest prefix suffix values
        // for the string pattern
        int lps[] = new int[M];

        // Store the index for pat[]
        int j = 0;

        // Preprocess the pattern
        // (calculate lps[] array)
        computeLPSArray(pat, M, lps);

        // Store the index for txt[]
        int i = 0;
        int res = 0;
        int next_i = 0;

        while (i < N) {
            if (pat.charAt(j) == txt.charAt(i)) {
                j++;
                i++;
            }
            if (j == M) {

                // If pattern is found the
                // first time, iterate again
                // to check for more patterns
                j = lps[j - 1];
                res++;

                // Start i to check for more
                // than once occurrence
                // of pattern, reset i to
                // previous start + 1
                if (lps[j] != 0)
                    i = ++next_i;
                j = 0;
            }

            // Mismatch after j matches
            else if (i < N
                     && pat.charAt(j) != txt.charAt(i)) {

                // Do not match lps[0..lps[j-1]]
                // characters, they will
                // match anyway
                if (j != 0)
                    j = lps[j - 1];
                else
                    i = i + 1;
            }
        }

        // Return the required frequency
        return res;
    }

    // Function to find count of substrings
    // of length M occurring exactly P times
    // in the string, S
    static void findCount(String S, int M, int P)
    {

        // Store all substrings of length M
        // set<string> vec;
        TreeSet<String> vec = new TreeSet<>();

        // Store the size of the string, S
        int n = S.length();

        // Pick starting point
        for (int i = 0; i < n; i++) {

            // Pick ending point
            for (int len = 1; len <= n - i; len++) {

                // If the substring is of
                // length M, insert it in vec
                String s = S.substring(i, i + len);
                if (s.length() == M) {
                    vec.add(s);
                }
            }
        }

        // Initialise count as 0 to store
        // the required count of substrings
        int count = 0;

        // Iterate through the set of
        // substrings
        for (String it : vec) {

            // Store its frequency
            int ans = KMPSearch(it, S);

            // If frequency is equal to P
            if (ans == P) {

                // Increment count by 1
                count++;
            }
        }

        // Print the answer
        System.out.println(count);
    }

    // Driver Code
    public static void main(String[] args)
    {

        String S = "abacaba";
        int M = 3, P = 2;

        // Function Call
        findCount(S, M, P);
    }
}

// This code is contributed by kingash.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to compute the LPS array
def computeLPSArray(pat, M, lps):

    # Length of the previous
    # longest prefix suffix
    len1 = 0
    i = 1
    lps[0] = 0

    # Iterate from [1, M - 1] to find lps[i]
    while (i < M):

        # If the characters match
        if (pat[i] == pat[len1]):
            len1 += 1
            lps[i] = len1
            i += 1

        # If pat[i] != pat[len]
        else:
            # If length is non-zero
            if (len1 != 0):
                len1 = lps[len1 - 1]

                # Also, note that i is
                # not incremented here

            # Otherwise
            else:
                lps[i] = len1
                i += 1

# Function to find the frequency of
# pat in the string txt
def KMPSearch(pat, txt):

    # Stores length of both strings
    M = len(pat)
    N = len(txt)

    # Initialize lps[] to store the
    # longest prefix suffix values
    # for the string pattern
    lps = [0 for i in range(M)]

    # Store the index for pat[]
    j = 0

    # Preprocess the pattern
    # (calculate lps[] array)
    computeLPSArray(pat, M, lps)

    # Store the index for txt[]
    i = 0
    res = 0
    next_i = 0

    while (i < N):
        if (pat[j] == txt[i]):
            j += 1
            i += 1
        if (j == M):

            # If pattern is found the
            # first time, iterate again
            # to check for more patterns
            j = lps[j - 1]
            res += 1

            # Start i to check for more
            # than once occurrence
            # of pattern, reset i to
            # previous start + 1
            if (lps[j] != 0):
                next_i += 1
                i = next_i
            j = 0

        # Mismatch after j matches
        elif (i < N and pat[j] != txt[i]):
            # Do not match lps[0..lps[j-1]]
            # characters, they will
            # match anyway
            if (j != 0):
                j = lps[j - 1]
            else:
                i = i + 1

    # Return the required frequency
    return res

# Function to find count of substrings
# of length M occurring exactly P times
# in the string, S
def findCount(S, M, P):

    # Store all substrings of length M
    vec = set()

    # Store the size of the string, S
    n = len(S)

    # Pick starting point
    for i in range(n):

        # Pick ending point
        for len1 in range(n - i + 1):

            # If the substring is of
            # length M, insert it in vec
            s = S[i:len1]

          #  if (len1(s) == M):
           #     vec.add(s)

    # Initialise count as 0 to store
    # the required count of substrings
    count = 1

    # Iterate through the set of
    # substrings
    for it in vec:

        # Store its frequency
        ans = KMPSearch(it, S)

        # If frequency is equal to P
        if (ans == P):

            # Increment count by 1
            count += 1

    # Print the answer
    print(count)

# Driver Code
if __name__ == '__main__':
    S = "abacaba"
    M = 3
    P = 2

    # Function Call
    findCount(S, M, P)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to compute the LPS array
  static void computeLPSArray(string pat, int M, int[] lps)
  {

    // Length of the previous
    // longest prefix suffix
    int len = 0;
    int i = 1;
    lps[0] = 0;

    // Iterate from [1, M - 1] to find lps[i]
    while (i < M)
    {

      // If the characters match
      if (pat[i] == pat[len])
      {
        len++;
        lps[i] = len;
        i++;
      }

      // If pat[i] != pat[len]
      else {

        // If length is non-zero
        if (len != 0) {
          len = lps[len - 1];

          // Also, note that i is
          // not incremented here
        }

        // Otherwise
        else {
          lps[i] = len;
          i++;
        }
      }
    }
  }

  // Function to find the frequency of
  // pat in the string txt
  static int KMPSearch(string pat, string txt)
  {

    // Stores length of both strings
    int M = pat.Length;
    int N = txt.Length;

    // Initialize lps[] to store the
    // longest prefix suffix values
    // for the string pattern
    int[] lps = new int[M];

    // Store the index for pat[]
    int j = 0;

    // Preprocess the pattern
    // (calculate lps[] array)
    computeLPSArray(pat, M, lps);

    // Store the index for txt[]
    int i = 0;
    int res = 0;
    int next_i = 0;

    while (i < N) {
      if (pat[j] == txt[i]) {
        j++;
        i++;
      }
      if (j == M) {

        // If pattern is found the
        // first time, iterate again
        // to check for more patterns
        j = lps[j - 1];
        res++;

        // Start i to check for more
        // than once occurrence
        // of pattern, reset i to
        // previous start + 1
        if (lps[j] != 0)
          i = ++next_i;
        j = 0;
      }

      // Mismatch after j matches
      else if (i < N
               && pat[j] != txt[i]) {

        // Do not match lps[0..lps[j-1]]
        // characters, they will
        // match anyway
        if (j != 0)
          j = lps[j - 1];
        else
          i = i + 1;
      }
    }

    // Return the required frequency
    return res;
  }

  // Function to find count of substrings
  // of length M occurring exactly P times
  // in the string, S
  static void findCount(string S, int M, int P)
  {

    // Store all substrings of length M
    HashSet<string> vec = new HashSet<string>();

    // Store the size of the string, S
    int n = S.Length;

    // Pick starting point
    for (int i = 0; i < n; i++) {

      // Pick ending point
      for (int len = 1;
           len <= n - i; len++) {

        // If the substring is of
        // length M, insert it in vec
        string s = S.Substring(i, len);
        if (s.Length == M) {
          vec.Add(s);
        }
      }
    }

    // Initialise count as 0 to store
    // the required count of substrings
    int count = 0;

    // Iterate through the set of
    // substrings
    foreach(string it in vec) {

      // Store its frequency
      int ans = KMPSearch(it, S);

      // If frequency is equal to P
      if (ans == P) {

        // Increment count by 1
        count++;
      }
    }

    // Print the answer
    Console.WriteLine(count);
  }

  // Driver code
  static void Main() {
    string S = "abacaba";
    int M = 3, P = 2;

    // Function Call
    findCount(S, M, P);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

//Javascript implementation of the approach

// Function to compute the LPS array
function computeLPSArray(pat, M, lps)
{
    // Length of the previous
    // longest prefix suffix
    var len = 0;
    var i = 1;
    lps[0] = 0;

    // Iterate from [1, M - 1] to find lps[i]
    while (i < M) {

        // If the characters match
        if (pat[i] == pat[len]) {

            len++;
            lps[i] = len;
            i++;
        }

        // If pat[i] != pat[len]
        else {

            // If length is non-zero
            if (len != 0) {
                len = lps[len - 1];

                // Also, note that i is
                // not incremented here
            }

            // Otherwise
            else {
                lps[i] = len;
                i++;
            }
        }
    }
}

// Function to find the frequency of
// pat in the string txt
function KMPSearch(pat, txt)
{
    // Stores length of both strings
    var M = pat.length;
    var N = txt.length;

    // Initialize lps[] to store the
    // longest prefix suffix values
    // for the string pattern
    var lps = new Array(M);

    // Store the index for pat[]
    var j = 0;

    // Preprocess the pattern
    // (calculate lps[] array)
    computeLPSArray(pat, M, lps);

    // Store the index for txt[]
    var i = 0;
    var res = 0;
    var next_i = 0;

    while (i < N) {
        if (pat[j] == txt[i]) {
            j++;
            i++;
        }
        if (j == M) {

            // If pattern is found the
            // first time, iterate again
            // to check for more patterns
            j = lps[j - 1];
            res++;

            // Start i to check for more
            // than once occurrence
            // of pattern, reset i to
            // previous start + 1
            if (lps[j] != 0)
                i = ++next_i;
            j = 0;
        }

        // Mismatch after j matches
        else if (i < N
                 && pat[j] != txt[i]) {

            // Do not match lps[0..lps[j-1]]
            // characters, they will
            // match anyway
            if (j != 0)
                j = lps[j - 1];
            else
                i = i + 1;
        }
    }

    // Return the required frequency
    return res;
}

// Function to find count of substrings
// of length M occurring exactly P times
// in the string, S
function findCount( S, M, P)
{

    // Store all substrings of length M
    var vec = new Set();

    // Store the size of the string, S
    var n = S.length;

    // Pick starting point
    for (var i = 0; i < n; i++) {

        // Pick ending point
        for (var len = 1;
             len <= n - i; len++) {

            // If the substring is of
            // length M, insert it in vec
            var s = S.substring(i, len);
            if (s.length == M) {
                vec.add(s);
            }
        }
    }

    // Initialise count as 0 to store
    // the required count of substrings
    var count = 0;

    // Iterate through the set of
    // substrings
    for (const it of vec){

        // Store its frequency
        var ans = KMPSearch(it, S);

        // If frequency is equal to P
        if (ans == P) {

            // Increment count by 1
            count++;
        }
    }

    // Print the answer
    document.write( count);
}

var S = "abacaba";
var M = 3, P = 2;
// Function Call
findCount(S, M, P);

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O((N * M)+(N<sup>2</sup>–M<sup>2</sup>)*
***辅助空间:**O(N–M)*