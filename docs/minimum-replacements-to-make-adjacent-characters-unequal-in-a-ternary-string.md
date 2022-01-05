# 三进制字符串中相邻字符不相等的最小替换数

> 原文:[https://www . geeksforgeeks . org/最小替换使相邻字符在三进制字符串中不相等/](https://www.geeksforgeeks.org/minimum-replacements-to-make-adjacent-characters-unequal-in-a-ternary-string/)

给定一个由“0”、“1”和“2”组成的字符串。任务是找到最小数量的替换，使相邻字符不相等。
**例:**

> **输入:** s = "201220211"
> **输出:** 2
> 变化后的合成字符串为 201210210
> **输入:** s = "0120102"
> **输出:** 0

**方法:**以下问题可以用贪心法解决。我们可以贪婪地比较每一对相邻的。如果相邻的第 i <sup>位</sup>和第 i-1 <sup>位</sup>的字符对相同，则用不等于第 i-1 <sup>位</sup>和第 i+1 <sup>位</sup>索引的字符替换第 i <sup>位</sup>的字符。如果是最后一个相邻的对，只需用不等于 i-1 <sup>第</sup>个索引处的字符替换即可。
以下是上述方法的实施:

## C++

```
// C++ program to count the minimal
// replacements such that adjacent characters
// are unequal
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// minimal replacements
int countMinimalReplacements(string s)
{
    // Find the length of the string
    int n = s.length();

    int cnt = 0;

    // Iterate in the string
    for (int i = 1; i < n; i++) {

        // Check if adjacent is similar
        if (s[i] == s[i - 1]) {
            cnt += 1;

            // If not the last pair
            if (i != (n - 1)) {

                // Check for character which is
                // not same  in i+1 and i-1
                for (auto it : "012") {
                    if (it != s[i + 1] &&
                        it != s[i - 1]) {
                        s[i] = it;
                        break;
                    }
                }
            }

            else // Last pair
            {
                // Check for character which is
                // not same in i-1 index
                for (auto it : "012") {
                    if (it != s[i - 1]) {
                        s[i] = it;
                        break;
                    }
                }
            }
        }
    }

    return cnt;
}

// Driver Code
int main()
{
    string s = "201220211";
    cout << countMinimalReplacements(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the minimal
// replacements such that adjacent
// characters are unequal
class GFG
{

    static final int MAX = 26;

    // Function to count the number of
    // minimal replacements
    static int countMinimalReplacements(char[] s)
    {
        // Find the length of the String
        int n = s.length;

        int cnt = 0;

        // Iterate in the String
        for (int i = 1; i < n; i++)
        {

            // Check if adjacent is similar
            if (s[i] == s[i - 1])
            {
                cnt += 1;

                // If not the last pair
                if (i != (n - 1))
                {

                    // Check for character which is
                    // not same in i+1 and i-1
                    for (char it : "012".toCharArray())
                    {
                        if (it != s[i + 1]
                                && it != s[i - 1])
                        {
                            s[i] = it;
                            break;
                        }
                    }
                }
                else // Last pair
                {
                    // Check for character which is
                    // not same in i-1 index
                    for (char it : "012".toCharArray())
                    {
                        if (it != s[i - 1])
                        {
                            s[i] = it;
                            break;
                        }
                    }
                }
            }
        }
        return cnt;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s = "201220211";
        System.out.println(countMinimalReplacements(s.toCharArray()));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to count the minimal
# replacements such that adjacent
# characters are unequal

# Function to count the number of
# minimal replacements
def countMinimalReplacements(s):

    # Find the length of the string
    n = len(s)

    cnt = 0

    # Iterate in the string
    for i in range(1, n):

        # Check if adjacent is similar
        if (s[i] == s[i - 1]):
            cnt += 1;

            # If not the last pair
            if (i != (n - 1)):

                # Check for character which is
                # not same in i+1 and i-1
                s = list(s)
                for j in "012":
                    if (j != s[i + 1] and
                        j != s[i - 1]):
                        s[i] = j
                        break

                s = ''.join(s)

            # Last pair
            else:

                # Check for character which is
                # not same in i-1 index
                s = list(s)

                for k in "012":
                    if (k != s[i - 1]):
                        s[i] = k
                        break
                s = ''.join(s)

    return cnt

# Driver Code
if __name__ == '__main__':
    s = "201220211"
    print(countMinimalReplacements(s))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to count the minimal
// replacements such that adjacent
// characters are unequal
using System;

class GFG
{
    static readonly int MAX = 26;

    // Function to count the number of
    // minimal replacements
    static int countMinimalReplacements(char[] s)
    {
        // Find the length of the String
        int n = s.Length;

        int cnt = 0;

        // Iterate in the String
        for (int i = 1; i < n; i++)
        {

            // Check if adjacent is similar
            if (s[i] == s[i - 1])
            {
                cnt += 1;

                // If not the last pair
                if (i != (n - 1))
                {

                    // Check for character which is
                    // not same in i+1 and i-1
                    foreach (char it in "012".ToCharArray())
                    {
                        if (it != s[i + 1] &&
                            it != s[i - 1])
                        {
                            s[i] = it;
                            break;
                        }
                    }
                }
                else // Last pair
                {
                    // Check for character which is
                    // not same in i-1 index
                    foreach (char it in "012".ToCharArray())
                    {
                        if (it != s[i - 1])
                        {
                            s[i] = it;
                            break;
                        }
                    }
                }
            }
        }
        return cnt;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String s = "201220211";
        Console.WriteLine(countMinimalReplacements(s.ToCharArray()));
    }
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count the minimal
// replacements such that adjacent
// characters are unequal

// Function to count the number of
// minimal replacements
function countMinimalReplacements($s)
{
    // Find the length of the string
    $n = strlen($s);

    $cnt = 0;
    $str = "012";

    // Iterate in the string
    for ($i = 1; $i < $n; $i++)
    {

        // Check if adjacent is similar
        if ($s[$i] == $s[$i - 1])
        {
            $cnt += 1;

            // If not the last pair
            if ($i != ($n - 1))
            {

                // Check for character which is
                // not same in i+1 and i-1
                for ($it = 0 ; $it < strlen($str); $it++)
                {
                    if ($str[$it] != $s[$i + 1] &&
                        $str[$it] != $s[$i - 1])
                    {
                        $s[$i] = $str[$it];
                        break;
                    }
                }
            }

            else // Last pair
            {
                // Check for character which is
                // not same in i-1 index
                for ($it = 0 ; $it< strlen($str); $it++)
                {
                    if ($str[$it] != $s[$i - 1])
                    {
                        $s[$i] = $str[$it];
                        break;
                    }
                }
            }
        }
    }

    return $cnt;
}

// Driver Code
$s = "201220211";
echo countMinimalReplacements($s);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
      // JavaScript program to count the minimal
      // replacements such that adjacent
      // characters are unequal

      // Function to count the number of
      // minimal replacements
      function countMinimalReplacements(s) {
        // Find the length of the string
        var n = s.length;

        var cnt = 0;
        var str = "012";

        // Iterate in the string
        for (var i = 1; i < n; i++) {
          // Check if adjacent is similar
          if (s[i] === s[i - 1]) {
            cnt += 1;

            // If not the last pair
            if (i !== n - 1) {
              // Check for character which is
              // not same in i+1 and i-1
              for (var it = 0; it < str.length; it++) {
                if (str[it] !== s[i + 1] && str[it] !== s[i - 1]) {
                  s[i] = str[it];
                  break;
                }
              }
            } // Last pair
            else {
              // Check for character which is
              // not same in i-1 index
              for (var it = 0; it < str.length; it++) {
                if (str[it] !== s[i - 1]) {
                  s[i] = str[it];
                  break;
                }
              }
            }
          }
        }

        return cnt;
      }

      // Driver Code
      var s = "201220211";
      document.write(countMinimalReplacements(s));
    </script>
```

**Output:** 

```
2
```

**时间复杂度:** O(n)