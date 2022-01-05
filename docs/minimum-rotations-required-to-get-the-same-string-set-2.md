# 获得相同字符串所需的最小旋转次数| Set-2

> 原文:[https://www . geeksforgeeks . org/最小旋转-需要获得相同的字符串集-2/](https://www.geeksforgeeks.org/minimum-rotations-required-to-get-the-same-string-set-2/)

给定一个字符串，我们需要找到获得相同字符串所需的最小旋转次数。在这种情况下，我们将只考虑左旋转。

**示例:**

> **输入:** s = "极客"
> T3】输出: 5
> 
> **输入:**s = " AAAA "
> T3】输出: 1

**天真方法:**基本方法是从第一个位置开始不断旋转字符串，并计算旋转次数，直到我们得到初始字符串。

**高效方法:**我们将遵循基本方法，但会尽量减少生成旋转所花费的时间。
想法如下:

*   生成输入字符串两倍大小的新字符串，如下所示:

```
newString = original string excluding first character 
            + original string with the first character.

+ denotes concatenation here.  
```

*   如果原始字符串是 str = "abcd "，新字符串将是" bcdabcd "。
*   现在，任务仍然是在新生成的字符串中搜索原始字符串，以及在所需的旋转次数中找到该字符串的索引。
*   对于字符串匹配，我们将使用 [KMP 算法](https://www.geeksforgeeks.org/searching-for-patterns-set-2-kmp-algorithm/)，该算法在线性时间内执行字符串匹配。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;
void computeLPSArray(char* pat, int M, int* lps);

// Prints occurrences of txt[] in pat[]
int KMPSearch(char* pat, char* txt)
{
    int M = strlen(pat);
    int N = strlen(txt);

    // Create lps[] that will hold the longest
    // prefix suffix values for pattern
    int lps[M];

    // Preprocess the pattern (calculate lps[] array)
    computeLPSArray(pat, M, lps);

    // Index for txt[] , // index for pat[]
    int i = 0;
    int j = 0;
    while (i < N) {
        if (pat[j] == txt[i]) {
            j++;
            i++;
        }

        if (j == M) {
            return i - j;
            j = lps[j - 1];
        }

        // Mismatch after j matches
        else if (i < N && pat[j] != txt[i]) {

            // Do not match lps[0..lps[j-1]] characters,
            // they will match anyway
            if (j != 0)
                j = lps[j - 1];
            else
                i = i + 1;
        }
    }
}

// Fills lps[] for given pattern pat[0..M-1]
void computeLPSArray(char* pat, int M, int* lps)
{
    // Length of the previous longest prefix suffix
    int len = 0;

    // lps[0] is always 0
    lps[0] = 0;

    // The loop calculates lps[i] for i = 1 to M-1
    int i = 1;
    while (i < M) {
        if (pat[i] == pat[len]) {
            len++;
            lps[i] = len;
            i++;
        }

        // (pat[i] != pat[len])
        else
        {
            // This is tricky. Consider the example.
            // AAACAAAA and i = 7\. The idea is similar
            // to search step.
            if (len != 0) {
                len = lps[len - 1];
            }
            else
            {
                lps[i] = 0;
                i++;
            }
        }
    }
}

// Returns count of rotations to get the
// same string back
int countRotations(string s)
{
    // Form a string excluding the first character
    // and concatenating the string at the end
    string s1 = s.substr(1, s.size() - 1) + s;

    // Convert the string to character array
    char pat[s.length()], text[s1.length()];

    strcpy(pat, s.c_str());
    strcpy(text, s1.c_str());

    // Use the KMP search algorithm
    // to find it in O(N) time
    return 1 + KMPSearch(pat, text);
}

// Driver code
int main()
{
    string s1 = "geeks";

    cout << countRotations(s1);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

// Prints occurrences of txt[] in pat[]
static int KMPSearch(char []pat, char []txt)
{
    int M = pat.length;
    int N = txt.length;

    // Create lps[] that will hold the longest
    // prefix suffix values for pattern
    int lps[] = new int[M];

    // Preprocess the pattern (calculate lps[] array)
    computeLPSArray(pat, M, lps);

    // Index for txt[] , // index for pat[]
    int i = 0;
    int j = 0;
    while (i < N)
    {
        if (pat[j] == txt[i])
        {
            j++;
            i++;
        }

        if (j == M)
        {
            return i - j + 1;
            //j = lps[j - 1];
        }

        // Mismatch after j matches
        else if (i < N && pat[j] != txt[i])
        {

            // Do not match lps[0..lps[j-1]] characters,
            // they will match anyway
            if (j != 0)
                j = lps[j - 1];
            else
                i = i + 1;
        }
    }
    return 0;
}

// Fills lps[] for given pattern pat[0..M-1]
static void computeLPSArray(char []pat, int M, int []lps)
{

    // Length of the previous longest prefix suffix
    int len = 0;

    // lps[0] is always 0
    lps[0] = 0;

    // The loop calculates lps[i] for i = 1 to M-1
    int i = 1;
    while (i < M)
    {
        if (pat[i] == pat[len])
        {
            len++;
            lps[i] = len;
            i++;
        }

        // (pat[i] != pat[len])
        else
        {
            // This is tricky. Consider the example.
            // AAACAAAA and i = 7\. The idea is similar
            // to search step.
            if (len != 0) {
                len = lps[len - 1];
            }
            else
            {
                lps[i] = 0;
                i++;
            }
        }
    }
}

// Returns count of rotations to get the
// same String back
static int countRotations(String s)
{
    // Form a String excluding the first character
    // and concatenating the String at the end
    String s1 = s.substring(1, s.length() - 1) + s;

    // Convert the String to character array
    char []pat = s.toCharArray();
    char []text = s1.toCharArray();

    // Use the KMP search algorithm
    // to find it in O(N) time
    return 1 + KMPSearch(pat, text);
}

// Driver code
public static void main(String []args)
{
    String s1 = "geeks";
    System.out.print(countRotations(s1));
}
}

// This code is contributed by rutvik_56.
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Prints occurrences of txt[] in pat[]
def KMPSearch(pat, txt):

    M = len(pat)
    N = len(txt)

    # Create lps[] that will hold the longest
    # prefix suffix values for pattern
    lps = [0] * M

    # Preprocess the pattern (calculate lps[] array)
    computeLPSArray(pat, M, lps)

    # Index for txt[] , # index for pat[]
    i = 0
    j = 0
    while i < N:
        if pat[j] == txt[i]:
            j += 1
            i += 1

        if j == M:
            return i - j
            j = lps[j - 1]

        # Mismatch after j matches
        elif i < N and pat[j] != txt[i]:

            # Do not match lps[0..lps[j-1]] characters,
            # they will match anyway
            if j != 0:
                j = lps[j - 1]
            else:
                i = i + 1

# Fills lps[] for given pattern pat[0..M-1]
def computeLPSArray(pat, M, lps):

    # Length of the previous longest prefix suffix
    _len = 0

    # lps[0] is always 0
    lps[0] = 0

    # The loop calculates lps[i] for i = 1 to M-1
    i = 1
    while i < M:
        if pat[i] == pat[_len]:
            _len += 1
            lps[i] = _len
            i += 1

        # (pat[i] != pat[_len])
        else:

            # This is tricky. Consider the example.
            # AAACAAAA and i = 7\. The idea is similar
            # to search step.
            if _len != 0:
                _len = lps[_len - 1]
            else:
                lps[i] = 0
                i += 1

# Returns count of rotations to get the
# same string back
def countRotations(s):

    # Form a string excluding the first character
    # and concatenating the string at the end
    s1 = s[1 : len(s)] + s

    # Convert the string to character array
    pat = s[:]
    text = s1[:]

    # Use the KMP search algorithm
    # to find it in O(N) time
    return 1 + KMPSearch(pat, text)

# Driver code
s1 = "geeks"
print(countRotations(s1))

# This code is contributed by divyamohan123
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Prints occurrences of txt[] in pat[]
static int KMPSearch(char []pat, char []txt)
{
    int M = pat.Length;
    int N = txt.Length;

    // Create lps[] that will hold the longest
    // prefix suffix values for pattern
    int []lps = new int[M];

    // Preprocess the pattern (calculate lps[] array)
    computeLPSArray(pat, M, lps);

    // Index for txt[] , // index for pat[]
    int i = 0;
    int j = 0;

    while (i < N)
    {
        if (pat[j] == txt[i])
        {
            j++;
            i++;
        }

        if (j == M)
        {
            return i - j ;
            //j = lps[j - 1];
        }

        // Mismatch after j matches
        else if (i < N && pat[j] != txt[i])
        {

            // Do not match lps[0..lps[j-1]]
            // characters, they will match anyway
            if (j != 0)
                j = lps[j - 1];
            else
                i = i + 1;
        }
    }
    return 0;
}

// Fills lps[] for given pattern pat[0..M-1]
static void computeLPSArray(char []pat, int M,
                            int []lps)
{

    // Length of the previous longest
    // prefix suffix
    int len = 0;

    // lps[0] is always 0
    lps[0] = 0;

    // The loop calculates lps[i]
    // for i = 1 to M-1
    int i = 1;

    while (i < M)
    {
        if (pat[i] == pat[len])
        {
            len++;
            lps[i] = len;
            i++;
        }

        // (pat[i] != pat[len])
        else
        {

            // This is tricky. Consider the example.
            // AAACAAAA and i = 7\. The idea is similar
            // to search step.
            if (len != 0) {
                len = lps[len - 1];
            }
            else
            {
                lps[i] = 0;
                i++;
            }
        }
    }
}

// Returns count of rotations to get the
// same string back
static int countRotations(string s)
{

    // Form a string excluding the first character
    // and concatenating the string at the end
    string s1 = s.Substring(1, s.Length - 1) + s;

    // Convert the string to character array
    char []pat = s.ToCharArray();
    char []text = s1.ToCharArray();

    // Use the KMP search algorithm
    // to find it in O(N) time
    return 1 + KMPSearch(pat, text);
}

// Driver code
public static void Main(params string []args)
{
    string s1 = "geeks";

    Console.Write(countRotations(s1));
}
}

// This code is contributed by pratham76
```

## java 描述语言

```
<script>

    // JavaScript implementation of the above approach

    // Prints occurrences of txt[] in pat[]
    function KMPSearch(pat, txt)
    {
        let M = pat.length;
        let N = txt.length;

        // Create lps[] that will hold the longest
        // prefix suffix values for pattern
        let lps = new Array(M);
        lps.fill(0);

        // Preprocess the pattern (calculate lps[] array)
        computeLPSArray(pat, M, lps);

        // Index for txt[] , // index for pat[]
        let i = 0;
        let j = 0;

        while (i < N)
        {
            if (pat[j] == txt[i])
            {
                j++;
                i++;
            }

            if (j == M)
            {
                return i - j ;
                //j = lps[j - 1];
            }

            // Mismatch after j matches
            else if (i < N && pat[j] != txt[i])
            {

                // Do not match lps[0..lps[j-1]]
                // characters, they will match anyway
                if (j != 0)
                    j = lps[j - 1];
                else
                    i = i + 1;
            }
        }
        return 0;
    }

    // Fills lps[] for given pattern pat[0..M-1]
    function computeLPSArray(pat, M, lps)
    {

        // Length of the previous longest
        // prefix suffix
        let len = 0;

        // lps[0] is always 0
        lps[0] = 0;

        // The loop calculates lps[i]
        // for i = 1 to M-1
        let i = 1;

        while (i < M)
        {
            if (pat[i] == pat[len])
            {
                len++;
                lps[i] = len;
                i++;
            }

            // (pat[i] != pat[len])
            else
            {

                // This is tricky. Consider the example.
                // AAACAAAA and i = 7\. The idea is similar
                // to search step.
                if (len != 0) {
                    len = lps[len - 1];
                }
                else
                {
                    lps[i] = 0;
                    i++;
                }
            }
        }
    }

    // Returns count of rotations to get the
    // same string back
    function countRotations(s)
    {

        // Form a string excluding the first character
        // and concatenating the string at the end
        let s1 = s.substring(1, s.length) + s;

        // Convert the string to character array
        let pat = s.split('');
        let text = s1.split('');

        // Use the KMP search algorithm
        // to find it in O(N) time
        return 1 + KMPSearch(pat, text);
    }

    let s1 = "geeks";

    document.write(countRotations(s1));

</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(N)。