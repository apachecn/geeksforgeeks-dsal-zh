# 执行给定操作后包含所有小写字母的子字符串

> 原文:[https://www . geesforgeks . org/sub-string-包含执行给定操作后的所有小写字母/](https://www.geeksforgeeks.org/sub-string-that-contains-all-lowercase-alphabets-after-performing-the-given-operation/)

给定一个包含小写字母和字符**“？”的字符串**。任务是检查是否有可能让**串** **变好**。
如果一个字符串包含长度为 **26** 的子字符串，其中包含小写字母的每个字符，则该字符串被称为 **good** 。
任务是检查是否可以通过更换**“？”**任何小写字母的字符。如果可能，则打印修改后的字符串，否则打印 **-1** 。
**例:****** 

> ****输入:** str = "abcdefghijkl？nopqrstuvwxy？”
> **输出:**abcdefghijklmnopqrstuvwxyz
> 替换第一个“？”第一个是 m，第二个是 z。
> **输入:**str = " abcdefghijklmnopqrstuvwxyz？？？？？?"
> **输出:**abcdefghijklmnopqrstuvwxyzaaaaa
> 给定的字符串已经有一个包含所有 26 个小写字母的子字符串。**

****方法:**如果字符串长度小于 26，则打印 **-1** 。任务是生成一个长度为 26 的子字符串，其中包含所有小写字符。因此，最简单的方法是迭代长度为 26 的所有子串，然后对每个子串计算每个字母的出现次数，忽略问号。之后，如果存在出现两次或更多次的字符，那么这个子字符串不能包含字母表中的所有字母，我们处理下一个子字符串。否则，我们可以用子串中没有出现的字母填充问号，得到一个长度为 26 的子串，包含字母表中的所有字母。
以下是上述方法的实施:** 

## **C++**

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if every
// lowercase character appears atmost once
bool valid(int cnt[])
{
    // every character frequency must be not
    // greater than one
    for (int i = 0; i < 26; i++) {
        if (cnt[i] >= 2)
            return false;
    }

    return true;
}

// Function that returns the modified
// good string if possible
string getGoodString(string s, int n)
{
    // If the length of the string is less than n
    if (n < 26)
        return "-1";

    // Sub-strings of length 26
    for (int i = 25; i < n; i++) {

        // To store frequency of each character
        int cnt[26] = { 0 };

        // Get the frequency of each character
        // in the current sub-string
        for (int j = i; j >= i - 25; j--) {
            cnt[s[j] - 'a']++;
        }

        // Check if we can get sub-string containing all
        // the 26 characters
        if (valid(cnt)) {

            // Find which character is missing
            int cur = 0;
            while (cnt[cur] > 0)
                cur++;

            for (int j = i - 25; j <= i; j++) {

                // Fill with missing characters
                if (s[j] == '?') {
                    s[j] = cur + 'a';
                    cur++;

                    // Find the next missing character
                    while (cnt[cur] > 0)
                        cur++;
                }
            }

            // Return the modified good string
            return s;
        }
    }

    return "-1";
}

// Driver code
int main()
{
    string s = "abcdefghijkl?nopqrstuvwxy?";
    int n = s.length();

    cout << getGoodString(s, n);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function that returns true if every
// lowercase character appears atmost once
static boolean valid(int []cnt)
{
    // every character frequency must be not
    // greater than one
    for (int i = 0; i < 26; i++)
    {
        if (cnt[i] >= 2)
            return false;
    }

    return true;
}

// Function that returns the modified
// good string if possible
static String getGoodString(String ss, int n)
{
    char[] s=ss.toCharArray();

    // If the length of the string is less than n
    if (n < 26)
        return "-1";

    // To store frequency of each character
        int[] cnt = new int[27];

    // Sub-strings of length 26
    for (int i = 25; i < n; i++)
    {

        // Get the frequency of each character
        // in the current sub-string
        for (int j = i; j >= i - 25; j--)
        {
            if (s[j] != '?')
            cnt[((int)s[j] - (int)'a')]++;
        }

        // Check if we can get sub-string containing all
        // the 26 characters
        if (valid(cnt))
        {

            // Find which character is missing
            int cur = 0;
            while (cnt[cur] > 0)
                cur++;

            for (int j = i - 25; j <= i; j++)
            {

                // Fill with missing characters
                if (s[j] == '?')
                {
                    s[j] = (char)(cur + (int)('a'));
                    cur++;

                    // Find the next missing character
                    while (cnt[cur] > 0)
                        cur++;
                }
            }

            // Return the modified good string
            return new String(s);
        }
    }

    return "-1";
}

// Driver code
public static void main (String[] args)
{
    String s = "abcdefghijkl?nopqrstuvwxy?";
    int n = s.length();

    System.out.println(getGoodString(s, n));
}
}

// This code is contributed by chandan_jnu
```

## **蟒蛇 3**

```
# Python3 implementation of the approach

# Function that returns true if every
# lowercase character appears atmost once
def valid(cnt):

    # Every character frequency must
    # be not greater than one
    for i in range(0, 26):
        if cnt[i] >= 2:
            return False

    return True

# Function that returns the modified
# good string if possible
def getGoodString(s, n):

    # If the length of the string is
    # less than n
    if n < 26:
        return "-1"

    # Sub-strings of length 26
    for i in range(25, n):

        # To store frequency of each character
        cnt = [0] * 26

        # Get the frequency of each character
        # in the current sub-string
        for j in range(i, i - 26, -1):
            if s[j] != '?':
                cnt[ord(s[j]) - ord('a')] += 1

        # Check if we can get sub-string
        # containing the 26 characters all
        if valid(cnt):

            # Find which character is missing
            cur = 0
            while cur < 26 and cnt[cur] > 0:
                cur += 1

            for j in range(i - 25, i + 1):

                # Fill with missing characters
                if s[j] == '?':
                    s[j] = chr(cur + ord('a'))
                    cur += 1

                    # Find the next missing character
                    while cur < 26 and cnt[cur] > 0:
                        cur += 1

            # Return the modified good string
            return ''.join(s)

    return "-1"

# Driver code
if __name__ == "__main__":

    s = "abcdefghijkl?nopqrstuvwxy?"
    n = len(s)

    print(getGoodString(list(s), n))

# This code is contributed by Rituraj Jain
```

## **C#**

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true if every
// lowercase character appears atmost once
static bool valid(int []cnt)
{
    // every character frequency must be not
    // greater than one
    for (int i = 0; i < 26; i++)
    {
        if (cnt[i] >= 2)
            return false;
    }

    return true;
}

// Function that returns the modified
// good string if possible
static string getGoodString(string ss, int n)
{
    char[] s = ss.ToCharArray();

    // If the length of the string is less than n
    if (n < 26)
        return "-1";

    // To store frequency of each character
        int[] cnt = new int[27];

    // Sub-strings of length 26
    for (int i = 25; i < n; i++)
    {

        // Get the frequency of each character
        // in the current sub-string
        for (int j = i; j >= i - 25; j--)
        {
            if (s[j] != '?')
            cnt[((int)s[j] - (int)'a')]++;
        }

        // Check if we can get sub-string containing all
        // the 26 characters
        if (valid(cnt))
        {

            // Find which character is missing
            int cur = 0;
            while (cnt[cur] > 0)
                cur++;

            for (int j = i - 25; j <= i; j++)
            {

                // Fill with missing characters
                if (s[j] == '?')
                {
                    s[j] = (char)(cur + (int)('a'));
                    cur++;

                    // Find the next missing character
                    while (cnt[cur] > 0)
                        cur++;
                }
            }

            // Return the modified good string
            return new String(s);
        }
    }

    return "-1";
}

// Driver code
static void Main()
{
    string s = "abcdefghijkl?nopqrstuvwxy?";
    int n = s.Length;

    Console.WriteLine(getGoodString(s, n));
}
}

// This code is contributed by chandan_jnu
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP implementation of the approach

// Function that returns true if every
// lowercase character appears atmost once
function valid(&$cnt)
{
    // every character frequency must
    // be not greater than one
    for ($i = 0; $i < 26; $i++)
    {
        if ($cnt[$i] >= 2)
            return false;
    }

    return true;
}

// Function that returns the modified
// good string if possible
function getGoodString($s, $n)
{
    // If the length of the string is
    // less than n
    if ($n < 26)
        return "-1";

    // Sub-strings of length 26
    for ($i = 25; $i < $n; $i++)
    {

        // To store frequency of each character
        $cnt = array_fill(0, 26, NULL);

        // Get the frequency of each character
        // in the current sub-string
        for ($j = $i; $j >= $i - 25; $j--)
        {
            if ($s[$j] != '?')
            $cnt[ord($s[$j]) - ord('a')]++;
        }

        // Check if we can get sub-string
        // containing all the 26 characters
        if (valid($cnt))
        {

            // Find which character is missing
            $cur = 0;
            while ($cur < 26 && $cnt[$cur] > 0)
                $cur++;

            for ($j = $i - 25; $j <= $i; $j++)
            {

                // Fill with missing characters
                if ($s[$j] == '?')
                {
                    $s[$j] = chr($cur + ord('a'));
                    $cur++;

                    // Find the next missing character
                    while ($cur < 26 && $cnt[$cur] > 0)
                        $cur++;
                }
            }

            // Return the modified good string
            return $s;
        }
    }

    return "-1";
}

// Driver code
$s = "abcdefghijkl?nopqrstuvwxy?";
$n = strlen($s);
echo getGoodString($s, $n);

// This code is contributed by ita_c
?>
```

## **java 描述语言**

```
<script>
      // JavaScript implementation of the approach
      // Function that returns true if every
      // lowercase character appears atmost once
      function valid(cnt) {
        // every character frequency must be not
        // greater than one
        for (var i = 0; i < 26; i++) {
          if (cnt[i] >= 2) return false;
        }

        return true;
      }

      // Function that returns the modified
      // good string if possible
      function getGoodString(ss, n) {
        var s = ss.split("");
        // If the length of the string is less than n
        if (n < 26) return "-1";

        // Sub-strings of length 26
        for (var i = 25; i < n; i++) {
          // To store frequency of each character
          var cnt = new Array(26).fill(0);

          // Get the frequency of each character
          // in the current sub-string
          for (var j = i; j >= i - 25; j--) {
            cnt[s[j].charCodeAt(0) - "a".charCodeAt(0)]++;
          }

          // Check if we can get sub-string containing all
          // the 26 characters
          if (valid(cnt)) {
            // Find which character is missing
            var cur = 0;
            while (cnt[cur] > 0) cur++;

            for (var j = i - 25; j <= i; j++) {
              // Fill with missing characters
              if (s[j] === "?") {
                s[j] = String.fromCharCode(cur + "a".charCodeAt(0));
                cur++;

                // Find the next missing character
                while (cnt[cur] > 0) cur++;
              }
            }

            // Return the modified good string
            return s.join("");
          }
        }

        return "-1";
      }

      // Driver code
      var s = "abcdefghijkl?nopqrstuvwxy?";
      var n = s.length;
      document.write(getGoodString(s, n));
    </script>
```

****Output:** 

```
abcdefghijklmnopqrstuvwxyz
```**