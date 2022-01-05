# 检查在所有可能的“？”替换中，给定的二进制字符串中是否出现子字符串“10”带 1 或 0

> 原文:[https://www . geeksforgeeks . org/check-if-substring-10-in-给定二进制-string-in-all-replacements-with-1 或-0/](https://www.geeksforgeeks.org/check-if-substring-10-occurs-in-the-given-binary-string-in-all-possible-replacements-of-with-1-or-0/)

给定一个仅由**“0”**、**“1”**和**“？”组成的[弦](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S**** ，任务是检查在字符**“？”的每一个可能的替换中是否存在子串**“10”****带 **1** 或 **0** 。

**示例:**

> **输入:**S =“1？0"
> **输出:**是
> **解释:**
> 以下是“？”的所有可能替代项：
> 
> 1.  替换“？”用 0 将字符串修改为“100”。在修改字符串中，出现子字符串“10”。
> 2.  替换“？”用 1 将字符串修改为“110”。在修改字符串中，出现子字符串“10”。
> 
> 从以上所有可能的替换中，子字符串“10”出现在所有替换中，因此，打印“是”。
> 
> **输入:** S=？?"
> T3】输出:否

**方法:**给定的问题可以通过使用 [**贪婪方法**](https://www.geeksforgeeks.org/greedy-algorithms/) 来解决，该方法基于以下观察:如果字符串 **S** 包含许多连续的**“？”**，可以换成单个**'？'**最坏的情况下我们可以全部用 **1s** 或者 **0s** 代替。

因此，想法是通过替换连续的**“？”从给定的字符串 **S** 创建一个新的字符串**带单**“？”**然后检查是否存在**“10”**或**“1？0"** 作为子串，那么在所有可能的替换后就有可能得到 **"10"** 作为子串，因此，打印**是**。否则，打印**否**。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <iostream>
using namespace std;

// Function to check it possible to get
// "10" as substring after all possible
// replacements
string check(string S, int n)
{

  // Initialize empty string ans
  string ans = "";
  int c = 0;

  // Run loop n times
  for (int i = 0; i < n; i++) {

    // If char is "?", then increment
    // c by 1
    if (S[i] == '?') {
      c++;
    }
    else {

      // Continuous '?' characters
      if (c) {
        ans += "?";
      }
      c = 0;
      ans += S[i];
    }
  }

  // Their is no consecutive "?"
  if (c) {
    ans += "?";
  }

  // Check if "10" or "1?0" exists
  // in the string ans or not
  if (ans.find("10") != -1 || ans.find("1?0") != -1) {
    return "Yes";
  }
  else {
    return "No";
  }
}

// Driver code
int main()
{
  string S = "1?0";
  int n = S.size();
  string ans = check(S, n);
  cout << ans;
  return 0;
}
// This code is contributed by parthmanchanda81
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

 // Returns true if s1 is substring of s2
    static int isSubstring(String s1, String s2)
    {
        int M = s1.length();
        int N = s2.length();

        /* A loop to slide pat[] one by one */
        for (int i = 0; i <= N - M; i++) {
            int j;

            /* For current index i, check for
            pattern match */
            for (j = 0; j < M; j++)
                if (s2.charAt(i + j) != s1.charAt(j))
                    break;

            if (j == M)
                return i;
        }

        return -1;
    }

// Function to check it possible to get
// "10" as substring after all possible
// replacements
static String check(String S, int n)
{

  // Initialize empty string ans
  String ans = "";
  int c = 0;

  // Run loop n times
  for (int i = 0; i < n; i++) {

    // If char is "?", then increment
    // c by 1
    if (S.charAt(i) == '?') {
      c++;
    }
    else {

      // Continuous '?' characters
      if (c != 0) {
        ans += "?";
      }
      c = 0;
      ans += S.charAt(i);
    }
  }

  // Their is no consecutive "?"
  if (c != 0) {
    ans += "?";
  }

  // Check if "10" or "1?0" exists
  // in the string ans or not
  if (isSubstring("10", S) != -1 || isSubstring("1?0", S) != -1) {
    return "Yes";
  }
  else {
    return "No";
  }
}

// Driver Code
public static void main (String[] args)
{
    String S = "1?0";
        int n = S.length();
        String ans = check(S, n);
        System.out.println(ans);
}
}

// This code is contributed by avijitmondal1998.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to check it possible to get
# "10" as substring after all possible
# replacements
def check(S, n):

    # Initialize empty string ans
    ans = ""
    c = 0

    # Run loop n times
    for _ in range(n):

        # If char is "?", then increment
        # c by 1
        if S[_] == "?":
            c += 1
        else:

            # Continuous '?' characters
            if c:
                ans += "?"

            # Their is no consecutive "?"
            c = 0
            ans += S[_]

    # "?" still left
    if c:
        ans += "?"

    # Check if "10" or "1?0" exists
    # in the string ans or not
    if "10" in ans or "1?0" in ans:
        return "Yes"
    else:
        return "No"

# Driver Code
if __name__ == '__main__':

    S = "1?0"
    ans = check(S, len(S))
    print(ans)
```

## C#

```
// C# program for the approach
using System;
using System.Collections.Generic;

class GFG {

 // Returns true if s1 is substring of s2
    static int isSubstring(string s1, string s2)
    {
        int M = s1.Length;
        int N = s2.Length;

        /* A loop to slide pat[] one by one */
        for (int i = 0; i <= N - M; i++) {
            int j;

            /* For current index i, check for
            pattern match */
            for (j = 0; j < M; j++)
                if (s2[i + j] != s1[j])
                    break;

            if (j == M)
                return i;
        }

        return -1;
    }

// Function to check it possible to get
// "10" as substring after all possible
// replacements
static string check(string S, int n)
{

  // Initialize empty string ans
  string ans = "";
  int c = 0;

  // Run loop n times
  for (int i = 0; i < n; i++) {

    // If char is "?", then increment
    // c by 1
    if (S[i] == '?') {
      c++;
    }
    else {

      // Continuous '?' characters
      if (c != 0) {
        ans += "?";
      }
      c = 0;
      ans += S[i];
    }
  }

  // Their is no consecutive "?"
  if (c != 0) {
    ans += "?";
  }

  // Check if "10" or "1?0" exists
  // in the string ans or not
  if (isSubstring("10", S) != -1 || isSubstring("1?0", S) != -1) {
    return "Yes";
  }
  else {
    return "No";
  }
}

    // Driver Code
    public static void Main()
    {
        string S = "1?0";
        int n = S.Length;
        string ans = check(S, n);
        Console.Write(ans);
    }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
  <script>
        // JavaScript Program to implement
        // the above approach

        // Function to check it possible to get
        // "10" as substring after all possible
        // replacements
        function check(S, n) {

            // Initialize empty string ans
            ans = ""
            c = 0

            // Run loop n times
            for (let i = 0; i < n; i++) {

                // If char is "?", then increment
                // c by 1
                if (S[i] == "?")
                    c += 1
                else

                    // Continuous '?' characters
                    if (c != 0)
                        ans += "?"

                // Their is no consecutive "?"
                c = 0
                ans += S[i]

                // "?" still left
                if (c != 0)
                    ans += "?"
            }

            // Check if "10" or "1?0" exists
            // in the string ans or not

            if (ans.includes('10') || ans.includes('1?0'))
                return "Yes"
            else
                return "No"

        }

        // Driver Code
        S = "1?0"
        ans = check(S, S.length)
        document.write(ans)

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**注意:**同样的方法也可以用于子串“00”/“01”/“11”以及微小的改变。