# 回文排列数|第 1 组

> 原文:[https://www . geesforgeks . org/回文排列数-集合-1/](https://www.geeksforgeeks.org/number-of-palindromic-permutations-set-1/)

给定字符串，找到它的所有回文排列的计数。
**例:**

```
Input : str = "gfgf"
Output : 2
There are two palindromic 
permutations fggf and gffg

Input : str = "abc"
Output : 0
```

这个想法基于以下事实:

*   如果出现的奇数字符数最多为 1，则字符串可以置换为回文。
*   唯一奇数字符的一次出现总是出现在中间。
*   所有字符计数的一半决定结果。如果出现奇怪的字符，则为二分之一楼层。另一半是自动决定的

例如，如果输入字符串是“aabbccd”，回文置换的计数是 3！(取所有计数的一半的楼层得到三)
如果一半本身有重复字符怎么办？
我们应用一个简单的组合规则，除以一半的阶乘。
例如“aaaabbbb”，弦的一半是 5 楼。在回文串的一半，“a”重复三次，“b”重复两次，所以我们的结果是(5！) / (2!) * (3!).

## C++

```
// CPP program to find number of
// palindromic permutations of a
// given string
#include <bits/stdc++.h>
using namespace std;

const int MAX = 256;

// Returns factorial of n
long long int fact(int n)
{
    long long int res = 1;
    for (int i = 2; i <= n; i++)
        res = res * i;
    return res;
}

// Returns count of palindromic
// permutations of str.
int countPalinPermutations(string &str)
{
    // Count frequencies of all characters
    int n = str.length();
    int freq[MAX] = { 0 };
    for (int i = 0; i < n; i++)
        freq[str[i]]++;

    // Since half of the characters
    // decide count of palindromic
    // permutations, we take (n/2)!
    long long int res = fact(n / 2);

    // To make sure that there is at
    // most one odd occurring char
    bool oddFreq = false;

    // Traverse through all counts
    for (int i = 0; i < MAX; i++) {
        int half = freq[i] / 2;

        // To make sure that the
        // string can permute to
        // form a palindrome
        if (freq[i] % 2 != 0) {

            // If there are more than
            // one odd occurring chars
            if (oddFreq == true)
                return 0;
            oddFreq = true;
        }

        // Divide all permutations with
        // repeated characters
        res = res / fact(half);
    }

    return res;
}

// Driver code
int main()
{
    string str = "gffg";
    cout << countPalinPermutations(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of
// palindromic permutations of a
// given string
class GFG {

    static final int MAX = 256;

    // Returns factorial of n
    static long fact(int n)
    {
        long res = 1;

        for (int i = 2; i <= n; i++)
            res = res * i;

        return res;
    }

    // Returns count of palindromic
    // permutations of str.
    static int countPalinPermutations(String str)
    {

        // Count frequencies of all characters
        int n = str.length();
        int freq[]=new int[MAX];

        for (int i = 0; i < n; i++)
            freq[str.charAt(i)]++;

        // Since half of the characters
        // decide count of palindromic
        // permutations, we take (n/2)!
        long res = fact(n / 2);

        // To make sure that there is at
        // most one odd occurring char
        boolean oddFreq = false;

        // Traverse through all counts
        for (int i = 0; i < MAX; i++) {
            int half = freq[i] / 2;

            // To make sure that the
            // string can permute to
            // form a palindrome
            if (freq[i] % 2 != 0) {

                // If there are more than
                // one odd occurring chars
                if (oddFreq == true)
                    return 0;

                oddFreq = true;
            }

            // Divide all permutations with
            // repeated characters
            res = res / fact(half);
        }

        return (int)res;
    }

    // Driver code
    public static void main (String[] args)
    {

        String str = "gffg";

        System.out.print(
            countPalinPermutations(str));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find number of
# palindromic permutations of a
# given string
MAX = 256

# Returns factorial of n
def fact(n) :
    res = 1
    for i in range(2, n+1) :
        res = res * i
    return res

# Returns count of palindromic
# permutations of str.
def countPalinPermutations(str) :
    global MAX

    # Count frequencies of
    # all characters
    n = len(str)
    freq = [0] * MAX;
    for i in range(0, n) :
        freq[ord(str[i])] = freq[ord(str[i])] + 1;
    # Since half of the characters
    # decide count of palindromic
    # permutations, we take (n/2)!
    res = fact(int(n / 2))

    # To make sure that there is at
    # most one odd occurring char
    oddFreq = False

    # Traverse through all counts
    for i in range(0, MAX) :
        half = int(freq[i] / 2)

        # To make sure that the
        # string can permute to
        # form a palindrome
        if (freq[i] % 2 != 0):

            # If there are more than
            # one odd occurring chars
            if (oddFreq == True):
                return 0
            oddFreq = True

        # Divide all permutations
        # with repeated characters
        res = int(res / fact(half))

    return res

# Driver code
str = "gffg"
print (countPalinPermutations(str))

# This code is contributed by Manish Shaw
# (manishshaw1)
```

## C#

```
// C# program to find number of
// palindromic permutations of a
// given string
using System;

class GFG {

    static int MAX = 256;

    // Returns factorial of n
    static long fact(int n)
    {
        long res = 1;

        for (int i = 2; i <= n; i++)
            res = res * i;

        return res;
    }

    // Returns count of palindromic
    // permutations of str.
    static int countPalinPermutations(string str)
    {

        // Count frequencies of all characters
        int n = str.Length;
        int []freq=new int[MAX];

        for (int i = 0; i < n; i++)
            freq[str[i]]++;

        // Since half of the characters
        // decide count of palindromic
        // permutations, we take (n/2)!
        long res = fact(n / 2);

        // To make sure that there is at
        // most one odd occurring char
        bool oddFreq = false;

        // Traverse through all counts
        for (int i = 0; i < MAX; i++) {
            int half = freq[i] / 2;

            // To make sure that the
            // string can permute to
            // form a palindrome
            if (freq[i] % 2 != 0) {

                // If there are more than
                // one odd occurring chars
                if (oddFreq == true)
                    return 0;

                oddFreq = true;
            }

            // Divide all permutations with
            // repeated characters
            res = res / fact(half);
        }

        return (int)res;
    }

    // Driver code
    public static void Main ()
    {

        string str = "gffg";

        Console.WriteLine(
            countPalinPermutations(str));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number of
// palindromic permutations of a
// given string
$MAX = 256;

// Returns factorial of n
function fact($n)
{
    $res = 1;
    for ($i = 2; $i <= $n; $i++)
        $res = $res * $i;
    return $res;
}

// Returns count of palindromic
// permutations of str.
function countPalinPermutations(&$str)
{
    global $MAX ;

    // Count frequencies of
    // all characters
    $n = strlen($str);
    $freq = (0);
    for ($i = 0; $i < $n; $i++)

    // Since half of the characters
    // decide count of palindromic
    // permutations, we take (n/2)!
    $res = fact($n / 2);

    // To make sure that there is at
    // most one odd occurring char
    $oddFreq = false;

    // Traverse through all counts
    for ($i = 0; $i < $MAX; $i++)
    {
        $half = $freq[$i] / 2;

        // To make sure that the
        // string can permute to
        // form a palindrome
        if ($freq[$i] % 2 != 0)
        {

            // If there are more than
            // one odd occurring chars
            if ($oddFreq == true)
                return 0;
            $oddFreq = true;
        }

        // Divide all permutations
        // with repeated characters
        $res = $res / fact($half);
    }

    return $res;
}

// Driver code
$str = "gffg";
echo countPalinPermutations($str);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript program to find number of
    // palindromic permutations of a
    // given string

    let MAX = 256;

    // Returns factorial of n
    function fact(n)
    {
        let res = 1;

        for (let i = 2; i <= n; i++)
            res = res * i;

        return res;
    }

    // Returns count of palindromic
    // permutations of str.
    function countPalinPermutations(str)
    {

        // Count frequencies of all characters
        let n = str.length;
        let freq = new Array(MAX);
        freq.fill(0);

        for (let i = 0; i < n; i++)
            freq[str[i].charCodeAt()]++;

        // Since half of the characters
        // decide count of palindromic
        // permutations, we take (n/2)!
        let res = fact(n / 2);

        // To make sure that there is at
        // most one odd occurring char
        let oddFreq = false;

        // Traverse through all counts
        for (let i = 0; i < MAX; i++) {
            let half = freq[i] / 2;

            // To make sure that the
            // string can permute to
            // form a palindrome
            if (freq[i] % 2 != 0) {

                // If there are more than
                // one odd occurring chars
                if (oddFreq == true)
                    return 0;

                oddFreq = true;
            }

            // Divide all permutations with
            // repeated characters
            res = res / fact(half);
        }

        return res;
    }

    let str = "gffg";

    document.write(countPalinPermutations(str));

</script>
```

**Output :** 

```
2
```

上述解决方案很早就导致溢出。我们可以通过做模运算来避免溢出。在下一篇文章中，我们将讨论基于模块化算法的方法。