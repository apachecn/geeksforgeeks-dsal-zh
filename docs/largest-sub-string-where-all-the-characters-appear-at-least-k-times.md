# 所有字符出现至少 K 次的最大子串

> 原文:[https://www . geesforgeks . org/最大子字符串-所有字符出现的位置-至少 k 次/](https://www.geeksforgeeks.org/largest-sub-string-where-all-the-characters-appear-at-least-k-times/)

给定一个字符串 **str** 和一个整数 **K** ，任务是找到最长子字符串**S‘**的长度，使得**S‘**中的每个字符至少出现 **K** 次。

> **输入:**s = " xyyz "，k = 2
> **输出:**5
> “xyy”是最长的子串，其中
> 每个字符至少出现两次。
> **输入:** s = "geeksforgeeks "，k = 2
> **输出:** 2

**方法:**考虑所有可能的子串，对于每个子串，计算其每个字符的出现频率，检查所有字符是否至少出现 K 次。对于所有这样的有效子字符串，尽可能找到最大长度。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define MAX 26

// Function that return true if frequency
// of all the present characters is at least k
bool atLeastK(int freq[], int k)
{
    for (int i = 0; i < MAX; i++) {

        // If the character is present and
        // its frequency is less than k
        if (freq[i] != 0 && freq[i] < k)
            return false;
    }

    return true;
}

// Function to set every frequency to zero
void setZero(int freq[])
{
    for (int i = 0; i < MAX; i++)
        freq[i] = 0;
}

// Function to return the length of the longest
// sub-string such that it contains every
// character at least k times
int findlength(string str, int n, int k)
{

    // To store the required maximum length
    int maxLen = 0;

    int freq[MAX];

    // Starting index of the sub-string
    for (int i = 0; i < n; i++) {
        setZero(freq);

        // Ending index of the sub-string
        for (int j = i; j < n; j++) {
            freq[str[j] - 'a']++;

            // If the frequency of every character
            // of the current sub-string is at least k
            if (atLeastK(freq, k)) {

                // Update the maximum possible length
                maxLen = max(maxLen, j - i + 1);
            }
        }
    }

    return maxLen;
}

// Driver code
int main()
{
    string str = "xyxyyz";
    int n = str.length();
    int k = 2;

    cout << findlength(str, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation of the above approach
class GFG
{

static final int MAX = 26;

// Function that return true if frequency
// of all the present characters is at least k
static boolean atLeastK(int freq[], int k)
{
    for (int i = 0; i < MAX; i++)
    {

        // If the character is present and
        // its frequency is less than k
        if (freq[i] != 0 && freq[i] < k)
            return false;
    }

    return true;
}

// Function to set every frequency to zero
static void setZero(int freq[])
{
    for (int i = 0; i < MAX; i++)
        freq[i] = 0;
}

// Function to return the length of the longest
// sub-string such that it contains every
// character at least k times
static int findlength(String str, int n, int k)
{

    // To store the required maximum length
    int maxLen = 0;

    int freq[] = new int[MAX];

    // Starting index of the sub-string
    for (int i = 0; i < n; i++)
    {
        setZero(freq);

        // Ending index of the sub-string
        for (int j = i; j < n; j++)
        {
            freq[str.charAt(j) - 'a']++;

            // If the frequency of every character
            // of the current sub-string is at least k
            if (atLeastK(freq, k))
            {

                // Update the maximum possible length
                maxLen = Math.max(maxLen, j - i + 1);
            }
        }
    }

    return maxLen;
}

// Driver code
public static void main(String args[])
{
    String str = "xyxyyz";
    int n = str.length();
    int k = 2;

    System.out.println(findlength(str, n, k));

}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 26

# Function that return true if frequency
# of all the present characters is at least k
def atLeastK(freq, k) :

    for i in range(MAX) :

        # If the character is present and
        # its frequency is less than k
        if (freq[i] != 0 and freq[i] < k) :
            return False;

    return True;

# Function to set every frequency to zero
def setZero(freq) :

    for i in range(MAX) :
        freq[i] = 0;

# Function to return the length of the longest
# sub-string such that it contains every
# character at least k times
def findlength(string, n, k) :

    # To store the required maximum length
    maxLen = 0;

    freq = [0]*MAX;

    # Starting index of the sub-string
    for i in range(n) :
        setZero(freq);

        # Ending index of the sub-string
        for j in range(i,n) :
            freq[ord(string[j]) - ord('a')] += 1;

            # If the frequency of every character
            # of the current sub-string is at least k
            if (atLeastK(freq, k)) :

                # Update the maximum possible length
                maxLen = max(maxLen, j - i + 1);

    return maxLen;

# Driver code
if __name__ == "__main__" :

    string = "xyxyyz";
    n = len(string);
    k = 2;

    print(findlength(string, n, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# Implementation of the above approach
using System;

class GFG
{

static int MAX = 26;

// Function that return true if frequency
// of all the present characters is at least k
static Boolean atLeastK(int []freq, int k)
{
    for (int i = 0; i < MAX; i++)
    {

        // If the character is present and
        // its frequency is less than k
        if (freq[i] != 0 && freq[i] < k)
            return false;
    }

    return true;
}

// Function to set every frequency to zero
static void setZero(int []freq)
{
    for (int i = 0; i < MAX; i++)
        freq[i] = 0;
}

// Function to return the length of the longest
// sub-string such that it contains every
// character at least k times
static int findlength(String str, int n, int k)
{

    // To store the required maximum length
    int maxLen = 0;

    int []freq = new int[MAX];

    // Starting index of the sub-string
    for (int i = 0; i < n; i++)
    {
        setZero(freq);

        // Ending index of the sub-string
        for (int j = i; j < n; j++)
        {
            freq[str[j] - 'a']++;

            // If the frequency of every character
            // of the current sub-string is at least k
            if (atLeastK(freq, k))
            {

                // Update the maximum possible length
                maxLen = Math.Max(maxLen, j - i + 1);
            }
        }
    }

    return maxLen;
}

// Driver code
public static void Main(String []args)
{
    String str = "xyxyyz";
    int n = str.Length;
    int k = 2;

    Console.WriteLine(findlength(str, n, k));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var MAX = 26;

// Function that return true if frequency
// of all the present characters is at least k
function atLeastK(freq, k)
{
    for (var i = 0; i < MAX; i++) {

        // If the character is present and
        // its frequency is less than k
        if (freq[i] != 0 && freq[i] < k)
            return false;
    }

    return true;
}

// Function to set every frequency to zero
function setZero(freq)
{
    for (var i = 0; i < MAX; i++)
        freq[i] = 0;
}

// Function to return the length of the longest
// sub-string such that it contains every
// character at least k times
function findlength(str, n, k)
{

    // To store the required maximum length
    var maxLen = 0;

    var freq = Array(MAX).fill(0);

    // Starting index of the sub-string
    for (var i = 0; i < n; i++) {
        setZero(freq);

        // Ending index of the sub-string
        for (var j = i; j < n; j++) {
            freq[str[j].charCodeAt(0) - 'a'.charCodeAt(0)]++;

            // If the frequency of every character
            // of the current sub-string is at least k
            if (atLeastK(freq, k)) {

                // Update the maximum possible length
                maxLen = Math.max(maxLen, j - i + 1);
            }
        }
    }

    return maxLen;
}

// Driver code
var str = "xyxyyz";
var n = str.length;
var k = 2;
document.write( findlength(str, n, k));

</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(n <sup>2</sup> )
**辅助空间:** O(MAX)，其中 MAX 为字符串中唯一字符的最大个数。