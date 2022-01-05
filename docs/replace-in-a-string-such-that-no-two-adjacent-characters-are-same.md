# 替换“？”字符串中没有两个相邻字符相同

> 原文:[https://www . geeksforgeeks . org/替换字符串中没有两个相邻字符相同/](https://www.geeksforgeeks.org/replace-in-a-string-such-that-no-two-adjacent-characters-are-same/)

给定一根长度为 **N** 的绳子 **S** ，由**组成**和小写字母，任务是替换**“？”**用小写字母，这样没有相邻的字符是相同的。如果存在多个可能的组合，请打印其中任何一个。

**示例:**

> **输入:** S =？a？一个“
> **输出:**巴巴
> **解释:**
> 替换所有“？”带有“b”的 s 将字符串修改为“baba”。
> 由于“粑粑”中没有相邻的字符相同，所以打印字符串作为答案。
> 
> **输入:** S =？？?"
> **输出:** aca
> **解释:**
> 替换第一个“？”带 a。
> 替换第二个“？”带 c。
> 替换第三个“？”带 a。现在，修改后的字符串是“aca”。
> 因此，“ca”中没有相同的相邻字符。

**天真方法:**最简单的方法是尝试[生成由小写字母组成的给定字符串](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)的所有可能排列。可以有**26<sup>N</sup>T7】弦。在每个字符串中，检查相邻字符是否匹配，给定字符串中的所有小写字符是否匹配所选的字符串排列。**

***时间复杂度:** O(N*26 <sup>N</sup> ，其中 N 为给定字符串的长度。*
***辅助空间:** O(N)*

**高效途径:**优化上述途径，思路是替换每一个**“？”**通过字符**‘a’**检查该字符是否等于相邻字符。如果它等于相邻字符，则递增当前字符。以下是步骤:

1.  如果字符串的第一个字符是**“？”**然后用**‘a’**替换它，如果它等于下一个字符，则将当前字符增加 1
2.  在范围**【1，N–1】**内使用变量 **i** 遍历给定的字符串，如果当前字符是**“？”**并执行以下操作:
    *   将索引 **i** 处的字符更新为 s[i] = **'a'** 。
    *   现在，如果索引 **i** 和**(I–1)**处的字符相同，那么将当前字符增加 **1** 。
    *   现在，如果索引 **i** 和 **(i + 1)** 处的字符相同，那么将当前字符增加 **1** 。
    *   现在，如果索引 **i** 和**(I–1)**处的字符再次相同，那么将当前字符增加 **1** 。该步骤是强制性的，因为在上述步骤中增加字符后，索引 **i** 和**(I–1)**处的字符可能是相同的。
3.  如果字符串的最后一个字符是**'？'**然后用**‘a’**替换，如果它等于前一个字符，则最后一个字符增加 1
4.  完成上述步骤后打印字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include "bits/stdc++.h"
using namespace std;

// Function that replace all '?' with
// lowercase alphabets such that each
// adjacent character is different
string changeString(string S)
{
    // Store the given string
    string s = S;

    int N = (int)s.length();

    // If the first character is '?'
    if (s[0] == '?') {
        s[0] = 'a';
        if (s[0] == s[1]) {
            s[0]++;
        }
    }

    // Traverse the string [1, N - 1]
    for (int i = 1; i < N - 1; i++) {

        // If the current character is '?'
        if (s[i] == '?') {

            // Change the character
            s[i] = 'a';

            // Check equality with
            // the previous character
            if (s[i] == s[i - 1]) {
                s[i]++;
            }

            // Check equality with
            // the next character
            if (s[i] == s[i + 1]) {
                s[i]++;
            }

            // Check equality with
            // the previous character
            if (s[i] == s[i - 1]) {
                s[i]++;
            }
        }
    }

    // If the last character is '?'
    if (s[N - 1] == '?') {

        // Change character
        s[N - 1] = 'a';

        // Check with previous character
        if (s[N - 1] == s[N - 2]) {
            s[N - 1]++;
        }
    }

    // Return the resultant string
    return s;
}

// Driver Code
int main()
{
    // Given string S
    string S = "?a?a";

    // Function Call
    cout << changeString(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
class GFG{

// Function that replace all '?' with
// lowercase alphabets such that each
// adjacent character is different
static String changeString(String S)
{
  // Store the given String
  char []s = S.toCharArray();

  int N = (int)S.length();

  // If the first character is '?'
  if (s[0] == '?')
  {
    s[0] = 'a';
    if (s[0] == s[1])
    {
      s[0]++;
    }
  }

  // Traverse the String [1, N - 1]
  for (int i = 1; i < N - 1; i++)
  {
    // If the current
    // character is '?'
    if (s[i] == '?')
    {
      // Change the character
      s[i] = 'a';

      // Check equality with
      // the previous character
      if (s[i] == s[i - 1])
      {
        s[i]++;
      }

      // Check equality with
      // the next character
      if (s[i] == s[i + 1])
      {
        s[i]++;
      }

      // Check equality with
      // the previous character
      if (s[i] == s[i - 1])
      {
        s[i]++;
      }
    }
  }

  // If the last character is '?'
  if (s[N - 1] == '?')
  {
    // Change character
    s[N - 1] = 'a';

    // Check with previous
    // character
    if (s[N - 1] == s[N - 2])
    {
      s[N - 1]++;
    }
  }

  String ans = "";

  for(int  i = 0; i < s.length; i++)
  {
    ans += s[i];
  }

  // Return the resultant String
  return ans;
}

// Driver Code
public static void main(String[] args)
{
  // Given String S
  String S = "?a?a";

  // Function Call
  System.out.print(changeString(S));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function that replace all '?' with
# lowercase alphabets such that each
# adjacent character is different
def changeString(S):

    # Store the given String
    N = len(S)
    s = [' '] * (len(S))

    for i in range(len(S)):
        s[i] = S[i]

    # If the first character is '?'
    if (s[0] == '?'):
        s[0] = 'a'

        if (s[0] == s[1]):
            s[0] = chr(ord(s[0]) + 1)

    # Traverse the String [1, N - 1]
    for i in range(1, N - 1):

        # If the current
        # character is '?'
        if (s[i] == '?'):

            # Change the character
            s[i] = 'a'

            # Check equality with
            # the previous character
            if (s[i] == s[i - 1]):
                s[i] =  chr(ord(s[i]) + 1)

            # Check equality with
            # the next character
            if (s[i] == s[i + 1]):
                s[i] =  chr(ord(s[i]) + 1)

            # Check equality with
            # the previous character
            if (s[i] == s[i - 1]):
                s[i] =  chr(ord(s[i]) + 1)

    # If the last character is '?'
    if (s[N - 1] == '?'):

        # Change character
        s[N - 1] = 'a'

        # Check with previous
        # character
        if (s[N - 1] == s[N - 2]):
            s[N - 1] += 1

    ans = ""
    for i in range(len(s)):
        ans += s[i]

    # Return the resultant String
    return ans

# Driver Code
if __name__ == '__main__':

    # Given String S
    S = "?a?a"

    # Function Call
    print(changeString(S))

# This code is contributed by gauravrajput1
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function that replace all '?' with
// lowercase alphabets such that each
// adjacent character is different
static string changeString(string S)
{

  // Store the given String
  char []s = S.ToCharArray();

  int N = S.Length;

  // If the first character is '?'
  if (s[0] == '?')
  {
    s[0] = 'a';
    if (s[0] == s[1])
    {
      s[0]++;
    }
  }

  // Traverse the String [1, N - 1]
  for(int i = 1; i < N - 1; i++)
  {

    // If the current
    // character is '?'
    if (s[i] == '?')
    {

      // Change the character
      s[i] = 'a';

      // Check equality with
      // the previous character
      if (s[i] == s[i - 1])
      {
        s[i]++;
      }

      // Check equality with
      // the next character
      if (s[i] == s[i + 1])
      {
        s[i]++;
      }

      // Check equality with
      // the previous character
      if (s[i] == s[i - 1])
      {
        s[i]++;
      }
    }
  }

  // If the last character is '?'
  if (s[N - 1] == '?')
  {

    // Change character
    s[N - 1] = 'a';

    // Check with previous
    // character
    if (s[N - 1] == s[N - 2])
    {
      s[N - 1]++;
    }
  }

  string ans = "";

  for(int  i = 0; i < s.Length; i++)
  {
    ans += s[i];
  }

  // Return the resultant String
  return ans;
}

// Driver Code
public static void Main()
{

  // Given String S
  string S = "?a?a";

  // Function Call
  Console.WriteLine(changeString(S));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// Javascript program for
// the above approach

// Function that replace all '?' with
// lowercase alphabets such that each
// adjacent character is different
function changeString(S)
{
    // Store the given String
  let s = S.split("");

  let N = S.length;

  // If the first character is '?'
  if (s[0] == '?')
  {
    s[0] = 'a';
    if (s[0] == s[1])
    {
      s[0] = String.fromCharCode(s[0].charCodeAt(0)+1);
    }
  }

  // Traverse the String [1, N - 1]
  for (let i = 1; i < N - 1; i++)
  {
    // If the current
    // character is '?'
    if (s[i] == '?')
    {
      // Change the character
      s[i] = 'a';

      // Check equality with
      // the previous character
      if (s[i] == s[i - 1])
      {
        s[i] = String.fromCharCode(s[i].charCodeAt(0)+1);
      }

      // Check equality with
      // the next character
      if (s[i] == s[i + 1])
      {
        s[i] = String.fromCharCode(s[i].charCodeAt(0)+1);
      }

      // Check equality with
      // the previous character
      if (s[i] == s[i - 1])
      {
        s[i]=String.fromCharCode(s[i].charCodeAt(0)+1);
      }
    }
  }

  // If the last character is '?'
  if (s[N - 1] == '?')
  {
    // Change character
    s[N - 1] = 'a';

    // Check with previous
    // character
    if (s[N - 1] == s[N - 2])
    {
      s[N - 1]++;
    }
  }

  let ans = "";

  for(let  i = 0; i < s.length; i++)
  {
    ans += s[i];
  }

  // Return the resultant String
  return ans;
}

// Driver Code
// Given String S
let S = "?a?a";

// Function Call
document.write(changeString(S));

// This code is contributed by patel2127
</script>
```

**Output**

```
baba
```

***时间复杂度:** O(N)，其中 N 是给定字符串的长度。*
***辅助空间:** O(N)*