# 使用超出范围的字符形成范围【L，R】内的子串的方式数

> 原文:[https://www . geeksforgeeks . org/范围内子字符串可以使用范围外字符形成的方式数/](https://www.geeksforgeeks.org/number-of-ways-in-which-the-substring-in-range-l-r-can-be-formed-using-characters-out-of-the-range/)

给定一个字符串 **S** 和一个范围**【L，R】**。任务是找到使用字符串中存在但不在范围 S[L，R]内的字符构造范围 S[L，R]内的子字符串的方法数。
**例:**

> **输入:** s = "cabcaab "，l = 1，r = 3
> **输出:** 2
> 子串为“ABC”
> s[4]+s[6]+s[0]= ' a '+' b '+' c ' = ' ABC "
> s[5]+s[6]+s[0]= ' a '+' b '+' c ' = ' ABC "
> **输入:** s = "aaaa

**方法:**这个问题可以用哈希表和组合学来解决。解决上述问题可以遵循以下步骤:

*   计算哈希表中不在范围 L 和 R 内的每个字符的频率(比如 freq)。
*   分别从 L 到 R 迭代，计算路数。
*   对于范围 L 和 R 中的每个字符，路的数量乘以 **freq[s[i]-'a']** 并将 **freq[s[i]-'a']** 的值减 1。
*   如果 **freq[s[i]-'a']** 值为 0，我们没有任何字符来填充该位置，因此路的数量将为 0。
*   最后，整体乘法将是我们的答案。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of
// ways to form the sub-string
int calculateWays(string s, int n, int l, int r)
{

    // Initialize a hash-table
    // with 0
    int freq[26];
    memset(freq, 0, sizeof freq);

    // Iterate in the string and count
    // the frequency of characters that
    // do not lie in the range L and R
    for (int i = 0; i < n; i++) {

        // Out of range characters
        if (i < l || i > r)
            freq[s[i] - 'a']++;
    }

    // Stores the final number of ways
    int ways = 1;

    // Iterate for the sub-string in the range
    // L and R
    for (int i = l; i <= r; i++) {

        // If exists then multiply
        // the number of ways and
        // decrement the frequency
        if (freq[s[i] - 'a']) {
            ways = ways * freq[s[i] - 'a'];
            freq[s[i] - 'a']--;
        }

        // If does not exist
        // the sub-string cannot be formed
        else {
            ways = 0;
            break;
        }
    }

    // Return the answer
    return ways;
}

// Driver code
int main()
{
    string s = "cabcaab";
    int n = s.length();

    int l = 1, r = 3;
    cout << calculateWays(s, n, l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GfG {

// Function to return the number of
// ways to form the sub-string
static int calculateWays(String s, int n, int l, int r)
{

    // Initialize a hash-table
    // with 0
    int freq[] = new int[26];

    // Iterate in the string and count
    // the frequency of characters that
    // do not lie in the range L and R
    for (int i = 0; i < n; i++) {

        // Out of range characters
        if (i < l || i > r)
            freq[s.charAt(i)-'a']++;
    }

    // Stores the final number of ways
    int ways = 1;

    // Iterate for the sub-string in the range
    // L and R
    for (int i = l; i <= r; i++) {

        // If exists then multiply
        // the number of ways and
        // decrement the frequency
        if (freq[s.charAt(i) - 'a'] != 0) {
            ways = ways * freq[s.charAt(i) - 'a'];
            freq[s.charAt(i) - 'a']--;
        }

        // If does not exist
        // the sub-string cannot be formed
        else {
            ways = 0;
            break;
        }
    }

    // Return the answer
    return ways;
}

// Driver code
public static void main(String[] args)
{
    String s = "cabcaab";
    int n = s.length();

    int l = 1, r = 3;
    System.out.println(calculateWays(s, n, l, r));

}
}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the number of
# ways to form the sub-string
def calculateWays(s, n, l, r):

    # Initialize a hash-table
    # with 0
    freq = [0 for i in range(26)]

    # Iterate in the string and count
    # the frequency of characters that
    # do not lie in the range L and R
    for i in range(n):

        # Out of range characters
        if (i < l or i > r):
            freq[ord(s[i]) - ord('a')] += 1

    # Stores the final number of ways
    ways = 1

    # Iterate for the sub-string in the range
    # L and R
    for i in range(l, r + 1, 1):

        # If exists then multiply
        # the number of ways and
        # decrement the frequency
        if (freq[ord(s[i]) - ord('a')]):
            ways = ways * freq[ord(s[i]) - ord('a')]
            freq[ord(s[i]) - ord('a')] -= 1

        # If does not exist
        # the sub-string cannot be formed
        else:
            ways = 0
            break

    # Return the answer
    return ways

# Driver code
if __name__ == '__main__':
    s = "cabcaab"
    n = len(s)

    l = 1
    r = 3
    print(calculateWays(s, n, l, r))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GfG
{

// Function to return the number of
// ways to form the sub-string
static int calculateWays(String s, int n, int l, int r)
{

    // Initialize a hash-table
    // with 0
    int []freq = new int[26];

    // Iterate in the string and count
    // the frequency of characters that
    // do not lie in the range L and R
    for (int i = 0; i < n; i++)
    {

        // Out of range characters
        if (i < l || i > r)
            freq[s[i]-'a']++;
    }

    // Stores the final number of ways
    int ways = 1;

    // Iterate for the sub-string in the range
    // L and R
    for (int i = l; i <= r; i++)
    {

        // If exists then multiply
        // the number of ways and
        // decrement the frequency
        if (freq[s[i] - 'a'] != 0) {
            ways = ways * freq[s[i] - 'a'];
            freq[s[i] - 'a']--;
        }

        // If does not exist
        // the sub-string cannot be formed
        else {
            ways = 0;
            break;
        }
    }

    // Return the answer
    return ways;
}

// Driver code
public static void Main()
{
    String s = "cabcaab";
    int n = s.Length;

    int l = 1, r = 3;
    Console.WriteLine(calculateWays(s, n, l, r));

}
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the number of
// ways to form the sub-string
function calculateWays($s, $n, $l, $r)
{

    // Initialize a hash-table
    // with 0
    $freq = array();
    for($i = 0; $i < 26 ; $i++ )
    {
        $freq[$i] = 0;
    }

    // Iterate in the string and count
    // the frequency of characters that
    // do not lie in the range L and R
    for($i = 0; $i < $n ; $i++ )

    {

        // Out of range characters
        if ($i < $l || $i > $r)
            $freq[ord($s[$i]) - 97]++;
    }

    // Stores the final number of ways
    $ways = 1;

    // Iterate for the sub-string in the range
    // L and R
    for ($i = $l; $i <= $r; $i++)
    {

        // If exists then multiply
        // the number of ways and
        // decrement the frequency
        if ($freq[ord($s[$i]) - 97])
        {
            $ways = $ways * $freq[ord($s[$i]) - 97];
            $freq[ord($s[$i]) - 97]--;
        }

        // If does not exist
        // the sub-string cannot be formed
        else
        {
            $ways = 0;
            break;
        }
    }

    // Return the answer
    return $ways;
}

// Driver code
$s = "cabcaab";
$n = strlen($s);

$l = 1;
$r = 3;
echo calculateWays($s, $n, $l, $r);

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Function to return the number of
    // ways to form the sub-string
    function calculateWays( s , n , l , r) {

        // Initialize a hash-table
        // with 0
        var freq = Array(26).fill(0);

        // Iterate in the string and count
        // the frequency of characters that
        // do not lie in the range L and R
        for (i = 0; i < n; i++) {

            // Out of range characters
            if (i < l || i > r)
                freq[s.charCodeAt(i) - 'a'.charCodeAt(0)]++;
        }

        // Stores the final number of ways
        var ways = 1;

        // Iterate for the sub-string in the range
        // L and R
        for (i = l; i <= r; i++) {

            // If exists then multiply
            // the number of ways and
            // decrement the frequency
            if (freq[s.charCodeAt(i) - 'a'.charCodeAt(0)] != 0) {
                ways = ways * freq[s.charCodeAt(i) - 'a'.charCodeAt(0)];
                freq[s.charCodeAt(i) - 'a'.charCodeAt(0)]--;
            }

            // If does not exist
            // the sub-string cannot be formed
            else {
                ways = 0;
                break;
            }
        }

        // Return the answer
        return ways;
    }

    // Driver code

        var s = "cabcaab";
        var n = s.length;

        var l = 1, r = 3;
        document.write(calculateWays(s, n, l, r));

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N)，其中 N 为字符串的长度。
**辅助空间:** O(1)