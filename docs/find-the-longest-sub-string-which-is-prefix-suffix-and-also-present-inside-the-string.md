# 找出最长的子串，它是前缀、后缀，也存在于串内

> 原文:[https://www . geeksforgeeks . org/find-最长的子字符串-哪个是-前缀-后缀-并且还存在于字符串内部/](https://www.geeksforgeeks.org/find-the-longest-sub-string-which-is-prefix-suffix-and-also-present-inside-the-string/)

给定弦**弦**。任务是找到最长的子串，它是给定串的前缀、后缀和子串， ***串*** 。如果不存在这样的字符串，则打印 **-1** 。
**举例:**

> **输入:**str = " fix prefixsuffix "
> **输出:**fix
> “fix”是前缀、后缀，也存在于字符串内部。
> **输入:**str = " AAAA "
> “aa”是前缀、后缀，存在于字符串内部。

**方法:**让我们计算字符串所有前缀的最长前缀后缀。最长前缀后缀 lps[i]是前缀的最大长度，也是子串[0…i]的后缀。关于最长前缀后缀的更多信息，可以在 [kmp 算法](https://www.geeksforgeeks.org/kmp-algorithm-for-pattern-searching/)的描述中看到。
第一个可能的答案是长度为 lps[n-1]的前缀。如果 lps[n-1] = 0，则无解。为了检查第一个可能的答案，您应该迭代 lps[i]。如果其中至少有一个等于 lps[n-1](但当然不是第 n-1 个)——你就找到了答案。第二种可能的答案是长度为 lps[lps[n-1]-1]的前缀。如果 lps[lps[n-1]-1] = 0，你也无解。否则，你可以肯定答案已经找到了。这个子串是我们字符串的前缀和后缀。此外，它是长度为 lps[n-1]的前缀的后缀，放在所有字符串的内部。这个解决方案适用于 O(n)。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find longest prefix suffix
vector<int> compute_lps(string s)
{
    int n = s.size();

    // To store longest prefix suffix
    vector<int> lps(n);

    // Length of the previous
    // longest prefix suffix
    int len = 0;

    // lps[0] is always 0
    lps[0] = 0;
    int i = 1;

    // Loop calculates lps[i] for i = 1 to n - 1
    while (i < n) {
        if (s[i] == s[len]) {
            len++;
            lps[i] = len;
            i++;
        }

        // (pat[i] != pat[len])
        else {
            if (len != 0)
                len = lps[len - 1];
            // Also, note that we do not increment
            // i here

            // If len = 0
            else {
                lps[i] = 0;
                i++;
            }
        }
    }

    return lps;
}

// Function to find the longest substring
// which is prefix as well as a
// sub-string of s[1...n-2]
void Longestsubstring(string s)
{
    // Find longest prefix suffix
    vector<int> lps = compute_lps(s);
    int n = s.size();

    // If lps of n-1 is zero
    if (lps[n - 1] == 0) {
        cout << -1;
        return;
    }

    for (int i = 0; i < n - 1; i++) {

        // At any position lps[i] equals to lps[n - 1]
        if (lps[i] == lps[n - 1]) {
            cout << s.substr(0, lps[i]);
            return;
        }
    }

    // If answer is not possible
    if (lps[lps[n - 1] - 1] == 0)
        cout << -1;
    else
        cout << s.substr(0, lps[lps[n - 1] - 1]);
}

// Driver code
int main()
{
    string s = "fixprefixsuffix";

    // function call
    Longestsubstring(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    // Function to find longest prefix suffix
    static int [] compute_lps(String s)
    {
        int n = s.length();

        // To store longest prefix suffix
        int [] lps = new int [n];

        // Length of the previous
        // longest prefix suffix
        int len = 0;

        // lps[0] is always 0
        lps[0] = 0;
        int i = 1;

        // Loop calculates lps[i] for i = 1 to n - 1
        while (i < n)
        {
            if (s.charAt(i) == s.charAt(len))
            {
                len++;
                lps[i] = len;
                i++;
            }

            // (pat[i] != pat[len])
            else
            {
                if (len != 0)
                    len = lps[len - 1];
                // Also, note that we do not increment
                // i here

                // If len = 0
                else
                {
                    lps[i] = 0;
                    i++;
                }
            }
        }

        return lps;
    }

    // Function to find the longest substring
    // which is prefix as well as a
    // sub-string of s[1...n-2]
    static void Longestsubstring(String s)
    {
        // Find longest prefix suffix
        int [] lps = compute_lps(s);
        int n = s.length();

        // If lps of n-1 is zero
        if (lps[n - 1] == 0)
        {
            System.out.println(-1);
            return;
        }

        for (int i = 0; i < n - 1; i++)
        {

            // At any position lps[i] equals to lps[n - 1]
            if (lps[i] == lps[n - 1])
            {
                System.out.println(s.substring(0, lps[i]));
                return;
            }
        }

        // If answer is not possible
        if (lps[lps[n - 1] - 1] == 0)
            System.out.println(-1);
        else
            System.out.println(s.substring(0, lps[lps[n - 1] - 1]));
    }

    // Driver code
    public static void main (String [] args)
    {
        String s = "fixprefixsuffix";

        // function call
        Longestsubstring(s);

    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find longest prefix suffix
def compute_lps(s):

    n = len(s)

    # To store longest prefix suffix
    lps = [0 for i in range(n)]

    # Length of the previous
    # longest prefix suffix
    Len = 0

    # lps[0] is always 0
    lps[0] = 0
    i = 1

    # Loop calculates lps[i] for i = 1 to n - 1
    while (i < n):
        if (s[i] == s[Len]):
            Len += 1
            lps[i] = Len
            i += 1

        # (pat[i] != pat[Len])
        else:
            if (Len != 0):
                Len = lps[Len - 1]
            # Also, note that we do not increment
            # i here

            # If Len = 0
            else:
                lps[i] = 0
                i += 1

    return lps

# Function to find the longest substring
# which is prefix as well as a
# sub-of s[1...n-2]
def Longestsubstring(s):

    # Find longest prefix suffix
    lps = compute_lps(s)
    n = len(s)

    # If lps of n-1 is zero
    if (lps[n - 1] == 0):
        print(-1)
        exit()

    for i in range(0,n - 1):

        # At any position lps[i] equals to lps[n - 1]
        if (lps[i] == lps[n - 1]):
            print(s[0:lps[i]])
            exit()

    # If answer is not possible
    if (lps[lps[n - 1] - 1] == 0):
        print(-1)
    else:
        print(s[0:lps[lps[n - 1] - 1]])

# Driver code

s = "fixprefixsuffix"

# function call
Longestsubstring(s)

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to find longest prefix suffix
    static int [] compute_lps(string s)
    {
        int n = s.Length;

        // To store longest prefix suffix
        int [] lps = new int [n];

        // Length of the previous
        // longest prefix suffix
        int len = 0;

        // lps[0] is always 0
        lps[0] = 0;
        int i = 1;

        // Loop calculates lps[i] for i = 1 to n - 1
        while (i < n)
        {
            if (s[i] == s[len])
            {
                len++;
                lps[i] = len;
                i++;
            }

            // (pat[i] != pat[len])
            else
            {
                if (len != 0)
                    len = lps[len - 1];
                // Also, note that we do not increment
                // i here

                // If len = 0
                else
                {
                    lps[i] = 0;
                    i++;
                }
            }
        }

        return lps;
    }

    // Function to find the longest substring
    // which is prefix as well as a
    // sub-string of s[1...n-2]
    static void Longestsubstring(string s)
    {
        // Find longest prefix suffix
        int [] lps = compute_lps(s);
        int n = s.Length;

        // If lps of n-1 is zero
        if (lps[n - 1] == 0)
        {
            Console.WriteLine(-1);
            return;
        }

        for (int i = 0; i < n - 1; i++)
        {

            // At any position lps[i] equals to lps[n - 1]
            if (lps[i] == lps[n - 1])
            {
                Console.WriteLine(s.Substring(0, lps[i]));
                return;
            }
        }

        // If answer is not possible
        if (lps[lps[n - 1] - 1] == 0)
            Console.WriteLine(-1);
        else
            Console.WriteLine(s.Substring(0, lps[lps[n - 1] - 1]));
    }

    // Driver code
    public static void Main ()
    {
        string s = "fixprefixsuffix";

        // function call
        Longestsubstring(s);

    }
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Python3 implementation of the approach

// Function to find longest prefix suffix
function compute_lps($s)
{
    $n = strlen($s);

    // To store longest prefix suffix
    $lps = array();

    // Length of the previous
    // longest prefix suffix
    $len = 0;

    // lps[0] is always 0
    $lps[0] = 0;
    $i = 1;

    // Loop calculates lps[i] for i = 1 to n - 1
    while ($i < $n)
    {
        if ($s[$i] == $s[$len])
        {
            $len++;
            $lps[$i] = $len;
            $i++;
        }

        // (pat[i] != pat[len])
        else
        {
            if ($len != 0)
                $len = $lps[$len - 1];

            // Also, note that we do not increment
            // i here

            // If len = 0
            else
            {
                $lps[$i] = 0;
                $i++;
            }
        }
    }

    return $lps;
}

// Function to find the longest substring
// which is prefix as well as a
// sub-string of s[1...n-2]
function Longestsubstring($s)
{
    // Find longest prefix suffix
    $lps = compute_lps($s);
    $n = strlen($s);

    // If lps of n-1 is zero
    if ($lps[$n - 1] == 0)
    {
        echo -1;
        return;
    }

    for ($i = 0; $i < $n - 1; $i++)
    {

        // At any position lps[i] equals to lps[n - 1]
        if ($lps[$i] == $lps[$n - 1])
        {
            echo substr($s, 0, $lps[$i]);
            return;
        }
    }

    // If answer is not possible
    if ($lps[$lps[$n - 1] - 1] == 0)
        echo -1;
    else
        echo substr($s, 0, $lps[$lps[$n - 1] - 1]);
}

// Driver code
$s = "fixprefixsuffix";

// function call
Longestsubstring($s);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find longest prefix suffix
function compute_lps(s)
{
    var n = s.length;

    // To store longest prefix suffix
    var lps = Array(n);

    // Length of the previous
    // longest prefix suffix
    var len = 0;

    // lps[0] is always 0
    lps[0] = 0;
    var i = 1;

    // Loop calculates lps[i] for i = 1 to n - 1
    while (i < n) {
        if (s[i] == s[len]) {
            len++;
            lps[i] = len;
            i++;
        }

        // (pat[i] != pat[len])
        else {
            if (len != 0)
                len = lps[len - 1];
            // Also, note that we do not increment
            // i here

            // If len = 0
            else {
                lps[i] = 0;
                i++;
            }
        }
    }

    return lps;
}

// Function to find the longest substring
// which is prefix as well as a
// sub-string of s[1...n-2]
function Longestsubstring( s)
{
    // Find longest prefix suffix
    var lps = compute_lps(s);
    var n = s.length;

    // If lps of n-1 is zero
    if (lps[n - 1] == 0) {
        document.write( -1);
        return;
    }

    for (var i = 0; i < n - 1; i++) {

        // At any position lps[i] equals to lps[n - 1]
        if (lps[i] == lps[n - 1]) {
            document.write( s.substring(0, lps[i]));
            return;
        }
    }

    // If answer is not possible
    if (lps[lps[n - 1] - 1] == 0)
        document.write( -1);
    else
        document.write( s.substr(0, lps[lps[n - 1] - 1]));
}

// Driver code
var s = "fixprefixsuffix";

// function call
Longestsubstring(s);

</script>
```

**Output:** 

```
fix
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)