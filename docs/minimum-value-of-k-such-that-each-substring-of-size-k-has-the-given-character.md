# K 的最小值，使得大小为 K 的每个子串都具有给定的字符

> 原文:[https://www . geesforgeks . org/k 的最小值，这样每个大小为 k 的子串都有给定的字符/](https://www.geeksforgeeks.org/minimum-value-of-k-such-that-each-substring-of-size-k-has-the-given-character/)

给定一串小写字母 **S** 一个字符 **c** 。任务是找到最小值 **K** ，使得长度为 **K** 的每个**子串**包含给定的字符 **c** 。如果没有这样的 **K** 可能，返回 **-1** 。
**示例:**

> **输入:** S = "abdegb "，ch = 'b'
> **输出:** 4
> **说明:**
> 考虑 K 的值为 4。现在，大小为 K(= 4)的每个子串都是{“abde”、“bdeg”、“degb”}具有字符 ch(= b ')。
> 
> **输入:** S = "abfge "，ch = 'm'
> **输出:** -1

**天真方法:**解决给定问题的最简单方法是在范围**【1，N】**上迭代[子串](https://www.geeksforgeeks.org/substring-in-cpp/)的所有可能大小，并检查 **K** 的哪个最小值满足给定标准。如果 **K** 没有这样的值，那么打印**-1”**。

***时间复杂度:**O(N<sup>4</sup>)*
***辅助空间:** O(N)*

**有效方法:**上述方法也可以通过观察 **K** 的最小值等于给定字符**ch**T7】的[连续出现之间的最大差值来优化。对于大小为 **K** 的每个子串，必须至少有一个 **1** 字符作为 **ch** 。按照以下步骤解决给定的问题:](https://www.geeksforgeeks.org/program-count-occurrence-given-character-string/)

*   初始化一个变量，说**最大差值**为 **-1** ，存储 **K** 的合成值。
*   初始化一个变量，将 **previous** 设为 **0** ，存储字符串 **S** 中字符 **ch** 的[前一次出现。](https://www.geeksforgeeks.org/stdstringfind_last_of-in-c-with-examples/)
*   [使用变量 **i** 遍历给定字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，如果当前字符为 **ch** ，则将**最大差值**的值更新为**最大差值**和**(I–previous)**的最大值，并将 **previous** 的值更新为 **i** 。
*   完成上述步骤后，打印**最大差值**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum value
// of K such that char c occurs in all
// K sized substrings of string S
int findK(string s, char c)
{

    // Store the string length
    int n = s.size();

    // Store difference of lengths
    // of segments of every two
    // consecutive occurrences of c
    int diff;

    // Stores the maximum difference
    int max = 0;

    // Store the previous occurence
    // of char c
    int prev = 0;

    for (int i = 0; i < n; i++) {

        // Check if the current character
        // is c or not
        if (s[i] == c) {

            // Stores the difference of
            // consecutive occurrences of c
            diff = i - prev;

            // Update previous occurrence
            // of c with current occurence
            prev = i;

            // Comparing diff with max
            if (diff > max) {
                max = diff;
            }
        }
    }

    // If string doesn't contain c
    if (max == 0)
        return -1;

    // Return max
    return max;
}

// Driver Code
int main() {
    string S = "abdegb";
    char ch = 'b';
    cout<<(findK(S, ch));
    return 0;
}

// This code is contributed by 29AjayKumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    // Function to find the minimum value
    // of K such that char c occurs in all
    // K sized substrings of string S
    public static int findK(String s, char c)
    {

        // Store the string length
        int n = s.length();

        // Store difference of lengths
        // of segments of every two
        // consecutive occurrences of c
        int diff;

        // Stores the maximum difference
        int max = 0;

        // Store the previous occurence
        // of char c
        int prev = 0;

        for (int i = 0; i < n; i++) {

            // Check if the current character
            // is c or not
            if (s.charAt(i) == c) {

                // Stores the difference of
                // consecutive occurrences of c
                diff = i - prev;

                // Update previous occurrence
                // of c with current occurence
                prev = i;

                // Comparing diff with max
                if (diff > max) {
                    max = diff;
                }
            }
        }

        // If string doesn't contain c
        if (max == 0)
            return -1;

        // Return max
        return max;
    }

    // Driver Code
    public static void main(String args[]) {
        String S = "abdegb";
        char ch = 'b';
        System.out.println(findK(S, ch));

    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the minimum value
# of K such that char c occurs in all
# K sized substrings of string S
def findK(s, c):

    # Store the string length
    n = len(s)

    # Store difference of lengths
    # of segments of every two
    # consecutive occurrences of c
    diff = 0

    # Stores the maximum difference
    max = 0

    # Store the previous occurence
    # of char c
    prev = 0

    for i in range(0, n):

        # Check if the current character
        # is c or not
        if (s[i] == c):

            # Stores the difference of
            # consecutive occurrences of c
            diff = i - prev

            # Update previous occurrence
            # of c with current occurence
            prev = i

            # Comparing diff with max
            if (diff > max):
                max = diff

    # If string doesn't contain c
    if (max == 0):
        return -1

    # Return max
    return max

# Driver Code
if __name__ == "__main__":

    S = "abdegb"
    ch = 'b'
    print(findK(S, ch))

# This code is contributed by rakeshsahni
```

## C#

```
using System.Collections.Generic;
using System;
class GFG
{

    // Function to find the minimum value
    // of K such that char c occurs in all
    // K sized substrings of string S
    public static int findK(string s, char c)
    {

        // Store the string length
        int n = s.Length;

        // Store difference of lengths
        // of segments of every two
        // consecutive occurrences of c
        int diff;

        // Stores the maximum difference
        int max = 0;

        // Store the previous occurence
        // of char c
        int prev = 0;

        for (int i = 0; i < n; i++) {

            // Check if the current character
            // is c or not
            if (s[i] == c) {

                // Stores the difference of
                // consecutive occurrences of c
                diff = i - prev;

                // Update previous occurrence
                // of c with current occurence
                prev = i;

                // Comparing diff with max
                if (diff > max) {
                    max = diff;
                }
            }
        }

        // If string doesn't contain c
        if (max == 0)
            return -1;

        // Return max
        return max;
    }

    // Driver Code
    public static void Main()
  {
        string S = "abdegb";
        char ch = 'b';
        Console.WriteLine(findK(S, ch));

    }
}

// This code is contributed by amreshkumar3.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the minimum value
// of K such that char c occurs in all
// K sized substrings of string S
function findK(s, c)
{

  // Store the string length
  let n = s.length;

  // Store difference of lengths
  // of segments of every two
  // consecutive occurrences of c
  let diff;

  // Stores the maximum difference
  let max = 0;

  // Store the previous occurence
  // of char c
  let prev = 0;

  for (let i = 0; i < n; i++) {
    // Check if the current character
    // is c or not
    if (s[i] == c) {
      // Stores the difference of
      // consecutive occurrences of c
      diff = i - prev;

      // Update previous occurrence
      // of c with current occurence
      prev = i;

      // Comparing diff with max
      if (diff > max) {
        max = diff;
      }
    }
  }

  // If string doesn't contain c
  if (max == 0) return -1;

  // Return max
  return max;
}

// Driver Code

let S = "abdegb";
let ch = "b";
document.write(findK(S, ch));

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)