# 可以由给定字符不重复构成的 K 长度单词

> 原文:[https://www . geesforgeks . org/k-length-words-可以由给定字符不重复构成的单词/](https://www.geeksforgeeks.org/k-length-words-that-can-be-formed-from-given-characters-without-repetition/)

给定一个整数 **k** 和一个由小写英文字母组成的字符串 **str** ，任务是在不允许重复的情况下，统计 **str** 的字符可以组成多少个 **k** 字符单词(有无意义)。
**举例:**

> **输入:** str = "cat "，k = 3
> **输出:** 6
> 必选词为“cat”“CTA”“act”“ATC”“TCA”“tac”。
> **输入:** str = "geeksforgeeks "，k = 3
> **输出:** 840

**进场:**统计 **str** 中不同字符的个数并存储在 **cnt** 中，现在的任务是将 **cnt** 字符中的 **k** 字符排列出来，即 **<sup>n</sup> P <sub>r</sub> = n！/(n–r)！**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the required count
int findPermutation(string str, int k)
{
    bool has[26] = { false };

    // To store the count of distinct characters in str
    int cnt = 0;

    // Traverse str character by character
    for (int i = 0; i < str.length(); i++) {

        // If current character is appearing
        // for the first time in str
        if (!has[str[i] - 'a']) {

            // Increment the distinct character count
            cnt++;

            // Update the appearance of the current character
            has[str[i] - 'a'] = true;
        }
    }

    long long int ans = 1;

    // Since P(n, r) = n! / (n - r)!
    for (int i = 2; i <= cnt; i++)
        ans *= i;

    for (int i = cnt - k; i > 1; i--)
        ans /= i;

    // Return the answer
    return ans;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    int k = 4;
    cout << findPermutation(str, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class solution
{
// Function to return the required count
static int findPermutation(String str, int k)
{
    boolean[] has = new boolean[26];
    Arrays.fill(has,false);

    // To store the count of distinct characters in str
    int cnt = 0;

    // Traverse str character by character
    for (int i = 0; i < str.length(); i++) {

        // If current character is appearing
        // for the first time in str
        if (!has[str.charAt(i) - 'a'])
        {

            // Increment the distinct character count
            cnt++;

            // Update the appearance of the current character
            has[str.charAt(i) - 'a'] = true;
        }
    }

    int ans = 1;

    // Since P(n, r) = n! / (n - r)!
    for (int i = 2; i <= cnt; i++)
        ans *= i;

    for (int i = cnt - k; i > 1; i--)
        ans /= i;

    // Return the answer
    return ans;
}

// Driver code
public static void main(String args[])
{
    String str = "geeksforgeeks";
    int k = 4;
    System.out.println(findPermutation(str, k));

}
}
// This code is contributed by
// Sanjit_prasad
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math as mt

# Function to return the required count
def findPermutation(string, k):

    has = [False for i in range(26)]

    # To store the count of distinct
    # characters in str
    cnt = 0

    # Traverse str character by character
    for i in range(len(string)):

        # If current character is appearing
        # for the first time in str
        if (has[ord(string[i]) - ord('a')] == False):

            # Increment the distinct
            # character count
            cnt += 1

            # Update the appearance of the
            # current character
            has[ord(string[i]) - ord('a')] = True

    ans = 1

    # Since P(n, r) = n! / (n - r)!
    for i in range(2, cnt + 1):
        ans *= i

    for i in range(cnt - k, 1, -1):
        ans //= i

    # Return the answer
    return ans

# Driver code
string = "geeksforgeeks"
k = 4
print(findPermutation(string, k))

# This code is contributed
# by Mohit kumar 29
```

## C#

```
// C# implementation of the approach

using System;

class solution
{
// Function to return the required count
static int findPermutation(string str, int k)
{
    bool []has = new bool[26];

    for (int i = 0; i < 26 ; i++)
        has[i] = false;

    // To store the count of distinct characters in str
    int cnt = 0;

    // Traverse str character by character
    for (int i = 0; i < str.Length; i++) {

        // If current character is appearing
        // for the first time in str
        if (!has[str[i] - 'a'])
        {

            // Increment the distinct character count
            cnt++;

            // Update the appearance of the current character
            has[str[i] - 'a'] = true;
        }
    }

    int ans = 1;

    // Since P(n, r) = n! / (n - r)!
    for (int i = 2; i <= cnt; i++)
        ans *= i;

    for (int i = cnt - k; i > 1; i--)
        ans /= i;

    // Return the answer
    return ans;
}

// Driver code
public static void Main()
{
    string str = "geeksforgeeks";
    int k = 4;
    Console.WriteLine(findPermutation(str, k));

}
// This code is contributed by Ryuga
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the required count
function findPermutation($str, $k)
{
    $has = array();

    for ($i = 0; $i < 26; $i++)
    {
        $has[$i]= false;
    }

    // To store the count of distinct characters in $str
    $cnt = 0;

    // Traverse $str character by character
    for ($i = 0; $i < strlen($str); $i++)
    {

        // If current character is appearing
        // for the first time in $str
        if ($has[ord($str[$i]) - ord('a')] == false)
        {

            // Increment the distinct character count
            $cnt++;

            // Update the appearance of the current character
            $has[ord($str[$i]) - ord('a')] = true;
        }
    }

    $ans = 1;

    // Since P(n, r) = n! / (n - r)!
    for ($i = 2; $i <= $cnt; $i++)
        $ans *= $i;

    for ($i = $cnt - $k; $i > 1; $i--)
        $ans /= $i;

    // Return the answer
    return $ans;
}

// Driver code
$str = "geeksforgeeks";
$k = 4;
echo findPermutation($str, $k);

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach
      // Function to return the required count
      function findPermutation(str, k) {
        var has = new Array(26);

        for (var i = 0; i < 26; i++) has[i] = false;

        // To store the count of distinct characters in str
        var cnt = 0;

        // Traverse str character by character
        for (var i = 0; i < str.length; i++) {
          // If current character is appearing
          // for the first time in str

          if (!has[str[i].charCodeAt(0) - "a".charCodeAt(0)]) {
            // Increment the distinct character count
            cnt++;

            // Update the appearance of the current character
            has[str[i].charCodeAt(0) - "a".charCodeAt(0)] = true;
          }
        }

        var ans = 1;

        // Since P(n, r) = n! / (n - r)!
        for (var i = 2; i <= cnt; i++) ans *= i;

        for (var i = cnt - k; i > 1; i--) ans /= i;

        // Return the answer
        return ans;
      }

      // Driver code
      var str = "geeksforgeeks";
      var k = 4;
      document.write(findPermutation(str, k));
    </script>
```

**Output:** 

```
840
```