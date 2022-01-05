# 包含给定字符恰好 k 次的子字符串数量

> 原文:[https://www . geeksforgeeks . org/包含给定字符的子字符串数量-精确到 k 倍/](https://www.geeksforgeeks.org/number-of-sub-strings-that-contain-the-given-character-exactly-k-times/)

给定字符串 **str** 、字符 **c** 和整数 **k > 0** 。任务是精确地找到包含字符 **c** 的子串的数量 **k** 次。

**示例:**

> **输入:** str = "abada "，c = 'a '，K = 2
> **输出:** 4
> 所有可能的子串都是“aba”、“abad”、“bada”和“ada”。
> 
> **输入:** str = "55555 "，c = '5 '，k = 4
> T3】输出: 2

**天真的做法:**一个简单的解决方法是生成所有的子字符串，并检查给定字符的计数是否正好是 k 倍。
这个方法的时间复杂度是 **O(n <sup>2</sup> )** 。

**有效方法:**一种有效的解决方案是使用滑动窗口技术。从字符 c 开始，找到精确包含给定字符 k 次的子字符串。计算子字符串两边的字符数。将计数相乘，得到可能的子字符串的数量。这种方法的时间复杂度是 **O(n)** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of required sub-strings
int countSubString(string s, char c, int k)
{

    // Left and right counters for characters on
    // both sides of sub-string window
    int leftCount = 0, rightCount = 0;

    // Left and right pointer on both
    // sides of sub-string window
    int left = 0, right = 0;

    // Initialize the frequency
    int freq = 0;

    // Result and length of string
    int result = 0, len = s.length();

    // Initialize the left pointer
    while (s[left] != c && left < len) {
        left++;
        leftCount++;
    }

    // Initialize the right pointer
    right = left + 1;
    while (freq != (k - 1) && (right - 1) < len) {
        if (s[right] == c)
            freq++;
        right++;
    }

    // Traverse all the window sub-strings
    while (left < len && (right - 1) < len) {

        // Counting the characters on left side
        // of the sub-string window
        while (s[left] != c && left < len) {
            left++;
            leftCount++;
        }

        // Counting the characters on right side
        // of the sub-string window
        while (right < len && s[right] != c) {
            if (s[right] == c)
                freq++;
            right++;
            rightCount++;
        }

        // Add the possible sub-strings
        // on both sides to result
        result = result + (leftCount + 1) * (rightCount + 1);

        // Setting the frequency for next
        // sub-string window
        freq = k - 1;

        // Reset the left and right counters
        leftCount = 0;
        rightCount = 0;

        left++;
        right++;
    }
    return result;
}

// Driver code
int main()
{
    string s = "abada";
    char c = 'a';
    int k = 2;

    cout << countSubString(s, c, k) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count of required sub-strings
static int countSubString(char[] s, char c, int k)
{

    // Left and right counters for characters on
    // both sides of sub-string window
    int leftCount = 0, rightCount = 0;

    // Left and right pointer on both
    // sides of sub-string window
    int left = 0, right = 0;

    // Initialize the frequency
    int freq = 0;

    // Result and length of string
    int result = 0, len = s.length;

    // Initialize the left pointer
    while (s[left] != c && left < len)
    {
        left++;
        leftCount++;
    }

    // Initialize the right pointer
    right = left + 1;
    while (freq != (k - 1) && (right - 1) < len)
    {
        if (s[right] == c)
            freq++;
        right++;
    }

    // Traverse all the window sub-strings
    while (left < len && (right - 1) < len)
    {

        // Counting the characters on left side
        // of the sub-string window
        while (s[left] != c && left < len)
        {
            left++;
            leftCount++;
        }

        // Counting the characters on right side
        // of the sub-string window
        while (right < len && s[right] != c)
        {
            if (s[right] == c)
                freq++;
            right++;
            rightCount++;
        }

        // Add the possible sub-strings
        // on both sides to result
        result = result + (leftCount + 1) * (rightCount + 1);

        // Setting the frequency for next
        // sub-string window
        freq = k - 1;

        // Reset the left and right counters
        leftCount = 0;
        rightCount = 0;

        left++;
        right++;
    }
    return result;
}

// Driver code
public static void main(String[] args)
{
    String s = "abada";
    char c = 'a';
    int k = 2;

    System.out.println(countSubString(s.toCharArray(), c, k));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the count
# of required sub-strings
def countSubString(s, c, k):

    # Left and right counters for characters
    # on both sides of sub-string window
    leftCount = 0
    rightCount = 0

    # Left and right pointer on both
    # sides of sub-string window
    left = 0
    right = 0

    # Initialize the frequency
    freq = 0

    # Result and length of string
    result = 0
    len1 = len(s)

    # Initialize the left pointer
    while (s[left] != c and left < len1):
        left += 1
        leftCount += 1

    # Initialize the right pointer
    right = left + 1
    while (freq != (k - 1) and
          (right - 1) < len1):
        if (s[right] == c):
            freq += 1
        right += 1

    # Traverse all the window sub-strings
    while (left < len1 and
          (right - 1) < len1):

        # Counting the characters on left side
        # of the sub-string window
        while (s[left] != c and left < len1):
            left += 1
            leftCount += 1

        # Counting the characters on right side
        # of the sub-string window
        while (right < len1 and
             s[right] != c):
            if (s[right] == c):
                freq += 1
            right += 1
            rightCount += 1

        # Add the possible sub-strings
        # on both sides to result
        result = (result + (leftCount + 1) *
                           (rightCount + 1))

        # Setting the frequency for next
        # sub-string window
        freq = k - 1

        # Reset the left and right counters
        leftCount = 0
        rightCount = 0

        left += 1
        right += 1

    return result

# Driver code
if __name__ == '__main__':
    s = "abada"
    c = 'a'
    k = 2

    print(countSubString(s, c, k))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of required sub-strings
static int countSubString(char[] s, char c, int k)
{

    // Left and right counters for characters on
    // both sides of sub-string window
    int leftCount = 0, rightCount = 0;

    // Left and right pointer on both
    // sides of sub-string window
    int left = 0, right = 0;

    // Initialize the frequency
    int freq = 0;

    // Result and length of string
    int result = 0, len = s.Length;

    // Initialize the left pointer
    while (s[left] != c && left < len)
    {
        left++;
        leftCount++;
    }

    // Initialize the right pointer
    right = left + 1;
    while (freq != (k - 1) && (right - 1) < len)
    {
        if (s[right] == c)
            freq++;
        right++;
    }

    // Traverse all the window sub-strings
    while (left < len && (right - 1) < len)
    {

        // Counting the characters on left side
        // of the sub-string window
        while (s[left] != c && left < len)
        {
            left++;
            leftCount++;
        }

        // Counting the characters on right side
        // of the sub-string window
        while (right < len && s[right] != c)
        {
            if (s[right] == c)
                freq++;
            right++;
            rightCount++;
        }

        // Add the possible sub-strings
        // on both sides to result
        result = result + (leftCount + 1) * (rightCount + 1);

        // Setting the frequency for next
        // sub-string window
        freq = k - 1;

        // Reset the left and right counters
        leftCount = 0;
        rightCount = 0;

        left++;
        right++;
    }
    return result;
}

// Driver code
public static void Main(String[] args)
{
    String s = "abada";
    char c = 'a';
    int k = 2;

    Console.WriteLine(countSubString(s.ToCharArray(), c, k));
}
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of required sub-strings
function countSubString($s, $c, $k)
{

    // Left and right counters for characters on
    // both sides of sub-string window
    $leftCount = 0; $rightCount = 0;

    // Left and right pointer on both
    // sides of sub-string window
    $left = 0; $right = 0;

    // Initialize the frequency
    $freq = 0;

    // Result and length of string
    $result = 0; $len = strlen($s);

    // Initialize the left pointer
    while ($s[$left] != $c && $left < $len)
    {
        $left++;
        $leftCount++;
    }

    // Initialize the right pointer
    $right = $left + 1;
    while ($freq != ($k - 1) && ($right - 1) < $len)
    {
        if ($s[$right] == $c)
            $freq++;

        $right++;
    }

    // Traverse all the window sub-strings
    while ($left < $len && ($right - 1) < $len)
    {

        // Counting the characters on left side
        // of the sub-string window
        while ($s[$left] != $c && $left < $len)
        {
            $left++;
            $leftCount++;
        }

        // Counting the characters on right side
        // of the sub-string window
        while ($right < $len && $s[$right] != $c)
        {
            if ($s[$right] == $c)
                $freq++;

            $right++;
            $rightCount++;
        }

        // Add the possible sub-strings
        // on both sides to result
        $result = $result + ($leftCount + 1) *
                            ($rightCount + 1);

        // Setting the frequency for next
        // sub-string window
        $freq = $k - 1;

        // Reset the left and right counters
        $leftCount = 0;
        $rightCount = 0;

        $left++;
        $right++;
    }
    return $result;
}

    // Driver code
    $s = "abada";
    $c = 'a';
    $k = 2;

    echo countSubString($s, $c, $k), "\n";

    // This code is contributed by Ryuga

?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of required sub-strings
function countSubString(s, c, k)
{

    // Left and right counters for characters on
    // both sides of sub-string window
    var leftCount = 0, rightCount = 0;

    // Left and right pointer on both
    // sides of sub-string window
    var left = 0, right = 0;

    // Initialize the frequency
    var freq = 0;

    // Result and length of string
    var result = 0, len = s.length;

    // Initialize the left pointer
    while (s[left] != c && left < len) {
        left++;
        leftCount++;
    }

    // Initialize the right pointer
    right = left + 1;
    while (freq != (k - 1) && (right - 1) < len) {
        if (s[right] == c)
            freq++;
        right++;
    }

    // Traverse all the window sub-strings
    while (left < len && (right - 1) < len) {

        // Counting the characters on left side
        // of the sub-string window
        while (s[left] != c && left < len) {
            left++;
            leftCount++;
        }

        // Counting the characters on right side
        // of the sub-string window
        while (right < len && s[right] != c) {
            if (s[right] == c)
                freq++;
            right++;
            rightCount++;
        }

        // Add the possible sub-strings
        // on both sides to result
        result = result + (leftCount + 1) * (rightCount + 1);

        // Setting the frequency for next
        // sub-string window
        freq = k - 1;

        // Reset the left and right counters
        leftCount = 0;
        rightCount = 0;

        left++;
        right++;
    }
    return result;
}

// Driver code
var s = "abada";
var c = 'a';
var k = 2;
document.write( countSubString(s, c, k) + "<br>");

</script>
```

**Output:** 

```
4
```