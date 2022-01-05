# 计算所需的最少字符替换，以使给定字符串满足给定条件

> 原文:[https://www . geesforgeks . org/count-最小字符替换-必需-给定字符串满足给定条件/](https://www.geeksforgeeks.org/count-minimum-character-replacements-required-such-that-given-string-satisfies-the-given-conditions/)

给定一个由小写字母组成的长度为 **N** 的字符串 **S** ，任务是计算需要替换的最小字符数，以使给定的字符串 **S** 特殊。

> 一个字符串 **S** 是特殊的当且仅当对于所有可能的对 **(S[i]，S[j])** ( *基于 1 的索引*)其中 **1 ≤ i ≤ N/2** 和 **N / 2 + 1 ≤ j ≤ N** ，下列条件之一必须为真:
> 
> *   **S[i] < S[j]:** 对于索引 **(i，j)**左半部分( **S[i]** )中的每个字符都小于右半部分中的每个字符( **S[j]** )。
> *   **S[i] > S[j]:** 对于索引 **(i，j)，**左半部分的每个字符( **S[i]** )大于右半部分的每个字符( **S[j]** )。
> *   **S[i] = S[j]:** 对于索引 **(i，j)，**左半部分的每个字符( **S[i]** )等于右半部分的每个字符( **S[j]** )。

**示例:**

> **输入:**S =“aababc”
> **输出:** 2
> **解释:**
> 字符串的左右部分为 Left =“aab”，Right =“ABC”
> **操作 1:** 更改 s[4] → d
> **操作 2:** 更改 s[5] → d
> 应用上述更改后，生成的字符串为满足以下所有条件的“aabddc”
> 
> **输入:** S = "aabaab"
> **输出:** 2
> **解释:**
> 字符串的左右部分为 Left="aab" Right="aab"
> **操作 1:** 更改 s[3] → a
> **操作 2:** 更改 s[6] → a
> 应用上述更改后，生成的字符串为满足所有条件的“aaaaa”

**方法:**思路是观察 **s[i]==s[j]** 只有 26 个字母数量的变化可以用[统计字符的出现频率](https://www.geeksforgeeks.org/java-program-to-count-the-occurrence-of-each-character-in-a-string-using-hashmap/)来完成。按照以下步骤解决上述问题:

*   存储左右半部字符的[频率分别存储在](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)[阵](https://www.geeksforgeeks.org/introduction-to-arrays/) **左[]** 和**右[]** 中。
*   初始化一个变量**计数**以记录**要进行的最小更改次数**。
*   使用变量 **d** 遍历**【0，26】**范围，并按照以下情况更改字符:
    *   对于 **s[i]** 等于 **s[j]:** 使所有字符等于一个字符 c，那么 count 的值就是**(N–左–右)**。
    *   对于 **s[i]** 小于 **s[j]:**
        *   最初，用最大数量的变更，在左侧进行，让**变更**为 **N/2** 。
        *   将左侧所有 **≤ d** 的字符相减，找出剩余的待改字符。
        *   将右侧所有等于 d 的字符相加，将大于 d 的字符改为**变-=左**、**变+=右**。
    *   对于 **s[i]** 大于 **s[j]:**
        *   最初，以最大的修改次数，在右侧进行，让**修改**为 **N/2** 。
        *   减去右侧所有 **≤d** 的字符，找到剩余的需要修改的字符。
        *   添加左侧所有等于 d 的字符，将这些字符更改为> d(s[I]~~change+=左侧和 **change -=右侧**。~~
*   在上述情况下，所有计数的最小值就是要求的结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function that finds the minimum
// count of steps required to make
// the string special
int minChange(string s, int n)
{

    // Stores the frequency of the
    // left & right half of string
    int L[26] = {0};
    int R[26] = {0};

    // Find frequency of left half
    for(int i = 0; i < n / 2; i++)
    {
        char ch = s[i];
        L[ch - 'a']++;
    }

    // Find frequency of left half
    for(int i = n / 2; i < n; i++)
    {
        char ch = s[i];
        R[ch - 'a']++;
    }

    int count = n;

    // Make all characters equal
    // to character c
    for(char ch = 'a'; ch <= 'z'; ch++)
    {
        count = min(count,
                    n - L[ch - 'a'] -
                        R[ch - 'a']);
    }

    // Case 1: For s[i] < s[j]
    int change = n / 2;
    for(int d = 0; d + 1 < 26; d++)
    {

        // Subtract all the characters
        // on left side that are <=d
        change -= L[d];

        // Adding all characters on the
        // right side that same as d
        change += R[d];

        // Find minimum value of count
        count = min(count, change);
    }

    // Similarly for Case 2: s[i] > s[j]
    change = n / 2;

    for(int d = 0; d + 1 < 26; d++)
    {
        change -= R[d];
        change += L[d];
        count = min(change, count);
    }

    // Return the minimum changes
    return count;
}

// Driver Code
int main()
{

    // Given string S
    string S = "aababc";

    int N = S.length();

    // Function Call
    cout << minChange(S, N) << "\n";
}

// This code is contributed by sallagondaavinashreddy7
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;
class Main {

    // Function that finds the minimum
    // count of steps required to make
    // the string special
    public static int minChange(String s,
                                int n)
    {

        // Stores the frequency of the
        // left & right half of string
        int L[] = new int[26];
        int R[] = new int[26];

        // Find frequency of left half
        for (int i = 0; i < n / 2; i++) {
            char ch = s.charAt(i);
            L[ch - 'a']++;
        }

        // Find frequency of left half
        for (int i = n / 2; i < n; i++) {
            char ch = s.charAt(i);
            R[ch - 'a']++;
        }
        int count = n;

        // Make all characters equal
        // to character c
        for (char ch = 'a'; ch <= 'z'; ch++) {

            count = Math.min(
                count,
                n - L[ch - 'a']
                    - R[ch - 'a']);
        }

        // Case 1: For s[i] < s[j]
        int change = n / 2;
        for (int d = 0; d + 1 < 26; d++) {

            // Subtract all the characters
            // on left side that are <=d
            change -= L[d];

            // Adding all characters on the
            // right side that same as d
            change += R[d];

            // Find minimum value of count
            count = Math.min(count, change);
        }

        // Similarly for Case 2: s[i] > s[j]
        change = n / 2;

        for (int d = 0; d + 1 < 26; d++) {
            change -= R[d];
            change += L[d];
            count = Math.min(change, count);
        }

        // Return the minimum changes
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given string S
        String S = "aababc";

        int N = S.length();

        // Function Call
        System.out.println(minChange(S, N));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function that finds the minimum
# count of steps required to make
# the string special
def minChange (s, n):

    # Stores the frequency of the
    # left & right half of string
    L = [0] * 26;
    R = [0] * 26;

    # Find frequency of left half
    for i in range(0, n // 2):
        ch = s[i];
        L[ord(ch) -
          ord('a')] += 1;

    # Find frequency of left half
    for i in range(n // 2, n):
        ch = s[i];
        R[ord(ch) -
          ord('a')] += 1;

    count = n;

    # Make all characters equal
    # to character c
    for ch in range(ord('a'),
                    ord('z')):
        count = min(count, n - L[ch - ord('a')] -
                               R[ch - ord('a')]);

    # Case 1: For s[i] < s[j]
    change = n / 2;

    for d in range(0, 25):

        # Subtract all the characters
        # on left side that are <=d
        change -= L[d];

        # Adding all characters on the
        # right side that same as d
        change += R[d];

        # Find minimum value of count
        count = min(count, change);

    # Similarly for Case 2: s[i] > s[j]
    change = n / 2;

    for d in range(0, 25):
        change -= R[d];
        change += L[d];
        count = min(change, count);

    # Return the minimum changes
    return int(count);

# Driver Code
if __name__ == '__main__':

    # Given string S
    S = "aababc";

    N = len(S);

    # Function Call
    print(minChange(S, N));

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function that finds the minimum
// count of steps required to make
// the string special
public static int minChange(String s,
                            int n)
{

    // Stores the frequency of the
    // left & right half of string
    int []L = new int[26];
    int []R = new int[26];

    // Find frequency of left half
    for(int i = 0; i < n / 2; i++)
    {
        char ch = s[i];
        L[ch - 'a']++;
    }

    // Find frequency of left half
    for(int i = n / 2; i < n; i++)
    {
        char ch = s[i];
        R[ch - 'a']++;
    }
    int count = n;

    // Make all characters equal
    // to character c
    for(char ch = 'a'; ch <= 'z'; ch++)
    {
        count = Math.Min(count,
                         n - L[ch - 'a'] -
                             R[ch - 'a']);
    }

    // Case 1: For s[i] < s[j]
    int change = n / 2;
    for(int d = 0; d + 1 < 26; d++)
    {

        // Subtract all the characters
        // on left side that are <=d
        change -= L[d];

        // Adding all characters on the
        // right side that same as d
        change += R[d];

        // Find minimum value of count
        count = Math.Min(count, change);
    }

    // Similarly for Case 2: s[i] > s[j]
    change = n / 2;

    for(int d = 0; d + 1 < 26; d++)
    {
        change -= R[d];
        change += L[d];
        count = Math.Min(change, count);
    }

    // Return the minimum changes
    return count;
}

// Driver Code
public static void Main(String[] args)
{

    // Given string S
    String S = "aababc";

    int N = S.Length;

    // Function Call
    Console.WriteLine(minChange(S, N));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

      // JavaScript program for the above approach

      // Function that finds the minimum
      // count of steps required to make
      // the string special
      function minChange(s, n)
      {
        // Stores the frequency of the
        // left & right half of string
        var L = new Array(26).fill(0);
        var R = new Array(26).fill(0);

        // Find frequency of left half
        for (var i = 0; i < n / 2; i++) {
          var ch = s[i].charCodeAt(0);
          L[ch - "a".charCodeAt(0)]++;
        }

        // Find frequency of left half
        for (var i = n / 2; i < n; i++) {
          var ch = s[i].charCodeAt(0);
          R[ch - "a".charCodeAt(0)]++;
        }
        var count = n;

        // Make all characters equal
        // to character c
        for (var ch = "a".charCodeAt(0);
        ch <= "z".charCodeAt(0); ch++) {
          count = Math.min(
            count,
            n - L[ch - "a".charCodeAt(0)] -
            R[ch - "a".charCodeAt(0)]
          );
        }

        // Case 1: For s[i] < s[j]
        var change = parseInt(n / 2);
        for (var d = 0; d + 1 < 26; d++) {
          // Subtract all the characters
          // on left side that are <=d
          change -= L[d];

          // Adding all characters on the
          // right side that same as d
          change += R[d];

          // Find minimum value of count
          count = Math.min(count, change);
        }

        // Similarly for Case 2: s[i] > s[j]
        change = n / 2;

        for (var d = 0; d + 1 < 26; d++) {
          change -= R[d];
          change += L[d];
          count = Math.min(change, count);
        }

        // Return the minimum changes
        return count;
      }

      // Driver Code
      // Given string S
      var S = "aababc";
      var N = S.length;

      // Function Call
      document.write(minChange(S, N));

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)