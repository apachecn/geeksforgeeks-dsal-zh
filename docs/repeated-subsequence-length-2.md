# 长度大于等于 2 的重复子序列

> 原文:[https://www . geeksforgeeks . org/repeated-subserial-length-2/](https://www.geeksforgeeks.org/repeated-subsequence-length-2/)

给定一个字符串，查找是否有任何长度为 2 或更长的子序列重复自身，使得两个子序列在相同的位置没有相同的字符，即两个子序列中的任何第 0 个或第 1 个字符在原始字符串中不应该有相同的索引。

**示例:**

```
Input: ABCABD
Output: Repeated Subsequence Exists (A B is repeated) 

Input: ABBB
Output: Repeated Subsequence Exists (B B is repeated)

Input: AAB
Output: Repeated Subsequence Doesn't Exist (Note that 
A B cannot be considered as repeating because B is at
same position in two subsequences).

Input: AABBC
Output: Repeated Subsequence Exists (A B is repeated)

Input: ABCDACB
Output: Repeated Subsequence Exists (A B is repeated)

Input: ABCD
Output: Repeated Subsequence Doesn't Exist
```

问题是[最长公共子序列](https://www.geeksforgeeks.org/longest-repeating-subsequence/)问题的经典变异。我们已经在这里讨论了动态编程解决方案。动态规划解占用 O(n <sup>2</sup> )时间和空间。
本文讨论了 O(n)时空方法。

其思想是从字符串中删除所有不重复的字符，并检查结果字符串是否是回文。如果剩下的字符串是回文，那么它就不会重复，否则就有重复。我们需要处理像“AAA”这样的输入的一个特殊情况，它是回文，但是它们的重复子序列存在。如果回文字符串长度为奇数，并且中间字母与左(或右)字符相同，则重复子序列存在。

以下是上述想法的实现。

## C++

```
// C++ program to check if any repeated
// subsequence exists in the string
#include <bits/stdc++.h>
#define MAX_CHAR 256
using namespace std;

// A function to check if a string str is palindrome
bool isPalindrome(char str[], int l, int h)
{
    // l and h are leftmost and rightmost corners of str
    // Keep comparing characters while they are same
    while (h > l)
        if (str[l++] != str[h--])
            return false;

    return true;
}

// The main function that checks if repeated
// subsequence exists in the string
int check(char str[])
{
    // Find length of input string
    int n = strlen(str);

    // Create an array to store all characters and their
    // frequencies in str[]
    int freq[MAX_CHAR] = { 0 };

    // Traverse the input string and store frequencies
    // of all characters in freq[] array.
    for (int i = 0; i < n; i++)
    {
        freq[str[i]]++;

        // If the character count is more than 2
        // we found a repetition
        if (freq[str[i]] > 2)
            return true;
    }

    // In-place remove non-repeating characters
    // from the string
    int k = 0;
    for (int i = 0; i < n; i++)
        if (freq[str[i]] > 1)
            str[k++] = str[i];
    str[k] = '\0';

    // check if the resultant string is palindrome
    if (isPalindrome(str, 0, k-1))
    {
        // special case - if length is odd
        // return true if the middle character is
        // same as previous one
        if (k & 1)
            return str[k/2] == str[k/2 - 1];

        // return false if string is a palindrome
        return false;
    }

    // return true if string is not a palindrome
    return true;
}

// Driver code
int main()
{
    char str[] = "ABCABD";

    if (check(str))
        cout << "Repeated Subsequence Exists";
    else
        cout << "Repeated Subsequence Doesn't Exists";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if any repeated
// subsequence exists in the string
class GFG
{
    static int MAX_CHAR = 256;

    // A function to check
    // if a string str is palindrome
    public static boolean isPalindrome(String str,
                                       int l, int h)
    {

        // l and h are leftmost and rightmost corners of str
        // Keep comparing characters while they are same
        while(h > l)
            if (str.charAt(l++) != str.charAt(h--))
                return false;

        return true;
    }

    // The main function that checks if repeated
    // subsequence exists in the string
    public static boolean check(String str)
    {

        // Find length of input string
        int n = str.length();

        // Create an array to store all characters
        // and their frequencies in str[]
        int[] freq = new int[MAX_CHAR];

        // Traverse the input string and store frequencies
        // of all characters in freq[] array.
        for (int i = 0; i < n; i++)
        {
            freq[str.charAt(i)]++;

            // If the character count is more than 2
            // we found a repetition
            if (freq[str.charAt(i)] > 2)
                return true;
        }

        // In-place remove non-repeating characters
        // from the string
        int k = 0;
        for (int i = 0; i < n; i++)
            if (freq[str.charAt(i)] > 1)
                str.replace(str.charAt(k++),
                            str.charAt(i));
        str.replace(str.charAt(k), '\0');

        // check if the resultant string is palindrome
        if (isPalindrome(str, 0, k - 1))
        {

            // special case - if length is odd
            // return true if the middle character is
            // same as previous one
            if ((k & 1) == 1)
            {

                // It is checked so that
                // StringIndexOutOfBounds can be avoided
                if (k / 2 >= 1)
                    return (str.charAt(k / 2) ==
                            str.charAt(k / 2 - 1));
            }

            // return false if string is a palindrome
            return false;
        }

        // return true if string is not a palindrome
        return true;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str = "ABCABD";

        if (check(str))
            System.out.println("Repeated Subsequence Exists");
        else
            System.out.println("Repeated Subsequence" +
                               " Doesn't Exists");
    }
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to check if any repeated
# subsequence exists in the String
MAX_CHAR = 256

# A function to check
# if a String Str is palindrome
def isPalindrome(Str, l, h):

    # l and h are leftmost and rightmost corners of Str
    # Keep comparing characters while they are same
    while (h > l):
        if (Str[l] != Str[h]):
            l += 1
            h -= 1
            return False

    return True

# The main function that checks if repeated
# subsequence exists in the String
def check(Str):

    # Find length of input String
    n = len(Str)

    # Create an array to store all characters
    # and their frequencies in Str[]
    freq = [0 for i in range(MAX_CHAR)]

    # Traverse the input String and
    # store frequencies of all characters
    # in freq[] array.
    for i in range(n):

        freq[ord(Str[i])] += 1

        # If the character count is more than 2
        # we found a repetition
        if (freq[ord(Str[i])] > 2):
            return True

    # In-place remove non-repeating characters
    # from the String
    k = 0
    for i in range(n):
        if (freq[ord(Str[i])] > 1):
            Str[k] = Str[i]
            k += 1
    Str[k] = '\0'

    # check if the resultant String is palindrome
    if (isPalindrome(Str, 0, k - 1)):

        # special case - if length is odd
        # return true if the middle character is
        # same as previous one
        if (k & 1):
            return Str[k // 2] == Str[k // 2 - 1]

        # return false if String is a palindrome
        return False

    # return true if String is not a palindrome
    return True

# Driver code
S = "ABCABD"
Str = [i for i in S]

if (check(Str)):
    print("Repeated Subsequence Exists")
else:
    print("Repeated Subsequence Doesn't Exists")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to check if any repeated
// subsequence exists in the string
using System;

class GFG
{
    static int MAX_CHAR = 256;

    // A function to check
    // if a string str is palindrome
    public static Boolean isPalindrome(String str,
                                    int l, int h)
    {

        // l and h are leftmost and rightmost corners of str
        // Keep comparing characters while they are same
        while(h > l)
            if (str[l++] != str[h--])
                return false;

        return true;
    }

    // The main function that checks if repeated
    // subsequence exists in the string
    public static Boolean check(String str)
    {

        // Find length of input string
        int n = str.Length;

        // Create an array to store all characters
        // and their frequencies in str[]
        int[] freq = new int[MAX_CHAR];

        // Traverse the input string and store frequencies
        // of all characters in freq[] array.
        for (int i = 0; i < n; i++)
        {
            freq[str[i]]++;

            // If the character count is more than 2
            // we found a repetition
            if (freq[str[i]] > 2)
                return true;
        }

        // In-place remove non-repeating characters
        // from the string
        int k = 0;
        for (int i = 0; i < n; i++)
            if (freq[str[i]] > 1)
                str.Replace(str[k++],
                            str[i]);
        str.Replace(str[k], '\0');

        // check if the resultant string is palindrome
        if (isPalindrome(str, 0, k - 1))
        {

            // special case - if length is odd
            // return true if the middle character is
            // same as previous one
            if ((k & 1) == 1)
            {

                // It is checked so that
                // StringIndexOutOfBounds can be avoided
                if (k / 2 >= 1)
                    return (str[k / 2] ==
                            str[k / 2 - 1]);
            }

            // return false if string is a palindrome
            return false;
        }

        // return true if string is not a palindrome
        return true;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String str = "ABCABD";

        if (check(str))
            Console.WriteLine("Repeated Subsequence Exists");
        else
            Console.WriteLine("Repeated Subsequence" +
                            " Doesn't Exists");
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript program to check if any repeated
// subsequence exists in the string

    let MAX_CHAR = 256;

    // A function to check
    // if a string str is palindrome
    function isPalindrome(str,l,h)
    {
        // l and h are leftmost and rightmost corners of str
        // Keep comparing characters while they are same
        while(h > l)
            if (str[l++] != str[h--])
                return false;

        return true;
    }

    // The main function that checks if repeated
    // subsequence exists in the string
    function check(str)
    {
        // Find length of input string
        let n = str.length;

        // Create an array to store all characters
        // and their frequencies in str[]
        let freq = new Array(MAX_CHAR);
        for(let i=0;i<freq.length;i++)
        {
            freq[i]=0;
        }

        // Traverse the input string and store frequencies
        // of all characters in freq[] array.
        for (let i = 0; i < n; i++)
        {
            freq[str[i].charCodeAt(0)]++;

            // If the character count is more than 2
            // we found a repetition
            if (freq[str[i].charCodeAt(0)] > 2)
                return true;
        }

        // In-place remove non-repeating characters
        // from the string
        let k = 0;
        for (let i = 0; i < n; i++)
            if (freq[str[i].charCodeAt(0)] > 1)
                str.replace(str[k++],
                            str[i]);
        str.replace(str[k], '\0');

        // check if the resultant string is palindrome
        if (isPalindrome(str, 0, k - 1))
        {

            // special case - if length is odd
            // return true if the middle character is
            // same as previous one
            if ((k & 1) == 1)
            {

                // It is checked so that
                // StringIndexOutOfBounds can be avoided
                if (k / 2 >= 1)
                    return (str[Math.floor(k/2)] ==
                            str[Math.floor(k/2) -1]);
            }

            // return false if string is a palindrome
            return false;
        }

        // return true if string is not a palindrome
        return true;
    }

    // Driver Code
    let str = "ABCABD";
    if (check(str))
        document.write("Repeated Subsequence Exists");
    else
        document.write("Repeated Subsequence" +
                               " Doesn't Exists");

    // This code is contributed by unknown2108
</script>
```

**输出:**

```
Repeated Subsequence Exists
```

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息