# 另一个字符串的任意子字符串的字谜子字符串的数量

> 原文:[https://www . geeksforgeeks . org/子串数-这是另一个串的任意子串的字谜/](https://www.geeksforgeeks.org/number-of-sub-strings-which-are-anagram-of-any-sub-string-of-another-string/)

给定两个字符串 **S1** 和 **S2** ，任务是统计 **S1** 的子字符串数量，这些子字符串是 **S2** 的任意子字符串的字谜。
**举例:**

> **输入:**S1 =“ABB”，S2 =“BAB”
> **输出:**5
> S1 有 6 个子串:“A”、“B”、“B”、“AB”、“BB”和“ABB”
> 其中只有“BB”不是 S2 任何子串的字谜。
> **输入:**S1 =“plethehelpimlinepted”，S2 =“INAKICKSTARTFACTORY”
> **输出:** 9

**天真法:**一个简单的方法是对照 **S2** 的所有子串检查 **S1** 的所有子串是否是字谜。
**高效做法:**将 **S1** 的所有子串逐一说出 **temp** ，通过计算 **temp** 的所有字符的频率，并与 **S2** 的**长度=长度(temp)** 的子串的字符频率进行比较，检查 **temp** 是否为 **S2** 的任意子串的字谜。
这可以通过单次遍历来完成，取 **S2** 的第一个**长度(temp)** 字符，然后对于每次迭代，添加字符串的下一个字符的频率，并移除先前选择的子字符串的第一个字符的频率，直到遍历完整个字符串。
以下是上述方法的实施:

## C++

```
// C++ program to find the number of sub-strings
// of s1 which are anagram of any sub-string of s2

#include <bits/stdc++.h>
using namespace std;

#define ALL_CHARS 256

// This function returns true if
// contents of arr1[] and arr2[]
// are same, otherwise false.
bool compare(char* arr1, char* arr2)
{
    for (int i = 0; i < ALL_CHARS; i++)
        if (arr1[i] != arr2[i])
            return false;

    return true;
}

// This function search for all permutations
// of string pat[] in string txt[]
bool search(string pat, string txt)
{
    int M = pat.length();
    int N = txt.length();

    int i;

    // countP[]: Store count of all characters
    // of pattern
    // countTW[]: Store count of current
    // window of text
    char countP[ALL_CHARS] = { 0 };
    char countTW[ALL_CHARS] = { 0 };
    for (i = 0; i < M; i++) {
        (countP[pat[i]])++;
        (countTW[txt[i]])++;
    }

    // Traverse through remaining
    // characters of pattern
    for (i = M; i < N; i++) {

        // Compare counts of current
        // window of text with
        // counts of pattern[]
        if (compare(countP, countTW)) {
            // cout<<pat<<" "<<txt<<" ";
            return true;
        }

        // Add current character to current window
        (countTW[txt[i]])++;

        // Remove the first character
        // of previous window
        countTW[txt[i - M]]--;
    }

    // Check for the last window in text
    if (compare(countP, countTW))
        return true;

    return false;
}

// Function to return the number of sub-strings of s1
// that are anagrams of any sub-string of s2
int calculatesubString(string s1, string s2, int n)
{
    // initializing variables
    int count = 0, j = 0, x = 0;

    // outer loop for picking starting point
    for (int i = 0; i < n; i++) {

        // loop for different length of substrings
        for (int len = 1; len <= n - i; len++) {

            // If s2 has any substring which is
            // anagram of s1.substr(i, len)
            if (search(s1.substr(i, len), s2)) {

                // increment the count
                count = count + 1;
            }
        }
    }
    return count;
}

// Driver code
int main()
{
    string str1 = "PLEASEHELPIMTRAPPED";
    string str2 = "INAKICKSTARTFACTORY";

    int len = str1.length();

    cout << calculatesubString(str1, str2, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of sub-Strings
// of s1 which are anagram of any sub-String of s2
class GFG {

    static int MAX_LEN = 1005;
    static int MAX_CHAR = 26;

    static int ALL_CHARS = 256;

    // This function returns true if
    // contents of arr1[] and arr2[]
    // are same, otherwise false.
    static boolean compare(char[] arr1, char[] arr2)
    {
        for (int i = 0; i < ALL_CHARS; i++)
            if (arr1[i] != arr2[i])
                return false;

        return true;
    }

    // This function search for all permutations
    // of String pat[] in String txt[]
    static boolean search(String pat, String txt)
    {
        int M = pat.length();
        int N = txt.length();

        int i;

        // countP[]: Store count of all characters
        // of pattern
        // countTW[]: Store count of current
        // window of text
        char countP[] = new char[ALL_CHARS];
        char countTW[] = new char[ALL_CHARS];
        for (i = 0; i < M; i++) {
            (countP[pat.charAt(i)])++;
            (countTW[txt.charAt(i)])++;
        }

        // Traverse through remaining
        // characters of pattern
        for (i = M; i < N; i++) {

            // Compare counts of current
            // window of text with
            // counts of pattern[]
            if (compare(countP, countTW)) {
                // cout<<pat<<" "<<txt<<" ";
                return true;
            }

            // Add current character to current window
            (countTW[txt.charAt(i)])++;

            // Remove the first character
            // of previous window
            countTW[txt.charAt(i - M)]--;
        }

        // Check for the last window in text
        if (compare(countP, countTW))
            return true;

        return false;
    }

    // Function to return the number of sub-Strings of s1
    // that are anagrams of any sub-String of s2
    static int calculatesubString(String s1, String s2, int n)
    {
        // initializing variables
        int count = 0, j = 0, x = 0;

        // outer loop for picking starting point
        for (int i = 0; i < n; i++) {

            // loop for different length of subStrings
            for (int len = 1; len <= n - i; len++) {

                // If s2 has any subString which is
                // anagram of s1.substr(i, len)
                if (search(s1.substring(i, i + len), s2)) {

                    // increment the count
                    count = count + 1;
                }
            }
        }
        return count;
    }

    // Driver code
    public static void main(String args[])
    {
        String str1 = "PLEASEHELPIMTRAPPED";
        String str2 = "INAKICKSTARTFACTORY";

        int len = str1.length();

        System.out.println(calculatesubString(str1, str2, len));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the number of sub-strings
# of s1 which are anagram of any sub-string of s2
ALL_CHARS = 256

# This function returns true if
# contents of arr1[] and arr2[]
# are same, otherwise false.
def compare(arr1, arr2):
    for i in range(ALL_CHARS):
        if arr1[i] != arr2[i]:
            return False
    return True

# This function search for all permutations
# of string pat[] in string txt[]
def search(pat, txt):
    M = len(pat)
    N = len(txt)

    # countP[]: Store count of all characters
    # of pattern
    # countTW[]: Store count of current
    # window of text
    countP = [0] * ALL_CHARS
    countTW = [0] * ALL_CHARS
    for i in range(M):
        countP[ord(pat[i])] += 1
        countTW[ord(txt[i])] += 1

    # Traverse through remaining
    # characters of pattern
    for i in range(M, N):

        # Compare counts of current
        # window of text with
        # counts of pattern[]
        if compare(countP, countTW):
            return True

        # Add current character to current window
        countTW[ord(txt[i])] += 1

        # Remove the first character
        # of previous window
        countTW[ord(txt[i - M])] -= 1

    # Check for the last window in text
    if compare(countP, countTW):
        return True

    return False

# Function to return the number of sub-strings of s1
# that are anagrams of any sub-string of s2
def calculateSubString(s1, s2, n):

    # initializing variables
    count, j, x = 0, 0, 0

    # outer loop for picking starting point
    for i in range(n):

        # loop for different length of substrings
        for length in range(1, n - i + 1):

            # If s2 has any substring which is
            # anagram of s1.substr(i, len)
            if search(s1[i:i + length], s2):

                # increment the count
                count += 1

    return count

# Driver Code
if __name__ == "__main__":
    str1 = "PLEASEHELPIMTRAPPED"
    str2 = "INAKICKSTARTFACTORY"

    length = len(str1)

    print(calculateSubString(str1, str2, length))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to find the number of sub-Strings
// of s1 which are anagram of any sub-String of s2
using System;
using System.Collections.Generic;

class GFG {

    static int MAX_LEN = 1005;
    static int MAX_CHAR = 26;

    static int ALL_CHARS = 256;

    // This function returns true if
    // contents of arr1[] and arr2[]
    // are same, otherwise false.
    static bool compare(char[] arr1, char[] arr2)
    {
        for (int i = 0; i < ALL_CHARS; i++)
            if (arr1[i] != arr2[i])
                return false;

        return true;
    }

    // This function search for all permutations
    // of String pat[] in String txt[]
    static bool search(String pat, String txt)
    {
        int M = pat.Length;
        int N = txt.Length;

        int i;

        // countP[]: Store count of all characters
        // of pattern
        // countTW[]: Store count of current
        // window of text
        char[] countP = new char[ALL_CHARS];
        char[] countTW = new char[ALL_CHARS];
        for (i = 0; i < M; i++) {
            (countP[pat[i]])++;
            (countTW[txt[i]])++;
        }

        // Traverse through remaining
        // characters of pattern
        for (i = M; i < N; i++) {

            // Compare counts of current
            // window of text with
            // counts of pattern[]
            if (compare(countP, countTW)) {
                // cout<<pat<<" "<<txt<<" ";
                return true;
            }

            // Add current character to current window
            (countTW[txt[i]])++;

            // Remove the first character
            // of previous window
            countTW[txt[i - M]]--;
        }

        // Check for the last window in text
        if (compare(countP, countTW))
            return true;

        return false;
    }

    // Function to return the number of sub-Strings of s1
    // that are anagrams of any sub-String of s2
    static int calculatesubString(String s1, String s2, int n)
    {
        // initializing variables
        int count = 0, j = 0, x = 0;

        // outer loop for picking starting point
        for (int i = 0; i < n; i++) {

            // loop for different length of subStrings
            for (int len = 1; len <= n - i; len++) {

                // If s2 has any subString which is
                // anagram of s1.substr(i, len)
                if (search(s1.Substring(i, len), s2)) {

                    // increment the count
                    count = count + 1;
                }
            }
        }
        return count;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str1 = "PLEASEHELPIMTRAPPED";
        String str2 = "INAKICKSTARTFACTORY";

        int len = str1.Length;

        Console.WriteLine(calculatesubString(str1, str2, len));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

    // JavaScript program to find the number of sub-Strings
    // of s1 which are anagram of any sub-String of s2

    let MAX_LEN = 1005;
    let MAX_CHAR = 26;

    let ALL_CHARS = 256;

    // This function returns true if
    // contents of arr1[] and arr2[]
    // are same, otherwise false.
    function compare(arr1, arr2)
    {
        for (let i = 0; i < ALL_CHARS; i++)
            if (arr1[i] != arr2[i])
                return false;

        return true;
    }

    // This function search for all permutations
    // of String pat[] in String txt[]
    function search(pat, txt)
    {
        let M = pat.length;
        let N = txt.length;

        let i;

        // countP[]: Store count of all characters
        // of pattern
        // countTW[]: Store count of current
        // window of text
        let countP = new Array(ALL_CHARS);
        countP.fill(0);
        let countTW = new Array(ALL_CHARS);
        countTW.fill(0);
        for (i = 0; i < M; i++) {
            countP[pat[i].charCodeAt()]++;
            countTW[txt[i].charCodeAt()]++;
        }

        // Traverse through remaining
        // characters of pattern
        for (i = M; i < N; i++) {

            // Compare counts of current
            // window of text with
            // counts of pattern[]
            if (compare(countP, countTW)) {
                // cout<<pat<<" "<<txt<<" ";
                return true;
            }

            // Add current character to current window
            countTW[txt[i].charCodeAt()]++;

            // Remove the first character
            // of previous window
            countTW[txt[i - M].charCodeAt()]--;
        }

        // Check for the last window in text
        if (compare(countP, countTW))
            return true;

        return false;
    }

    // Function to return the number of sub-Strings of s1
    // that are anagrams of any sub-String of s2
    function calculatesubString(s1, s2, n)
    {
        // initializing variables
        let count = 0, j = 0, x = 0;

        // outer loop for picking starting point
        for (let i = 0; i < n; i++) {

            // loop for different length of subStrings
            for (let len = 1; len <= n - i; len++) {

                // If s2 has any subString which is
                // anagram of s1.substr(i, len)
                if (search(s1.substring(i, i + len), s2)) {

                    // increment the count
                    count = count + 1;
                }
            }
        }
        return count;
    }

    let str1 = "PLEASEHELPIMTRAPPED";
    let str2 = "INAKICKSTARTFACTORY";

    let len = str1.length;

    document.write(calculatesubString(str1, str2, len));

</script>
```

**Output:** 

```
9
```

**时间复杂度:** O(N <sup>2</sup> )

**空间复杂度:** O(M)，其中 M 是字符 ALL_CHARS 的最大长度