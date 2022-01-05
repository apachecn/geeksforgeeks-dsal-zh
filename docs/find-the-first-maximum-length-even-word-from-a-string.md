# 从一个字符串中找出第一个最大长度的偶数字

> 原文:[https://www . geeksforgeeks . org/从字符串中找到第一个最大长度的偶数单词/](https://www.geeksforgeeks.org/find-the-first-maximum-length-even-word-from-a-string/)

给定一串由空格分隔的单词。任务是从字符串中找到第一个最大长度的偶数字。例句:“给你一组 n 个数字”答案应该是“一”而不是“的”，因为“一”在“的”之前。
**例:**

```
Input:  "this is a test string"
Output:  string
Even length words are this, is, test, string. Even
maximum length word is string.

Input:  "geeksforgeeks is a platform for geeks"
Output:  platform
Only even length word is platform.
```

**做法:**思路是遍历输入字符串，找到每个单词的长度。检查单词的长度是否均匀。如果是偶数，则将长度与目前发现的最大长度进行比较。如果长度严格大于最大长度，则将当前单词存储为所需字符串。
以下是上述办法的实施:

## C++

```
// C++ program to find maximum length even word

#include <bits/stdc++.h>
using namespace std;

// Function to find maximum length even word
string findMaxLenEven(string str)
{
    int n = str.length();

    int i = 0;

    // To store length of current word.
    int currlen = 0;

    // To store length of maximum length word.
    int maxlen = 0;

    // To store starting index of maximum
    // length word.
    int st = -1;

    while (i < n) {

        // If current character is space then
        // word has ended. Check if it is even
        // length word or not. If yes then
        // compare length with maximum length
        // found so far.
        if (str[i] == ' ') {
            if (currlen % 2 == 0) {
                if (maxlen < currlen) {
                    maxlen = currlen;
                    st = i - currlen;
                }
            }

            // Set currlen to zero for next word.
            currlen = 0;
        }
        else {
            // Update length of current word.
            currlen++;
        }

        i++;
    }

    // Check length of last word.
    if (currlen % 2 == 0) {
        if (maxlen < currlen) {
            maxlen = currlen;
            st = i - currlen;
        }
    }

    // If no even length word is present
    // then return -1.
    if (st == -1)
        return "-1";

    return str.substr(st, maxlen);
}

// Driver code
int main()
{
    string str = "this is a test string";

    cout << findMaxLenEven(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum length even word
class GFG
{

// Function to find maximum length even word
static String findMaxLenEven(String str)
{
    int n = str.length();

    int i = 0;

    // To store length of current word.
    int currlen = 0;

    // To store length of maximum length word.
    int maxlen = 0;

    // To store starting index of maximum
    // length word.
    int st = -1;

    while (i < n)
    {

        // If current character is space then
        // word has ended. Check if it is even
        // length word or not. If yes then
        // compare length with maximum length
        // found so far.
        if (str.charAt(i) == ' ')
        {
            if (currlen % 2 == 0)
            {
                if (maxlen < currlen)
                {
                    maxlen = currlen;
                    st = i - currlen;
                }
            }

            // Set currlen to zero for next word.
            currlen = 0;
        }
        else
        {
            // Update length of current word.
            currlen++;
        }

        i++;
    }

    // Check length of last word.
    if (currlen % 2 == 0)
    {
        if (maxlen < currlen)
        {
            maxlen = currlen;
            st = i - currlen;
        }
    }

    // If no even length word is present
    // then return -1.
    if (st == -1)
        return "-1";

    return str.substring(st, st + maxlen);
}

// Driver code
public static void main(String args[])
{
    String str = "this is a test string";

    System.out.println( findMaxLenEven(str));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find maximum
# length even word

# Function to find maximum length
# even word
def findMaxLenEven(str):
    n = len(str)
    i = 0

    # To store length of current word.
    currlen = 0

    # To store length of maximum length word.
    maxlen = 0

    # To store starting index of maximum
    # length word.
    st = -1

    while (i < n):

        # If current character is space then
        # word has ended. Check if it is even
        # length word or not. If yes then
        # compare length with maximum length
        # found so far.
        if (str[i] == ' '):
            if (currlen % 2 == 0):
                if (maxlen < currlen):
                    maxlen = currlen
                    st = i - currlen

            # Set currlen to zero for next word.
            currlen = 0

        else :

            # Update length of current word.
            currlen += 1

        i += 1

    # Check length of last word.
    if (currlen % 2 == 0):
        if (maxlen < currlen):
            maxlen = currlen
            st = i - currlen

    # If no even length word is present
    # then return -1.
    if (st == -1):
        print("trie")
        return "-1"

    return str[st: st + maxlen]

# Driver code
if __name__ == "__main__":

    str = "this is a test string"

    print(findMaxLenEven(str))

# This code is contributed by Ita_c
```

## C#

```
// C# program to find maximum length even word

using System;

class GFG
{

    // Function to find maximum length even word
    static String findMaxLenEven(string str)
    {
        int n = str.Length;

        int i = 0;

        // To store length of current word.
        int currlen = 0;

        // To store length of maximum length word.
        int maxlen = 0;

        // To store starting index of maximum
        // length word.
        int st = -1;

        while (i < n)
        {

            // If current character is space then
            // word has ended. Check if it is even
            // length word or not. If yes then
            // compare length with maximum length
            // found so far.
            if (str[i] == ' ')
            {
                if (currlen % 2 == 0)
                {
                    if (maxlen < currlen)
                    {
                        maxlen = currlen;
                        st = i - currlen;
                    }
                }

                // Set currlen to zero for next word.
                currlen = 0;
            }
            else
            {
                // Update length of current word.
                currlen++;
            }

            i++;
        }

        // Check length of last word.
        if (currlen % 2 == 0)
        {
            if (maxlen < currlen)
            {
                maxlen = currlen;
                st = i - currlen;
            }
        }

        // If no even length word is present
        // then return -1.
        if (st == -1)
            return "-1";

        return str.Substring(st, maxlen);
    }

    // Driver code
    public static void Main()
    {
        string str = "this is a test string";

        Console.WriteLine(findMaxLenEven(str));
    }
    // This code is contributed by Ryuga
}
```

## java 描述语言

```
<script>

// Javascript program to find maximum length even word

// Function to find maximum length even word
function findMaxLenEven(str)
{
    var n = str.length;

    var i = 0;

    // To store length of current word.
    var currlen = 0;

    // To store length of maximum length word.
    var maxlen = 0;

    // To store starting index of maximum
    // length word.
    var st = -1;

    while (i < n) {

        // If current character is space then
        // word has ended. Check if it is even
        // length word or not. If yes then
        // compare length with maximum length
        // found so far.
        if (str[i] == ' ') {
            if (currlen % 2 == 0) {
                if (maxlen < currlen) {
                    maxlen = currlen;
                    st = i - currlen;
                }
            }

            // Set currlen to zero for next word.
            currlen = 0;
        }
        else {
            // Update length of current word.
            currlen++;
        }

        i++;
    }

    // Check length of last word.
    if (currlen % 2 == 0) {
        if (maxlen < currlen) {
            maxlen = currlen;
            st = i - currlen;
        }
    }

    // If no even length word is present
    // then return -1.
    if (st == -1)
        return "-1";

    return str.substr(st, maxlen);
}

// Driver code
var str = "this is a test string";
document.write( findMaxLenEven(str));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
string
```

**时间复杂度:** O(N)，其中 N 为字符串的长度。
**辅助空间:** O(1)