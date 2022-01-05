# 去除频率不等于 2 次方的字符后，通过字符排序修改字符串

> 原文:[https://www . geeksforgeeks . org/按排序修改字符串-移除频率不等于 2 次方的字符后的字符/](https://www.geeksforgeeks.org/modify-string-by-sorting-characters-after-removal-of-characters-whose-frequency-is-not-equal-to-power-of-2/)

给定一个由 **N** 个小写字母组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是[从频率不是 2](https://www.geeksforgeeks.org/remove-all-occurrences-of-a-character-in-a-string/) 的[次方的字符串](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)中移除字符，然后[按升序排序该字符串](https://www.geeksforgeeks.org/program-sort-string-descending-order/)。

**示例:**

> **输入:**S = " aacbb "
> **输出:** bbc
> **解释:**给定字符串中‘a’、‘b’和‘c’的频率为 3、2、1。只有字符“a”的频率(= 3)不是 2 的幂。因此，从字符串 S 中移除“a”会将其修改为“cbb”。因此，排序后修改后的字符串为“bbc”。
> 
> **输入:**S = " geeksforgeks "
> T3】输出:eeeefggkkors

**方法:**给定的问题可以通过[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)来解决。按照以下步骤解决给定的问题:

*   初始化一个大小为 **26** 的辅助[数组](https://www.geeksforgeeks.org/array-data-structure/)，比如说 **freq[]** ，将每个字符的[频率存储在字符串](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/) **S** 中，使得索引 **0** 代表字符**“a”**， **1** 代表字符**“b”**等等。
*   [遍历给定的字符串**S**T3】并将数组**freq【】**中每个字符**S【I】**的频率增加 **1** 。](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)
*   [遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **freq[]** ，如果 **freq[i]** [的值是 2 的幂](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)，则打印字符 **('a' + i)，freq[i]** 的次数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to remove all the characters
// from a string that whose frequencies
// are not equal to a perfect power of 2
void countFrequency(string S, int N)
{
    // Stores the frequency of
    // each character in S
    int freq[26] = { 0 };

    // Iterate over characters of string
    for (int i = 0; i < N; i++) {

        // Update frequency of current
        // character in the array freq[]
        freq[S[i] - 'a']++;
    }

    // Traverse the array freq[]
    for (int i = 0; i < 26; i++) {

        // Check if the i-th letter
        // is absent from string S
        if (freq[i] == 0)
            continue;

        // Calculate log of frequency
        // of the current character
        // in the string S
        int lg = log2(freq[i]);

        // Calculate power of 2 of lg
        int a = pow(2, lg);

        // Check if freq[i]
        // is a power of 2
        if (a == freq[i]) {

            // Print letter i + 'a'
            // freq[i] times
            while (freq[i]--)
                cout << (char)(i + 'a');
        }
    }
}

// Driver Code
int main()
{
    string S = "aaacbb";
    int N = S.size();
    countFrequency(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to remove all the characters
// from a string that whose frequencies
// are not equal to a perfect power of 2
static void countFrequency(String S, int N)
{

    // Stores the frequency of
    // each character in S
    int []freq = new int[26];
    //Array.Clear(freq, 0, freq.Length);

    // Iterate over characters of string
    for(int i = 0; i < N; i++)
    {

        // Update frequency of current
        // character in the array freq[]
        freq[(int)S.charAt(i) - 'a'] += 1;
    }

    // Traverse the array freq[]
    for(int i = 0; i < 26; i++)
    {

        // Check if the i-th letter
        // is absent from string S
        if (freq[i] == 0)
            continue;

        // Calculate log of frequency
        // of the current character
        // in the string S
        int lg = (int)(Math.log(freq[i]) / Math.log(2));

        // Calculate power of 2 of lg
        int a = (int)Math.pow(2, lg);

        // Check if freq[i]
        // is a power of 2
        if (a == freq[i])
        {

            // Print letter i + 'a'
            // freq[i] times
            while (freq[i] > 0)
            {
                freq[i] -= 1;
                System.out.print((char)(i + 'a'));
            }
        }
    }
}

// Driver Code
public static void main(String args[])
{
    String S = "aaacbb";
    int N = S.length();

    countFrequency(S, N);
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import log2

# Function to remove all the characters
# from a that whose frequencies are not
# equal to a perfect power of 2
def countFrequency(S, N):

    # Stores the frequency of
    # each character in S
    freq = [0] * 26

    # Iterate over characters of string
    for i in range(N):

        # Update frequency of current
        # character in the array freq[]
        freq[ord(S[i]) - ord('a')] += 1

    # Traverse the array freq[]
    for i in range(26):

        # Check if the i-th letter
        # is absent from S
        if (freq[i] == 0):
            continue

        # Calculate log of frequency
        # of the current character
        # in the S
        lg = int(log2(freq[i]))

        # Calculate power of 2 of lg
        a = pow(2, lg)

        # Check if freq[i]
        # is a power of 2
        if (a == freq[i]):

            # Print letter i + 'a'
            # freq[i] times
            while (freq[i]):
                print(chr(i + ord('a')), end = "")
                freq[i] -= 1

# Driver Code
if __name__ == '__main__':

    S = "aaacbb"
    N = len(S)

    countFrequency(S, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to remove all the characters
// from a string that whose frequencies
// are not equal to a perfect power of 2
static void countFrequency(string S, int N)
{

    // Stores the frequency of
    // each character in S
    int []freq = new int[26];
    Array.Clear(freq, 0, freq.Length);

    // Iterate over characters of string
    for(int i = 0; i < N; i++)
    {

        // Update frequency of current
        // character in the array freq[]
        freq[(int)S[i] - 'a'] += 1;
    }

    // Traverse the array freq[]
    for(int i = 0; i < 26; i++)
    {

        // Check if the i-th letter
        // is absent from string S
        if (freq[i] == 0)
            continue;

        // Calculate log of frequency
        // of the current character
        // in the string S
        int lg = (int)Math.Log((double)freq[i], 2.0);

        // Calculate power of 2 of lg
        int a = (int)Math.Pow(2, lg);

        // Check if freq[i]
        // is a power of 2
        if (a == freq[i])
        {

            // Print letter i + 'a'
            // freq[i] times
            while (freq[i] > 0)
            {
                freq[i] -= 1;
                Console.Write((char)(i + 'a'));
            }
        }
    }
}

// Driver Code
public static void Main()
{
    string S = "aaacbb";
    int N = S.Length;

    countFrequency(S, N);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to remove all the characters
      // from a string that whose frequencies
      // are not equal to a perfect power of 2
      function countFrequency(S, N)
      {

        // Stores the frequency of
        // each character in S
        var freq = new Array(26).fill(0);

        // Iterate over characters of string
        for (var i = 0; i < N; i++)
        {

          // Update frequency of current
          // character in the array freq[]
          freq[S[i].charCodeAt(0) - "a".charCodeAt(0)]++;
        }

        // Traverse the array freq[]
        for (var i = 0; i < 26; i++)
        {

          // Check if the i-th letter
          // is absent from string S
          if (freq[i] === 0) continue;

          // Calculate log of frequency
          // of the current character
          // in the string S
          var lg = parseInt(Math.log2(freq[i]));

          // Calculate power of 2 of lg
          var a = Math.pow(2, lg);

          // Check if freq[i]
          // is a power of 2
          if (a === freq[i])
          {

            // Print letter i + 'a'
            // freq[i] times
            while (freq[i]--)
              document.write(String.fromCharCode(i + "a".charCodeAt(0)));
          }
        }
      }

      // Driver Code
      var S = "aaacbb";
      var N = S.length;
      countFrequency(S, N);

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
bbc
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)