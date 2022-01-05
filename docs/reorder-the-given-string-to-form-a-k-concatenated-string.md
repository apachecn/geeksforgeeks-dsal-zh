# 对给定的字符串重新排序，形成一个 K 连接的字符串

> 原文:[https://www . geeksforgeeks . org/将给定字符串重新排序以形成 a-k 连接字符串/](https://www.geeksforgeeks.org/reorder-the-given-string-to-form-a-k-concatenated-string/)

给定一个字符串 S 和一个整数 K，任务是形成一个字符串 T，使得字符串 T 是字符串 S 的重新排序，其方式是**K-连接字符串**。如果一个字符串恰好包含某个字符串的 K 个副本，那么它就被称为 K 连接字符串。
例如，字符串“极客”是由字符串“极客”的 2 个副本串联而成的 2-串联字符串。
**注**:可多选答案。
**举例:**

> **输入**:s =【gkeekee】，k=2
> **输出**:极客
> eegkeek 是另一种可能的 K-串接串
> **输入**:s =【ABCD】，k=2
> **输出**:不可能

**方法:**要找到一个有效的排序，即 K 连接字符串，迭代整个字符串，并为字符维护一个频率数组，以保存每个字符在字符串中出现的次数。因为，在 K 连接字符串中，一个字符出现的次数应该可以被 K 整除。如果发现任何字符不在此之后，则该字符串不能以任何方式排序来表示 K 连接字符串，否则在 K 连接字符串的单个副本中可能正好有 I<sup>字符的**(I<sup>第</sup>字符的频率/ K)** 副本。当重复 K 次时，这样的单个拷贝形成一个有效的 K 连接串。
以下是上述方法的实施:</sup> 

## C++

```
// C++ program to form a
// K-Concatenated-String from a given string
#include <bits/stdc++.h>
using namespace std;

// Function to print the k-concatenated string
string kStringGenerate(string str, int k)
{

    // maintain a frequency table
    // for lowercase letters
    int frequency[26] = { 0 };

    int len = str.length();

    for (int i = 0; i < len; i++) {

        // for each character increment its frequency
        // in the frequency array
        frequency[str[i] - 'a']++;
    }

    // stores a single copy of a string,
    // which on repeating forms a k-string
    string single_copy = "";

    // iterate over frequency array
    for (int i = 0; i < 26; i++) {

        // if the character occurs in the string,
        // check if it is divisible by k,
        // if not divisible then k-string cant be formed
        if (frequency[i] != 0) {

            if ((frequency[i] % k) != 0) {

                string ans = "Not Possible";
                return ans;
            }
            else {

                // ith character occurs (frequency[i]/k) times in a
                // single copy of k-string
                int total_occurrences = (frequency[i] / k);

                for (int j = 0; j < total_occurrences; j++) {
                    single_copy += char(i + 97);
                }
            }
        }
    }

    string kString;

    // append the single copy formed k times
    for (int i = 0; i < k; i++) {
        kString += single_copy;
    }

    return kString;
}

// Driver Code
int main()
{
    string str = "gkeekgee";
    int K = 2;

    string kString = kStringGenerate(str, K);
    cout << kString;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to form a
// K-Concatenated-String
// from a given string
import java.io.*;
import java.util.*;
import java.lang.*;

class GFG
{

// Function to print
// the k-concatenated string
static String kStringGenerate(String str,
                              int k)
{

    // maintain a frequency table
    // for lowercase letters
    int frequency[] = new int[26];
    Arrays.fill(frequency,0);
    int len = str.length();

    for (int i = 0; i < len; i++)
    {

        // for each character
        // increment its frequency
        // in the frequency array
        frequency[str.charAt(i) - 'a']++;
    }

    // stores a single copy
    // of a string, which on
    // repeating forms a k-string
    String single_copy = "";

    // iterate over
    // frequency array
    for (int i = 0; i < 26; i++)
    {

        // if the character occurs
        // in the string, check if
        // it is divisible by k,
        // if not divisible then
        // k-string cant be formed
        if (frequency[i] != 0)
        {

            if ((frequency[i] % k) != 0)
            {
                String ans = "Not Possible";
                return ans;
            }
            else
            {

                // ith character occurs
                // (frequency[i]/k) times in
                // a single copy of k-string
                int total_occurrences = (frequency[i] / k);

                for (int j = 0;
                         j < total_occurrences; j++)
                {
                    single_copy += (char)(i + 97);
                }
            }
        }
    }

    String kString = "";

    // append the single
    // copy formed k times
    for (int i = 0; i < k; i++)
    {
        kString += single_copy;
    }

    return kString;
}

// Driver Code
public static void main(String[] args)
{
    String str = "gkeekgee";
    int K = 2;

    String kString = kStringGenerate(str, K);
    System.out.print(kString);
}
}
```

## 蟒蛇 3

```
# Python 3 program to form a
# K-Concatenated-String from a given string

# Function to print the k-concatenated string

def kStringGenerate(st, k):

    # maintain a frequency table
    # for lowercase letters
    frequency = [0] * 26

    length = len(st)

    for i in range(length):

        # for each character increment its frequency
        # in the frequency array
        frequency[ord(st[i]) - ord('a')] += 1

    # stores a single copy of a string,
    # which on repeating forms a k-string
    single_copy = ""

    # iterate over frequency array
    for i in range(26):

        # if the character occurs in the string,
        # check if it is divisible by k,
        # if not divisible then k-string cant be formed
        if (frequency[i] != 0):

            if ((frequency[i] % k) != 0):

                ans = "Not Possible"
                return ans

            else:

                # ith character occurs (frequency[i]/k) times in a
                # single copy of k-string
                total_occurrences = (frequency[i] // k)

                for j in range(total_occurrences):
                    single_copy += chr(i + 97)

    kString = ""

    # append the single copy formed k times
    for i in range(k):
        kString += single_copy

    return kString

# Driver Code
if __name__ == "__main__":

    st = "gkeekgee"
    K = 2

    kString = kStringGenerate(st, K)
    print(kString)

    # This code is contributed by ukasp.
```

## C#

```
// C# program to form a
// K-Concatenated-String
// from a given string
using System;

class GFG
{

// Function to print
// the k-concatenated string
static String kStringGenerate(String str,
                            int k)
{

    // maintain a frequency table
    // for lowercase letters
    int []frequency = new int[26];
    int len = str.Length;

    for (int i = 0; i < len; i++)
    {

        // for each character
        // increment its frequency
        // in the frequency array
        frequency[str[i]- 'a']++;
    }

    // stores a single copy
    // of a string, which on
    // repeating forms a k-string
    String single_copy = "";

    // iterate over
    // frequency array
    for (int i = 0; i < 26; i++)
    {

        // if the character occurs
        // in the string, check if
        // it is divisible by k,
        // if not divisible then
        // k-string cant be formed
        if (frequency[i] != 0)
        {

            if ((frequency[i] % k) != 0)
            {
                String ans = "Not Possible";
                return ans;
            }
            else
            {

                // ith character occurs
                // (frequency[i]/k) times in
                // a single copy of k-string
                int total_occurrences = (frequency[i] / k);

                for (int j = 0;
                        j < total_occurrences; j++)
                {
                    single_copy += (char)(i + 97);
                }
            }
        }
    }

    String kString = "";

    // append the single
    // copy formed k times
    for (int i = 0; i < k; i++)
    {
        kString += single_copy;
    }

    return kString;
}

// Driver Code
public static void Main(String[] args)
{
    String str = "gkeekgee";
    int K = 2;

    String kString = kStringGenerate(str, K);
    Console.Write(kString);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
      // JavaScript program to form a
      // K-Concatenated-String
      // from a given string

      // Function to print
      // the k-concatenated string
      function kStringGenerate(str, k) {
        // maintain a frequency table
        // for lowercase letters
        var frequency = new Array(26).fill(0);
        var len = str.length;

        for (var i = 0; i < len; i++) {
          // for each character
          // increment its frequency
          // in the frequency array
          frequency[str[i].charCodeAt(0) - "a".charCodeAt(0)]++;
        }

        // stores a single copy
        // of a string, which on
        // repeating forms a k-string
        var single_copy = "";

        // iterate over
        // frequency array
        for (var i = 0; i < 26; i++) {
          // if the character occurs
          // in the string, check if
          // it is divisible by k,
          // if not divisible then
          // k-string cant be formed
          if (frequency[i] != 0) {
            if (frequency[i] % k != 0) {
              var ans = "Not Possible";
              return ans;
            } else {
              // ith character occurs
              // (frequency[i]/k) times in
              // a single copy of k-string
              var total_occurrences = parseInt(frequency[i] / k);

              for (var j = 0; j < total_occurrences; j++) {
                single_copy += String.fromCharCode(i + 97);
              }
            }
          }
        }

        var kString = "";

        // append the single
        // copy formed k times
        for (var i = 0; i < k; i++) {
          kString += single_copy;
        }

        return kString;
      }

      // Driver Code
      var str = "gkeekgee";
      var K = 2;

      var kString = kStringGenerate(str, K);
      document.write(kString);

    </script>
```

**Output:** 

```
eegkeegk
```

**时间复杂度:** O(N)，其中 N 为字符串的长度。