# 形成字典上最小的字符串，最小替换数等于 0、1 和 2s

> 原文:[https://www . geeksforgeeks . org/form-按字典顺序排列-最小替换字符串-具有相等数量的 0-1-和-2s/](https://www.geeksforgeeks.org/form-lexicographically-smallest-string-with-minimum-replacements-having-equal-number-of-0s-1s-and-2s/)

给定长度为 **n** 的字符串**字符串**(n 是 3 的倍数)，仅包含集合 **{0，1，2}** 中的字符。任务是更新字符串，使每个字符以最少的操作次数具有相同的频率。在一次操作中，字符串中的任何字符都可以被任何其他字符(也来自同一个集合)替换。如果有多个可能的字符串，那么打印字典最小的一个。
**举例:**

> **输入:** str = "000000"
> **输出:** 001122
> 将第 3 <sup>rd</sup> 和第 4<sup>th</sup>0’替换为“1”并将第 5 <sup>th</sup> 和第 6<sup>th</sup>0’替换为“2”，从而满足给定的条件，并形成字典上最小的字符串
> **输入:**str = " 211111

**方法:**这个问题可以用贪婪的方法解决。我们只需要 **n / 3** 每种类型的字符数，其中 **n** 是字符串的大小。迭代字符串并计算每种类型的字符数。再次，遍历字符串，现在检查当前字符的计数是否等于 **n / 3** ，则不需要对当前字符执行任何操作。
但是如果**计数(currentChar)！= n / 3** 然后，我们可能需要根据字符的值执行替换操作，以保持最小的字典顺序，如下所示:

*   如果当前字符是零(0)，并且我们已经处理了所需数量的零，那么如果**计数为【1】<(n/3)**则需要用一(1)替换该字符，或者如果**计数为【2】<(n/3)**则需要用两(1)替换该字符。
*   如果当前字符是一(1)，那么如果**计数为【0】<(n/3)**则我们可以用零(0)替换它，或者如果**计数为【2】<(n/3)**则我们可以用两(2)替换它，并且我们已经处理了所需数量的 1 以保持最低的词典顺序
*   如果当前字符是两(2)，那么如果**计数为【0】<(n/3)**我们可以用零(0)替换它，或者如果**计数为【2】<(n/3)**我们可以用两(2)替换它。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns the modified lexicographically
// smallest string after performing minimum number
// of given operations
string formStringMinOperations(string s)
{
    // Stores the initial frequencies of characters
    // 0s, 1s and 2s
    int count[3] = { 0 };
    for (auto& c : s)
        count++;

    // Stores number of processed characters upto that
    // point of each type
    int processed[3] = { 0 };

    // Required number of characters of each type
    int reqd = (int)s.size() / 3;
    for (int i = 0; i < s.size(); i++) {

        // If the current type has already reqd
        // number of characters, no need to perform
        // any operation
        if (count[s[i] - '0'] == reqd)
            continue;

        // Process all 3 cases
        if (s[i] == '0' && count[0] > reqd &&
                     processed[0] >= reqd) {

            // Check for 1 first
            if (count[1] < reqd) {
                s[i] = '1';
                count[1]++;
                count[0]--;
            }

            // Else 2
            else if (count[2] < reqd) {
                s[i] = '2';
                count[2]++;
                count[0]--;
            }
        }

        // Here we need to check processed[1] only
        // for 2 since 0 is less than 1 and we can
        // replace it anytime
        if (s[i] == '1' && count[1] > reqd) {
            if (count[0] < reqd) {
                s[i] = '0';
                count[0]++;
                count[1]--;
            }
            else if (count[2] < reqd &&
                    processed[1] >= reqd) {
                s[i] = '2';
                count[2]++;
                count[1]--;
            }
        }

        // Here we can replace 2 with 0 and 1 anytime
        if (s[i] == '2' && count[2] > reqd) {
            if (count[0] < reqd) {
                s[i] = '0';
                count[0]++;
                count[2]--;
            }
            else if (count[1] < reqd) {
                s[i] = '1';
                count[1]++;
                count[2]--;
            }
        }

        // keep count of processed characters of each
        // type
        processed[s[i] - '0']++;
    }
    return s;
}

// Driver Code
int main()
{
    string s = "011200";
    cout << formStringMinOperations(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function that returns the
    // modified lexicographically
    // smallest String after
    // performing minimum number
    // of given operations
    static String formStringMinOperations(char[] s)
    {

        // Stores the initial frequencies
        // of characters 0s, 1s and 2s
        int count[] = new int[3];
        for (char c : s)
        {
            count[(int)c - 48] += 1;
        }

        // Stores number of processed characters
        // upto that point of each type
        int processed[] = new int[3];

        // Required number of characters of each type
        int reqd = (int) s.length / 3;
        for (int i = 0; i < s.length; i++)
        {

            // If the current type has already
            // reqd number of characters, no
            // need to perform any operation
            if (count[s[i] - '0'] == reqd)
            {
                continue;
            }

            // Process all 3 cases
            if (s[i] == '0' && count[0] > reqd
                    && processed[0] >= reqd)
            {

                // Check for 1 first
                if (count[1] < reqd)
                {
                    s[i] = '1';
                    count[1]++;
                    count[0]--;
                }

                // Else 2
                else if (count[2] < reqd)
                {
                    s[i] = '2';
                    count[2]++;
                    count[0]--;
                }
            }

            // Here we need to check processed[1] only
            // for 2 since 0 is less than 1 and we can
            // replace it anytime
            if (s[i] == '1' && count[1] > reqd)
            {
                if (count[0] < reqd)
                {
                    s[i] = '0';
                    count[0]++;
                    count[1]--;
                }
                else if (count[2] < reqd
                        && processed[1] >= reqd)
                {
                    s[i] = '2';
                    count[2]++;
                    count[1]--;
                }
            }

            // Here we can replace 2 with 0 and 1 anytime
            if (s[i] == '2' && count[2] > reqd)
            {
                if (count[0] < reqd)
                {
                    s[i] = '0';
                    count[0]++;
                    count[2]--;
                }
                else if (count[1] < reqd)
                {
                    s[i] = '1';
                    count[1]++;
                    count[2]--;
                }
            }

            // keep count of processed
            // characters of each type
            processed[s[i] - '0']++;
        }
        return String.valueOf(s);
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s = "011200";
        System.out.println(formStringMinOperations(s.toCharArray()));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math

# Function that returns the modified
# lexicographically smallest string after
# performing minimum number of given operations
def formStringMinOperations(ss):

    # Stores the initial frequencies of
    # characters 0s, 1s and 2s
    count = [0] * 3;
    s = list(ss);
    for i in range(len(s)):
        count[ord(s[i]) - ord('0')] += 1;

    # Stores number of processed characters
    # upto that point of each type
    processed = [0] * 3;

    # Required number of characters of each type
    reqd = math.floor(len(s) / 3);
    for i in range(len(s)):

        # If the current type has already reqd
        # number of characters, no need to
        # perform any operation
        if (count[ord(s[i]) - ord('0')] == reqd):
            continue;

        # Process all 3 cases
        if (s[i] == '0' and count[0] > reqd and
                            processed[0] >= reqd):

            # Check for 1 first
            if (count[1] < reqd):
                s[i] = '1';
                count[1] += 1;
                count[0] -= 1;

            # Else 2
            elif (count[2] < reqd):
                s[i] = '2';
                count[2] += 1;
                count[0] -= 1;

        # Here we need to check processed[1] only
        # for 2 since 0 is less than 1 and we can
        # replace it anytime
        if (s[i] == '1' and count[1] > reqd):
            if (count[0] < reqd):
                s[i] = '0';
                count[0] += 1;
                count[1] -= 1;
            elif (count[2] < reqd and
                  processed[1] >= reqd):
                s[i] = '2';
                count[2] += 1;
                count[1] -= 1;

        # Here we can replace 2 with 0 and 1 anytime
        if (s[i] == '2' and count[2] > reqd):
            if (count[0] < reqd):
                s[i] = '0';
                count[0] += 1;
                count[2] -= 1;
            elif (count[1] < reqd):
                s[i] = '1';
                count[1] += 1;
                count[2] -= 1;

        # keep count of processed characters
        # of each type
        processed[ord(s[i]) - ord('0')] += 1;
    return ''.join(s);

# Driver Code
s = "011200";
print(formStringMinOperations(s));

# This code is contributed by mits
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns the
    // modified lexicographically
    // smallest String after
    // performing minimum number
    // of given operations
    static String formStringMinOperations(char[] s)
    {

        // Stores the initial frequencies
        // of characters 0s, 1s and 2s
        int []count = new int[3];
        foreach (char c in s)
        {
            count[(int)c - 48] += 1;
        }

        // Stores number of processed characters
        // upto that point of each type
        int []processed = new int[3];

        // Required number of characters of each type
        int reqd = (int) s.Length / 3;
        for (int i = 0; i < s.Length; i++)
        {

            // If the current type has already
            // reqd number of characters, no
            // need to perform any operation
            if (count[s[i] - '0'] == reqd)
            {
                continue;
            }

            // Process all 3 cases
            if (s[i] == '0' && count[0] > reqd
                    && processed[0] >= reqd)
            {

                // Check for 1 first
                if (count[1] < reqd)
                {
                    s[i] = '1';
                    count[1]++;
                    count[0]--;
                }

                // Else 2
                else if (count[2] < reqd)
                {
                    s[i] = '2';
                    count[2]++;
                    count[0]--;
                }
            }

            // Here we need to check processed[1] only
            // for 2 since 0 is less than 1 and we can
            // replace it anytime
            if (s[i] == '1' && count[1] > reqd)
            {
                if (count[0] < reqd)
                {
                    s[i] = '0';
                    count[0]++;
                    count[1]--;
                }
                else if (count[2] < reqd
                        && processed[1] >= reqd)
                {
                    s[i] = '2';
                    count[2]++;
                    count[1]--;
                }
            }

            // Here we can replace 2 with 0 and 1 anytime
            if (s[i] == '2' && count[2] > reqd)
            {
                if (count[0] < reqd)
                {
                    s[i] = '0';
                    count[0]++;
                    count[2]--;
                }
                else if (count[1] < reqd)
                {
                    s[i] = '1';
                    count[1]++;
                    count[2]--;
                }
            }

            // keep count of processed
            // characters of each type
            processed[s[i] - '0']++;
        }
        return String.Join("",s);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String s = "011200";
        Console.WriteLine(formStringMinOperations(s.ToCharArray()));
    }
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns the modified lexicographically
// smallest string after performing minimum number
// of given operations
function formStringMinOperations($s)
{
    // Stores the initial frequencies of
    // characters 0s, 1s and 2s
    $count = array_fill(0, 3, 0);

    for ($i = 0; $i < strlen($s) ; $i++)
        $count[$s[$i] - '0']++;

    // Stores number of processed characters
    // upto that point of each type
    $processed = array_fill(0, 3, 0);

    // Required number of characters of each type
    $reqd = floor(strlen($s) / 3);
    for ($i = 0; $i < strlen($s); $i++)
    {

        // If the current type has already reqd
        // number of characters, no need to
        // perform any operation
        if ($count[$s[$i] - '0'] == $reqd)
            continue;

        // Process all 3 cases
        if ($s[$i] == '0' && $count[0] > $reqd &&
                             $processed[0] >= $reqd)
        {

            // Check for 1 first
            if ($count[1] < $reqd)
            {
                $s[$i] = '1';
                $count[1]++;
                $count[0]--;
            }

            // Else 2
            else if ($count[2] < $reqd)
            {
                $s[$i] = '2';
                $count[2]++;
                $count[0]--;
            }
        }

        // Here we need to check processed[1] only
        // for 2 since 0 is less than 1 and we can
        // replace it anytime
        if ($s[$i] == '1' && $count[1] > $reqd)
        {
            if ($count[0] < $reqd)
            {
                $s[$i] = '0';
                $count[0]++;
                $count[1]--;
            }
            else if (count[2] < $reqd &&
                                $processed[1] >= $reqd)
            {
                $s[$i] = '2';
                $count[2]++;
                $count[1]--;
            }
        }

        // Here we can replace 2 with 0 and 1 anytime
        if ($s[$i] == '2' && $count[2] > $reqd)
        {
            if ($count[0] < $reqd)
            {
                $s[$i] = '0';
                $count[0]++;
                $count[2]--;
            }
            else if ($count[1] < $reqd)
            {
                $s[$i] = '1';
                $count[1]++;
                $count[2]--;
            }
        }

        // keep count of processed characters
        // of each type
        $processed[$s[$i] - '0']++;
    }
    return $s;
}

// Driver Code
$s = "011200";
echo formStringMinOperations($s);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

      // JavaScript implementation of the approach

      // Function that returns the
      // modified lexicographically
      // smallest String after
      // performing minimum number
      // of given operations
      function formStringMinOperations(s)
      {
        // Stores the initial frequencies
        // of characters 0s, 1s and 2s
        var count = new Array(3).fill(0);
        for (const c of s) {
          count += 1;
        }

        // Stores number of processed characters
        // upto that point of each type
        var processed = new Array(3).fill(0);

        // Required number of characters of each type
        var reqd = parseInt(s.length / 3);
        for (var i = 0; i < s.length; i++) {
          // If the current type has already
          // reqd number of characters, no
          // need to perform any operation
          if (count[s[i].charCodeAt(0) -
          "0".charCodeAt(0)] === reqd) {
            continue;
          }

          // Process all 3 cases
          if (s[i] === "0" && count[0] >
          reqd && processed[0] >= reqd) {
            // Check for 1 first
            if (count[1] < reqd) {
              s[i] = "1";
              count[1]++;
              count[0]--;
            }

            // Else 2
            else if (count[2] < reqd) {
              s[i] = "2";
              count[2]++;
              count[0]--;
            }
          }

          // Here we need to check processed[1] only
          // for 2 since 0 is less than 1 and we can
          // replace it anytime
          if (s[i] === "1" && count[1] > reqd) {
            if (count[0] < reqd) {
              s[i] = "0";
              count[0]++;
              count[1]--;
            } else if (count[2] < reqd &&
            processed[1] >= reqd) {
              s[i] = "2";
              count[2]++;
              count[1]--;
            }
          }

          // Here we can replace 2 with 0 and 1 anytime
          if (s[i] === "2" && count[2] > reqd) {
            if (count[0] < reqd) {
              s[i] = "0";
              count[0]++;
              count[2]--;
            } else if (count[1] < reqd) {
              s[i] = "1";
              count[1]++;
              count[2]--;
            }
          }

          // keep count of processed
          // characters of each type
          processed[s[i].charCodeAt(0) -
          "0".charCodeAt(0)]++;
        }
        return s.join("");
      }

      // Driver Code
      var s = "011200";
      document.write(formStringMinOperations(s.split("")));

</script>
```

**Output:** 

```
011202
```